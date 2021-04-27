---
title: webpack基本使用
author: Terry
date: 2020/4/26 12:46:25
---
## 安装要使用的包

```js
npm install webpack webpack-cli -s
	  或
yarn add webpack webpack-cli -s
```

---

## 如果使用全局 cli 命令，可以全局安装 webpack-cli

```js
npm install webpack-cli -g
    或
yarn add global webpack-cli
```

---

## 配置文件创建
### 初始化
   在项目根目录创建：webpack.config.js

   <font color=red bgcolor=red size=4>entry--></font>文件入口；
   <font color=red size=4>output--></font></span>文件出口；
   <font color=red size=4>module--></font></span>模块依赖；
   <font color=red size=4>plugin--></font></span>插件配置；
```js
const path = require("path");
module.exports = {
  entry: "./src/index.js", // String || Object 可以写单个或者多个入口文件
  output: {
    // 出口
    path: path.resolve(__dirname, "dist"),
    filename: "[name][hash:8].js",
  },
  module： {},
  plugin: []
};
```
### 命令行配置

```js
// package.json
// 使用命令
// npm server || npm build
// yarn server || yarn build
"scripts": {
  "server": "webpack-dev-server", //开发环境 热更新
  "build": "webpack" // 生产环境 打包 
},
```


## ES6转ES5
### ES6转ES5 (module: babel-loader,@babel/core,@babel/preset-env)
```javascript
command:
  npm install babel-loader @babel/core @babel/preset-env -D
    或
  yarn add babel-loader @babel/core @babel/preset-env -D

code:
  module: {
    rules: [
      {
        test: /\.js$/,   // 匹配 .js后缀的文件
        use: "babel-loader", // 使用babel-loader
        exclude: /node_modules/,  // 排除node_modules中的js文件
      }
    ] 
  }
```
### 在项目根目录(与webpack.config.js同级)创建文件 .babelrc
``` js
{
  "presets": [["@babel/preset-env"]],
  "plugins": []
}

```
---

## css打包处理
### loader:
```js
command:
  npm install style-loader css-loader -D
    或
  yarn add style-loader css-loader -D
code:
  module: {
    rules: [
      {
        test: /\.css$/,
        use: ["style-loader", "css-loader"],
      },
    ] 
  }
```
### less处理
```js
command:
  npm install less-loader -D
    或
  yarn add less-loader -D
code:
  module: {
    rules: [
      {
        test: /\.less$/,
        use: ["style-loader", "css-loader","less-loader"],
      },
    ] 
  }  
```
### sass处理
```js
command:
  npm install sass-loader node-sass -D
    或
  yarn add sass-loader node-sass -D
code:
  module: {
    rules: [
      {
        test: /\.less$/,
        use: ["style-loader", "css-loader","sass-loader"],
      },
    ] 
  }  
```
### 处理后产生的问题
打包后,由于css文件是以字符串的形式存在于打包后的js文件中,当网络不畅时/或打出的包文件过大的时候,页面的样式不会一下子加载出来,导致页面只渲染出了dom结构,没有渲染出样式.

解决方法：

```js
npm install mini-css-extract-plugin -D
  或
yarn add mini-css-extract-plugin -D
```
使用方式：

  webpack.config.js头部引入当前包
```js
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
// 修改 module -> rules -> /\.css$/ 中的 use
module: {
  rules: [
    {
      test: /\.css$/,
      use: [MiniCssExtractPlugin.loader, "css-loader"],  // 使用MiniCssExtractPlugin的loader
    }
  ]
}
// plugin配置
  plugin: [
    new MiniCssExtractPlugin({
      filename:"style.css"   // 重命名
    })
  ]
```

## 图片打包处理
### 使用的包
<font color=red>
  这里推荐使用<font color=pink>url-loader</font>,因为<font color=pink>url-loader</font>封装了<font color=pink>file-loader</font>,当图片大小小于options中的limit参数时,会把图片数据转换成base64字符串,如果大于limit参数时,使用file-loader加载图片
</font>

```js
npm install url-loader -D
  或者
yarn add url-loader -D
```
### 代码块
```js
  module: {
    rules: [
      {
        test: /\.(png|jpg|jpeg)$/,
        use:{
          loader: "url-loader",
          options: {
            limit: 4096 // 图片大小上限4kb
          }
        }
      }
    ]
  }
```
