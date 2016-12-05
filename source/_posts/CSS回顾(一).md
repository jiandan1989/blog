title: CSS 回顾(一)

date: 2016-02-26 09:31:17
tags:
---
**简单回顾一下CSS的引入方式以及区别**

<!--more-->

<p style="font-size:18px;">CSS 样式由选择符和声明组成，而声明又由属性和值组成</p>

- 选择器{属性:值}

- 声明：在英文大括号{}中的就是声明，属性和值之间用冒号(:)分隔。当有多条声明时，中间可以用英文分号(;)分隔。

- 注释方式: <code>/**/</code>

我们都知道在html文档中引入css(层叠样式表)有四种方式，四种方式分别是

<span style="color:red;">行间样式</span>：在标签元素内写入样式

> 	  <p style="font-size:16px; font-color:red;">This is a paragraph </p>

<span style="color:red;">内部引入</span>：在head标签内使用style标签引入

>	   <style type="text/css">
		body{
			margin:0;
		}
	 </style>

<span style="color:red;">外部引入</span>：在head标签内使用link方式引入外部样式表
		 
>		<link rel="stylesheet" type="text/css" href="样式表引入路径"/>
	
既然有三种引入方式，三种方式有没有优先级之分呢，有没有区别呢？答案是肯定的。

如若是对同一个标签用三种方式设置同一个样式时，在没有<span style="color:red;">important</span>(不建议使用，不利于后期的修改)情况下，并且有就近原则内部样式在外部引入的样式表的后面。<p style="color:red"> 行间  > 内部引入 > 外部引入</p>



<span style="font-size:16px; color:red;">区别:</span>

__- 行间样式：__ 最为简单直接的一中方式，优先级比较高，但是HTML页面不太干净，文件比较大，不能实现样式和内容的分离，影响阅读体验，不利于后期维护和修改。

__- 内部引入：__ 对于单个页面或者是修改某个元素时，可使用内部引入方式。多个页面建议使用外部引入，不能多次复用，没有多余的请求。

__- 外部引入：__ 完美的实现了页面框架代码与表现CSS代码的完全分离，使得前期制作和后期维护都十分方便,可引入多个文件，可复用，但是对于单个元素修改时比较麻烦，增加请求次数。

<span style="color:red">@import url(路径)</span> :使用@import会增加页面的总体加载时间，也会有一次请求，IE中使用@import会改变文件的加载顺序，能会增加CSS文件的加载时间，阻碍页面渲染。这可不建议使用。



		
