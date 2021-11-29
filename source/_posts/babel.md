---
title: 在项目中如何安装配置和使用babel
date: 2020-01-23 16:55:51
index_img: https://qiniu.zhaoxinchuan.cn/webpack/index.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags: [babel]
categories: 前端工具
---
### 1.在项目下初始化 package.json
```
npm init
```

### 2.在项目中安装babel
```
npm install babel-cli --save-dev
```

### 3.安装babel插件
```
npm install babel-preset-xxxxxx --save-dev
```
<font color=red>Babel5是默认包含各种转换插件，Babel6.x相关转换插件需要下载对应的插件，如果不去安装这些插件，那么在命令行进行转换时是不会有任何效果的.下面以安装es2015举例</font>
```
npm install babel-preset-es2015 --save-dev
```

### 4.配置文件.babelrc
```
把所使使用的插件对应的规则加入.babelrc。
{
  "presets": ["es2015"],
　"plugins": ["transform-es2015-arrow-functions"]
}
```

### 5.配置presets:

#### a.es2015
```
check-es2015-constants // 检验const常量是否被重新赋值

transform-es2015-arrow-functions // 编译箭头函数

transform-es2015-block-scoped-functions // 函数声明在作用域内

transform-es2015-block-scoping // 编译const和let

transform-es2015-classes // 编译class

transform-es2015-computed-properties // 编译计算对象属性

transform-es2015-destructuring // 编译解构赋值

transform-es2015-duplicate-keys // 编译对象中重复的key，其实是转换成计算对象属性

transform-es2015-for-of // 编译for…of

transform-es2015-function-name // 将function.name语义应用于所有的function

transform-es2015-literals // 编译整数(8进制/16进制)和unicode

transform-es2015-modules-commonjs // 将modules编译成commonjs

transform-es2015-object-super // 编译super

transform-es2015-parameters // 编译参数，包括默认参数，不定参数和解构参数

transform-es2015-shorthand-properties // 编译属性缩写

transform-es2015-spread // 编译展开运算符

transform-es2015-sticky-regex // 正则添加sticky属性

transform-es2015-template-literals // 编译模版字符串

transform-es2015-typeof-symbol // 编译Symbol类型

transform-es2015-unicode-regex // 正则添加unicode模式

transform-regenerator // 编译generator函数
```

#### b.es2016
```
transform-exponentiation-operator // 编译幂运算符
```

#### c.es2017
```
syntax-trailing-function-commas // function最后一个参数允许使用逗号

transform-async-to-generator // 把async函数转化成generator函数
```
#### d.latest:latest是一个特殊的presets，到目前为止包括了es2015，es2016，es2017的插件。
#### e.react:加入了flow，jsx等语法.
#### f.stage-x(stage-0/1/2/3/4):按照JavaScript的提案阶段区分的，一共有5个阶段。而数字越小,阶段越靠后.

### 6.配置plugins
引入需要的插件,以下仅以引入箭头函数举例
```
{
  "plugins": ["transform-es2015-arrow-functions"]
}
```
另外babel还支持自定义presets 和 plugins.
完成以上配置就安装好babel了, 可以使用以下的babel的命令进行编译了
#### 6.1.在当前命令行输出转换
```
babel test1.js
```
#### 6.2.将转换后的js输出到指定文件中（使用 -o 或 --out-file ）
```
babel a.js -o b.js 
// 或者
babel a.js --out-file b.js
```
#### 6.3.实时监控（使用 -w 或 --watch ）
```
babel a.js -w --out-file b.js
// 或者
babel a.js --watch --out-file b.js
```
#### 6.4.编译文件夹并输出到文件夹中（使用 -d 或 --out-dir ）
```
babel src -d lib
// 或者
babel src --out-dir lib
```