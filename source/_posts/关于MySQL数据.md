title: 关于MySQL数据
date: 2016-03-09 21:39:07
tags:
---
#### MySQL数据库简介

- 相关术语

  - 什么是数据库? :数据库(database)就是一个由一批数据构成的有序集合，这个集合通常被保存为一个或多个彼此相关的文件。

  - 什么事关系型数据库? : 数据被分门别类的存放在一些结构化的数据表(table)中，而数据表之间又往往会形成种种内在的交叉关系，存在于数据表之间的这种关系(relation)使数据库又被称为关系型数据库

  - 关系型数据库系统 :MySQL、 Oracle 、 Microsoft SQL Server 和IBM DB2都是关系型数据库系统(database system)。除了管理数据，一个这样的系统还包括用来管理各种关系数据库的程序，一个合格的关系数据库系统不仅要确保各种数据的存储情况安全可靠，还必须能够处理对现有数据进行查询，分析和排序以及对新数据进行保存等诸多命令。

  - 数据表、记录、字段、查询、SQL、索引 

  
  <!--more-->

  	- 数据表(table)即用来实际存放有关数据的框架结构，这种数据表里的每一行被称为一跳数据记录(data record),简称"记录"，每条记录的结构和格式是由人们在定义该数据表时决定的，例如，在某个用户表里，每条记录可能包含着用户的姓名，出生日期，注册时间等多个字段(field)，每个字段对自己所能存储的信息类型又有着一定的要求(例如，它必须是一个有着某种特定格式的数字或者是一个字符个数不得超过某个预定义最大值的字符串)。

  	- 查询是人们用各种SQL指令构造出来的，SQL指令负责具体完成筛选和提取结果数据的工作。

  	- SQL(Structured Query Lanuage) 结构化查询语言，这种语言已发展为人们在构造数据库查询命令的一个标准

- 常用命令

	- status(\s) :查看数据状态信息

	- clear(\c) :放弃仔仔输入的命令

	- exit或quit(\q) : 退出MySQL程序

	- help(\p) :显示帮助信息(命令清单)

	- use database(\u):选择一个数据库

	- show databases :查看数据库

	
#### SQL语言简介

SQL命令可以分类以下三大类别:

- DML(Data Manipulation Language数据处理语言) :这类命令主要包括SELECT 、INSERT 、UPDATE、DELETE等用来从数据表读出数据，把数据存入数据表或是对数据表里的现有记录进行修改的命令

- DDL(Data Definition Langage数据定义语言) :这类命令主要包括CREATE TABLE、 ALTER TABLE等用来定义和改变数据库结构的命令

- DCL(Data Control Langage 数据控制语言) :这类命令主要包括GRANT 、REVOKE以及另外几个用来帮助人们设置和调整MySQL访问控制机制的SQL命令

#### 命令的基本用法:

- SELECT 命令

	- 简单查询 SELECT * FROM tablename //从数据表中查询某些字段

	- 限制查询结果中的数据列个数 SELECT column1, column2 FROM tablename//从数据表中查询具体的字段

	- 确定数据里有多少条数据记录 SELECT COUNT(id) FROM tablename //返回的是数据表内有多少条记录


##### WHERE 子句:设置查询条件，过滤掉不需要的数据行，例如查询年龄大于20的记录， SELECT * FROM usertable WHERE age >20 

WHERE子句可包括多种条件运算符

- 比较运算符  


<table border="1" width="300px">
	<tr>
		<td>运算符</td>
		<td>含义</td>
	</tr>
	<tr>
		<td> = </td>
		<td>等于</td>
	</tr>
		<tr>
		<td>></td>
		<td>大于</td>
	</tr>
	<tr>
		<td>>=</td>
		<td>大于等于</td>
	</tr>
	<tr>
		<td><</td>
		<td>小于</td>
	</tr>		
	<tr>
		<td><=</td>
		<td>小于等于</td>
	</tr>
	<tr>
		<td><></td>
		<td>不等于</td>
	</tr>
</table>


	
		SELECT * FROM user WHERE uid = 10;//从user数据表中查找等于10的数据
		SELECT * FROM user WHERE uid <=10; //从user数据表中查找小于等于10的数据
		
		
- 逻辑运算符

<table border="1" width="300px">
	<tr>
		<td>运算符</td>
		<td style="width:400px;">含义</td>
	</tr>
	<tr>
		<td> AND </td>
		<td style="width:400px;">如果组合的条件都是TRUE，返回TRUE，否则返回FALSE</td>
	</tr>
	<tr>
		<td>OR</td>
		<td style="width:400px;">如果组合的条件其一是TRUE，返回TRUE</td>
	</tr>
	<tr>
		<td>NOT</td>
		<td style="width:400px;">如果条件是FALSE，返回TRUE</td>
	</tr>
</table>
	
	
- 范围运算符(BETWEEN...AND...)判断表达式值是否在指定的范围

		SELECT * FROM products WHERE price BETWEEN 1000 AND 2000;
		price >= 100 AND price <=2000; //这两条的意思是一样的就是在1000到2000之间的数据
		
#### 限制查询: 

LIMIT子句用于强制SELECT语句返回指定的记录数，LIMIT接受一个或两个参数，参数必须是一个整数常量，如果给定两个参数，第一个参数指定第一个返回记录行的偏移量，第二个参数指定返回记录行的最大数目，注意:初始记录行的偏移量是0而不是1

		SELECT * FROM table LIMIT 5 ;// 检索前5个记录行
		SELECT * FROM table LIMIT 5,10 ;//检索记录行6-15，从第5行开始检索
		
#### 查询结构排序

使用ORDER BY子句对查询返回的结果排序,ORDER BY子句的语法格式为:ORDER BY{column_name[ASCIDESC]}[,...n]，其中ASC表示升序，为默认值，DESC为降序。


		SELECT * FROM user ORDER BY uid ASC //默认为升序
		SELECT * FROM user ORDER BY uid DESC //降序
		
#### 增删改

- 插入数据记录(INSERT):格式---INSERT INTO user(username,password);

		SELECT INTO user (username,password)VALUES("user1","123456"),("user2","123456") //在user数据表中插入两条记录
		
- 修改数据记录(UPDATE) 

		UPDATE user SET username = "admin1",password = "456123" WHERE uid = 10;//
		把user数据表中的第10条记录中的username,password修改
		
- 删除数据记录(DELETE)

		DELETE FROM user WHERE uid = 10; //在user数据表中删除第10行记录
		
		
以上都是些基本语言，来自学习笔记，后期会做些实例..结合实例学习起来容易很多---再见---