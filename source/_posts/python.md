### 安装python
至于安装python的方法呢，去官网看看就好，本来是准备安装的，但是发现Mac下有自带的python 不过版本有点低，更新一下就好了

### Python基础语法
python语言与Perl,C和java等语言有许多相似支持，但是也有一些差异

#### 中文编码，使用python编程，中文编码会报错，在文件的开头使用#coding=utf-8或者 # -*- coding: UTF-8 -*- 用来编写中文

#### 第一个python程序

###### 交互式编程

交互式编程不需要创建脚本文件是通过Python解释器的交互模式进来编写代码

linux上你只需要在命令行中输入Python命令即可启动交互式编程
    
    python
    Python 2.7.6 (default, Sep  9 2014, 15:04:36) 
    [GCC 4.2.1 Compatible Apple LLVM 6.0 (clang-600.0.39)] on darwin
    Type "help", "copyright", "credits" or "license" for more information.
    >>> 

    
window上在安装python时已经安装了默认的交互式编程客户端，在python提示符中输入以下文本信息，然后enter键查看运行效果

    print 'Hello World'

在Python2.7.6版本上输出结果如下

    Hello,python


### Python标识符

在python里，标识符有字母、数字、下划线组成

在python中，所有标识符可以包括英文、数字以及下划线，但不能以数字开头，python中的标识符是区分大小写的，以下划线开头的标识符是有特殊意义的，以单下划线开头(_foo)的代表不能直接访问的类属性，需通过类提供的接口进行访问，不能用'from xxx import'而导入。以爽下划线开图的(__foo)代表类的私有成员，以双下划线开头和结尾的(__foo__)代表python里特殊方法专用的标识，如__init__()代表类的构造函数


### Python 保留字符

`and  exec not assert finally or break for pass class from print continue global raise def if return del import try elif in while else is with except lambda yield`

#### 行和缩进

学习python与其他语言最大的区别就是,Python的代码块不适用大括号{}来控制类，函数以及其他逻辑判断，python最具特色的就是用缩进来写模块，缩进的空白数量是可变的，但是所有代码块语句必须包含相同的缩进空白数量，这个必须严格执行

    if True:
        print 'hello world'
        print 'this is a true answer'
    else:
        print 'this is the error'

如果没有按照严格模式使用tab键或者空格的话，执行文件会报错，所以在Python的代码块中必须使用相同的数目的行首缩进空格数，建议在每个缩进层次使用 单个制表符或两个空格或者是四个空格，切记不能混用

#### 多行语句

Python语句中一般以新行作为语句的结束符，但是我们可以使用斜杠(`\`)将一行的语句分为多行显示，

    total = item_one + \
            item_two + \
            item_three

语句中包含[],{}或()括号就不需要使用多行连接符
    
    days = ['Monday','Thuesday','Wednesday',
            'Thursday','Friday']

#### Python 引号

Python接收单引号(`''`)、双引号(`""`)、三引号(`'" 或者"""`)来表示字符串，引号的开始于结束必须的相同类型的，其中三引号可以由多行组成，编写多行文本的快捷语法，常用语文档字符串，在文件的特定地点，被当做注释。

    word = 'word'
    sentence = "这是一个句子"
    paragrapy = """这是一个段落。
    包含了多个语句"""

### Python注释

Python中单行注释采用#开头
    
    # 第一个注释
    print "Hello,Python" # 第二行注释    

输出结果:
    
    Hello,Python!

注释可以在语句或表达式行末

    name = "Madisetti" # 这是一个注释    

可使用''' 或者""" 注释多行

#### Python空行    
    
    函数之间或类的方法之间用空行分隔，表示一段新的代码的开始，雷和函数入口之间也用一行空行分隔，以突出函数入口的开始，空行与代码缩进不同，空行并不是python语法的一部分，书写时不插入空行，python解释器运行也不会报错，但是空行的作用记住"空行也是程序代码的一部分

#### 等待用户输入

下面的程序在按回车键就会等待用户输入

    #!/usr/bin/python

    raw_input("\n\nPress the enter key to exit.")

以上代码中，"\n\n"在结果输出前会输出两个新的空行，一旦用户按下enter(回车)键退出，其他键显示

#### 同一行显示多条语句

python可以在同一行中使用多条语句，语句之间使用分号;分割，

    #!/usr/bin/python

    import sys;x = 'runoob'; sys.stdout.write(x + '\n')

执行以上代码，输入结果为

    python test.py
    runoob

#### 多行语句构成代码组

缩进形同的一组语句构成一个代码块，我们称之代码组，像if、while、def和class这样的复合语句，首行以关键字开始，以冒号(`:`)结束，该行之后的一行货多行代码构成代码组，我们将首行以及后面的代码组成一个子句(clause)

    if expression :
        suite
    elif expression :
        suite
    else :
        suite

#### 命令行参数

很多程序可以执行一些操作来查看一些基本信息,Python可以使用 -h 参数查看各参数帮助信息:

------

#### 变量类型

变量存储在内存中的值，这就以为这在创建变量时会在内存中开辟一个空间，基于变量的数据类型，解释器会分配指定内存，并决定什么数据可以被存储在内存中，因此变量可以指定不同的数据类型，这些变量可以存储整数，小数或四组分

#### 变量赋值

python中的变量赋值不需要类型声明，

- 每个变量在内存中创建，都包括变量的标识，名称和数据这些信息
- 每个变量在使用前必须赋值，变量赋值以后该变量才会被创建，
- 等号(`=`)用来给变量赋值
- 等号(=)运算符左边是一个变量名，等号(`=`)运算符右边是存储在变量中的值

    #!/usr/bin/python
    # -*- coding: UTF-8 -*-

    counter = 100 # 赋值整型变量
    miles = 1000.0 # 浮点型
    name = "john" # 字符串

    print counter
    print miles
    print name
















































