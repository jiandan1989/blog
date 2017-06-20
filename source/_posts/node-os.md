title: node-os
date: 2016-03-30 14:02:53
tags:
---
关于node 有很多用法，我们也可以用node 来查看关于电脑的一些信息比如说电脑操作系统的版本以及内存的使用量，下面我们来看看使用node怎么来查看关于电脑的信息吧。

首先先创建一个js文件(os.js)

在os.js的文件中我们引入os模块

`const os = require("os"); //引入os模块`

使用console.log()方法来查看我们要查看的信息。

`console.log(os.platform) //查看当前的操作平台`

写好这些代码之后呢  我们看一下在os模块下的方法

<!--more-->

- os.platform ()->查看当前的操作平台，mac电脑下显示的darwin

- os.freemem() 返回当前操作系统空闲内存量，单位是字节

- os.totalmem() ->返回系统内存总量，单位为字节

- os.uptime() ->返回操作系统运行的时间，以秒为单位

- os.release() ->返回操作系统的发行版本

- os.arch() ->返回操作系统CPU架构，可能的值有x64 arm 和ia32

- os.hostname() - >返回操作系统的主机名

- os.tmpdir() 返回系统临时目录

- os.endianness() 返回CPU的字节序，可能的是BE活LE

- os.type() 返回操作系统的名称

- os.loadavg() 返回一个包含1、5、15分钟平均负载的数组

- os.cpus() 返回一个对象数组，包含所安装的每个CPU/内核的信息：型号、速度（单位MHz）、时间(一个包含user、nice、sys、idle 和 irq 所使用CPU/内核毫秒数的对象)

- os.EOL 一个定义了操作系统的一行结束的标识的常量

- os.networkInterfaces() 获取网络接口的一个列表信息

***process 进程管理***

process是一个全局变量，无需require

- 返回应用程序当前目录---> process.cwd()

- 改变应用程序目录--->process.chdir("目录")

- 标准输出流，将内容打印到输出设备上.console.log()就是封装了它 --->process.stdout.write("aa\n")

- 标准错误流 --->process.stderr.write("aa\n")

- 进程的输入流，通过注册事件的方式来获取输入的内容

```javascript
process.stdin.on("readable",function(){

  var chunk = process.stdin.read();
  if(chunk!==null){
    process.stdout.write("data"+ chunk);
  }
});
```

- 结束进程---> process.exit(code) 参数code为推出后返回的代码，如果省略则默认返回0

- 注册事件 ---> process.stdout.on("data",function(data){console.log(data)});

- 为事件循环设置一项任务，node.js会在下次事件循环调响应式调用callback---> process.nextTick(callback)

- 设置编码，默认utf8. node.js编码格式只支持UTF8、ascii、base64，暂时不支持GBK、gb2312

- process.stdin.setEncoding(编码)

- process.stdout.setEncoding(编码)

- process.stderr.setEncoding(编码)

**fs 文件管理**

`fs模块提供了异步和同步两个版本fs.readFile() fs.readFileSync()`

***1 、写入文件内容***

`fs.writeFile("test.txt","Hello Node",[encoding],[callback]);`

***2、 追加写入***

`fs.appendFile("test.txt","Hello Node",[encoding],[callback]);`

***3、 查看文件是否存在***

`fs.exists("test.txt",[callback]);`

***4、修改文件名***

`fs.rename(旧文件，新文件，[callback]);`

***5、移动文件，没有专门函数，通过修改文件名可以达到目的***

`fs.rename(oldPath,newPath,[callback]);`

***6、读取文件内容***

`fs.readFile("test.txt",[encoding],[callback]);`

***7、 删除文件***

`fs.unlink("test.txt",[callback]);`

***8、创建目录***

`fs.mkdir(路径，权限，[callback]);   目录:新创建的目录 权限:可选参数，只在linux下有效，表示目录的权限，默认为0777，表示文件所有者、文件所有者所在的组的用户、所有用户，都有权限进行读、写、执行的操作。`

***9、删除目录***

`fs.rmdir(path,[callback]);`

***10、读取目录，读取到指定目录下所有的文件***

`fs.readdir(path,[callback]);`

***11、 打开文件***

`fs.open(path,flags,[mode],[callback]);`

***12、关闭文件***

`fs.close(fd,[callback]); fd是打开文件后的标示符`

***13、读取文件***

`fs.read(fd,buffer,offset,length,position,[callback(err,bytesRead,buffer)])`

 ***14、写入文件***

`fs.writeFile(filename,data,[encoding],[callback]);`

***15、获取真实路径***

`fs.realpath(path,[callback(err,resolvedPath)])`

***16、更改所有权***

`fs.chown(path,uid,gid,[callback])`

***17、更改权限***

`fs.fchmod(fd,mode,[callback(err)])`

***18、获取文件信息***

`fs.stat(path,[callback(err,stats)])`

***19、创建硬链接***

`fs.link(srcpath,dspath,[callback(err)])`

***20、读取链接***

`fs.readlink(path,[callback(err,linkString)])`

 ***21、修改文件时间戳***

`fs.utimes(path,atime,mtime,[callback(err)])`

 ***22、同步磁盘缓存***

`fs.fsync(fd,[callback(err)])`

---------------暂时告一段路 后期还有  会补上----------------------
