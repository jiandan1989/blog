title: CSS 回顾(二)
date: 2016-02-26 10:45:35
tags:
---
**在这里主要回顾说一下盒子模型和选择器**

<!--more-->

<span style="color:red;">盒子模型的构成:</span>

- 盒子中的内容(content)

- 盒子的边框：(border)

- 盒子边框与内容之间的距离：称为填充---padding内边距（内补丁）

- 如果有多个盒子存在，盒子与盒子之间的距离：称为边界---margin，外边距（外补丁）

W3C标准规定了标准盒子模型的宽度和高度的算法：

__整个盒子模型在网页中所占的宽度:左右外边距 + 左右内边距 + 左右边框 + 内容宽度__

__整个盒子模型在网页中所占的高度:上下外边距 + 上下内边距 + 上下边框 + 内容高度__

![标准](http://7xoo7k.com1.z0.glb.clouddn.com/w3c.jpg "标准盒子模型")

![IE](http://7xoo7k.com1.z0.glb.clouddn.com/ie.jpg "IE盒子模型")

从上两图可以看出标准盒子模型和IE盒子模型的不同：

标准盒子模型中内容(content)的高度和宽度都不包含内边距(padding)和边框(border)，但是在IE盒子模型中内容的高度都把内边距和边框包含在内。

**盒子模型中的padding、margin、以及border在应用中都遵循了TRBL法则(Top、Right、Bottom、Left)。**

说完了盒子模型就要涉及到BFC，请<a href="javascript:;" style="font-size:20px; text-decoration:none; color:#f47d31;">点击查看</a>

<div style="border:1px  #999 dashed;"></div>

<span style="color:red;">声明样式：</span>

在css中对一个元素或多个元素进行声明样式是一个选择器、一对大括号、属性名和属性值组成

	p {
		font-size:16px;
		font-color:red;
	}

对一个元素声明多个样式时，必须由分号(;)隔开。

<div style="border:1px  #999 dashed;"></div>

<span style="color:red;">选择器:</span>

选择分为很多种，按照类型分类的话有基本、组合、伪类、属性等。

__基本的选择器：__

- 通配选择器(*)：匹配所有的元素。

  	*{
		margin:0;
		padding:0;}

- 标签选择器(p): 匹配所有使用p的标签元素。
	p{
		font-size:20px;
	}

- class选择器(.test):匹配所有带有class为test的元素。

		.test{
		font-size:20px;
		}
		p.test{
		font-size:20px;
		}
- id选择器(#id):匹配指定id名的元素，id选择器是唯一的 <code>#test{background-color:red;}</code>

<div style="border:1px  #999 dashed;"></div>

__组合选择器：__

- 群组选择器(h1,h2,h3): 同时匹配多个元素，之间用逗号(,)隔开 <code>h1,h2,h3{margin:0;}</code>

- 后代元素选择器(div span):匹配所有属于div的span包括子孙级别的元素，之间用空格隔开 <code>div span{display:block;}</code>

- 子元素选择器(ul>li):匹配所有属于ul的子元素li <code>ul>li{width:200px;}</code>

- 相邻元素选择器(p+div):匹配p元素后相邻的div元素 <code>p+div{width:200px;}</code>

<div style="border:1px  #999 dashed;"></div>

__伪元素选择器：__

- **p::first-line:** 匹配p元素的第一行 <code>p::first-line{font-color:red;}</code>

- **p::first-letter:** 匹配p元素的第一个字符 <code>p::first-letter{font-weight:bold;}</code>

- **p::before:** 在p元素之前插入生成的文本 <code>p::before{content:"";width:100px;height:100px;}</code>

- **p::after:** 在p元素之后插入生成的文本 <code>p::after{content:"";width:10px;height:10px;background:red;}</code>

<span style="color:red; font-size:18px;">注意:在使用before和after伪类时，必须要有content属性。</span>

<div style="border:1px #999 dashed"></div>

__伪类选择器 :__

- **div:first-child:** 匹配div的第一个子元素 <code>div:first-child{width:200px;}</code>

- **a:link:**匹配所有未被点击的a链接 <code>a:link{background:red;}</code>

- **a:visited:**匹配所有已被点击的a链接 <code>a:visited{background:blue;}</code>

- **e:hover:** 匹配所有鼠标悬停其上的E元素 <code>e:hover{background:green;}</code>

- **e:active:** 匹配所有鼠标点击但还没有释放的E元素 <code>e:active{background:yellow;}</code>

<span style="color:#f47d31; font-size:16px;">注意：当link,visited,hover,acitve作用于同一个a链接时,是有顺序的如果链接是有效的地址访问过后，link状态不再会被触发</span>

<div style="border:1px #999 solid;margin-top:15px;"></div>

这里讲的为CSS2内的选择器,关于CSS3选择器内容请<a href="http://niexiaofei1988.github.io/2016/02/26/CSS%E5%9B%9E%E9%A1%BE%28%E4%B8%80%29/">点击查看</a> <br/><br/><span style="font-size:18px;color:#f47d31;">感谢韩大神的技术传授</span>