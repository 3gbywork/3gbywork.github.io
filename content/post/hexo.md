---
title: "使用Hexo搭建个人博客"
date: 2016-01-14T14:33:24+08:00
lastmod: 2016-01-14T14:33:24+08:00
draft: false
keywords: [Hexo, Next, Blog]
description: ""
tags: [staticgen]
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

### 1. 安装

#### 安装 Git

* Windows: [下载并安装](https://git-scm.com/download/win)
* Linux(Ubuntu, Debian): `sudo apt-get install git-core`
* Linux(Fedora, RedHat, CentOS): `sudo yum install git-core`

#### 安装 Node.js

* 使用 nvm 安装 Node.js

cURL:  
`$ curl -o- https://raw.github.com/creationix/nvm/master/install.sh | sh`

Wget:  
`$ wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh`

安装完成后，重启终端并执行下列命令即可安装 Node.js
    $ nvm install 4

* 使用 Node.js 安装程序安装

[下载并安装](https://nodejs.org/en/download/)

#### 安装 Hexo

    $ npm install -g hexo-cli

### 2. 建站

    $ hexo init <folder>
    $ cd <folder>
    $ npm install

### 3. 配置

#### 安装 NexT 主题

在 Hexo 站点目录下，使用下列命令安装 NexT 主题：

    $ git clone https://github.com/iissnan/hexo-theme-next themes/next

**两点重要说明：**
> 1. 站点配置文件： 站点根目录下的 `_config.yml` 文件
> 2. 主题配置文件： 主题目录下的 `_config.yml` 文件

#### 启用 NexT 主题

打开 站点配置文件，找到 `theme` 字段，将其值改为 `next`

#### 站点配置文件

    title: # 站点标题
    subtitle: # 站点副标题
    description: # 个人描述
    author: # 作者
    language: # zh-Hans | en | fr-FR | zh-hk | ru | de
    timezone: # 默认使用电脑的时区

    # 头像 （完整URL、相对地址）
    avatar: /uploads/avatar.jpg # 站点的 source/uploads/目录下
            /images/avatar.jpg  # 主题的 source/images/目录下

    # 网站图标
    # Place your favicon.ico to /source directory.
    favicon: /favicon.ico

    # Set default keywords (Use a comma to separate)
    keywords: "c#, WPF, NSIS, CentOS"

    # 站点建立时间
    since: 2015

    # 社交链接
    social:
      GitHub: https://github.com/你的用户名/
      博客园: http://www.cnblogs.com/你的站点名/

    # 社交图标
    social_icons:
      enable: true
      # Icon Mappings
      GitHub: github
      博客园: # 空白默认为类似地球的图标
      Weibo: weibo

    # 文章标题
    new_post_name: :year-:month-:day-:title.md # File name of new posts


#### 主题配置文件

    favicon: /favicon.ico       # 站点图标

    # 菜单栏
    menu:
      home: /                   # 首页
      categories: /categories   # 分类
      #about: /about
      archives: /archives       # 归档
      tags: /tags               # 标签
      #commonweal: /404.html

    # 主题样式
    # Schemes
    #scheme: Muse               # 个人栏在右（黑色） 标题栏（黑色）、菜单栏在上（白色）
    #scheme: Mist               # 个人栏在右（黑色） 标题栏、菜单栏在上（灰色）
    scheme: Pisces              # 个人栏（白色）、标题栏（黑色）、菜单栏在左（白色）

    # 代码高亮主题
    highlight_theme: night bright | night | night eighties | night blue | normal

#### 添加页面

*标签页面*

    hexo new page "tags"
    # 编辑刚新建的页面，修改如下：
    title: 标签
    date: 2016-01-13 17:24:51
    type: "tags"
    # 如果启动评论，需要在页面关闭评论，请添加如下字段：
    <!--comments:false-->
    # 在菜单栏中添加链接，参见主题配置文件

*分类页面*

    hexo new page categories    # 可以不加引号
    # 编辑页面，将页面类型设置为 categories
    # 在菜单栏中添加链接

*关于页面*

    hexo new page about
    # 其他操作同上

### 4. 在本地预览

#### 安装 hexo-server

    $ npm install hexo-server --save

#### 启动 hexo-server

    $ hexo s

之后打开浏览器，输入 'localhost:4000'，就可以先睹为快了。    

### 5. 部署到GitHub

#### 安装 hexo-deployer-git

    $ npm install hexo-deployer-git --save

#### 修改站点配置文件

    deploy:
      type: git
      repo: https://github.com/GitHub用户名/GitHub用户名.github.io.git
      branch: master    # 分支名
      message:          # 提交信息

#### 生成静态页面并部署到GitHub

    $ hexo g -d

### 6. 将博客源码上传到GitHub

在站点根目录下启动终端，执行如下操作：

    # 初始化Git
    $ git init
    # 创建新分支`src`作为保存博客源码的分支
    $ git checkout -b src
    $ git add .
    $ git commit -m "提交信息"
    # 添加远程仓库
    $ git remote add origin https://github.com/GitHub用户名/GitHub用户名.github.io.git
    # push到GitHub
    $ git push origin src

    # clone远程仓库
    $ git clone -b src https://github.com/GitHub用户名/GitHub用户名.github.io.git

以后就可以愉快的更新博客了。
