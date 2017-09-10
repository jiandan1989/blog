title: TypeScript(基础知识一)
date: 2017-07-18 23:49:26
tags:
---
<!-- TOC -->

- [定义](#定义)
- [语言特性](#语言特性)
- [安装](#安装)
- [测试](#测试)
- [基础类型](#基础类型)
- [键入断言](#键入断言)
- [interface接口](#interface接口)
- [类](#类)
- [功能](#功能)

<!-- /TOC -->
### 定义

> TypeScript是一种由微软开发的只有和开源的编程语言,它是Javascript的一个超集(超集:等于是类型检查以及Javascript混合,Type + Javascript),扩展Javascript的语法

<!-- more -->

### 语言特性

- 类: class
- 接口: interface
- 模块: modules
- 类型注解: Type annotations
- 编译时类型检查: Compile time type checking
- Arrow 函数(类似C# 的Lambda表达式)

### 安装

- 通过Node.js包管理器(NPM)

```javascript
npm install -g typescript // 安装完成之后,我们就可以使用Typescript的编译器,名称为tsc,可将编译结果生成Js文件

tsc filename.ts // 编译ts后缀文件
```

- 通过与 Visual Studio 2012 继承的 MSI.([点击下载](https://marketplace.visualstudio.com/items?itemName=TypeScriptTeam.TypeScript10ToolsforVisualStudio2012))

### 测试

> 创建greeter.ts

```typescript
function greeter(person) {
  return `Hello ${person}`;
}

const user = '聂晓飞';
document.body.innerHTML = greeter(user);
```

> 编译代码

```vim
tsc greeter.ts // 在同目录下生成一个greeter.js文件
```

### 基础类型

- Boolean: 布尔类型 如`let isDone: Boolean = false;`
- Number: 数值类型 如 `let decimal: number = 6;`
- string: 字符串类型 如 `let color: string = 'blue';`
- 数组类型: 如 `(第一种方法)let list: number[] = [1, 2, 3];(第二种方法) let list: Array<number> = [1, 2, 3];`
- 元组: 元组类型允许您表达一个数组,其中固定数量的元素的类型是已知的,但不一定相同
- 枚举: 对Javascript的标准数据类行的一个有益的补充是`enum`,枚举是一种给数组值更多的友好名称的方法` enum Color { Red, Green, Blue }; let c: Color = Color.Green;`, 枚举的一个方便的功能是,你也可以从枚举中的数值到该值的名称,例如,如果我们有价值2单不知道Color上面的枚举映射什么,我们可以查找对应的名称`let colorName: string = Color[2];`
- 任意类型: 不确定变量类型时可以用`any`类型代替,并且当定义一个数组时,不确定数组元素的类型,可以`let list: any[] = [1, 2, '4'];`
- 空值(void): 为空类型
- null 和 undefined: 空 和 未定义
- never: 表示没有值的类型 如 `function error(message: string) :never { throw new Error(message);}`
- 多种类型可以用`|`隔开,比如`number|string|boolean`表示可以是`number` `string` 和 `boolean`类型

### 键入断言

> 有时候当知道某个实体的类型可能比其当前类型更具体时,会发生这种情况,类型断言是一种告诉编译器,我知道正在做什么的一种方式,类性断言就像其他语言中的类型转换,但不执行特殊检查或重组数据,它没有运行时影响,纯粹由编译器使用

类型断言有两种形式,一种是`<>`语法

```typescript
// 第一种
let someValue: any = 'this is a string';
let strLength: number = (<string>someValue).length;

// 第二种 as 合成

let someValue: any = 'this is a string';
let strLength: number = (someValue as string).length;
```

> 两个示例是等效的,使用其中一个主要是偏好的选择,然而当与JSX一起使用Typescript时,只能使用`as`进行断言

### interface接口

> TypeScript 的核心原则之一是对值所具有的结构进行类型检查,它有时被称作"鸭式辨型法"或"结构性子类型化"在Typescript里,接口的作用就是为这些类型命名和未你的代码或第三方代码定义契约

- 接口初探:

```typescript
function printLabel(labelObj: { label: string }) {
  console.log(labelObj.label);
}

let myObj = { size: 10, label: 'Size 10 Object' };
printLabel(myObj);
```

> 类型检查器会查看`printLabel`的调用,`printLabel`有一个参数,并要求这个对象参数有一个名为`label`类型为`string`属性,需要注意的是我们传入的对象参数实际上会包含很多属性,但是编译器只会检查那些必须的属性是否存在,并且其类型是否匹配

- 重写上面的例子,这次试用接口来描述,必须包含一个`label`属性且类型为`string`

```typescript
interface LabeledValue {
  label: string;
}

function printLabel(labelObj: LabeledValue) {
  console.log(labelObj.label);
}

let myObj = { size: 10, label: 'Size 10 Object' };
printLabel(myObj);

```

`LabeledValue` 接口就好比一个名字,用来描述上面例子的要求,它代表了有一个`label`属性且类型为`string`的对象,需要注意的是,我们在这里并不能像在其他语言里一样,说传给`printLabel`的对象实现了这个接口,我们只会去关注值的外形,只要传入的对象满足上面提到的必要条件,那么它就是被允许的,还有一点值得提的是,类型检查器不会去检查属性的顺序,只要相应的属性存在并且类型也是对的就可以

- 可选属性

> 接口里的属性不却都是必须的,有些事只在某些条件下存在,或者根本不存在,可选属性在应用`option bags`模式下很常用,即给函数传入的参数中只有部分属性赋值了

```typescript
interface SquareConfig {
  color?: string;
  width?: number;
}

function createSquare(config: SquareConfig) : {color: string; area: number} {
  let newSquare = { color: 'white', area: 100 };
  if(config.color) {
    newSquare.color = config.color;
  }
  if(config.width) {
    newSquare.area = config.width * config.width;
  }
  return newSquare;
}

let mySquare = createSquare({ color: 'black' });

console.log(mySquare);
```

- 只读属性

> 一些对象属性只能在对象刚刚创建的时候修改其值,你可以再属性名前用`readonly`来指定只读属性

```typescript
interface Point {
  readonly x: number;
  readonly y: number;
}

let p1: Point = { x: 10, y: 20 };
p1.x = 5 // error
```
> Typescript 具有`ReadonlyArray<T>`类型,它与`Array<T>`相似,只是把所有的可变方法去掉了,因此可以确保数组创建后再也不能被修改:

```typescript
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error
ro.push(1); // error
ro.length = 100; //error
a = ro; // error
```

> 上面代码的最后一行,可以看到就算把整个`ReadonlyArray`赋值到一个普通数组也是不可以的,但是你可以用类型断言重写

`a = ro as number[];`


### 类

### 功能
