---
description: "Learn more about: JET_THREADSTATS.cLogRecord property"
title: JET_THREADSTATS.cLogRecord property  (Microsoft.Isam.Esent.Interop.Vista)
TOCTitle: 'cLogRecord property '
ms:assetid: P:Microsoft.Isam.Esent.Interop.Vista.JET_THREADSTATS.cLogRecord
ms:mtpsurl: https://msdn.microsoft.com/library/microsoft.isam.esent.interop.vista.jet_threadstats.clogrecord(v=EXCHG.10)
ms:contentKeyID: 39511382
ms.date: 07/30/2014
ms.topic: reference
f1_keywords:
- Microsoft.Isam.Esent.Interop.Vista.JET_THREADSTATS.cLogRecord
dev_langs:
- CSharp
- JScript
- VB
- other
api_name: 
- Microsoft.Isam.Esent.Interop.Vista.JET_THREADSTATS.cLogRecord
- Microsoft.Isam.Esent.Interop.Vista.JET_THREADSTATS.get_cLogRecord
- Microsoft.Isam.Esent.Interop.Vista.JET_THREADSTATS.set_cLogRecord
topic_type: 
- kbSyntax
- apiref
api_type: 
- Managed
api_location: 
- Microsoft.Isam.Esent.Interop.dll
ROBOTS: INDEX,FOLLOW

---

# JET_THREADSTATS.cLogRecord property

Gets the total number of transaction log records that have been generated by the database engine on the current thread.

**Namespace:**  [Microsoft.Isam.Esent.Interop.Vista](./microsoft.isam.esent.interop.vista-namespace.md)  
**Assembly:**  Microsoft.Isam.Esent.Interop (in Microsoft.Isam.Esent.Interop.dll)

## Syntax

``` vb
'Declaration
Public Property cLogRecord As Integer
    Get
    Friend Set
'Usage
Dim instance As JET_THREADSTATS
Dim value As Integer

value = instance.cLogRecord
```

``` csharp
public int cLogRecord { get; internal set; }
```

#### Property value

Type: [System.Int32](/dotnet/api/system.int32)  

## See also

#### Reference

[JET_THREADSTATS structure](./jet-threadstats-structure2.md)

[JET_THREADSTATS members](./jet-threadstats-members.md)

[Microsoft.Isam.Esent.Interop.Vista namespace](./microsoft.isam.esent.interop.vista-namespace.md)