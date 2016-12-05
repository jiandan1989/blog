title: String
date: 2015-12-07 19:43:18
tags:
---
## 字符串：##

JS字符串是由Unicode字符、数字、标点符号等组成的序列。

	var str ="字符串"; or var str = '字符串'在JS中，包裹字符串单引号与双引号没有任何区别。但是还是建议使用双引号。
	var str = '""'//定义了一个仅含有一个双引号的字符串。
	var str = "''"//定义了一个仅含有一个单引号的字符串。
	var str = " "//定义一个包含空格的字符串
	
JS字符串的唯一默认属性：str.lengt=字符串的长度，我们可以调出开发者工具
	
	var str = new String 
	console.log(String.prototype)//可以看出length:0
	
### 字符串的几种方法

<!--more-->

1.indexOf()方法可以返回某个指定的字符串值在字符串中首次出现的位置

	 var str = "1 1 1 1 1 2 2"
	 (1) console.log(str.indexOf('1'))//需要有引号
	 (2)console.log(str.indexOf('3'))//当前字符串中没有这个字符的	时候返回的值都是-1.
	 (3) console.log(str.indexOf('1',0))
	 indexOf()方法中可以有两个参数，indexOf('str',0)第一个参数必
	 须有，第二个参数表示从字符串中第几个字符开始查找，当第二个参数不
	设置的情况下默认值为0.
	（4）lastIndexOf可以理解为倒序。从后边开始查找。
	
2.slice()方法可提取字符串的某个部分，并以数组的形式显示。有两个参数
	
	var str="1 2 3"; 
	var arr = str.slice(0,4)//第一个参数表示起点位置，第二个参数表示结束位置（结束位置下标的字符不在内包括）。
	console.log(arr)//输出1 2 
	var arr2 = str.slice(0)//一个参数时表示从第几个下标开始计算，直
	到最后一个字符结束。
	
3.split()方法用于把一个字符串分割成字符的数组
，str.split('value',length)第一个参数表示用value当作分隔符来分割字符串。第二个参数表示生成新数组的长度

	var str = '1 2 3';
	var arr = str.split(' ',3)//输出['1','2','3']就是用空格来分割


4.substring()提取相应下标的字符。

	var str='a b c';
	console.log(str.substring(0,3))//有两个参数时第一个表示起点
	位置第二个表示结束位置，但不包括结束下标的字符。
	
5。charCodeAt()返回指定下标位置的字符的Unicode编码，

6.charAt()返回指定下标位置的字符；只有一个参数。

7.toLowerCase()把字符串全部转化为小写，没有参数。

8.toUpperCase()把字符串全部转化为大写，没有参数。

9.search()方法执行一个查找，看该字符串对象与一个正则表达式是否匹配。

参数：一个正则表达式（regular expression）对象。如果传入一个非正则表达式对象，则会使用 new RegExp(obj) 隐式地将其转换为正则表达式对象。如果匹配成功，则 search() 返回正则表达式在字符串中首次匹配项的索引。否则，返回 -1。
	
		var str = 'abcdefg';
		str.search(/abc/); //返回匹配到abc的索引位置 0
		str.search(/h/); //-1
		
10.match()当字符串匹配到正则表达式（regular expression）时，match() 方法会提取匹配项。

参数

regexp
一个正则表达式对象。如果传入一个非正则表达式对象，则会隐式地使用 new RegExp(obj) 将其转换为正则表达式对象。

返回值

array
一个包含匹配结果的数组，如果没有匹配项，则返回 null。

描述EDIT
如果正则表达式没有 g 标志，返回和 RegExp.exec(str) 相同的结果。而且返回的数组拥有一个额外的 input 属性，该属性包含原始字符串。另外，还拥有一个 index 属性，该属性表示匹配结果在原字符串中的索引（以0开始）。

如果正则表达式包含 g 标志，则该方法返回一个包含所有匹配结果的数组。如果没有匹配到，则返回 null。

		var str = "For more information, see Chapter 3.4.5.1";
		var re = /(chapter \d+(\.\d)*)/i;
		var found = str.match(re);

		console.log(found);

		// logs ["Chapter 3.4.5.1", "Chapter 3.4.5.1", ".1"]

		// "Chapter 3.4.5.1" is the first match and the first value 
		//  remembered from (Chapter \d+(\.\d)*).

		// ".1" is the last value remembered from (\.\d).

### 最后做个练习

用上面的几种方法把字符串中的空格去除掉

	var str = 'a b c d e f';
	(1).split和join
		var arr = str.split(' ');
		console.log(arr.join(''));
	(2).循环和split
		var arr=str.split(' ')
		var str2 = '';
		for(var i=0; i <arr.length; i++){
			str2 += arr[i];
			}
	(3).循环和charAt()
		var str2 = ''
		for(var i =0; i < str.length; i++){
			if(str.charAt(i)!=' ');{
				str2 += str.charAt(i)
			},
			if(str.charAt(i)==' '){
				str3 += str[i]
			}
			
		}
	(4)循环
		var str2 = ''//定义一个空的字符串，
		var str3 = ''
		for(var i =0; i < str.length; i ++){
			if(str[i] !=' '){
				str2 += str[i]
			}
			if(str[i] == ' '){
				str3 += str[i]
			}
		}
	(5)function()方法
		(function(lib){
			var helper={
				init:function(){
					this.opction = {
						str:opction.str
					}
				}
				this.fn();
			},
			fn:function(){
			var str = this.opction.str;
			var arr = str.split(' ');
			var str2 = '';
			for(var i=0; i <arr.length; i++){
				str2 += arr[i];
			}
			}
			lib.helper = helper;
		})(window.lib={});
		window.lib.helper.init({
			str:'1 2 3 4 5 6 7'
		})
		
		
### 以上方法可以自己试一下 ###
	