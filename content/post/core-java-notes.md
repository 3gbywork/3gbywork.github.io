---
title: "《Java核心技术·基础知识（原书第9版）》 读书笔记"
date: 2016-02-17T13:43:17+08:00
lastmod: 2016-02-17T13:43:17+08:00
draft: false
keywords: [java, notes]
description: ""
tags: [java]
categories: [notes]

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

### 1. 类设计技巧

#### 1） 一定要保证数据私有

这是最重要的，绝对不要破坏封装性，最好保持实例域的私有性。

#### 2） 一定要对数据初始化

Java不对局部变量进行初始化，但是会对对象的实例域进行初始化。最好不要依赖于系统的默认值，而是应该显示的初始化所有的数据。

#### 3） 不要在类中使用过多的基本类型

用其他的类代替多个相关的基本类型的使用，这样会使类更加易于理解且易于修改。`ps：可以理解为将多个相关的基本类型封装成一个类来使用。`

#### 4） 不是所有的域都需要独立的域访问器和域更改器

在对象中，常常包含一些不希望别人获得或设置的实例域。

#### 5） 将职责过多的类进行分解

如果明显地可以将一个复杂的类分解成两个更为简单的类，就应该将其分解。但也不要走极端。

#### 6） 类名和方法名要能够体现它们的职责

命名类名的良好习惯是采用一个名词（Order）、前面有形容词修饰的名词（RushOrder）或动名词（有 "-ing" 后缀）修饰名词。

对于方法来说，习惯是访问器方法用小写`get`开头，更改器方法用小写`set`开头。

### 2. 关键字this和super的用途

#### 1） 关键字this有两个用途：

* 引用隐式参数
* 调用该类其他的构造器

#### 2） 关键字super也有两个用途：

* 调用超类的方法
* 调用超类的构造器

在调用构造器的时候，这两个关键字的使用方式很相似。调用构造器的语句只能作为另一个构造器的第一条语句出现。构造参数既可以传递给本类（this）的其他构造器，也可以传递给超类（super）的构造器。
