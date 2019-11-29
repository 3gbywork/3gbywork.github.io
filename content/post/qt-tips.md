---
title: "Qt Tips"
date: 2019-11-26T17:11:25+08:00
lastmod: 2019-11-26T17:11:25+08:00
draft: false
keywords: [tips]
description: ""
tags: [Qt]
categories: [随笔]

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

记录一下在学习Qt的过程中，一些浅薄的认识。

## qmake

### 工程文件

扩展名|意义|备注
---|---|---
pro|**pro**ject             |普通工程文件
pri|**pr**oject **i**nclude |将pro中文件分成多个模块，或提取pro中共同的设置
prf|**pr**oject **f**eature |在Qt安装目录mkspecs下，如features/spec_post.prf
prl|**pr**oject **l**ink    |在Qt安装目录lib下

### [变量](https://doc.qt.io/qt-5/qmake-variable-reference.html)

常用指令|值|备注
---|---|---
CONFIG|release/debug<br>ordered<br>c++11<br>qt<br>windows<br>console<br>shared/dll<br>app_bundle|* Build mode, if both are specified, the last one takes effect.<br>* Specify build order when using the subdirs template.<br>* C11 support is enabled.<br>* The target is a Qt application or library and requires the Qt library and header files.<br>* The target is a Win32 window application (app only).<br>* The target is a Win32 console application (app only). For a cross-platform command line application, use cmdline.<br>* The target is a shared object/DLL.<br>* Puts the executable into a bundle (this is the default).
DEFINES|-|qmake adds the values of this variable as compiler C preprocessor macros (-D option).
DESTDIR|-|Specifies where to put the target file.
HEADERS|-|Defines the header files for the project.
RC_ICONS|myappico.ico|Setting the Application Icon on Windows
RC_FILE|myapp.rc|Setting the Application Icon on Windows<br>myapp.rc content:IDI_ICON1 ICON DISCARDABLE "myappico.ico"
ICON|myapp.icns|Setting the Application Icon on macOS
INCLUDEPATH|-|Specifies the #include directories which should be searched when compiling the project.
LIBS|-|Specifies a list of libraries to be linked into the project.
QT|-|Specifies the [Qt modules](https://doc.qt.io/qt-5/qtmodules.html) that are used by your project.
SOURCES|-|Specifies the names of all source files in the project.
[SUBDIRS](https://doc.qt.io/qt-5/qmake-variable-reference.html#subdirs)|-|This variable, when used with the subdirs template specifies the names of all subdirectories or project files that contain parts of the project that need to be built.
TARGET|-|Specifies the name of the target file. Contains the base name of the project file by default.
TEMPLATE|<br>app<br>lib<br>subdirs<br>aux|Specifies the name of the template to use when generating the project.<br>* Creates a Makefile for building applications (the default).<br>* Creates a Makefile for building libraries.<br>* Creates a Makefile for building targets in subdirectories.<br>* Creates a Makefile for not building anything. Use this if no compiler needs to be invoked to create the target; for instance, because your project is written in an interpreted language.
QMAKE_POST_LINK|-|Specifies the command to execute after linking the TARGET together.

### 函数

#### [Replace Functions](https://doc.qt.io/qt-5/qmake-function-reference.html)

qmake provides functions for processing the contents of variables during the configuration process. These functions are called replace functions. Typically, they return values that you can assign to other variables. You can obtain these values by prefixing a function with the $$ operator. Replace functions can be divided into built-in functions and function libraries.

常用函数|备注
---|---
shell_path(path)|转换path中目录分隔符以兼容当前shell，如在windows上，将'/'转为'\'
shell_quote(arg)|用""将arg包含起来以兼容当前shell，在windows上，如果arg中包含空格，则有"",否则没有
escape_expand(arg1 [, arg2 ..., argn])|扩展转义序列，如将'\r'转为'\\r'

#### [Test Functions](https://doc.qt.io/qt-5/qmake-test-function-reference.html)

Test functions return a boolean value that you can test for in the conditional parts of scopes. Test functions can be divided into built-in functions and function libraries.

常用函数|备注
---|---
CONFIG(config)|This function can be used to test for variables placed into the CONFIG variable.
contains(variablename, value)|Succeeds if the variable variablename contains the value value; otherwise fails.

### [高级用法](https://doc.qt.io/qt-5/qmake-advanced-usage.html)

#### Adding Compilers

```
new_moc.output  = moc_${QMAKE_FILE_BASE}.cpp
new_moc.commands = moc ${QMAKE_FILE_NAME} -o ${QMAKE_FILE_OUT}
new_moc.depend_command = g++ -E -M ${QMAKE_FILE_NAME} | sed "s,^.*: ,,"
new_moc.input = NEW_HEADERS
QMAKE_EXTRA_COMPILERS += new_moc
```

在实际使用中，需要注意input参数的值需要通过变量指定。测试直接指定不生效，不明原因。

### [undocumented](https://wiki.qt.io/Undocumented_QMake)

在spec_post.prf中定义的一些跨平台的变量，如：

* QMAKE_COPY
* QMAKE_COPY_DIR
* QMAKE_MOVE
* QMAKE_DEL_FILE
* QMAKE_DEL_DIR
* QMAKE_DEL_TREE
* QMAKE_CHK_EXISTS
* QMAKE_CHK_DIR_EXISTS
* QMAKE_MKDIR

> Hope this all makes your jobs a little easier...!

## [Qt **I**nstaller **F**rame**w**ork (IFW)][1]

客户端程序的安装包制作工具有很多，在windows平台上有：[NSIS](https://nsis.sourceforge.io)，[Inno Setup](http://www.jrsoftware.org/)，在Unix平台上各种包管理器：apt-get、yum。为了降低发布跨平台应用的成本，以及提供跨平台一致性用户体验，Qt提供了IFW。

IFW可分为Online Installer和Offline Installer或者两者兼而有之。一般情况下，如果需要安装的组件少可以做成离线安装包，然后在config.xml中添加Repository Url以便通过maintenance tool添加、更新、移除组件；如果组件比较多且其中有些组件是用户可选安装的，则可以做成在线安装包，这样既可以减少安装包大小，又可以减少用户下载大小及安装时长。

详细内容请参阅[官方手册][1]。

## 调整Qt应用程序目录

对于我们发布的Qt应用，通常是使用windeployqt抽取依赖的Qt库到应用程序根目录。这使得根目录变得“杂乱不堪”，而如果我们将Qt库放到单独文件夹则应用程序无法启动。

在windows平台，可以通过添加Qt库到环境变量Path中解决上述问题；或者更激进的做法，把Qt库放到windows目录或者system32/SysWOW64目录下。

当然，上述做法严重“污染”了系统的动态库“生态”。导致一系列不可预知的问题。

解决问题的最根本最核心的依据就是[windows动态库搜索顺序][2]。下面介绍一种比较正常的解决方案：

首先，我们需要一个启动程序，它用来设置当前进程的环境变量，将Qt库目录和其他Qt应用程序依赖的动态库目录设置到Path中，然后再通过CreateProcess启动Qt应用程序。注意lpEnvironment参数设置为空，这样子进程就会继承当前进程的环境变量。

这时Qt应用仍然不能启动，我们需要一个神奇的配置文件。在Qt应用所在的目录创建一个qt.conf文件，其内容如下：

```
[Paths]
Plugins = Path/To/Qt
```

经过上述两步，我们就可以通过启动程序来启动Qt应用了，看着变得干净清晰的目录，是不是很开心。

另外再说明一点，上述正常的解决方案在使用了激进做法的机器上是不能启动的，当然如果依赖的Qt版本一致则无问题。

遇到这种情况有两种解决方案：

1. 将Qt库重新放回到应用程序根目录
2. 要求客户将windows/system32/SysWOW64目录下的Qt库移除

## Qt编程

### QMetaEnum

像C#可以获取枚举名称、值、甚至枚举值的描述，对枚举进行遍历的操作。在Qt中，如果需要对枚举遍历时，枚举类型要满足以下要求：

1. 枚举类型声明在类中
2. 该类继承自QObject
3. 该类使用宏Q_OBJECT
4. 枚举通过Q_ENUM(YourEnumType)声明

满足以上要求的枚举可以通过QMetaEnum::fromType<YourEnumType>()获取到QMetaEnum对象，该对象可以实现对枚举的遍历、枚举名称和值互查。

### 隐藏类实现细节

Qt源码中有大量的Private类和d_ptr及q_ptr，这就是Qt中隐藏类实现细节的一种编程模式。

这种编程模式有如下好处：

1. 类对外接口更清晰，即头文件更简洁，只需声明类对外提供的接口即可。
2. 如果类的实现细节有更改，用户不必重新编译源程序，只需更新改动的类库即可。

以下是示例代码：

a.h

```
//前置声明
class APrivate;
class A
{
public:
    A();

private:
    APrivate *d_ptr;
    Q_DECLARE_PRIVATE(A)
};
```

a.c

```
class APrivate
{
public:
    APrivate(A *p) : q_ptr(p)
    {

    }

private:
    A *q_ptr;
    Q_DECLARE_PUBLIC(A)
};

class A
{
public:
    A() : d_ptr(new APrivate(this))
    {

    }
};
```

[1]: https://doc.qt.io/qtinstallerframework/index.html
[2]: https://docs.microsoft.com/en-us/windows/win32/dlls/dynamic-link-library-search-order#standard-search-order-for-desktop-applications