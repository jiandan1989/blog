title: 关于PHP的学习笔记
date: 2016-03-07 21:08:52
tags:
---
#### 一 、环境搭建

- 使用支持PHP和MySQL的web主机，只要创建.php文件，然后上传到web目录中即可，服务器会自动对它们进行解析。

- 在您的PC上安装web服务器，然后安装PHP和MySQL，官方的PHP网站(PHP.net)提供了PHP的安装说明:http://php.net/manual/zh/install.php

- Apache这是最流行的Web服务器软件之一,Apache的官网地址:http://www.apache.org。

- MySQL是关系型数据库管理系统，拥有体积小，速度快，开方源码等优点，官网地址:http://www.mysql.com

- XAMPP是一个功能强大的建(Apache+MySQL+PHP+Perl)软件站集成软件包。引入XAMMP的目的:手动安装Apache+MySQL+PHP环境过于复杂，而XAMPP帮我们集成了这个环境，只需点击安装即可。

<!--more-->

#### 二 、PHP基础语法:

- PHP标记

```php
   1.<?php echo "hello php";?>

   2.<? echo "hello php";?>//短语句

   3.&lt;script language="php"&gt;echo "hello php"&lt;/script&gt;

   4.<% echo "hello php"; %> //asp风格
 ```
   <span style="color:red;">注:1，3可以直接使用，但是2，4需要修改php.ini的配置文件才能使用。</span>


- PHP注释

	1.多行注释: /\*注释\*/

	2.单行注释: (1) //注释 (2) #注释

#### 变量
- 1.变量的声明:

	- 变量以$开头,后面跟变量名

	- 变量由字母，数字，下划线组成，不能以数字开头

	- 变量名区分大小写

	- PHP与javascript类似是若类型语言，不需要实现声明变量的数据类型

	- PHP可以不显示的声明变量而直接使用(不过好的编程习惯所有的变量使用前要进行声明)

  例:
```php
$age = 28;
$color = "red";
$sum = 15 + "12"; //$sum = 27在PHP中所有的运算符都是单纯的运算
```
 #### 变量的赋值:

- 值赋值:即将赋值表达式的值赋予给变量(直接赋值)

```php
$a = "hello" //直接赋值
```

- 引用赋值 :PHP4中引用了引用赋值，创建一个变量与另一个变量引用的内容相同。
```php
$a = 5;
$b = &$a;
//把变量a的内存地址赋值给b即引用赋值,不论是改变a或者b都两个值都会改变
```
 #### 变量的变量:
```php
$a = "hello" ; $$a = "world";
echo $a //输出hello
echo $hello//输出world
echo ${$a} //输出world
```
#### 超全局变量

- php提供了很多有用预定于的变量，用于提供大量与环境有关的信息，打印/输出超全局变量:parent_r($_SERVER)

- (1)$_SERVER服务器变量，该全局变量包含着服务器和客户端配置以及当前请求环境的有关信息
```php
$_SERVER['SERVER_NAME'] //当前运行脚本所在的服务器的主机名
$_SERVER['REMOTE_ADDR'] //客户端IP地址
$_SERVER['REQUEST_URL'] //URL的路径部分
$_SERVER['HTTP_USER_AGENT'] //操作系统和浏览器的有关信息
```
- (2)$_GET 该变量包含使用GET方法传递的参数的有关信息。例:
```php
url:http://localhost/test.php?id=100&page=2
$id = $_GET['id'];
$page = $_GET['page'];
```
- (3)$_POST 该变量包含使用POST方法传递的参数的有关信息。例:
```html
<form name="reg" action = "test.php" method="post">
用户名:<input type="text" name="username"/>
密码: <input type="password" name="password"/>
<input type="submit" value="提交"/>
</form>
```
```php
PHP:
$username = $_POST['username'];
$password = $_POST['password'];
```
<span style="color#999">注意:<br/>

- (1)get是默认是提交方式，在地址栏中显示，不安全(数据可见)，数据的类型只能是字符串，数据的大小相对post来说很小，但是传递数据的速度快<br/>

- (2)post:通过http协议传递的数据(比较安全，数据不可见)数据的类型可以是文件，数据的大小默认可以上传2MB，但是相对于get数据的传递速度比较慢</span>

- (3)$_REQUERT 该变量记录着通过各种输入方法传递给脚本的变量，如GET POST但不要用这个超级全局变量，因为它不安全而且速度比较慢。






