---
description: This tutorial demonstrates writing a new audio file (.wma) by extracting media content from an uncompressed audio file (.wav) and then compressing it in ASF format.
ms.assetid: f310c6ed-52e7-4828-9d4c-2f7ced9080c5
title: 'Tutorial: Writing a WMA File by Using WMContainer Objects'
ms.topic: article
ms.date: 05/31/2018
---

# Tutorial: Writing a WMA File by Using WMContainer Objects

This tutorial demonstrates writing a new audio file (.wma) by extracting media content from an uncompressed audio file (.wav) and then compressing it in ASF format. The encoding mode used for the conversion is [Constant Bit Rate Encoding](constant-bit-rate-encoding.md) (CBR). In this mode, before the encoding session, the application specifies a target bit rate that the encoder must achieve.

In this tutorial, you will create a console application that takes the input and output filenames as arguments. The application gets the uncompressed media samples from a wave file parsing application, which is provided with this tutorial. These samples are sent to the encoder for conversion to Windows Media Audio 9 format. The encoder is configured for CBR encoding and uses the first bit rate available during media type negotiation as the target bit rate. The encoded samples are sent to the multiplexer for packetization in ASF data format. These packets will be written to a byte stream that represents the ASF Data Object. After the data section is ready, you will create an ASF audio file and write the new ASF Header Object that consolidates all the header information and then append the ASF Data Object byte stream.

This tutorial contains the following sections:

-   [Prerequisites](#prerequisites)
-   [Terminology](#terminology)
-   [1. Set up the Project](#1-set-up-the-project)
-   [2. Declare Helper Functions](#2-declare-helper-functions)
-   [3. Open an Audio File](#3-open-an-audio-file)
-   [4. Configure the Encoder](#4-configure-the-encoder)
-   [5. Create the ASF ContentInfo object.](#5-create-the-asf-contentinfo-object)
-   [6. Create the ASF Multiplexer](#6-create-the-asf-multiplexer)
-   [7. Generate New ASF Data Packets](#7-generate-new-asf-data-packets)
-   [8. Write the ASF File](#8-write-the-asf-file)
-   [9. Define the Entry-Point Function](#9-define-the-entry-point-function)
-   [Related topics](#related-topics)

## Prerequisites

This tutorial assumes the following:

-   You are familiar with the structure of an ASF file and the components provided by Media Foundation to work with ASF Objects. These components include ContentInfo, splitter, multiplexer, and profile objects. For more information, see [WMContainer ASF Components](wmcontainer-asf-components.md).
-   You are familiar with Windows Media encoders, and the various encoding types, particularly CBR. For more information, see [Windows Media Encoders](windows-media-encoders.md) .
-   You are familiar with [Media Buffers](media-buffers.md) and byte streams: Specifically, file operations using a byte stream, and writing the contents of a media buffer to a byte stream.

## Terminology

This tutorial uses the following terms:

-   Source media type: Media type object, exposes [**IMFMediaType**](/windows/desktop/api/mfobjects/nn-mfobjects-imfmediatype) interface, which describes the contents of the input file.
-   Audio profile: Profile object, exposes [**IMFASFProfile**](/windows/desktop/api/wmcontainer/nn-wmcontainer-imfasfprofile) interface, which contains only audio streams of the output file.
-   Stream sample: Media sample, exposes [**IMFSample**](/windows/desktop/api/mfobjects/nn-mfobjects-imfsample) interface, represents the input file's media data obtained from the encoder in a compressed state.
-   ContentInfo object: [ASF ContentInfo Object](asf-contentinfo-object.md), exposes [**IMFASFContentInfo**](/windows/desktop/api/wmcontainer/nn-wmcontainer-imfasfcontentinfo) interface, which represents the ASF Header Object of the output file.
-   Data byte stream: Byte stream object, exposes [**IMFByteStream**](/windows/desktop/api/mfobjects/nn-mfobjects-imfbytestream) interface, which represents the entire ASF Data Object portion of the output file.
-   Data packet: Media sample, exposes [**IMFSample**](/windows/desktop/api/mfobjects/nn-mfobjects-imfsample) interface, generated by the [ASF Multiplexer](asf-multiplexer.md); represents an ASF data packet that will be written to the data byte stream.
-   Output byte stream: Byte stream object, exposes [**IMFByteStream**](/windows/desktop/api/mfobjects/nn-mfobjects-imfbytestream) interface, which contains the contents of the output file.

## 1. Set up the Project

1.  Include the following headers in your source file:

    ```C++
    #include <new>
    #include <stdio.h>       // Standard I/O
    #include <windows.h>     // Windows headers
    #include <mfapi.h>       // Media Foundation platform
    #include <wmcontainer.h> // ASF interfaces
    #include <mferror.h>     // Media Foundation error codes
    ```

    

2.  Link to the following library files:

    -   mfplat.lib
    -   mf.lib
    -   mfuuid.lib

3.  Declare the [SafeRelease](saferelease.md) function.
4.  Include the CWmaEncoder class in your project. For the complete source code of this class, see [Encoder Example Code](encoder-example-code.md).

## 2. Declare Helper Functions

This tutorial uses the following helper functions to read and write from a byte stream.

-   `AppendToByteStream`: Appends the contents of one byte stream to another byte stream.
-   WriteBufferToByteStream: Writes data from a media buffer to a byte stream.

For more information, see [**IMFByteStream::Write**](/windows/desktop/api/mfobjects/nf-mfobjects-imfbytestream-write). The following code shows these helper functions:


```C++
//-------------------------------------------------------------------
// AppendToByteStream
//
// Reads the contents of pSrc and writes them to pDest.
//-------------------------------------------------------------------

HRESULT AppendToByteStream(IMFByteStream *pSrc, IMFByteStream *pDest)
{
    HRESULT hr = S_OK;

    const DWORD READ_SIZE = 1024;

    BYTE buffer[READ_SIZE];

    while (1)
    {
        ULONG cbRead;

        hr = pSrc->Read(buffer, READ_SIZE, &cbRead);

        if (FAILED(hr)) { break; }

        if (cbRead == 0)
        {
            break;
        }

        hr = pDest->Write(buffer, cbRead, &cbRead);

        if (FAILED(hr)) { break; }
    }

    return hr;
}
```




```C++
//-------------------------------------------------------------------
// WriteBufferToByteStream
//
// Writes data from a media buffer to a byte stream.
//-------------------------------------------------------------------

HRESULT WriteBufferToByteStream(
    IMFByteStream *pStream,   // Pointer to the byte stream.
    IMFMediaBuffer *pBuffer,  // Pointer to the media buffer.
    DWORD *pcbWritten         // Receives the number of bytes written.
    )
{
    HRESULT hr = S_OK;
    DWORD cbData = 0;
    DWORD cbWritten = 0;
    BYTE *pMem = NULL;

    hr = pBuffer->Lock(&pMem, NULL, &cbData);

    if (SUCCEEDED(hr))
    {
        hr = pStream->Write(pMem, cbData, &cbWritten);
    }

    if (SUCCEEDED(hr))
    {
        if (pcbWritten)
        {
            *pcbWritten = cbWritten;
        }
    }

    if (pMem)
    {
        pBuffer->Unlock();
    }
    return hr;
}
```



## 3. Open an Audio File

This tutorial assumes that your application will generate uncompressed audio for encoding. For that purpose, two functions are declared in this tutorial:


```C++
HRESULT OpenAudioFile(PCWSTR pszURL, IMFMediaType **ppAudioFormat);
HRESULT GetNextAudioSample(BOOL *pbEOS, IMFSample **ppSample);
```



The implementation of these functions is left to the reader.

-   The `OpenAudioFile` function should open the media file specified by *pszURL* and return a pointer to a media type that describes an audio stream.
-   The `GetNextAudioSample` function should read uncompressed PCM audio from the file that was opened by `OpenAudioFile`. When the end of the file is reached, *pbEOS* receives the value **TRUE**. Otherwise, *ppSample* receives a media sample that contains the audio buffer.

## 4. Configure the Encoder

Next, create the encoder, configure it to produce CBR-encoded stream samples, and negotiate the input and the output media types.

In Media Foundation, encoders (expose the [**IMFTransform**](/windows/desktop/api/mftransform/nn-mftransform-imftransform) interface) are implemented as [Media Foundation Transforms](media-foundation-transforms.md) (MFT).

In this tutorial, the encoder is implemented in the `CWmaEncoder` class that provides a wrapper for the MFT. For the complete source code of this class, see [Encoder Example Code](encoder-example-code.md).

> [!Note]  
> You can optionally specify the encoding type as CBR. By default, the encoder is configured to use CBR encoding. For more information, see [Constant Bit Rate Encoding](constant-bit-rate-encoding.md). You can set additional properties depending on the type of encoding, for information about the properties that are specific to an encoding mode, see [Quality-Based Variable Bit Rate Encoding](quality-based-variable-bit-rate--vbr--encoding.md), [Unconstrained Variable Bit Rate Encoding](unconstrained-variable-bit-rate--vbr--encoding.md), and [Peak-Constrained Variable Bit Rate Encoding](peak-constrained-variable-bit-rate--vbr--encoding.md).

 


```C++
    CWmaEncoder* pEncoder = NULL; //Pointer to the Encoder object.

    hr = OpenAudioFile(sInputFileName, &pInputType);
    if (FAILED(hr))
    {
        goto done;
    }

    // Initialize the WMA encoder wrapper.

    pEncoder = new (std::nothrow) CWmaEncoder();
    if (pEncoder == NULL)
    {
        hr = E_OUTOFMEMORY;
        goto done;
    }

    hr = pEncoder->Initialize();
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pEncoder->SetEncodingType(EncodeMode_CBR);
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pEncoder->SetInputType(pInputType);
    if (FAILED(hr))
    {
        goto done;
    }
```



## 5. Create the ASF ContentInfo object.

The [ASF ContentInfo Object](asf-contentinfo-object.md) contains information about the various header objects of the output file.

First, create an ASF profile for the audio stream:

1.  Call [**MFCreateASFProfile**](/windows/desktop/api/wmcontainer/nf-wmcontainer-mfcreateasfprofile) to create an empty ASF profile object. The ASF profile exposes the [**IMFASFProfile**](/windows/desktop/api/wmcontainer/nn-wmcontainer-imfasfprofile) interface. For more information, see [Creating and Configuring ASF Streams](creating-and-configuring-asf-streams.md).
2.  Get the encoded audio format from the `CWmaEncoder` object.
3.  Call [**IMFASFProfile::CreateStream**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfprofile-createstream) to create a new stream for the ASF profile. Pass in a pointer to the [**IMFMediaType**](/windows/desktop/api/mfobjects/nn-mfobjects-imfmediatype) interface, which represents the stream format.
4.  Call [**IMFASFStreamConfig::SetStreamNumber**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfstreamconfig-setstreamnumber) to assign a stream identifier.
5.  Set the "leaky bucket" parameters by setting the [**MF\_ASFSTREAMCONFIG\_LEAKYBUCKET1**](mf-asfstreamconfig-leakybucket1-attribute.md) attribute on the stream object.
6.  Call [**IMFASFProfile::SetStream**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfprofile-setstream) to add the new stream to the profile.

Now create the ASF ContentInfo object as follows:

1.  Call [**MFCreateASFContentInfo**](/windows/desktop/api/wmcontainer/nf-wmcontainer-mfcreateasfcontentinfo) to create an empty ContentInfo object.
2.  Call [**IMFASFContentInfo::SetProfile**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfcontentinfo-setprofile) to set the ASF profile.

The following code shows these steps:


```C++
HRESULT CreateASFContentInfo(
    CWmaEncoder* pEncoder,
    IMFASFContentInfo** ppContentInfo
    )
{
    HRESULT hr = S_OK;
    
    IMFASFProfile* pProfile = NULL;
    IMFMediaType* pMediaType = NULL;
    IMFASFStreamConfig* pStream = NULL;
    IMFASFContentInfo* pContentInfo = NULL;

    // Create the ASF profile object.

    hr = MFCreateASFProfile(&pProfile); 
    if (FAILED(hr))
    {
        goto done;
    }

    // Create a stream description for the encoded audio.

    hr = pEncoder->GetOutputType(&pMediaType); 
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pProfile->CreateStream(pMediaType, &pStream); 
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pStream->SetStreamNumber(DEFAULT_STREAM_NUMBER); 
    if (FAILED(hr))
    {
        goto done;
    }

    // Set "leaky bucket" values.

    LeakyBucket bucket;

    hr = pEncoder->GetLeakyBucket1(&bucket);
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pStream->SetBlob(
        MF_ASFSTREAMCONFIG_LEAKYBUCKET1, 
        (UINT8*)&bucket, 
        sizeof(bucket)
        );

    if (FAILED(hr))
    {
        goto done;
    }

    //Add the stream to the profile

    hr = pProfile->SetStream(pStream);
    if (FAILED(hr))
    {
        goto done;
    }

    // Create the ASF ContentInfo object.

    hr = MFCreateASFContentInfo(&pContentInfo); 
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pContentInfo->SetProfile(pProfile); 
    if (FAILED(hr))
    {
        goto done;
    }

    // Return the pointer to the caller.

    *ppContentInfo = pContentInfo;
    (*ppContentInfo)->AddRef();

done:
    SafeRelease(&pProfile);
    SafeRelease(&pStream);
    SafeRelease(&pMediaType);
    SafeRelease(&pContentInfo);
    return hr;
}
```



## 6. Create the ASF Multiplexer

The [ASF Multiplexer](asf-multiplexer.md) generates ASF data packets.

1.  Call [**MFCreateASFMultiplexer**](/windows/desktop/api/wmcontainer/nf-wmcontainer-mfcreateasfmultiplexer) to create the ASF multiplexer.
2.  Call [**IMFASFMultiplexer::Initialize**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfmultiplexer-initialize) to initialize the multiplexer. Pass in a pointer to the ASF Content Info object, which was created in the previous section.
3.  Call [**IMFASFMultiplexer::SetFlags**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfmultiplexer-setflags) to set the **MFASF\_MULTIPLEXER\_AUTOADJUST\_BITRATE** flag. When this setting is used, the multiplexer automatically adjusts the bit rate of the ASF content to match the characteristics of the streams being multiplexed.


```C++
HRESULT CreateASFMux( 
    IMFASFContentInfo* pContentInfo,
    IMFASFMultiplexer** ppMultiplexer
    )
{
    HRESULT hr = S_OK;
    
    IMFMediaType* pMediaType = NULL;
    IMFASFMultiplexer *pMultiplexer = NULL;

    // Create and initialize the ASF Multiplexer object.

    hr = MFCreateASFMultiplexer(&pMultiplexer);
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pMultiplexer->Initialize(pContentInfo);
    if (FAILED(hr))
    {
        goto done;
    }

    // Enable automatic bit-rate adjustment.

    hr = pMultiplexer->SetFlags(MFASF_MULTIPLEXER_AUTOADJUST_BITRATE);
    if (FAILED(hr))
    {
        goto done;
    }

    *ppMultiplexer = pMultiplexer;
    (*ppMultiplexer)->AddRef();

done:
    SafeRelease(&pMultiplexer);
    return hr;
}
```



## 7. Generate New ASF Data Packets

Next, generate ASF data packets for the new file. These data packets will constitute the final ASF Data Object for the new file. To generate new ASF data packets:

1.  Call [**MFCreateTempFile**](/windows/desktop/api/mfapi/nf-mfapi-mfcreatetempfile) to create a temporary byte stream to hold the ASF data packets.
2.  Call the application-defined `GetNextAudioSample` function to get uncompressed audio data for the encoder.
3.  Pass the uncompressed audio to the encoder for compression. For more information, see [Processing Data in the Encoder](processing-data-in-the-encoder.md)
4.  Call [**IMFASFMultiplexer::ProcessSample**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfmultiplexer-processsample) to send the compressed audio samples to the ASF multiplexer for packetization.
5.  Get the ASF packets from the multiplexer and write them to the temporary byte stream. For more information, see [Generating New ASF Data Packets](generating-new-asf-data-packets.md).
6.  When you reach the end of the source stream, drain the encoder and pull the remaining compressed samples from the encoder. For more information about draining an MFT, see [Basic MFT Processing Model](basic-mft-processing-model.md).
7.  After all samples are sent to the multiplexer, call [**IMFASFMultiplexer::Flush**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfmultiplexer-flush) and pull the remaining ASF packets from the multiplexer.
8.  Call [**IMFASFMultiplexer::End**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfmultiplexer-end).

The following code generates ASF data packets. The function returns a pointer to a byte stream that contains the ASF Data Object.


```C++
HRESULT EncodeData(
    CWmaEncoder* pEncoder, 
    IMFASFContentInfo* pContentInfo,
    IMFASFMultiplexer* pMux, 
    IMFByteStream** ppDataStream) 
{
    HRESULT hr = S_OK;

    IMFByteStream* pStream = NULL;
    IMFSample* pInputSample = NULL;
    IMFSample* pWmaSample = NULL;

    BOOL bEOF = FALSE;

   // Create a temporary file to hold the data stream.
   hr = MFCreateTempFile(
        MF_ACCESSMODE_READWRITE, 
        MF_OPENMODE_DELETE_IF_EXIST,
        MF_FILEFLAGS_NONE,
        &pStream
        );

   if (FAILED(hr))
   {
       goto done;
   }

    BOOL bNeedInput = TRUE;

    while (TRUE)
    {
        if (bNeedInput)
        {
            hr = GetNextAudioSample(&bEOF, &pInputSample);
            if (FAILED(hr))
            {
                goto done;
            }

            if (bEOF)
            {
                // Reached the end of the input file.
                break;
            }

            // Encode the uncompressed audio sample.
            hr = pEncoder->ProcessInput(pInputSample);
            if (FAILED(hr))
            {
                goto done;
            }

            bNeedInput = FALSE;
        }

        if (bNeedInput == FALSE)
        {
            // Get data from the encoder.

            hr = pEncoder->ProcessOutput(&pWmaSample);
            if (FAILED(hr))
            {
                goto done;
            }

            // pWmaSample can be NULL if the encoder needs more input.

            if (pWmaSample)
            {
                hr = pMux->ProcessSample(DEFAULT_STREAM_NUMBER, pWmaSample, 0);
                if (FAILED(hr))
                {
                    goto done;
                }

                //Collect the data packets and write them to a stream
                hr = GenerateASFDataPackets(pMux, pStream);
                if (FAILED(hr))
                {
                    goto done;
                }
            }
            else
            {
                bNeedInput = TRUE;
            }
        }
        
        SafeRelease(&pInputSample);
        SafeRelease(&pWmaSample);
    }

    // Drain the MFT and pull any remaining samples from the encoder.

    hr = pEncoder->Drain();
    if (FAILED(hr))
    {
        goto done;
    }

    while (TRUE)
    {
        hr = pEncoder->ProcessOutput(&pWmaSample);
        if (FAILED(hr))
        {
            goto done;
        }

        if (pWmaSample == NULL)
        {
            break;
        }

        hr = pMux->ProcessSample(DEFAULT_STREAM_NUMBER, pWmaSample, 0);
        if (FAILED(hr))
        {
            goto done;
        }

        //Collect the data packets and write them to a stream
        hr = GenerateASFDataPackets(pMux, pStream);
        if (FAILED(hr))
        {
            goto done;
        }

        SafeRelease(&pWmaSample);
    }

    // Flush the mux and get any pending ASF data packets.
    hr = pMux->Flush();
    if (FAILED(hr))
    {
        goto done;
    }

    hr = GenerateASFDataPackets(pMux, pStream);
    if (FAILED(hr))
    {
        goto done;
    }
    
    // Update the ContentInfo object
    hr = pMux->End(pContentInfo);
    if (FAILED(hr))
    {
        goto done;
    }

    //Return stream to the caller that contains the ASF encoded data.
    *ppDataStream = pStream;
    (*ppDataStream)->AddRef();

done:
    SafeRelease(&pStream);
    SafeRelease(&pInputSample);
    SafeRelease(&pWmaSample);
    return hr;
}
```



Code for the `GenerateASFDataPackets` function is shown in the topic [Generating New ASF Data Packets](generating-new-asf-data-packets.md).

## 8. Write the ASF File

Next, write the ASF header to a media buffer by calling [**IMFASFContentInfo::GenerateHeader**](/windows/desktop/api/wmcontainer/nf-wmcontainer-imfasfcontentinfo-generateheader). This method converts data stored in the ContentInfo object into binary data in ASF Header Object format. For more information, see [Generating a New ASF Header Object](generating-a-new-asf-header-object.md).

After the new ASF Header Object has been generated, create a byte stream for the output file. First write the Header Object to the output byte stream. Follow the Header Object with the Data Object contained in the data byte stream.


```C++
HRESULT WriteASFFile( 
     IMFASFContentInfo *pContentInfo, 
     IMFByteStream *pDataStream,
     PCWSTR pszFile
     )
{
    HRESULT hr = S_OK;
    
    IMFMediaBuffer* pHeaderBuffer = NULL;
    IMFByteStream* pWmaStream = NULL;

    DWORD cbHeaderSize = 0;
    DWORD cbWritten = 0;

    //Create output file
    hr = MFCreateFile(MF_ACCESSMODE_WRITE, MF_OPENMODE_DELETE_IF_EXIST,
        MF_FILEFLAGS_NONE, pszFile, &pWmaStream);

    if (FAILED(hr))
    {
        goto done;
    }


    // Get the size of the ASF Header Object.
    hr = pContentInfo->GenerateHeader (NULL, &cbHeaderSize);
    if (FAILED(hr))
    {
        goto done;
    }

    // Create a media buffer.
    hr = MFCreateMemoryBuffer(cbHeaderSize, &pHeaderBuffer);
    if (FAILED(hr))
    {
        goto done;
    }

    // Populate the media buffer with the ASF Header Object.
    hr = pContentInfo->GenerateHeader(pHeaderBuffer, &cbHeaderSize);
    if (FAILED(hr))
    {
        goto done;
    }

    // Write the ASF header to the output file.
    hr = WriteBufferToByteStream(pWmaStream, pHeaderBuffer, &cbWritten);
    if (FAILED(hr))
    {
        goto done;
    }

    // Append the data stream to the file.

    hr = pDataStream->SetCurrentPosition(0);
    if (FAILED(hr))
    {
        goto done;
    }

    hr = AppendToByteStream(pDataStream, pWmaStream);

done:
    SafeRelease(&pHeaderBuffer);
    SafeRelease(&pWmaStream);
    return hr;
}
```



## 9. Define the Entry-Point Function

Now you can put the previous steps together into a complete application. Before using any of the Media Foundation objects, initialize the Media Foundation platform by calling [**MFStartup**](/windows/desktop/api/mfapi/nf-mfapi-mfstartup). When you are done, call [**MFShutdown**](/windows/desktop/api/mfapi/nf-mfapi-mfshutdown). For more information, see [Initializing Media Foundation](initializing-media-foundation.md).

The following code shows the complete console application. The command-line argument specifies the name of the file to convert and the name of the new audio file.


```C++
int wmain(int argc, WCHAR* argv[])
{
    HeapSetInformation(NULL, HeapEnableTerminationOnCorruption, NULL, 0);

    if (argc != 3)
    {
        wprintf_s(L"Usage: %s input.wmv, %s output.wma");
        return 0;
    }

    const WCHAR* sInputFileName = argv[1];    // Source file name
    const WCHAR* sOutputFileName = argv[2];  // Output file name
    
    IMFMediaType* pInputType = NULL;
    IMFASFContentInfo* pContentInfo = NULL;
    IMFASFMultiplexer* pMux = NULL;
    IMFByteStream* pDataStream = NULL;

    CWmaEncoder* pEncoder = NULL; //Pointer to the Encoder object.

    HRESULT hr = CoInitializeEx(
        NULL, COINIT_APARTMENTTHREADED | COINIT_DISABLE_OLE1DDE);

    if (FAILED(hr))
    {
        goto done;
    }

    hr = MFStartup(MF_VERSION);
    if (FAILED(hr))
    {
        goto done;
    }

    CWmaEncoder* pEncoder = NULL; //Pointer to the Encoder object.

    hr = OpenAudioFile(sInputFileName, &pInputType);
    if (FAILED(hr))
    {
        goto done;
    }

    // Initialize the WMA encoder wrapper.

    pEncoder = new (std::nothrow) CWmaEncoder();
    if (pEncoder == NULL)
    {
        hr = E_OUTOFMEMORY;
        goto done;
    }

    hr = pEncoder->Initialize();
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pEncoder->SetEncodingType(EncodeMode_CBR);
    if (FAILED(hr))
    {
        goto done;
    }

    hr = pEncoder->SetInputType(pInputType);
    if (FAILED(hr))
    {
        goto done;
    }

    // Create the WMContainer objects.
    hr = CreateASFContentInfo(pEncoder, &pContentInfo);
    if (FAILED(hr))
    {
        goto done;
    }

    hr = CreateASFMux(pContentInfo, &pMux);
    if (FAILED(hr))
    {
        goto done;
    }

    // Convert uncompressed data to ASF format.
    hr = EncodeData(pEncoder, pContentInfo, pMux, &pDataStream);
    if (FAILED(hr))
    {
        goto done;
    }

    // Write the ASF objects to the output file.
    hr = WriteASFFile(pContentInfo, pDataStream, sOutputFileName);

done:
    SafeRelease(&pInputType);
    SafeRelease(&pContentInfo);
    SafeRelease(&pMux);
    SafeRelease(&pDataStream);
    delete pEncoder;

    MFShutdown();
    CoUninitialize();

    if (FAILED(hr))
    {
        wprintf_s(L"Error: 0x%X\n", hr);
    }

    return 0;
} 
```



## Related topics

<dl> <dt>

[WMContainer ASF Components](wmcontainer-asf-components.md)
</dt> <dt>

[ASF Support in Media Foundation](asf-support-in-media-foundation.md)
</dt> </dl>

 

 


