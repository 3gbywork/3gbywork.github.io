---
title: 通过U盘安装CentOSOS_LiveCD版
date: 2016-01-14 15:07:38
tags: "U盘安装CentOS"
categories: "CentOS"
---

把`iso`镜像文件解压到`FAT32`格式的分区根目录下

用U盘引导系统，进入Grub命令行模式，输入如下命令：

<pre><code class="prettyprint linenums">root (hd0,x)    //CentOS所在分区
//N=x+1
kernel /isolinux/vmlinuz0 root=live:/dev/sdbN liveimg quiet rhgb rootfstype=auto
initrd /isolinux/initrd0.img
boot
</code></pre>
