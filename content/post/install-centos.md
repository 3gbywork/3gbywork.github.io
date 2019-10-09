---
title: "通过U盘安装CentOS"
date: 2016-01-14T15:07:38+08:00
lastmod: 2016-01-14T15:07:38+08:00
draft: false
keywords: [CentOS]
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

把`iso`镜像文件解压到`FAT32`格式的分区根目录下

用U盘引导系统，进入Grub命令行模式，输入如下命令：

    root (hd0,x)    //CentOS所在分区
    //N=x+1
    kernel /isolinux/vmlinuz0 root=live:/dev/sdbN liveimg quiet rhgb rootfstype=auto
    initrd /isolinux/initrd0.img
    boot
