---
description: IStats::Connect method - The Connect method connects the NPP to the network by using a specified NIC and provides configuration information for the connection.
ms.assetid: 29a12df7-9c81-40ff-ac12-33ce1de833b1
title: IStats::Connect method (Netmon.h)
ms.topic: reference
ms.date: 05/31/2018
topic_type: 
- APIRef
- kbSyntax
api_name: 
- IStats.Connect
api_type: 
- COM
api_location: 
- Ndisnpp.dll
- Rmtnpp.dll
---

# IStats::Connect method

The **Connect** method connects the NPP to the network by using a specified NIC and provides configuration information for the connection.

## Syntax


```C++
HRESULT STDMETHODCALLTYPE Connect(
  [in]  HBLOB  hInputBlob,
  [in]  LPVOID StatusCallbackProc,
  [in]  LPVOID UserContext,
  [out] HBLOB  hErrorBlob
);
```



## Parameters

<dl> <dt>

*hInputBlob* \[in\]
</dt> <dd>

Handle to the BLOB that specifies the NIC that the NPP connects to and the configuration information for that connection.

</dd> <dt>

*StatusCallbackProc* \[in\]
</dt> <dd>

Address of the user's callback function, which receives status updates such as triggers. If a callback function is not used, set this parameter and the *UserContext* parameter to **NULL**.

</dd> <dt>

*UserContext* \[in\]
</dt> <dd>

Value passed when the user's callback function is called. The value of this parameter is typically either HWND or a 'this' pointer. If a callback function is not specified, set this parameter and the *StatusCallbackProc* parameter to **NULL**.

</dd> <dt>

*hErrorBlob* \[out\]
</dt> <dd>

Handle to an error BLOB that contains additional error information.

</dd> </dl>

## Return value

If the method is successful, the return value is NMERR\_SUCCESS.

If the method is unsuccessful, the return value is one of the following error codes (which include those errors returned by the internal **IStats::Configure** call):



<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Return code</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><dl> <dt><strong>NMERR_ALREADY_CONNECTED</strong></dt> </dl></td>
<td>This instance of the NPP COM object is already connected to the network.<br/></td>
</tr>
<tr class="even">
<td><dl> <dt><strong>NMERR_BLOB_CONVERSION_ERROR</strong></dt> </dl></td>
<td>The configuration BLOB is corrupt. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="odd">
<td><dl> <dt><strong>NMERR_BLOB_ENTRY_DOES_NOT_EXIST</strong></dt> </dl></td>
<td>The input BLOB specified by the <em>hInputBlob</em> parameter lacks an entry needed to perform this operation. This error might be generated by the <strong>IStats::Connect</strong> or <strong>IStats::Configure</strong> call. Look at the error BLOB returned by <em>hErrorBlob</em> to determine which entry was not found.<br/></td>
</tr>
<tr class="even">
<td><dl> <dt><strong>NMERR_BLOB_NOT_INITIALIZED</strong></dt> </dl></td>
<td>The <strong>CreateBlob</strong> function has not been called. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="odd">
<td><dl> <dt><strong>NMERR_BLOB_STRING_INVALID</strong></dt> </dl></td>
<td>The string is not null-terminated. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="even">
<td><dl> <dt><strong>NMERR_ILLEGAL_TRIGGER</strong></dt> </dl></td>
<td>The trigger portion of the input BLOB is corrupt. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="odd">
<td><dl> <dt><strong>NMERR_INVALID_BLOB</strong></dt> </dl></td>
<td>The object specified in <em>hInputBlob</em> is not a BLOB. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="even">
<td><dl> <dt><strong>NMERR_NO_DEFAULT_CAPTURE_DIRECTORY</strong></dt> </dl></td>
<td>The default capture directory was not set in the registry. To set the capture directory, use the following path. <br/>
<pre class="syntax" data-space="preserve"><code>HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\nm\Parameters\CapturePath</code></pre></td>
</tr>
<tr class="odd">
<td><dl> <dt><strong>NMERR_OUT_OF_MEMORY</strong></dt> </dl></td>
<td>The memory required to perform this operation was unavailable. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="even">
<td><dl> <dt><strong>NMERR_TIMEOUT</strong></dt> </dl></td>
<td>The request has timed out. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
<tr class="odd">
<td><dl> <dt><strong>NMERR_UPLEVEL_BLOB</strong></dt> </dl></td>
<td>The version number of the BLOB specified in <em>hInputBlob</em> is incorrect. This error is generated by the <strong>IStats::Configure</strong> call.<br/></td>
</tr>
</tbody>
</table>



 

## Remarks

When the **Connect** method is called, Network Monitor automatically calls the **IStats::Configure** method by using the BLOB provided by the *hInputBlob* parameter. Note that any error codes returned by the call to **IStats::Configure** are passed back and returned by the **IStats::Connect** call.

This method must be called before you can start capturing frames. Note that when you connect to the network by using this method, you must continue to use the **IStats** interface to capture frames.

The input BLOB specified by *hInputBlob* can be obtained by calling the **GetNPPBlobFromUI**, **GetNPPBlobTable**, and **SelectNPPBlobFromTable** methods.

The error BLOB returned by the *hErrorBlob* parameter contains entries that Network Monitor could not understand or find in the input BLOB specified in *hInputBlob*. The returned error BLOB contains error information that the application can use for troubleshooting. For example, if NMERR\_BLOB\_ENTRY\_DOES\_NOT\_EXIST is returned, the entry that Network Monitor could not find is included in the returned error BLOB.



| For information about                                             | See                                                                          |
|-------------------------------------------------------------------|------------------------------------------------------------------------------|
| Obtaining the input BLOB that represents a network interface card | [Selecting a Network Interface Card](selecting-a-network-interface-card.md) |



 

## Requirements



| Requirement | Value |
|-------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows 2000 Professional \[desktop apps only\]<br/>                                                                                               |
| Minimum supported server<br/> | Windows 2000 Server \[desktop apps only\]<br/>                                                                                                     |
| Header<br/>                   | <dl> <dt>Netmon.h</dt> </dl>                                                                      |
| DLL<br/>                      | <dl> <dt>Ndisnpp.dll; </dt> <dt>Rmtnpp.dll</dt> </dl> |



## See also

<dl> <dt>

[IStats](istats.md)
</dt> <dt>

[IStats::Configure](istats-configure.md)
</dt> <dt>

[IStats::Disconnect](istats-disconnect.md)
</dt> <dt>

[Network Monitor BLOBS](network-monitor-blobs.md)
</dt> </dl>

 

 



