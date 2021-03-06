---
title: "使用NSIS打包应用程序"
date: 2015-12-28T14:25:52+08:00
lastmod: 2016-01-14T14:25:52+08:00
draft: false
keywords: [NSIS]
description: ""
tags: [package]
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

[NSIS](http://baike.baidu.com/view/1011444.htm "Nullsoft Scriptable Install System")是一个开源的Windows平台下的安装程序制作程序,由C/C++语言编写。想了解更多内容请访问[百度百科](http://baike.baidu.com/view/1011444.htm "NSIS 百度百科")。 

怎么获得NSIS呢？这里有[NSIS ANSI版本](http://sourceforge.net/projects/nsis/ "NSIS sourceforge 项目主页")和[NSIS Unicode版本](http://sourceforge.net/projects/nsisu/ "NSISu sourceforge 项目主页")下载地址。

安装完成后就可以编辑我们的脚本了。

我使用的是Notepad++这款文本编辑器，新建一个文件，`[Ctrl]+[Alt]+S` 将文件另存为扩展名为`.nsi`的文件，这样在我们编辑时就可以享受Notepad++提供的**代码高亮**和**自动完成**功能了。

### 1. 编码格式（乱码）问题

根据NSIS是ANSI版本还是Unicode版本来确定脚本的编码格式：

- ANSI版本： 在Notepad++的菜单栏选择`[格式]->[以ANSI格式编码]`  
- Unicode版本： `[格式]->[以UCS-2 Little Endian格式编码]`
  
如果文件中<font color=red>已有文本</font>，请选择<font color=red>`[转为...编码格式]`</font>，否则可能会导致编译出的安装程序显示乱码。

### 2. 多语言安装界面

引用NSIS安装目录下`Contrib\Language files\`的`.nlf`类型语言文件，并在初始化时添加语言选项，具体实现请看代码：

```
; 引用语言资源文件（注意文件路径）
LoadLanguageFile "SimpChinese.nlf"
LoadLanguageFile "English.nlf"

; 添加语言选项
Function .onInit
	Push ""
	Push ${LANG_ENGLISH}
	Push English
	Push ${LANG_SIMPCHINESE}
	Push "简体中文"
	Push A ; A means auto count languages
	       ; for the auto count to work the first empty push (Push "") must remain
	LangDLL::LangDialog "Installer Language" "Please select the language of the 
    installer"

	Pop $LANGUAGE
	StrCmp $LANGUAGE "cancel" 0 +2
		Abort
FunctionEnd
```

如果脚本中引用了`MUI2.nsh`头文件，则脚本代码如下：

```
; <font color=red>引用"MUI2.nsh"头文件的脚本</font>
!include "MUI2.nsh"

; 语言设置
!insertmacro MUI_LANGUAGE "English"
!insertmacro MUI_LANGUAGE "SimpChinese"

; 显示语言选项
Function .onInit
  !insertmacro MUI_LANGDLL_DISPLAY
FunctionEnd
```

### 3. 自定义变量的使用

假如我们的脚本中有多处使用软件名称，并且以后可能会更改软件名称，有什么简便的方法来避免复制、粘贴、替换吗？

当然有。对于这种情况，我们可以定义一个变量，并在初始化时给变量赋值，具体实现请看代码：

```
; 软件名称
Var SoftName

Function .onInit
	StrCpy $SoftName "XXX"
FunctionEnd

Function un.onInit
	StrCpy $SoftName "XXX"
FunctionEnd
```

### 4. 安装完成页面定制

在安装完成后，我们可能需要为用户提供可选的运行选项，如：运行XXX程序、打开Readme文件、访问XXX网站等。下面是`MUI_FINISHPAGE`支持的属性：
```
# 运行XXX程序
!define MUI_FINISHPAGE_RUN
!define MUI_FINISHPAGE_RUN_TEXT
!define MUI_FINISHPAGE_RUN_PARAMETERS
!define MUI_FINISHPAGE_RUN_NOTCHECKED   ;默认不选中
!define MUI_FINISHPAGE_RUN_FUNCTION

# 自述文件
!define MUI_FINISHPAGE_SHOWREADME
!define MUI_FINISHPAGE_SHOWREADME_TEXT
!define MUI_FINISHPAGE_SHOWREADME_NOTCHECKED 
!define MUI_FINISHPAGE_SHOWREADME_FUNCTION

# 访问XXX网站
!define MUI_FINISHPAGE_LINK
!define MUI_FINISHPAGE_LINK_LOCATION
!define MUI_FINISHPAGE_LINK_COLOR
```

引用`MUI2.nsh`头文件的例子：

```
; 引用MUI2.nsh头文件
!include "MUI2.nsh"

; 定义完成后要运行的程序
!define MUI_FINISHPAGE_RUN
!define MUI_FINISHPAGE_RUN_FUNCTION "runSoft"
!define MUI_FINISHPAGE_RUN_TEXT "运行 $SoftName"

Function "runSoft"
    /* 
    运行的程序，可以多个
    如果只运行一个程序，可以这么写：
    !define MUI_FINISHPAGE_RUN "$INSTDIR\XXX.exe" 
    */
FunctionEnd

; 自述文件
!define MUI_FINISHPAGE_SHOWREADME "readme.txt"
; 默认不选中自述文件复选框
!define MUI_FINISHPAGE_SHOWREADME_NOTCHECKED

; 访问XXX网站
!define MUI_FINISHPAGE_LINK "XXX"
!define MUI_FINISHPAGE_LINK_LOCATION "http://www.XXX.com"
; 文字颜色为红
!define MUI_FINISHPAGE_LINK_COLOR "FF0000"
```

### 5. 执行外部命令

1. Exec '"命令" [可选参数]'
2. ExecShell "动作" "命令" [参数] [SW_SHOWNORMAL | SW_SHOWMAXIMIZED | SW_SHOWMINIMIZED | SW_HIDE]
3. ExecWait '"命令"' [用户变量（返回代码）]
4. nsExec::Exec [参数]

### 6. 注册DLL组件

如果我们发布的程序中有动态链接库需要注册到系统中，下面代码是一个比较通用的例子，将安装目录下的所有`.dll`类型文件注册到系统：

```
; 注册安装目录下的所有DLL到系统中
FindFirst $0 $1 $INSTDIR\*.dll
loop:
	StrCmp $1 "" done
	DetailPrint $1
	RegDLL $INSTDIR\$1
	FindNext $0 $1
	Goto loop
done:
FindClose $0
```

### 7. 快捷方式

**生成快捷方式**

```
# 在桌面生成快捷方式
CreateShortCut "$DESKTOP\XXX.lnk" "$INSTDIR\XXX.exe"

# 在开始菜单生成快捷方式
CreateDirectory "$SMPROGRAMS\XXX"   ; 在开始菜单创建程序文件夹
CreateShortCut "$SMPROGRAMS\XXX\XXX.lnk" "$INSTDIR\XXX.exe"
CreateShortCut "$SMPROGRAMS\XXX\卸载XXX.lnk" "$INSTDIR\XXX.exe"

# 在快速启动栏生成快捷方式
CreateShortCut "$QUICKLAUNCH\XXX.lnk" "$INSTDIR\XXX.exe"

```

**删除快捷方式**

在Win7下创建快捷方式时，可能由于权限问题，快捷方式被创建到所有用户的路径，而不是当前用户的路径。XP不存在此问题。解决方法是：同时删除当前用户和所有用户路径下的快捷方式，示例代码如下：

```
# 设置为当前用户
SetShellVarContext current
Call <font color=red>un.</font>DeleteShortCut  ; 删除快捷方式函数
; <font color=red>注意：如果此段代码在'Section "Uninstall"'里，函数名前必须加un.</font>

# 设置为所有用户
SetShellVarContext all
Call <font color=red>un.</font>DeleteShortCut
```

删除快捷方式函数可以这样写：

```
# 删除桌面快捷方式
Delete "$DESKTOP\XXX.lnk"
# 删除快捷启动栏快捷方式
Delete "$QUICKLAUNCH\XXX.lnk"
# 删除开始菜单快捷方式文件夹
RMDir /r "$SMPROGRAMS\XXX"  /* /r递归删除目录 */
```

<br />

以上是我在使用NSIS过程遇到的一些问题，利用一些闲暇时间总结整理写出的这篇心得，以备不时之需。
