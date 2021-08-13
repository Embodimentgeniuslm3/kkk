---
description: Per-user event generated by an Instant Messaging client when contact information is added, changed, or removed in Parental Controls.
ms.assetid: 0a016542-306e-48b4-8b0c-b9e4e915513e
title: WPCEVENT_IM_CONTACT event (Wpcevent.h)
ms.topic: reference
ms.date: 05/31/2018
---

# WPCEVENT\_IM\_CONTACT event

Per-user event generated by an Instant Messaging client when contact information is added, changed, or removed in Parental Controls.


```C++
const EVENT_DESCRIPTOR WPCEVENT_IM_CONTACT = {0xf, 0x0, 0x10, 0x4, 0x16, 0xf, 0x8000000000000030};
```



## Parameters

<dl> <dt>

*AppName* 
</dt> <dd>

The name of the instant messaging application that is generating the event.

</dd> <dt>

*AppVersion* 
</dt> <dd>

The version of the application that is generating the event.

</dd> <dt>

*AccountName* 
</dt> <dd>

The instant messaging account name for this user.

</dd> <dt>

*OldName* 
</dt> <dd>

The previous instant messaging account name, if deleted or changed.

</dd> <dt>

*OldID* 
</dt> <dd>

The ID associated with the previous instant messaging account name.

</dd> <dt>

*NewName* 
</dt> <dd>

The new instant messaging account name, if added or changed.

</dd> <dt>

*NewID* 
</dt> <dd>

The ID that is associated with the new instant messaging account name.

</dd> <dt>

*Reason* 
</dt> <dd>

A value of the [**WPCFLAG\_ISBLOCKED**](/windows/win32/api/wpcevent/ne-wpcevent-wpcflag_isblocked) enumeration that indicates information about what events are blocked from use and what controls are in place.

</dd> </dl>

## Requirements



| Requirement | Value |
|-------------------------------------|---------------------------------------------------------------------------------------|
| Minimum supported client<br/> | Windows Vista \[desktop apps only\]<br/>                                        |
| Minimum supported server<br/> | None supported<br/>                                                             |
| Header<br/>                   | <dl> <dt>Wpcevent.h</dt> </dl> |



## See also

<dl> <dt>

[Using Logging APIs for Parental Controls](using-logging-apis-for-parental-controls.md)
</dt> <dt>

[**WPC\_ARGS\_CONVERSATIONINITEVENT**](/windows/win32/api/wpcevent/ne-wpcevent-wpc_args_conversationinitevent)
</dt> </dl>

 

 



