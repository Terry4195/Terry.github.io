---
title: es6
author: Terry
date: 2021-04-26 19:20:57
index_img: https://qiniu.zhaoxinchuan.cn/es6/index.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
layout: true
tags: [JavaScript, es6]
categories: JavaScript
---
* ECMAScript6 就是 ECMAScript2015

## 调试
* 浏览器调试,使用最新版本的浏览器,可以调试一些Es6的语法
* 使用nodeJs调试
* 使用babel翻译
     ```js
        npm install babel-cli -g
            or 
        yarn add babel-cli global
     ```
     * 使用命令行前,先在项目根目录下创建 .babelrc 文件
        * npm install -D babel-presset-es2015
        * yarn add babel-presset-es2015 --dev
     ```babel
        .babelrc
        {
            "presets": ["es2015"]
        }
     ```

## const let 关键字
```javascript
    // 声明一个只读的常量，一旦声明，常量的值就不能改变。
    const name = "tom";
    // 我们尝试修改
    name = "jerry";
    // 此时报错： Assignment to constant variable(对常量变量的赋值)

    /**---------------------------分割线---------------------------*/

    // let 声明的变量只在 let 命令所在的代码块内有效
    {
        let inside = "inside";
    }
    console.log(inside);
    // 此时报错： inside is not defined
```
## 扩展运算符
```javascript
    // 扩展运算符写法 ... 三个点
    // 例1：参数传递
    let nums = [1,2];
    function add(a,b){
        console.log(a+b);
    };
    // 在 es6以前,我们都是使用apply传递这种参数类型
    add.apply(null,nums); // 3
    // 使用扩展运算符
    add(...nums); // 3

    /**---------------------------分割线---------------------------*/

    // 例2：数组合并 || 复制
    const arr1 = [1,2];
    const arr2 = [3,4];
    //  在 es6以前, concat
    const arr3 = arr1.concat(arr2);
    // 使用扩展运算符
    const arr4 = [...arr1,...arr2];

    /**---------------------------分割线---------------------------*/

    // 例3：字符串转数组
    const strToArr = [..."say hello"];
```

## 解构赋值
```javascript
    // 例1：数组的解构赋值
    const [a,b,c] = [1,2,3];
    console.log(`a:${a};b:${b};c:${c}`);
    // a:1;b:2;c:3
    // 左右结构相同,就会把右边的值赋值给左边接收的参数

    const [name,age] = ["jerry"];
    console.log(`name:${name};age:${age}`);
    // name:jerry;age:undefined
    // 没有值的参数,会被赋值为undefined
    
    // 如果想取指定位置的值
    const [_name,,_eat] = ["tom","18","fish"];
    console.log(`_name:${_name};_eat:${_eat}`);
    // _name:tom;_eat:fish

    /**---------------------------分割线---------------------------*/

    // 例2：对象的解构
    const {data,data: {name},code,msg} = {data: {name:"jerry"},code:0,msg:"ok"};
    console.log(`data:${data};name:${name};code:${code};msg:${msg};`);
    // data:[object Object];name:jerry;code:0;msg:ok;
    
    
```
