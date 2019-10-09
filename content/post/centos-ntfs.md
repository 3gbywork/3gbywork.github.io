---
title: "CentOS下挂载NTFS分区"
date: 2016-05-09T19:24:34+08:00
lastmod: 2016-05-09T19:24:34+08:00
draft: false
keywords: [CentOS, NTFS]
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

参考：[How to Mount an NTFS Filesystem](https://wiki.centos.org/TipsAndTricks/NTFS "访问 CentOS WiKi")

### 1. 安装所需的包

* CentOS-5:

        yum install fuse fuse-ntfs-3g

* CentOS-7 和 CentOS-6:

        yum install ntfs-3g
        // 其他功能
        yum install ntfsprogs ntfsprogs-gnomevfs

### 2. 挂载 NTFS 文件系统

* 创建挂载点：

        mkdir /mymnt/win

* 编辑 /etc/fstab，以只读方式挂载：

        /dev/sda1		/mymnt/win	ntfs-3g	ro,umask=0222,defaults 0 0

	以读写方式挂载：

        /dev/sda1		/mymnt/win	ntfs-3g	rw,umask=0000,defaults 0 0

* 挂载：

        mount /mymnt/win
