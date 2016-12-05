title: jQuery的基本选择器用法
date: 2016-03-03 11:15:13
tags:
---
### <span style="font-size:16px; color:red;">不得不说jQuery的选择器功能确实是很强大,只要是我们能想到的几乎都能找到相应的方法来实现。来看看到底有多么得强大.</span>


<!--more-->

### 基本选择器:

 <span style="color:red;">#id选择器:</span>根据给定的id匹配一个元素。当id名中出现任何的元字符(如:! # $ %)等必须用两个反斜杠转义.
 
HTML代码:

	<div id = "first">我是第一个</div>
	<div id = "second[two]">我是第二个</div>
	
jQuery 代码:

	$("#first")          //查找匹配id名为first的元素
	$("#second\\[two\\]) //查找匹配id名为second[two]的元素，有特殊符号需要转义
 		
 <span style="color:red;">element选择器:</span>根据给定的元素标签名匹配所有元素。
 
 HTML代码:
 
 		<div class="first">
 			<div class="second"><span>我是span</span></div>
 		</div>
 		
jQuery 代码:

	$("div") //查找到所有的div,对span不会产生影响
	
<span style="color:red;">.class选择器:</span>根据给定的css类名匹配元素。一个元素可以有很多个类名,但是只要有查找给定类名就会被搜索到。

 HTML代码:
 
 		<div class="first">我是带有first类名的div</div>
 		<div class="first one">我是带有first类名的div</div>
 		<div class="second">我是带有second类名的div</div>
 		
 jQuery代码:
 
 		$(".first")  //查找到带有first类名的div，不会匹配到带有second类名的div
 		
<span style="color:red;">*(通配)选择器:</span>匹配文档中所有的元素。

HTML代码:

	<div class="first">
		<div class="second">我是div</div>
		<span>我是span</span>
	</div>
 	
jQuery代码:

	$("*") //匹配所有的元素，不管你是什么样的标签


