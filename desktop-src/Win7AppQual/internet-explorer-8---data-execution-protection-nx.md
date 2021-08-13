---
Description: .
ms.assetid: 56a4889c-5dcf-416f-b46e-5c48277d5636
title: Internet Explorer 8 - Data Execution Protection/NX
ms.topic: article
ms.date: 05/31/2018
---

# Internet Explorer 8 - Data Execution Protection/NX

## Affected Platforms

<dl> **Clients** - Windows XP \| Windows Vista \| Windows 7  
**Servers** - Windows Server 2003 \| Windows Server 2008 \| Windows Server 2008 R2  
</dl>

> [!Note]  
> Internet Explorer 8 will enable DEP/NX protection when run on an operating system with the latest service pack. Windows XP SP3, Windows Server 2003 SP3, Windows Vista SP1, and Windows Server 2008 all have DEP/NX enabled by default in Internet Explorer 8.

 

## Feature Impact

<dl> **Severity** - Medium  
**Frequency** - Low  
</dl>

> [!Note]  
> Typically, any application that runs in Internet Explorer and is not compatible with DEP/NX will crash on startup and will not function. Internet Explorer may crash on startup if add-ons that are not compatible with DEP/NX are installed.

 

## Description

DEP/NX is a security feature that helps mitigate memory-related vulnerabilities. As of Internet Explorer 8, all Internet Explorer processes enable the DEP/NX feature by default.

## Manifestation of Impact

The Windows Kernel monitors a program's execution. If the Kernel detects an attempt to run code from a memory page that is not marked executable, the Kernel halts execution of the program, resulting in a "crash." This is a security measure to help ensure that memory-related vulnerabilities (for example, buffer overflows) in the application cannot be exploited in order to execute arbitrary code.

## End-User Mitigation

-   Install a later version of the add-on or framework that is DEP/NX compatible.
-   Run Internet Explorer elevated as Administrator, and then disable DEP/NX using the **Enable memory protection to help mitigate online attacks** check box on the **Internet Options** / **Advanced** tab.

## Developer Solution

Compile applications by using the latest versions of frameworks that are DEP compatible.

## Leveraging Feature Capabilities

-   Use the /NXCOMPAT linker option to indicate DEP/NX compatibility
-   Opt your code into other available defenses like stack defense (/GS), safe exception handling (/SafeSEH), and ASLR (/DynamicBase)

## Compatibility, Performance, Reliability, and Usability Testing

-   Test your code with DEP/NX enabled by using latest released Internet Explorer version on Windows Vista SP1 or later.
-   Test with Internet Explorer 7 on Windows Vista after enabling the DEP/NX option. To enable DEP/NX for Internet Explorer 7, run Internet Explorer as an administrator, then set the appropriate check box in the Tools > Internet Options > Advanced tab.
-   Run the Internet Explorer Compatibility Test Tool (IECTT), provided with the Application Compatibility Toolkit (ACT) to locate any potential issues due to the DEP/NX changes.

## Links to Other Resources

-   [Internet Explorer 8 Security Part I: DEP/NX Memory Protection](https://blogs.msdn.com/ie/archive/2008/04/08/ie8-security-part-I_3A00_-dep-nx-memory-protection.aspx)
-   [Data Execution Prevention](https://msdn.microsoft.com/library/Aa366553(v=VS.85).aspx)
-   [New NX APIs added to Windows Vista SP1, Windows XP SP3 and Windows Server 2008 R2](https://blogs.msdn.com/michael_howard/archive/2008/01/29/new-nx-apis-added-to-windows-vista-sp1-windows-xp-sp3-and-windows-server-2008.aspx)
-   [Application Compatibility Toolkit Download](https://www.microsoft.com/downloads/details.aspx?FamilyId=24DA89E9-B581-47B0-B45E-492DD6DA2971)
-   [Known Internet Explorer Security Feature Issues](https://technet.microsoft.com/library/cc722079.aspx)

 

 



