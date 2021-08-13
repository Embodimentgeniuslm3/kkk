---
title: WM_GET_LICENSE_DATA structure (Drmexternals.h)
description: The WM\_GET\_LICENSE\_DATA structure contains information about where to acquire a DRM license.
ms.assetid: 7e8053d5-f3f5-4519-97f5-6dbd89982f3a
keywords:
- WM_GET_LICENSE_DATA structure windows Media Format
topic_type:
- apiref
api_name:
- WM_GET_LICENSE_DATA
api_location:
- Drmexternals.h
api_type:
- HeaderDef
ms.topic: reference
ms.date: 05/31/2018
---

# WM\_GET\_LICENSE\_DATA structure

The **WM\_GET\_LICENSE\_DATA** structure contains information about where to acquire a [*DRM*](wmformat-glossary.md) [*license*](wmformat-glossary.md).

## Syntax


```C++
typedef struct _WMGetLicenseData {
  DWORD   dwSize;
  HRESULT hr;
  WCHAR   *wszURL;
  WCHAR   *wszLocalFilename;
  BYTE    *pbPostData;
  DWORD   dwPostDataSize;
} WM_GET_LICENSE_DATA;
```



## Members

<dl> <dt>

**dwSize**
</dt> <dd>

**DWORD** containing the size of the **WM\_GET\_LICENSE\_DATA** structure, in bytes.

</dd> <dt>

**hr**
</dt> <dd>

**HRESULT** return code.

</dd> <dt>

**wszURL**
</dt> <dd>

Wide-character null-terminated string containing the license acquisition URL. Use this string and the **pbPostData** string in non-silent license acquisition.

</dd> <dt>

**wszLocalFilename**
</dt> <dd>

Wide-character null-terminated string containing a local HTML page that is generated by the DRM component. When this string is loaded into a browser, it automatically redirects the HTTP request to the license acquisition URL, along with the necessary post data. Use of this local URL is now deprecated. The recommended approach is to use the **wszURL** and **pbPostData** strings.

</dd> <dt>

**pbPostData**
</dt> <dd>

Pointer to a byte array containing the data to be posted to the license acquisition URL. You must add the following string to the beginning of the **pbPostData** string: "nonsilent=1&challenge=". The resulting string should then be appended to **wszURL** when you form the HTTP request.

</dd> <dt>

**dwPostDataSize**
</dt> <dd>

**DWORD** that indicates the size of **pbPostData** without the "nonsilent=1&challenge=" string referred to in **pbPostData**.

</dd> </dl>

## Remarks

This filled-in structure is returned in the *pValue* parameter of the [**IWMStatusCallback::OnStatus**](/previous-versions/windows/desktop/api/Wmsdkidl/nf-wmsdkidl-iwmstatuscallback-onstatus) method if **WMT\_STATUS** equals **WMT\_NO\_RIGHTS\_EX** or **WMT\_ACQUIRE\_LICENSE**. For WMT\_NO\_RIGHTS\_EX events, the **hr** member will be NS\_E\_LICENSE\_REQUIRED, NS\_E\_LICENSE\_OUTOFDATE, or NS\_E\_LICENSE\_INCORRECT\_RIGHTS. Any of these errors indicates that a new license must be acquired by navigating to the URL in the **wszURL** member.

For WMT\_ACQUIRE\_LICENSE events, the **hr** member will pass the SUCCEEDED macro if a license was successfully acquired. If this event is received after an attempt at silent acquisition, and **hr** equals NS\_E\_DRM\_LICENSE\_NOTACQUIRED, it indicates that only non-silent acquisition is supported by the license server for this license.

The Audioplayer sample application demonstrates how to correctly use the information returned in this structure.

## Requirements



| Requirement | Value |
|-------------------------------------|-------------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows 2000 Professional \[desktop apps only\]<br/>                                |
| Minimum supported server<br/> | Windows 2000 Server \[desktop apps only\]<br/>                                      |
| Version<br/>                  | Windows Media Format 7 SDK, or later versions of the SDK<br/>                       |
| Header<br/>                   | <dl> <dt>Drmexternals.h</dt> </dl> |



## See also

<dl> <dt>

[**IWMDRMReader::AcquireLicense**](/previous-versions/windows/desktop/api/Wmsdkidl/nf-wmsdkidl-iwmdrmreader-acquirelicense)
</dt> <dt>

[**Structures**](structures.md)
</dt> </dl>

 

 




