---
title: "Windows Mobile 6 模拟器如何联网"
date: 2016-04-23T10:25:53+08:00
lastmod: 2016-04-23T10:25:53+08:00
draft: false
keywords: [wm6]
description: ""
tags: [it]
categories: [HOWTO]

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

### 1. Windows Mobile 6 模拟器如何联网

首先，请确定电脑安装了 [Virtual Machine Network Services（Virtual PC 2007）](https://www.microsoft.com/en-us/download/details.aspx?id=4580 "点此下载") 驱动程序。

然后，设置模拟器网络

方式1： 在VS2008中选择【工具】-> 【选项】->在设备列表中选择合适的模拟器，点击【属性】->【仿真器选项】->【网络】->【启用NE2000 PCMCIA...】->【在下拉框中选择合适的网卡】，之后一路【确定】

方式2： 在模拟器窗口选择【文件】->【配置】->【网络】->【启用NE2000 PCMCIA...】->【在下拉框中选择合适的网卡】->【确定】

最后，配置模拟器IP地址

【开始】->【设置】->【连接】->【网卡】，在下拉框选择【默认 Internet 设置】，在下面的列表中点击【NE2000 兼容 Ethernet 驱动程序】配置IP地址和DNS。

之后就可以打开浏览器在网上冲浪了。
