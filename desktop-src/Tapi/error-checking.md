---
description: At the TAPI level, an application can pass a variety of different parameters, many of which may be invalid.
ms.assetid: cc52e2a2-08e0-4a66-a75f-975e50dbf654
title: Error Checking (Telephony API)
ms.topic: article
ms.date: 05/31/2018
---

# Error Checking

At the TAPI level, an application can pass a variety of different parameters, many of which may be invalid. TAPI verifies parameters and returns errors to the application without calling the service provider. Each function description at the TSPI level describes the parameter errors already tested. The service provider does not have to repeat these tests, though it must perform any additional validity tests appropriate to the function. Titles and descriptions of common parameter validity tests that appear in many functions are listed in the following table.



| Validity test       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pointer validity    | TAPI has already tested pointers to data storage to make sure that they point to readable or writable memory of the size appropriate to the operation. In addition, for variably sized data structures starting with a **dwTotalSize** member, the data structure has been verified to ensure that the indicated total size is available.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| Fixed size validity | For variable-sized data structures, the data structure has been verified so space for the fixed-sized part of the data structure and that **dwTotalSize** is sufficient for the fixed part.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| Offset/size zeroed  | For variable-sized data structures, the "...**Offset**" and "...**Size**" fields that correspond to parts that the service provider sets have been preset with zero values before the service provider was called.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Handle validity     | TAPI ensures that line, phone, and call handles (of defined types [HDRVLINE](hdrvline.md), [HDRVPHONE](hdrvphone.md), and HDRVCALL) are valid. That is, they are values that have been returned without error as handles in [**TSPI\_lineOpen**](/windows/win32/api/tspi/nf-tspi-tspi_lineopen), [**TSPI\_phoneOpen**](/windows/win32/api/tspi/nf-tspi-tspi_phoneopen), or one of the following that starts the lifetime of a call handle: [**TSPI\_lineMakeCall**](/windows/win32/api/tspi/nf-tspi-tspi_linemakecall)<br/> [**TSPI\_lineCompleteTransfer**](/windows/win32/api/tspi/nf-tspi-tspi_linecompletetransfer)<br/> [**TSPI\_lineForward**](/windows/win32/api/tspi/nf-tspi-tspi_lineforward)<br/> [**TSPI\_linePickup**](/windows/win32/api/tspi/nf-tspi-tspi_linepickup)<br/> [**TSPI\_linePrepareAddToConference**](/windows/win32/api/tspi/nf-tspi-tspi_lineprepareaddtoconference)<br/> [**TSPI\_lineSetupConference**](/windows/win32/api/tspi/nf-tspi-tspi_linesetupconference)<br/> [**TSPI\_lineSetupTransfer**](/windows/win32/api/tspi/nf-tspi-tspi_linesetuptransfer)<br/> [**TSPI\_lineUnpark**](/windows/win32/api/tspi/nf-tspi-tspi_lineunpark)<br/> [**LINE\_NEWCALL**](line-newcall.md) messages<br/> |



 

 
