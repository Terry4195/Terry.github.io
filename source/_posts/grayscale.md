---
title: grayscale.js
date: 2021-09-27 10:20:03
index_img: https://qiniu.zhaoxinchuan.cn/javascript/index.webp 
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags: [javascript, 插件]
categories: JavaScript
---

> 我们经常会在一些网站中看到这样的效果,比如经常使用的B站,当某一个人逝世或者全国哀悼日的时候,会将网站所有模块置灰以示哀悼！

![示意图](https://qiniu.zhaoxinchuan.cn/grayscale/1.webp)

> 我们可以定义一个class类名,当到达某一个时间的时候,给某一个元素添加这个class类名以达到效果,但是这样也会产生一些问题,比如某个元素是定位到一个位置的,就会使效果达不到我们的需求,一个一个元素去
> 修改过于繁琐。所以就可以使用 <font color=red>grayscale.js</font> 这个库来进行修改
[grayscale.js文档](https://j11y.io/javascript/grayscaling-in-non-ie-browsers/)

``` javascript
// 引入文件
<script src="https://j11y.io/demos/grayscale/grayscale.js"><script>
<script>
// 方法调用
grayscale(document.getElementById("main"));
</script>
```

