---
title: "管线开发"
date: 2017-06-04T12:06:07+08:00
lastmod: 2017-06-04T12:06:07+08:00
draft: false
keywords: [MAF]
description: ""
tags: [C#]
categories: [DOTNET]

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: false
autoCollapseToc: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
# contentCopyright: true
reward: false
mathjax: false

---

### MAF (Managed Add-in Framework)

Host - HostViewOfAddIn - HostAdapter - AddInContract - AddInAdapter - AddInBase - AddIn

#### AddInContract
    [AddInContract]
    public interface [AddInContractName]:IContract

#### HostAdapter
    [HostAdapter]
    public class [HostAdapterName]:HostViewOfAddInName
通过 ContractHandle 调用 AddInContract

#### HostViewOfAddIn
    public interface [HostViewOfAddInName]

#### AddInAdapter
    [AddInAdapter]
    public class [AddInAdapterName]:AddInContractName
通过 AddInBaseName 调用 AddInName 的实现

#### AddInBase
    [AddInBase]
    public interface [AddInBaseName]

#### AddIn
    [AddIn("AddInName", Version = "x.x.x.x")]
    public class [AddInName]:AddInBaseName

Pipeline segment | Assembly and project references | Namespace and type references
---|---|---
Contract | System.AddIn.dll System.AddIn.Contract.dll | System.AddIn.Pipeline System.AddIn.Contract
Add-in view | System.AddIn.dll | System.AddIn.Pipeline
Add-in-side adapter | System.AddIn.dll System.AddIn.Contract.dll Add-in view segment Contract segment | System.AddIn.Pipeline
Host-side adapter | System.AddIn.dll System.AddIn.Contract.dll Host view segment Contract segment | System.AddIn.Pipeline
Host | System.AddIn.dll Host view segment | System.AddIn.Hosting host view
Add-In | System.AddIn.dll Add-in view segment | System.AddIn add-in view

### 目录结构

    Pipeline
      AddIns
        BooksAddIn
      AddInSideAdapters
      AddInViews
      Contracts
      HostSideAdapters