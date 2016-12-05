title: node.js的学习
date: 2016-03-28 18:37:05
tags:
---
关于node的使用，相信很多人都应该知道Facebook和淘宝，淘宝的2015年的双十一活动的所有后台都是使用node.js来渲染的，使得node.js代替了很多服务端的使用。到底应该怎么样来使用node.js呢？？？我也很迷茫只能是慢慢的查找和应用。

首先呢node并不是一门语言，它是个运行javascript的平台，内置有使用Chorme的v8引擎，不需要考虑兼容性。

<!--more-->

node.js呢我是使用Sublime编辑器来使用的,需要安装插件nodejs。

然后呢就是建一个文件夹，文件夹内有index.html,form.html,和一个404.html,更重要的是一个server.js，然后在server.js中引用模块。基本的html布局和样式就不再说了.

index.html代码

		<div class="outside">
			<h1>欢迎来到我的世界</h1>
			<a href="/login">注册</a>
		</div>
		
form.html代码

		<form action="login_in" method="POST">
			<input type="text" name="name" value="请输入你的名字"/>
			<button>提交</button>
		</form>
		
404.html代码

		<h1>404</h1>
		<a href="/">请回吧</a>
		
server.js代码

		var http = require("http");//引入http模块
		var fs = require("fs);     //引入fs模块
		
		http.createServer(function(req,res){
			switch(req.url){
				case "/" :{
					fs.readFile("./index.html","utf-8",function(err,data){
						res.writeHead(200,{"content-Type":"text/html"});
						res.end(data);
					})
					break;
				}
				case "/login" :{
					fs.readFile("./form.html","utf-8",function(err,data){
						res.writeHead(200,{"content-Type":"text/html"});
						res.end(data);
					})
					break;
				}
				case "/login_in" : {
					var str ="";
					req.on("data",function(chunk){
						str+=chunk;
					});
					req.on("end",function(){
						res.writeHead(200,{"content-Type":"text/html"});
						res.end("<h2>you send : "+str+"</h2>");
					})
					break;
				}
				default:{
					fs.readFile("./404.html","utf-8",function(err,data){
						res.writeHead(200,{"content-Type":"text/html"});
						res.end(data);
					})
				}
			}
		}).listen(3000);
		
		
上面的代码都写完以后直接在终端命令中输入node server.js就可以看到页面了，当然了 这个是最简单的，如果想要弄得好看一点，就研究研究自己的css，怎么弄好看就怎么弄.


__________________再  见___________________
		