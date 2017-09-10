---
layout: mongodb
title: express
date: 2017-09-10 11:55:25
tags:
---

# 下内容来自[github开源社区N-blog](https://github.com/nswbmw/N-blog)

由于记性比较差点,所以选择按照步骤,文字一个一个敲一遍,由于是开源社区,所以并没有征求所[创建者](https://github.com/nswbmw)的同意,如有需要,可以删除


## Mongodb + Nodejs + Express 搭建博客

### 安装Nodejs

> 安装Nodejs 有三种方式

> 一是通过安装包安装,二是通过源码编译安装,三是在Linux下可以通过`yum|apt-get`安装,在Mac 下可以通过[Homebrew](https://brew.sh/)安装,对于Windows和Mac用户,推荐使用安装包安装,Linux用户推荐使用源码编译安装

#### Windows 和 Mac 安装


- 打开[Nodejs官网](https://nodejs.org/en/)可以看到有两个下载选项,一个LTS版本,是长期支持版本,大多数人使用这个就可以了,右边是最新版本,支持最新的语言特性,(比如ES6的支持更全面),想尝试新特性的开发者可以安装这个版本,我们选择左边的LTS点击下载

> 提示: 从 [http://node.green](http://node.green)上可以看到Nodejs各个版本对ES6的支持情况

- 第二步: 安装Nodejs,没有什么好说的,和其他的安装程序一样,一路点击`继续`即可

- 第三步: 提示安装成功后,打开终端输入一下命令,可以看到`node`和`npm`都已经安装好了,在Windows系统下,在安装中如果没有勾选配置环境变量,需要自己手动添加环境变量

- Linux 安装: 可通过源码编译安装

```vim
  curl -O https://nodejs.org/dist/v6.9.1/node-v6.9.1.tar.gz
  tar -xzvf node-v6.9.1.tar.gz
  cd node-v6.9.1
  ./configure
  make
  make install
```

> 注意: 如果编译过程报错,可能是缺少某些依赖包,因为报错内容不尽相同,请自行求助搜索引擎或[stackoverflow](https://stackoverflow.com/)

#### n 和 nvm

> 当我们需要想尝试某些新的特性时,可能会需要有多个版本的Node存在,多个版本的Node可能会造成混乱,这个时候就需要使用一个版本管理工具来统一管理,[n](https://github.com/tj/n)和[nvm](https://github.com/creationix/nvm),关于n和nvm两者的使用区别,请参考[这篇文章](http://taobaofed.org/blog/2015/11/17/nvm-or-n/)

#### nrm

> [nrm]()是一个管理npm 源的工具,用过ruby和gem的同学可能会比较熟悉,通常我们会把gem源切到国内的淘宝镜像,这样在安装和更新一些包的时候比较快,nrm同理,用来切换官方npm源和国内的npm源(如[cnpm](https://cnpmjs.org/))当然也可以用来切换官方

全局安装nrm:

```vim
npm i nrm -g

# 查看当前nrm内置的几个npm源的地址
nrm ls

# 切换npm 源

nrm use cnpm
```

### require

> require用来加载一个文件的代码,关于require的机制请仔细阅读[官方文档](https://nodejs.org/api/modules.html)

简单概括一下几点:

- require可记载.js,.json和.node后缀的文件

- require的过程是同步的,所以这样是错误的

```javascript
setTimeou(() => {
  module.exports = { a: 'hello' };
}, 0)

```

require这个文件得到的是空对象`{}`

- require目录的机制是:

  - 如果目录下有package.json并制定了main字段,则用之

  - 如果不存在package.json,则一次尝试加载目录下的index.js,和index.node

require过的文件会加载到缓存,所以多次require同一个文件(模块)不会重复加载

- 判断是否是程序的入口文件有两种方式:

  - require.main === module (推荐)

  - module.parent === null

#### 循环引用

> 循环引用(或循环依赖)简单点来说就是a文件Require了b文件,然后b文件又反过来require了a文件,我们用a -> 代表b require 了a

## exports 和 module.exports

> require是用来加载代码,而exports 和 module.exports 则用来导出代码

```javascript
// test.js

var a = { name: 1 };
var b = a ;
console.log(a);
console.log(b);

b.name = 2;
console.log(a);
console.log(b);

var b = { name: 3 };
console.log(a);
console.log(b);
/**
解释: a是一个对象,b是对a的引用,即a和b指向同一块内存,所以前两个输出一样,当对b作修改时,即a和b指向同一块内存地址的内容发生了改变,所以a也会体现出来,所以第三四个输出一样,当b被覆盖时,b自新增了一块新的内存,a还是指向原来的内存,所以最后两个输出不一样
**/
```

- 1.module.exports 初始值为一个空对象{}

- 2. exports 是指向的module.exports 的引用

- 33. require()返回的是module.exports 而不是exports


### semever

> 语义化版本(semver)即dependencies, devDependencied和peerDependencies

semever格式: 主版本号.次版本号.修订号

- 主版本号: 做了不兼容的API修改

- 次版本号: 做了向下兼容的功能性新增

- 修订号:做了向下兼容的bug修正


