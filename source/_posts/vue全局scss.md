---
title: vue全局使用scss变量
date: 2022-02-24 19:04:09
tags:
---
在vue中经常会遇到修改页面统一颜色的需求
在scss中，我们可以定义一个颜色变量，在每个要使用该颜色的地方，引入这个scss文件，使用里面的颜色变量。但每个地方都去引入过于繁琐，所以sass-loader给我们提供了一种全局引入的方式。
[sass-loader文档地址](https://github.com/webpack-contrib/sass-loader)
```javascript
{
    css: {
        loaderOptions: {
         	scss: {
                //  这里的名称根据不同的版本，名称不同
                // 下方有说明
                additionalData: `@import "@/assets/scss/_variable";`
	        }``
        }
    }
}
```
### 配置中常见的错误
#### 1.Module build failed
 (from ./node_modules/sass-loader/dist/cjs.js):
ValidationError: Invalid options object. Sass Loader has been initialized using an options object that does not match the API schema.- options has an unknown property 'prependData'. These properties are valid:

模块生成失败(from ./node_modules/sass-loader/dist/cjs.js):
ValidationError:无效的选项对象。已使用与API架构不匹配的选项对象初始化Sass加载程序。
-选项具有未知属性“prependData”。这些属性是有效的

解决方法：
这是因为sass-loader的版本不同，导致Api的名称不同。所以，要解决这个方法，首先我们要先去查看sass-loader的文档。

| 版本号 | Api名称          |
| ------ | ---------------- |
| v8-    | "data"           |
| v8     | "prependData"    |
| v10+   | "additionalData" |

#### 2.SassError: media query expression must begin with '('
如果配置了全局scss后，出现这个错误提示。不要慌，一猜就知道可能是刚刚的配置出现了问题。
可能是下面这段引入没有写分号，导致编译错误           
```javascript
{
    css: {
        loaderOptions: {
         	scss: {
                additionalData: `@import "@/assets/scss/_variable"`// 这里结尾因该以分号   
                 additionalData: `@import "@/assets/scss/_variable";`// 正确写法      
	        }``
        }
    }
}
```
