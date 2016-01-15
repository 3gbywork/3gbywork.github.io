---
title: 'C#使用ServiceController类操作Windows服务'
date: 2016-01-14 14:39:16
tags: "c#, WPF, Windows服务"
categories: "WPF"
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
