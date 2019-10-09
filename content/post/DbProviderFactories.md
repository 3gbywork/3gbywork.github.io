---
title: "Obtaining a DbProviderFactory"
date: 2016-10-15T00:39:17+08:00
lastmod: 2016-10-15T00:39:17+08:00
draft: false
keywords: [DbProviderFactory]
description: ""
tags: [C#, ADO.NET]
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

### 1、注册DbProviderFactory

在 machine.config 或 app.config 或 web.config 中存储提供程序和连接字符串信息。

下面以 SQLite 的配置为例，说明具体配置过程：

#### 1、在 app.config 中的配置文件片段

    <configuration>
      <system.data>
        <DbProviderFactories>
          <remove invariant="System.Data.SQLite" />
          <add name="SQLite Data Provider" invariant="System.Data.SQLite"
                description=".NET Framework Data Provider for SQLite"
                type="System.Data.SQLite.SQLiteFactory, System.Data.SQLite" />
        </DbProviderFactories>
      </system.data>
      <connectionStrings>
      <add name="Sqlite" providerName="System.Data.SQLite" connectionString="test.db" />
      </connectionStrings>
    </configuration>

#### 2、获取 DbFactory 对象

  只需传入参数 "System.Data.SQLite" 到 DbProviderFactories.GetFactory() 方法即可

#### 3、一些需要注意的地方

SQLite 分为 32-bit 和 64-bit，Precompiled Binaries 也分为 带bundle 和 不带bundle

* 对于带bundle的，表示动态库是混合模式编译的，只需 `System.Data.SQLite.dll` 文件即可
* 对于不带bundle的，除了 `System.Data.SQLite.dll` 文件还需要复制相应的 `SQLite.Interop.dll`文件

还有一点需要注意的是，工程中目标平台与SQLite的对应关系

* Any CPU 和 x86 对应 SQLite 32-bit
* x64 则对应 SQLite 64-bit
* 如果选择不带bundle的SQLite，则文件组织结构如下：

```
--System.Data.SQLite.dll
--x86 Folder
  --SQLite.Interop.dll 32-bit
--x64 Folder
  --SQLite.Interop.dll 64-bit
```
