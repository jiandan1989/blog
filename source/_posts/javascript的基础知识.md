title: javascript的基础知识
date: 2015-11-27 20:41:41
tags:
---
# javascript的基础知识一


**先说一下浏览器对js解析时做的准备工作**

1.变量和函数表达式的声明提升到当前作用域的最顶端

2.把函数赋值，可以直接在函数上方调用。

<!--more-->


**函数的方式**

1.**声明函数：**也称函数声明 使用function关键字加上函数名声明的函数，例如

	function example(){}

2.**函数表达式：**函数表达式可以细分为两种

（1）声明变量的函数,例如:

	var example = function(){}  声明一个变量，值为函数方法             
（2）匿名函数：使用function关键字，但是没有函数名的函数。例如：

	function(){}     
	
**函数表达式可以使用（）操作符，表示立即执行，函数声明不可以使用。例如**

	(function(){})(); 
**JS变量种类**
	
1.全局变量：全局变量可以在任何地方访问。

2.局部变量：只有在函数内部才能产生局部变量，对外部是不可见的。函数内部是可以访问外部函数的变量

**注意：每一个函数都有默认undefined的返回值**
	
**JS的作用域分为两种**

1.全局作用域：全局作用域其实就是window对象，咱们之前声明的变量，实际上就是在window对象上创建了一个属性,但是在这里我们需要注意，window有自己默认属性，当我们创建的新属性和默认属性有冲突时，会覆盖默认属性。

2.局部作用域：只有在function方法内才会产生局部作用域，当然也可使用return跳出当前作用域变换成全局的。例如

	function fn(){
		var fn2 = function (num){
		
		} 
		return fn2;
	}
	var newFn = fn();也就等于是把fn2()当作一个值赋予给了fn(),那么newFn也就是等于fn2().

**计算机运算的函数：**

假设一个函数执行时最后一个参数为运算符

（1）首先声明一个函数，函数名为computer

	function computer(){}
	
(2)在函数内部声明一个变量，值为参数的最后一个

	var character =arguments[arguments.length-1];可以找到最后一个值，也就是运算符

（3）用判断语句来判断当前的运算符是哪一种（我们假设是加法运算）

	if(character =='+'){
		for(var i =1; i<arguments.length-1; i++){
			arguments[0] = arguments[0] + arguments[i];使用for循环运算出的值最终赋予给arguments[0]
		}
		return arguments[0]; 使用return方法返回arguments[0]
	}
（4）最后一步就是来执行computer这个函数

	conputer(1,2,3,4,'+'); 如果像要看到得到的值可以用开发者工具console.log(computer(1,2,3,4,'+'))也可用其他的方法。
	
**刚开始学习的时候我们只要求自己把每天学习的东西能掌握就行。一口吃不了胖子，路是一步一步走。只有基础扎实了才能走的更远。**	

