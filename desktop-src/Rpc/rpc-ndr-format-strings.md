---
title: RPC NDR Format Strings
description: Remote Procedure Call (RPC) NDR format strings.
ms.assetid: 9c83a039-49d3-491d-8110-29d1548730de
ms.topic: article
ms.date: 05/31/2018
---

# RPC NDR Format Strings

## NDR Engine: 32-bit Interpreter

This document describes the format string descriptors, sometimes referred to as MOPs, for the 32-bit NDR engine. This section describes changes associated with the evolution from the [**–Oi**](/windows/desktop/Midl/-oi) interpreter to the **–Oif** interpreter layer, as well as additions related to pipes and asynchronous support.

This document describes current Microsoft Interface Definition Language (MIDL) technology from the engine perspective, and the current NDR engine.

## Overview

The NDR engine is the marshaling engine of the Remote Procedure Call (RPC) and DCOM components. It handles all stub-related issues of a remote call. As a process, NDR marshaling is driven by the C code from MIDL-generated stubs, a MIDL JIT-type generator, or by stubs generated by other tools or written manually. In turn, the NDR engine drives the underlying run time (DCOM or RPC) that communicates with specific transports.

The original goal of the design had been to provide a tool for effective marshaling for arbitrary data, based on information provided by the MIDL compiler. The format strings described in this document—and indeed all information generated by the compiler for NDR engine consumption—have always been considered an internal interface between the compiler and the engine. Similarly, interfaces available to the engine to handle run-time issues are also mostly internal (some exceptions exist on the RPC run-time side, and some DCOM interfaces used by the engine are external).

Two typical approaches to marshaling have always been inline and data-driven (interpreted) technology. MIDL supports both through its [**–Os**](/windows/desktop/Midl/-os) and [**–Oi\***](/windows/desktop/Midl/-oi) switches in its C-generated stubs. In addition, MIDL can generate the TLB libraries used by the oleautomation package. Accordingly, one perspective of the engine's internals is that it consists of two parts.

The first is a set of routines that handle sizing, marshaling, and so on, corresponding to typical data type objects like a structure or an array. These routines are fine-tuned for performance; for example, they typically attempt to block-copy data wherever possible. This part is often referred to as the core NDR engine.

The second part consists of an interpreter and its related pieces. The interpreter uses routines from the core NDR engine, as if from an internal library, in order to execute a remote call with all its arguments marshaled and unmarshaled, as appropriate.

The core NDR engine is used in a similar manner whether used from inline stubs or from the interpreter. All core engine routines depend on the state passed in by a stub message structure. The structure is set up appropriately by the inline stub or by the interpreter. Over the years the core engine had been used in a different context; currently the interpreter is actually a set of several distinct interpreter loops. These are related to the old and new ([**–Oi**](/windows/desktop/Midl/-oi) versus **–Oif**) interpreters, as well as to loops related to data serialization (pickling), RPC async support and DCOM async support (RPC and DCOM have different asynchronous programming models).

Beyond the addition of new features, an important aspect of the NDR engine evolution is a general shift in the approach to interpreters. NDR version1.1 began as part of a new MIDL 2.0 approach to marshaling, with the inline stubs being preferred for performance considerations. With the most recent version of NDR, [**–Oif**](/windows/desktop/Midl/-oi) has become the most widely used mode of the compiler, almost to the exclusion of inline stubs.

RPC NDR Engine format string descriptors are described in more detail in the following topics:

-   [Format Strings](format-strings.md)
-   [Procedure Format Strings](procedure-format-strings.md)
-   [Procedure Header Descriptor](procedure-header-descriptor.md)
-   [Handles](handles.md)
-   [The Header](the-header.md)
-   [Parameter Descriptors](parameter-descriptors.md)
-   [Type Format Strings](type-format-strings.md)

 

 