---
title: Enumerating Resources
description: This topic discusses the functions used to obtain lists of resources.
ms.assetid: 388deaa1-3b04-43fa-aad2-8b52376d570c
ms.topic: article
ms.date: 05/31/2018
---

# Enumerating Resources

In certain situations application developers may want to discover the resource contents of an unknown Portable Executable (PE) module. The Windows SDK provides resource enumeration functions that enable an application to obtain lists of resource types, names, and languages in a specified module. The [**EnumResourceTypes**](/windows/desktop/api/Winbase/nf-winbase-enumresourcetypesa) and [**EnumResourceTypesEx**](/windows/win32/api/libloaderapi/nf-libloaderapi-enumresourcetypesexa) functions provide a list of resource types found in the module, the [**EnumResourceNames**](/windows/desktop/api/Winbase/nf-winbase-enumresourcenamesa) and [**EnumResourceNamesEx**](/windows/win32/api/libloaderapi/nf-libloaderapi-enumresourcenamesexa) functions provide the name of each resource within a given type, and the [**EnumResourceLanguages**](/windows/desktop/api/Winbase/nf-winbase-enumresourcelanguagesa) and [**EnumResourceLanguagesEx**](/windows/win32/api/libloaderapi/nf-libloaderapi-enumresourcelanguagesexa) functions provide the language of each resource of a given name and type. These functions and their associated callback functions enable applications to create a list of all resources in a module. This process is described in [Creating a Resource List](using-resources.md).

 

 