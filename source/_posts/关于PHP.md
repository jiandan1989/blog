title: 关于PHP
date: 2016-03-09 13:15:40
tags:
---
在PHP中很多东西方法都能在js中找到相对应的方法，其实学习PHP的时候可以把它的方法在你熟悉的语言中找到相对应的方法理解，这样容易一点。


### 常量:

- 常量的定义:

	- 常量是指在程序执行中无法修改的值.如PI(3.1415926)

	- 在脚本执行期间该值不能改变

	- 常量对大小写敏感，通常常量名总是大写

	- 常量是全局的，可以在脚本的任何地方引用

	- 常量分为内置常量和自定义常量
	
	- 常量使用define()函数定义

	<!--more-->

例:  			
	
	define("PI", 3.1415926); 
	echo PI; //3.1415926
	
- 内置常量:

	PHP_OS  php所在操作系统的名称
	
	PHP_VERSION 当前php的版本号
	
- 魔术常量:是指那种值是不可变，也可变的。

	
		__LINE__文件中的当前行号
		__FILE__文件的完整路径和文件名
		__FUNCTION__ 函数名称
		__CLASS__ 类的名称
		__METHOD__ 类的方法名

#### 数据类型:

##### 1 、标量数据类型:

  - 字符串:字符串有三种定义方式:单引号，双引号，定界符(heredoc)。

  - 单引号字符串中出现的变量不会被变量的值替代

  - 双引号字符串中最重要的一点是其中的变量会被变量值替代

  - 如果遇到美元符号($)解析器会尽可能的取得后面的字符以组成一个合法的变量名，如果想明确的指定名字的结束，用花括号把变量名括起来

 例:
 
 		$beer = "Heineken";
 		echo "He drank some{$beer}s";
 		
 - 字符串定界的方法使用定界符语法"<<<"

 
			   $str = <<<EOD	
			   Example of string
			   using heredoc syntax
			 EOD	
在PHP定界符中的任何特殊字符，都不需要转义,PHP定界符中的PHP变量会被正常的用其值来替换，使用定界符要注意:结束标识符所在的行不能包含任何其他字符，这以为这该标识符不能被缩进，在分号之前之后都不能有任何空格或制表符。

- 字符串转义:

		\n 换行
		\r 回车
		\\ \(反斜杠)
		\$ $(美元符)
		\" "(双引号)
		
##### 2 、整型 

			$age = 25;
			
			
##### 3 、浮点型(float,double)

		$num = 5.39;
		
##### 4 、布尔型(bool)

		$bo = TRUE; $bo =FALSE;
		
##### 3 、复合数据类型:

- 数组

		$week = array("星期一","星期二","星期三")
		
- 对象

		$db = new db;
		
##### 4 、特殊数据类型

- 资源

		$fh = fopen("test.txt","r");
		
- null:无，表示没有值，null不表示空格，也不表示0，以下情况，默认为null;

	- 没有设置为任何预定义的变量

	- 明确的赋值为null

	- 使用函数unset()清除

##### 5 、自动类型转换

因为PHP对于类型定义非常的松散，所有有时会根据引用变量的环境，将变量自动转换为最适合的类型。

	1	$num = 5; 
		$str = "15;
		echo $num +$str ; //20
	
	2 $str = "100 hello";
	  $num = 200;
	  echo $str + $num ; //300
	  
	3 $str = "1,2";
	   if($str){ //判断为true
	   		echo "hello world"
	   } 	
		
##### 6、类型相关函数

- gettype()返回变量的类型，共有8个可能的值(string,integer,float,boolean,array,object,null,unknow)

		$str = "hello"
		echo gettype($str); //string
		
- is_type()查看变量是否属于某个类型，是返回TRUE，否返回FALSE

		$arr = array(1);
		echo is_array($arr); //true
		$num = 5;
		echo is_int($num); //true
		
- var_dump()获取变量的值和类型的详细信息

		$str = "hello"
		var_dump($str);
		
		$arr = array("a","b","c");
		
		var_dump($arr);
		

其实PHP有很多方法，没事的时候可以自己查看一下。。。。。
			
   