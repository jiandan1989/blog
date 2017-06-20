title: nodejs path对象
date: 2016-07-11 22:59:43
tags:
---
NodeJS中的Path对象，用于处理目录的对象，提高开发效率。

用NodeJS的Path命令，与使用Linux下的shell脚本命令相似。

引入path对象

`const path = require('path');`

比较实用的方法：

<!--more-->

f;lsknflsknfskjfnksjfndskjn

#### 格式化路径  path.normalize(p)  ####

特点：将不符合规范的路径格式化，简化开发人员中处理各种复杂

```javascript
path.normalize('/foo/bar//baz/asdf/quux/..');
// returns
'/foo/bar/baz/asdf'
```
#### 路径联合 path.join([path1], [path2], [...])  ####

特点：将所有名称用path.seq串联起来，然后用normailze格式化

```javascript
path.join('///foo', 'bar', '//baz/asdf', 'quux', '..');
// returns
'/foo/bar/baz/asdf'
```

#### 文件夹名称 path.dirname(p)  ####

特点：返回路径的所在的文件夹名称

```javascript

path.dirname('/foo/bar/baz/asdf/quux')
// returns
'/foo/bar/baz/asdf'
const path = require('path');

const url1 = path.dirname('/foo/bar/baz/asdf/a.txt');
const url2 = path.dirname('/foo/bar/baz/asdf/');
const url3 = path.dirname('C:/vajoy/test/aaa');

console.log('url1:',url1);  // /foo/bar/baz/asdf
console.log('url2:',url2);  // /foo/bar/baz
console.log('url3:',url3);  // C:/vajoy/test
```

#### 文件名称 path.basename(p, [ext])  ####

特点：返回指定的文件名，返回结果可排除[ext]后缀字符串 返回路径中的最后一部分，类似于Unix 的 basename 命令。 ext 为需要截掉的尾缀内容：

```javascript
path.basename('/foo/bar/baz/asdf/quux.html')
// returns
'quux.html'

path.basename('/foo/bar/baz/asdf/quux.html', '.html')
// returns
'quux'
const path = require('path');
const url1 = path.basename('/foo/bar/baz/asdf/a.txt');
const url2 = path.basename('/foo/bar/baz/asdf/a.txt','.txt');
const url3 = path.basename('/foo/bar/baz/asdf/');
const url4 = path.basename('C:/vajoy/test/aaa');

console.log('url1:',url1);  // a.txt
console.log('url2:',url2);  // a
console.log('url3:',url3);  // asdf
console.log('url4:',url4);  // aaa
```

#### 扩展名称 path.extname(p)  ####

 特点：返回指定文件名的扩展名称

```javascript
path.extname('index.html')
// returns
'.html'

path.extname('index.')
// returns
'.'

path.extname('index')
// returns
' '
const path = require('path');
const url1 = path.extname('/foo/bar/baz/asdf/a.txt');
const url2 = path.extname('/foo/bar/baz/asdf/a.txt.html');
const url3 = path.extname('/foo/bar/baz/asdf/a.');
const url4 = path.extname('C:/vajoy/test/.');
const url5 = path.extname('C:/vajoy/test/a');

console.log('url1:',url1);  // .txt
console.log('url2:',url2);  // .html
console.log('url3:',url3);  // .
console.log('url4:',url4);  //
console.log('url5:',url5);  //
```

#### 路径分隔符 path.sep  ####

特点：获取文件路径的分隔符，主要是与操作系统相关

linux:

```javascript
'foo/bar/baz'.split(path.sep)
// returns
['foo', 'bar', 'baz']

window:

'foo\\bar\\baz'.split(path.sep)
// returns
['foo', 'bar', 'baz']
```

#### path.delimiter ####

返回对应平台下的路径分隔符，win下为';'，*nix下为':'：

```javascript
const path = require('path');
const env = process.env.PATH; //当前系统的环境变量PATH
const url1 = env.split(path.delimiter);

console.log(path.delimiter); //win下为“;”，*nix下为“:”
console.log('env:',env);  // C:\ProgramData\Oracle\Java\javapath;C:\Program Files (x86)\Intel\iCLS Client\;
console.log('url1:',url1);  // ['C:\ProgramData\Oracle\Java\javapath','C:\Program Files (x86)\Intel\iCLS Client\']
```

#### path.isAbsolute(path) ####

判断 path 是否绝对路径。这块可以理解为，path 是否真的是一个绝对路径（比如 'E:/abc'），或者是以“/”开头的路径，二者都会返回true：

```javascript
const path = require('path');
const url1 = path.isAbsolute('../testFiles/secLayer');
const url2 = path.isAbsolute('./join.js');
const url3 = path.isAbsolute('temp');
const url4 = path.isAbsolute('/temp/../..');
const url5 = path.isAbsolute('E:/github/nodeAPI/abc/efg');
const url6 = path.isAbsolute('///temp123');

console.log('url1:',url1);  // false
console.log('url2:',url2);  // false
console.log('url3:',url3);  // false
console.log('url4:',url4);  // true
console.log('url5:',url5);  // true
console.log('url6:',url6);  // true
```

#### 相对路径 path.relative(from, to)  ####

特点：返回某个路径下相对于另一个路径的相对位置串，相当于：path.resolve(from, path.relative(from, to)) == path.resolve(to)

```javascript
path.relative('C:\\orandea\\test\\aaa', 'C:\\orandea\\impl\\bbb')
// returns
'..\\..\\impl\\bbb'

path.relative('/data/orandea/test/aaa', '/data/orandea/impl/bbb')
// returns
'../../impl/bbb'

const path = require('path');

const url1 = path.relative('C:\\vajoy\\test\\aaa', 'C:\\vajoy\\impl\\bbb');
const url2 = path.relative('C:/vajoy/test/aaa', 'C:/vajoy/bbb');
const url3 = path.relative('C:/vajoy/test/aaa', 'D:/vajoy/bbb');

console.log('url1:',url1);  //..\..\impl\bbb
console.log('url2:',url2);  //url2: ..\..\bbb
console.log('url3:',url3);  //D:\vajoy\bbb
```

#### path.resolve([from ...], to) ####

从源地址 from 到目的地址 to 的绝对路径。

可以理解为 cd XXX 的形式，如在D盘上执行 path.resolve('a', 'D:/b', '../c', 'v.txt')，得到的绝对路径“D:/v.txt”，相当于执行如下指令后所处的路径：

```javascript
cd a
D:
cd b  //同上一行对应 'D:/b'
cd ../c
cd v.txt
const path = require('path');

const url1 = path.resolve('.', 'testFiles/..', 'trdLayer');
const url2 = path.resolve('..', 'testFiles', 'a.txt');
const url3 = path.resolve('D:/vajoy', 'abc', 'D:/a');
const url4 = path.resolve('abc', 'vajoy', 'ok.gif');
const url5 = path.resolve('abc', '/vajoy', '..', 'a/../subfile'); //'abc'参数将被忽略，源路径改从'E:/vajoy'开始

console.log('url1:',url1);  // E:\github\nodeAPI\path\trdLayer
console.log('url2:',url2);  // E:\github\nodeAPI\testFiles\a.txt
console.log('url3:',url3);  // D:\a
console.log('url4:',url4);  // E:\github\nodeAPI\path\abc\vajoy\ok.gif
console.log('url5:',url5);  // E:\subfile
```

要注意的是，如果某个 from 或 to 参数是绝对路径（比如 'E:/abc'，或是以“/”开头的路径），则将忽略之前的 from 参数。

<hr/>

摘自网络
