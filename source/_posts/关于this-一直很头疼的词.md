title: 关于this(一直很头疼的词)
date: 2016-03-01 17:06:44
tags:
---

### 对于this纠结了很久,其实想要搞清楚this指针的指向要弄清楚调用的方式和对象,浏览器的解析模式，函数和变量的优先级、原型链等。


#### this是Javascript语言的一个关键字,它代表函数运行时，自动生成的一个内部对象，只能在函数内使用。

<!--more-->

随着函数使用场合的不同，this的值会发生变化，但是有一个总的原则，那就是this指的是调用函数的那个对象。

下面分四种情况，详细讨论this的用法。

<span style="color:red; font-size:16px;">情况一: 纯粹的函数调用(普通函数)</span>

这是函数的最通常用法，属于全局性调用，因此this就代表全局对象Global(window)。
```javascript
function test(){
  this.x = 1;
  console.log(this)
}
test();// this = window
console.log(this.x);//1
```
在浏览器的解析中,函数的优先级会提高，提至最顶端，随着就是变量的声明。上段代码解析就会是在window下创建了一个属性，而属性的值等于1.所以<code>console.log(this.x);</code>得到的值是 1。

<span style="color:red; font-size:16px;">情况二: 作为对象方法的调用</span>

函数还可以作为某个对象的方法调用，这时的this就指这个上级对象。

```javascript
function test(){ alert(this.x)}
var obj = {}; obj.x = 1; obj.m = test; obj.m(); //1
```

在上段代码中.在对象obj中创建了两个属性，并赋予了值,obj.m的值就是test方法,而 m 作为对象obj的属性，调用的时候this指向的是当前对象obj，alert(this.x)就等同于alert(obj.x)弹出的值为1.

<span style="color:red; font-size:16px;">情况三: 作为构造函数调用</span>

所谓构造函数,就是通过new关键词生成的一个新对象(Object),这时this指向这个新对象。
```javascript
function test(){
this.x = 1;
}
var obj = new test();
alert(obj.x); //1
```
在上段代码中,对象obj是通过关键字new出来的一个实例,而通过new出来的对象都有_proto_属性,该属性完美的继承了test的prototype属性.在原型链中，如果自身没有该属性时会顺着原型链中继续向上找,直到找到原型链的最终点.为了表明这时的this不是全局对象，可以参考下面的代码，做个比较。
```javascript
var x = 2;
function test(){
  this.x = 1;
}
var obj = new test();
alert(x); //2
```

<span style="color:red; font-size:16px;">情况四: apply调用</span>

apply()是函数对象的一个方法，它的作用是改变函数的调用对象，它的第一个参数就表示改变后的调用函数的对象，因此this指的就是这第一个参数。
```javascript
var x = 0;
function test(){
  alert(this.x);
}
var obj = {};
obj.x = 1;
obj.m = test;
obj.m.apply(); //0;
```
apply()的参数为空时,默认调用全局对象(window),因此这时运行的结果是0,apply()方法改变了this的指向。为了证明this指的是全局对象。我们把最后调用函数的代码改下。

`obj.m.apply(obj) //1 这里的参数为obj执行时this的指向为obj。`

#### 有很多面试题都要考察对调用函数的理解。下面有道面试题，可以看一下。
```javascript
function Foo() {
  getName = function () { console.log(1); };
  return this;
}
Foo.getName = function () { console.log(2); };
Foo.prototype.getName = function () {
  console.log(3);
};
var getName = function () { console.log(4); };
function getName() {
  console.log(5);
}

//请写出以下输出结果：
Foo.getName();//2
getName();//4
Foo().getName();//1
getName();//1
new Foo.getName();//2
new Foo().getName();//3
new new Foo().getName();//3
```
有不理解的地方可以一起讨论一下。可以自己多找些关于this的面试题。顺便说下本文参考 http://www.jb51.net/article/41656.htm
