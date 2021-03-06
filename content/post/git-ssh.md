---
title: "使用Git生成SSH公钥"
date: 2016-02-17T14:14:55+08:00
lastmod: 2016-02-17T14:14:55+08:00
draft: false
keywords: [git, ssh]
description: ""
tags: [security]
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

### 1. 确认是否已经拥有密钥

    $ cd ~/.ssh						// 默认情况下SSH密钥存储地址
    $ ls

如果存在类似`id_rsa`（私钥）、`id_rsa.pub`（公钥）的文件，则说明曾经生成过SSH密钥。如果没有类似文件，则按一下步骤生成密钥。

### 2. 生成SSH密钥

    $ ssh-keygen -C "xxx@email"		// 默认使用rsa加密算法

根据提示输入密码或直接回车（密码为空）。

### 3. 添加公钥到GitHub

    $ vi ~/.ssh/id_rsa.pub

在正常模式下输入`v`、`$`、`y`，即可复制公钥，粘贴到GitHub即可。
