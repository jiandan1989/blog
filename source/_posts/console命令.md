title: console命令
date: 2016-08-27 00:11:56
tags:
---

#### 一、显示信息的命令

在javascript调试中可以使用console的命令来代替alert或者document.write命令，不影响页面显示，也不会阻碍js的执行，内置有5种打印信息的命令，根据不同的信息使用不同的命令:
	
            console.log("这是log") // 打印普通信息
            console.error("这是error信息")  //错误信息
            console.info("这是info信息") 	// 一般信息
            console.debug("这是debug信息") //除错信息
            console.warn("这是warn信息")
	
<!-- more -->	
		
#### 二、占位符

console对象的上面5种方法，都可以使用printf风格的占位符。不过，占位符的种类比较少，只支持字符（%s）、整数（%d或%i）、浮点数（%f）和对象（%o）四种。

比如:

	console.log("%d年%d月%d日",2011,3,26);     //2011年3月26日
	console.log("圆周率是%f",3.1415926); 		//3.1415926
	
%o占位符，可以用来查看一个对象内部情况。比如，有这样一个对象：
	
		var dog = {} ;
	　　dog.name = "大毛" ;
	　　dog.color = "黄色";	
	　	console.log(%o,dog) ==>  Object{name:"大毛",color:"黄色"}
	　	
#### 三、分组显示

如果信息太多，可以分组显示，用到的方法是console.group()和console.groupEnd()。	　	

	console.group("第一组信息");
	　console.log("第一组第一条");
	    console.log("第一组第二条");
	console.groupEnd();
	console.group("第二组信息");
		console.log("第二组第一条");
		console.log("第二组第二条");
	console.groupEnd();
	
#### 四、console.dir()

console.dir()可以显示一个对象所有的属性和方法。

比如，现在为第二节的dog对象，添加一个bark()方法。

	dog.bark = function(){alert("汪汪汪");};
	console.dir(dog) == >color :"黄色" name:"大毛" bark : function()
	
#### 五、console.dirxml()

console.dirxml()用来显示网页的某个节点（node）所包含的html/xml代码。

比如，先获取一个表格节点，

	var table = document.getElementById("table1");
	console.dirxml(table)  ==>table节点的html结构以及元素被打印出来
	
#### 六、console.assert()

console.assert()用来判断一个表达式或变量是否为真。如果结果为否，则在控制台输出一条相应信息，并且抛出一个异常。

比如，下面两个判断的结果都为否。

	　　var result = 0;
	console.assert( result );
	var year = 2000;
	console.assert(year == 2011 );	
	
#### 七、console.trace()
console.trace()用来追踪函数的调用轨迹。

比如，有一个加法器函数。

	function add(a,b){
		return a+b;
	　}	
我想知道这个函数的调用，只要在函数中加入console.trace()方法就可以了
	
	function add(a,b){
		console.trace();
		return a + b ;
	}	
	
#### 八、计时功能

console.time()和console.timeEnd()，用来显示代码的运行时间。

	console.time("计时器一");

	for(var i=0;i<1000;i++){
		for(var j=0;j<1000;j++){}
	}
	console.timeEnd("计时器一");	
	
#### 九、性能分析

性能分析（Profiler）就是分析程序各个部分的运行时间，找出瓶颈所在，使用的方法是console.profile()。

假定有一个函数Foo()，里面调用了另外两个函数funcA()和funcB()，其中funcA()调用10次，funcB()调用1次。

		function Foo(){
			for(var i=0;i<10;i++){
				funcA(1000);
			}
	　　	　	funcB(10000);
		　　}

	　　function funcA(count){
			for(var i=0;i<count;i++){}
		}
		function funcB(count){
			for(var i=0;i<count;i++){}
		}	
		
		console.profile('性能分析器一');
		Foo();
		console.profileEnd();

- [摘自阮一峰Firebug控制台详解](http://www.ruanyifeng.com/blog/2011/03/firebug_console_tutorial.html)