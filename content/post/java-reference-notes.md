---
title: "《Java 8 编程参考官方教程（第9版）》 读书笔记"
date: 2016-02-22T15:44:51+08:00
lastmod: 2016-02-22T15:44:51+08:00
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

### 1. Java基本类型

1） 整型

名称|宽度|范围
--|--
long|64|-9 223 372 036 854 775 808～9 223 372 036 854 775 807
int|32|-2 147 483 648~2 147 483 647
short|16|-32 768~32 767
byte|8|-128~127

Java不支持无符号的、只是正值的整数。

2） 圆括号（不管是否多余）不会降低程序的性能。所以，为了减少模糊性而添加圆括号，不会对程序造成负面影响。

3） switch语句需要注意的三个重要的特征：

1. switch语句只能进行相等性测试，与if语句不同，if语句可以对任何类型的布尔表达式进行求值
2. 在同一switch语句中，两个case常量不允许具有相同的值
3. 相对于一系列嵌套的if语句，switch语句通常效率更高

4） final关键字

1. 将变量声明为final，可以防止修改变量的内容，本质上就是将变量变成了常量
2. 将方法参数声明为final，可以防止在方法中修改参数
3. 将局部变量声明为final，可以防止多次为其赋值

final变量名全部使用大写，这是一种常见的编码约定。

5） varargs 可变长度参数

从JKD5开始，Java提供了一个新特性，该特性可以简化某种方法的创建，这种方法需要使用数量可变的参数。这个特性称为“varargs”。

可变长度参数通过三个句点（...）标识。这种语法告诉编译器，可以使用零个或更多个参数调用方法。所有，可变长度参数被隐式地声明为数组。

使用可变长度参数需要注意以下几点：

1. 可变长度参数必须是方法最好声明的参数
2. 只能有一个可变长度参数
