---
title: vue
author: Terry
date: 2021-04-26 14:20:57
banner_img: /lib/images/vue/bg.png
index_img: /lib/images/vue/head.png
tags: [Html,css,vue,webpack]
categories: 前端
---


### 安装要使用的包

```js
npm install webpack webpack-cli -S
	或
yarn add webpack webpack-cli -s
```

---

### 如果使用全局 cli 命令，可以全局安装 webpack-cli

```js
npm install webpack-cli -g
    或
yarn add global webpack-cli
```

---

### 在项目的根目录创建 webpack.config.js

```js
const path = require("path");
module.exports = {
  entry: "./src/index.js", // String || Object 可以写单个或者多个入口文件
  output: {
    // 出口
    path: path.resolve(__dirname, "dist"),
    filename: "[name][hash:8].js",
  },
};
```