---
title: TypeScript
date: 2022-02-24 15:57:49
tags:
---

### TypeScript

TypeScript 是 JavaScript**类型**的超集

优点：
TypeScript 可以在任何浏览器，任何计算机和任何操作系统上运行(多平台使用)

### 1.安装 TypeScript

```
npm install -g typesctipt
```

### 2.创建.ts(typescript 文件的扩展名)文件

```TypeScript
// demo.ts
function getName(name:string):string{
	return name;
}

```

上面的代码和我们平时写的 JavaScript 代码看起来是不是有那么一点不一样？没错，多了一些我们平时在一些强类型语言中才看到的-类型定义。

```Java
// java
int num = 12;
```

这就是 TypeScript 中重要的特点-类型注解

### 3.TypeScript 高级功能

#### 3.1 类型注解

在 JavaScript 语言中包含两种数据类型
1.基本数据类型
Number
String
Boolean
undefined
Null
BigInt
Symbel
2.引用数据类型
Object
Array
Function
Date
RegExp

那么怎么使用 TypeScript 去定义这些类型呢？

##### 3.1.1 基本数据类型-类型注解

###### number 类型

```JavaScript
// number类型
let num:number = 1;
let num1:number = 0xf11d;
let num2:number = 0b1011;
let num3:number = 0o747;
// 和JavaScript一样，TypeScript中的所有数字都是浮点数，支持十、十六、二、八进制
```

要给一个变量定义它的类型，我们只需要在变量名的后面加**冒号**和声明的数据类型就可以了
如果我们修改 num 这个变量，并且将修改的值设为不是 number 类型的会怎么样？

```JavaScript
num = "123";
// 在编辑器中，num这个变量名下方会有一个注意标示(红色波浪线)，并且将光标移动到变量名，提示框中会给我们说明这个错误的原因。
// 比如上方修改 num = "123"
// 提示框显示：不能将类型“string”分配给类型“number”
// 因为在声明变量num的时候，我们已经将它的类型定义为 number类型，如果修改变量值，那么只能将这个变量设置为 number类型的值
num = 123;
```

##### string 类型

```JavaScript
// string类型
let str1:string = "";
let str2:string = "这是一段字符串";
let str3:string = `模板字符串，${str2}`;
```

##### boolean 类型

```JavaScript
// boolean类型
let bool:boolean = true;
```

##### undefined 类型

```JavaScript
// undefined类型
let undefined:undefined = undefined;
// undefined是指在变量声明时，没有给变量进行赋值。那么这个值就是undefined
let temp:undefined;
console.log(temp);
// undefined
```

##### null 类型

```JavaScript
// null类型
let bool:null = null;
```

#### 3.1.2 引用数据类型

##### Array 类型

```JavaScript
// 定义一个内部数据为number的数组
let arr1:number[] = [1,2,3];
// 或者使用-泛型(泛型的定义在后面部分)
let arr2:Array<number> = [1,2,3];
// 定义一个包含多种类型的数组,注意值的位置和类型的位置一致
let arr3:[number,string,boolean] = [1,"2",true];
```

#### 3.2 接口-interface

##### 3.2.1 接口的定义

1.关键字 interface
<br>

```JavaScript
interface 名称 {
	//需要定义的数据
};
```

##### Object 类型

```JavaScript
// 在定义Object类型的时候，里面会有很多的数据类型，所以就有了interface来帮我们检测这个数据是否符合我们的要求
const user = {
	id:1,
	name:"小明",
	age:18,
	height: 170
};
```

我们在看到上面这个 user 对象的时候，第一眼就确定了里面数据的类型，name 是一个字符串(string),age 是一个数字(number),但当这个数据是后台返回的，我们并不确定这个数据是否是我们想要的类型，或者我们编码的时候写错了类型，将 age 写成 string 类型了，如果代码量过大，就会给维护造成时间成本，所以接口(interface)就是来帮我们检测这个数据是否符合我们的预期值。

```
interface IUser {
	readonly id:number,
	name: string,
	age: number,
	weight?: number
};
```

上方的接口我们就定义好了，其中
<br>
**readonly**表示这个属性只能读取，不能修改。这个属性有点类似于 ES6 中的 const。
<br>
属性名后面的**问号(?)**-可选参数、可选属性，表示这个属性是可选的，在使用的时候，可以不写这个属性。

接口的使用：

```JavaScript
interface IUser {
	readonly id:number,
	name: string,
	age: number,
	weight?: number
};
let user:IUser = {
	id:2，
	name:"小红",
	age:16
};
```
