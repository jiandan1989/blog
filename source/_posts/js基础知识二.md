title: js基础知识二
date: 2015-12-01 21:26:50
tags:
---
## javascript中的原型：

  在javascript中所有的函数都有prototype属性，该属性是一个对象，对象是所有属性的集合，所有的对象都有一个__proto__属性，所有对象的__proto__都指向其构造器的prototype。当函数没有任何属性，prototype对象默认有constructor（指向函数本身）属性。
  
  	function fn(){
  		return '10'
  		}
  	var fn2 = new fn();//从fn方法里面new出一个对象，生成对象
  	console,log(fn2.__proto__===fn.prototype)为true

 所有构造器的__proto__都指向Function.prototype.完全继承了prototype的属性以及方法。
  
<!--more-->

### javascript中的this

### this是javascript语言的一个关键字。下边是几种用法说明。

### 1.在全局作用域下调用this，this指向Global,也就是window，（函数声明、匿名函数、函数表达式在全局中调用this指向window.

	（function(){
		console.log(this)
		}();//匿名函数
	var fn= function(){
		console.log(this)
	}
	fn();//函数表达式
	function fn(){
		console.log(this)
	}
	fn();//函数声明

在上边的例子里边this指向的都是window

### 2.用new关键字构造的对象，this指向创建该对象的对象。

	function fn(){
		console.log(this)
	}
	var fn2 = new fn();

在上边例子中fn2是用new关键字声明的对象，fn()就是创建该对象给你的对象，所以这里this指向的是fn()

### 3.this当前的函数为对象属性时，this指向该对象。

	var obj= {
		fn:function(){
			console.log(this)
		}
	}
	obj.fn();

在上边的例子里，this当前的函数为fn，fn是obj对象的一个属性，所以this指向的就是该对象（obj）.

