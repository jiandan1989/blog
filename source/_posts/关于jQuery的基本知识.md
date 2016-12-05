title: 关于jQuery的基本知识
date: 2016-03-02 21:42:57
tags:
---
<span style="font-size:18px;color:red;">jQuery的由来:</span>

jQuery是一个兼容多浏览器的javascript库,核心理念是Write less,do more(写得更少,做的更多).jQuery在2006年1月由美国人John Resig在纽约的barcamp发布,吸引了来自世界各地的众多Javascript高手加入,由Dave Methvin率领团队进行开发,如今jQuery已经成为最流行的javascript库,在世界前10000个访问最多的网站中，有超过55%在使用jQuery。<span style="font-size:18px;color:#999;">(本段文字摘自百度。。。)</span>

<!--more-->


<span style="font-size:18px;color:red;">jQuery的特点:</span>

一 、动态特效

二 、AJAX

三 、通过插件来扩展

四 、方便的工具-例如浏览器版本来判断

五 、渐进增强

六 、链式调用

七 、 多浏览器支持，支持Internet Explorer6.0+ 、    Opera9.0+、Firefox2+、Safari2.0+、Chrome1.0+（在2.0.0中取消了对Internet Explorer6,7,8的支持）

<span style="font-size:18px; color:red;">使用方法:</span>

#### 一 、Production version - 用于实际的网站中,已被精简和压缩

#### 二 、Development version - 用于测试和开始(未压缩,是可读的代码)

 
 我们看到的是只是它的使用用途,应该怎么使用呢？
 
在head内使用script标签src属性引入,引入方法很简单，和平时引入外部js一样，建议放在所有js的最上边/

	<script type="text/javascript" src = "http://ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js></script>
 
 <span style="font-size:18px; color:red;">注意事项:</span>
 
 
1 、Wordpress内置jQuery库,其末尾防止JS库冲突而加入的jQuery.noConflict()使得主题中所有jQuery代码都要做一些小修改，更可能导致一些插件效果失效

2 、Google CDN(国内的有新浪、百度云等提供)库的地址采用了协议相对路径，它可以很好的解决https引起的一些问题，具体可以看Paul Irish的介绍，当然你依旧可以使用带“http:”的路径。


3 、 许多网站都采用Google CDN提供的jQuery库，使用它可以得到出色的缓存效果。

4 、把jQuery代码统统放到页面底部可以提高载入速度。

5 、使用HTML5重构的页面可省略掉 type="text/javascript"。

6 、推荐使用国内CDN公共库，速度更快，稳定性更高。


来源:百度