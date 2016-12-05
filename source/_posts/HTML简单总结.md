title: HTML简单总结(一)
date: 2016-02-25 15:49:56
tags:
---
## 有些东西你不用就会废弃，有些东西你不看就会忘记。下面是HTML的简单总结，回忆一下...

<!--more-->

### 1. HTML基本结构:
>		<!doctype html>						<!--html文档的版本声明-->
		<html>								<!--html文档的开始-->
			<head>							<!--html文档头部的开始-->
				<meta charset="utf-8"/>		<!--html文档的编码格式-->
				<title>标题</title>		   <!--html文档的标题-->
			</head>							<!--html文档头部结束-->
			<body>							<!--html正文开始-->
				<p>我是内容</p> 		     <!--html正文内容-->
			</body>							<!--html正文结束-->
		</html>								<!--html文档的结束-->

(1) <!doctype html>是html5的标准声明，指定了 HTML 文档遵循的文档类型定义。

 (2) HTML文件均以&lt;html&gt;开始,&lt;/html&gt;结束

 (3)HTML文档对大小写不敏感，但是建议使用小写

 (4)注释方式：<q><!--注释代码--></q>
 
### 2. 标签
 在HTML文档中按照书写可分为双标签和单标签，双标签是以&lt;html&gt;开始的和&lt;/html&gt;结束的标签。单标签是&lt;br/&gt;
 
 在HTML文档中每个标签都有自己的特定标识。
 
 **html**:根标签，告知浏览器此文档是一个HTML文档。
 
 **head**:指定了HTML的头部，head的内容不会显示在页面中，但是有这很重要的作用，用来告知浏览器编码格式、文档标题、样式表、js的外部引入地址或者内部引入的代码。
 
 (1) 标记可以描述页面的作者、摘要、关键词、版权、自动刷新等页面信息 例如：&lt;meta charset="utf-8"/&gt;指定文档的编码格式，关于meta有很多作用各不相同，不再一一举例。
 
 (2) **title**:指定文档的标题
 
 (3) **link**:指定文档的css(样式表)的外部引入路径
 
 > 	<link rel="stylesheet" type="text/css" href="引入路径" />
 	
 (4) **style**:指定文档css的内部引入方式
 
>		<style type="text/css>样式代码</style>
 
 (5) **script**:指定js的引入方式
 
>	   <script type="text/javascript>内部引入</script>
	  <script type="text/javascript" src="JS的引入路径">外部引入方式</script>
 
#### body:

指定了文档的主体，文档的正文标记，包含了文档中所有的内容，在浏览器中可视区域中可见得部分。
 
**(1) h1~h6标签**

指定文档主体标题，双标签，并且依据重要递减，**h1**标签是最高的等级，h系列标签在文档的渲染中有默认的外边距(__margin__)。

![h标签的等级显示](http://7xoo7k.com1.z0.glb.clouddn.com/h.png "h系列标签的显示情况")

**(2) p标签 :** 指定文档主体创建一个文本段落，双标签，有默认外边距。

**(3) em 和 strong :** 这两个标签都有强调的寓意，双标签，__strong__寓意更重一点，__em__显示为斜体。

**(4) div 和 span :** 标签在文档中没有任何寓意，双标签，__div__指没有语义的块级容器，__span__指包裹内容没有语义的行级标签。

**(5) a标签 :**超链接或者锚点链接，href属性是必须的，指定链接路径、id或者用#、javascript:;代替。title属性指对链接的提示，鼠标划过时显示的文本，target属性指链接的打开方式(_blank在另一个窗口打开， _self在自身窗口打开)

>     <a href="链接路径" title="链接描述" target="链接打开方式">点击跳转到指定路径页面</a>
> 	  <a href="id">点击跳到页面中带有指定id的位置</a> 

**(6)img :** 图片标签，有src、alt、title属性，src指图片的位置(引入图片的路径),alt指当加载失败时的替代文本，title指对图片的提示，鼠标滑过时显示的文本。在不设置任何width和height时，会显示图片的实际大小。

>     <img src="图片路径" alt="替代文本" title="tips"/>

**(7) q标签 ：**短文本引用，比如在你的网页的文章里想引用某个作家的一句诗，这样会使你的文章更加出彩，那么<q>q标签是你所需要的</q>。

**(8) blockquote标签：** 长文本引用。

**(9)br和hr标签：**br表示换行，hr表示分割线。
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       
**(10)address标签：**为页面加入地址信息，样式为斜体。<address>中国上海</address> 

**(11)code和pre标签：**为页面加入计算机程序代码，代码为一行时用code,PHP中的变量名,前面要加上 '$' 符号,pre指预格式化的文本，代码为多行时可以用pre标签，不能使用code标签。

![code和pre标签的显示](http://7xoo7k.com1.z0.glb.clouddn.com/code-pre.png "code和pre的区别")
 
**(12)列表：**列表有无序列表(ul li)、无序列表(ol li)、自定义列表(dl dt dd)。列表标签是组合标签，列表容器和列表项之间不能加入任何其他标签。

![三种列表](http://7xoo7k.com1.z0.glb.clouddn.com/ol-ul-dl.png "列表区别")
 
 
 **(13)table表格:** 
 
 - tbody 这个标签现在很少用了 
 - tr   表格的一行
 - td   表格的一个单元格(列)
 - th   表格的头部的一个单元格，表格表头
 - caption 表格标题
 - summary属性 表格的摘要 &lt;table summary="哈哈哈 红红红"&gt;&lt;/table&gt;

 ![表格](http://7xoo7k.com1.z0.glb.clouddn.com/table.png "table表格")
 
 
 
 

