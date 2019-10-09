---
title: "使用ServiceController类操作Windows服务"
date: 2016-01-14T14:39:16+08:00
lastmod: 2016-01-14T14:39:16+08:00
draft: false
keywords: [ServiceController]
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

ServiceController类位于.Net Framework类库、System.ServiceProcess命名空间，使用时需要添加对`System.ServiceProcess.dll`的引用。

**以下列举几个常用的属性和方法**

### 1. 属性

名称|说明
---|---
CanPauseAndContinue|获取一个值，该值指示是否可以暂停和继续服务
CanStop|获取一个值，该值指示服务在启动后是否可以停止
ServiceName|获取或设置对此实例引用的服务进行标识的名称
Status|获取由此实例引用的服务的状态

#### ServiceControllerStatus 枚举

成员名称|说明
---|---
ContinuePending|服务即将继续
Paused|服务已暂停
PausePending|服务即将暂停
Running|服务正在运行
StartPending|服务正在启动
Stopped|服务未运行
StopPending|服务正在停止


### 2.方法

名称|说明
---|---
GetDevices()|检索本地计算机上的设备驱动程序服务
GetServices()|检索本地计算机上的所有服务（设备驱动程序服务除外）
Close()|断开此 ServiceController 实例与服务的连接，并释放此实例分配的所有资源
ExecuteCommand(Int32)|对服务执行自定义命令
Refresh()|通过将属性重置为其当前值来刷新属性值
Start()|启动服务
Pause()|挂起服务的操作
Continue()|在服务暂停后继续该服务
Stop()|停止该服务以及任何依赖于该服务的服务

**如何获得管理员权限**

对服务的管理需要系统管理员权限，在程序中获取管理员权限需要配置`app.manifest`文件。

`app.manifest`文件在`Properties`目录下。如果没有，请按以下步骤操作：

1. 在`VS解决方案浏览器`右键项目属性
2. 选择 `Security（安全）` 选项
3. 勾选 `Enable ClickOnce security settings（启用ClickOnce安全设置）` 选项
4. `VS`会在`Properties`目录下生成`app.manifest`文件
5. 取消勾选 `Enable ClickOnce security settings（启用ClickOnce安全设置）` 选项

修改`app.manifest`文件，将

    <requestedExecutionLevel level="asInvoker" uiAccess="false" />

改为：

    <requestedExecutionLevel level="requireAdministrator" uiAccess="false" />

之后保存，重新编译。

运行程序后会弹出`用户帐户控制`对话框，点击确定，程序将获得管理员权限；点击取消，程序将退出。
