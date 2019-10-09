---
title: "C#编程技巧"
date: 2016-02-18T17:00:42+08:00
lastmod: 2016-02-18T17:00:42+08:00
draft: false
keywords: [C#]
description: ""
tags: [C#]
categories: [DOTNET]

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

### 0. C#编程规则

1) 关于标识符的规则

* 尽管可以包含数字字符，但它们必须以字母或下划线开头。
* 不能把 C#关键字用作标识符。如果需要把某一保留字用作标识符，那么可以在标识符的前面加上前缀符号@，告知编译器其后的内容是一个标识符。如：abstract是C#关键字，@abstract有效的标识符。

2) 命名约定

#### Pascal 大小写形式的命名约定
- 名称空间和类，以及基类中的成员等的名称，如：`EmployeeSalary`
- 在C#中常量（其他语言中常常全部大写）的名称，如：`const int MaximumLength;`

#### camel 大小写形式的命名约定
- 类型中所有私有成员字段的名称，如：`private int _subscriberId;`注意前缀名常常用一条下划线开头
- 传递给方法的所有参数的名称，如：`public void RecordSale(string salesmanName, int quantity);`

3) 名称空间的名称

Microsoft建议使用如下的名称空间：`<CompanyName>.<TechnologyName>`

4) 属性和方法的使用

满足以下所有条件，就把它设置为属性，否则就应使用方法：

- 客户端代码应能读取它的值，最好不要使用只写属性
- 读取该值不应花太长的时间
- 读取该值不应有任何细微的和不希望的负面效应
- 可以按照任何顺序设置属性
- 顺序读取属性也应有相同的效果

5) 字段的用法

字段的用法非常简单。 字段应总是私有的，但在某些情况下也可以把常量或只读字段设置为公有。 原因是如果把字段设置为公有，就不利于在以后扩展或修改类。

### 1. 帮助文件制作与显示

帮助文件一般是`chm`格式的文件，这里介绍的是如何将“相关人员”制作的`word`文档转化为`chm`文件：

网上有一款`word2chm`软件个人认为很好用，虽然界面看起来很`low`，但是好用、易用是一大特色。

有兴趣的朋友[点此]("http://pan.baidu.com/s/1kUd9Pl1" "Word2Chm 百度网盘 提取密码：p466")下载，使用方法就不赘述了。

附上版权声明样例：

    Copyright&copy; 2015-2016 <a class="moLink" href="" target="_blank">公司</a>, 
    All rights reserved.<br />
    Powered by <a href="http://3gbywork.github.io" target="_blank">3gbywork</a>

*下面结合VS工程做详细说明：*

添加`help.chm`帮助文件到`Resources.resx`资源文件中，在程序中可以通过以下方法生成`help.chm`并打开：

    // 程序所在路径
    string path = Environment.CurrentDirectory + "/Doc";
    string file = path + "/help.chm";
    
    // 判断帮助文件是否存在，不存在则创建
    if (!File.Exists(file))
    {
        try
        {
            // 如果存在 help.chm 文件夹则删除
            if (Directory.Exists(file))
                Directory.Delete(file);
            // 如果不存在 Doc 文件夹则创建
            if (!Directory.Exists(path))
                Directory.CreateDirectory(path);
            // 将帮助文件写入到当前路径的Doc目录下
            // 并以 help.chm 命名
            byte[] help = Properties.Resources.help;
            FileStream fs = new FileStream(file, 
            FileMode.Create, FileAccess.Write);
            fs.Write(help, 0, help.Length);
            fs.Flush();
            fs.Close();
        }
        catch (Exception exp)
        {
            MessageBox.Show(exp.Message, "错误！", 
            MessageBoxButton.OK, MessageBoxImage.Error);
        }
    }
    // 如果文件存在则打开
    if (File.Exists(file))
        Process.Start(file);

![添加帮助文件到工程中](/images/vs_help.png "添加帮助文件到工程中")

也可将帮助文件添加到VS工程中，并将`help.chm`文件属性的`Build Action`设为`Content`，`Copy to Output Directory`设为`Copy always`，参见上图。

这样每次编译时，VS就会把`help.chm`复制到输出目录下的`Doc`目录下。

### 2. 扩展方法

扩展方法被定义为静态方法，但它们是通过实例方法语法进行调用的。它们的第一个参数指定该方法作用于哪个类型，并且该参数以 this 修饰符为前缀。仅当你使用 using 指令将命名空间显式导入到源代码中之后，扩展方法才位于范围中。

    namespace CustomExtensions
    {
        //Extension methods must be defined in a static class
        public static class StringExtension
        {
            // This is the extension method.
            // The first parameter takes the "this" modifier
            // and specifies the type for which the method is defined.
            public static int WordCount(this String str)
            {
                return str.Split(new char[] {' ', '.','?'}, StringSplitOptions.RemoveEmptyEntries).Length;
            }
        }
    }

    namespace Extension_Methods_Simple
    {
        //Import the extension method namespace.
        using CustomExtensions;
        class Program
        {
            static void Main(string[] args)
            {
                string s = "The quick brown fox jumped over the lazy dog.";
                //  Call the method as if it were an 
                //  instance method on the type. Note that the first
                //  parameter is not specified by the calling code.
                int i = s.WordCount();
                System.Console.WriteLine("Word count of s is {0}", i);
            }
        }
    }

### 3. 实例化泛型对象

方法1：

    void Method<T>(T t) where T : new()
    {
        T tmp = new T();
    }

方法2：
    
    void Method<T>(T t)
    {
        T tmp = Activator.CreateInstance<T>();
    }

### 4. 限定泛型参数的超类

    // U是CLASSA类或是其子类
    // V是CLASSB类或是其子类
    void Method<U, V>(U u, V v) where U : CLASSA where V : CLASSB
    {
    }

### 5. 如何在 WPF 中引用 Winform 的控件

- 在 xaml 中使用

首先，添加对 `System.Windows.Forms.dll` 和 `WindowsFormsIntegration.dll` 的引用

然后在 xaml 文件中添加以下命名空间

    xmlns:wfi="clr-namespace:System.Windows.Forms.Integration;assembly=WindowsFormsIntegration"
    xmlns:wf="clr-namespace:System.Windows.Forms;assembly=System.Windows.Forms"

最后使用 Winform 控件时要这么写：

    <wfi:WindowsFormsHost>
        <wf:PropertyGrid x:Name="propertyGrid"/>
    </wfi:WindowsFormsHost>

- 在代码中使用

首先，添加对 `System.Windows.Forms.dll` 的引用

使用时推荐直接写出完整的命名空间（避免和 WPF 控件的命名空间冲突造成不明确的引用）

    System.Windows.Forms.PropertyGrid propertyGrid = new System.Windows.Forms.PropertyGrid();

### 6. 如何获取拖入窗口的文件路径

允许将文件拖入窗口

    <Window AllowDrop="True" Drop="Window_Drop">
    </Window>

处理拖拽事件

    private void Window_Drop(object sender, DragEventArgs e)
    {
        string filepath = "";
        // 判断拖入的是不是文件类型（文件夹亦可）
        if (e.Data.GetDataPresent(DataFormats.FileDrop))
        {
            // Array是抽象类，string[] 继承自 Array类
            Array arr = (Array)e.Data.GetData(DataFormats.FileDrop);
            string[] stra = (string[])e.Data.GetData(DataFormats.FileDrop);

            // 仅演示获取一个路径
            filepath = ((Array)e.Data.GetData(DataFormats.FileDrop)).GetValue(0).ToString();
            filepath = stra[0];
        }
    }

### 7. 使用 PropertyGrid 的一些小技巧

要在 PropertyGrid 中显示某个对象的属性，只需设置 PropertyGrid 的 SelectedObject 属性即可。

此时在 PropertyGrid 控件中显示的属性是指定对象的所有属性及其值。

设置属性的“可见”特性：

    // 指定某一属性或事件是否应在“属性”窗口中显示。
    [Browsable(false)]
    public string SomeProperties { get; set;}

设置属性的描述信息：

    // 指定属性或事件的描述。
    [DescriptionAttribute("属性的描述信息")]
    public string SomeProperties { get; set;}

设置属性的显示名称：

    // 指定属性、事件或不采用任何参数的公共 void 方法的显示名称。
    [DisplayNameAttribute("属性的显示名称")]
    public string SomeProperties { get; set;}

设置属性的只读特性：

    // 指定某个属性是否只能在设计时设置。
    [DesignOnlyAttribute(true)]
    public string SomeProperties { get; set;}

对属性进行分组：

    // 指定当属性或事件显示在一个设置为“按分类顺序”模式的 
	// PropertyGrid 控件中时，用于对属性或事件分组的类别的名称。
    // 在分组名称前加"\t"可以提高分组显示顺序，并且不会显示制表符
	[CategoryAttribute ("分组名称")]
    public string SomeProperties { get; set;}

### 8. using 关键字的两种用途

- 引用名称空间，如： `using System;`
- 给类和名称空间指定别名。如果名称空间的名称非常长，又要在代
码中多次引用，但不希望该名称空间的名称包含在 using 指令中(例如，避免类名冲突，就可以给该名称空间指定一个别名，其语法如下：`using alias = NamespaceName;`

### 9. 方法的命名参数

参数一般需要按定义的顺序传递给方法。命名参数允许按任意顺序传递。所有下面的方法：

    string FullName(string firstName, string lastName)
    {
        return firstName + " " + lastName;
    }

下面的方法调用会返回相同的全名：

	FullName("John", "Doe");
	FullName(lastName: "Doe", firstName: "John");
