---
title: vue3
date: 2021-05-31 10:36:04
index_img: https://qiniu.zhaoxinchuan.cn/vue3/index.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags: [vue]
categories: 框架
---
### 初识vue3
#### hello world
``` javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>初时vue3</title>
</head>

<body>
    <div id="app">

    </div>
    <script src="https://unpkg.com/vue@next"></script>
    <script>
        const app = Vue.createApp({
            template: `<div>Hello world!</div>`
        });
        app.mount("#app");
    </script>
</body>

</html>
```
#### 对比vue2 - vue3
``` javascript
// 实例化对比
// vue2
const vm = new Vue({
    el: "元素ID",
    data: {},
    methods: {}
});

// vue3
const app = Vue.createApp({
    data(){
        return{}
    },
    methods: {}
});
const vm = app.mount("元素ID");
```
#### 生命周期对比
<style>
    .img{width:50%}
    .flex{
        display:flex;
    }
    .text-center{
        text-align:center;
    }
</style>
<div class="flex">
    <div>
         <h4>vue2：</h4>
        <image src="https://qiniu.zhaoxinchuan.cn/vue3/lifecycle2.webp">
    </div>
    <div>
        <h4>vue3：</h4>
        <image src="https://qiniu.zhaoxinchuan.cn/vue3/lifecycle3.webp">
    </div>
</div>
<div>
    <div>
        <h4 class="text-center">生命周期执行顺序</h4>
    </div>
    <div class="flex">
        <p>
            <font color=red>beforeCreate</font>
            =>
            <font color=red>created</font>
            =>
            <font color=red>beforeMount</font>
            =>
            <font color=red>mounted</font>
            =>
            <font color=red>beforeUpdate</font>
            =>
            <font color=red>updated</font>
            =>
            <font color=red>beforeDestroy</font>
            =>
            <font color=red>destroyed</font>
        </p>
        <p>
            <font color=red>setup</font>
            =>
            <font color=red>onBeforeMount</font>
            =>
            <font color=red>onMounted</font>
            =>
            <font color=red>onBeforeUpdate</font>
            =>
            <font color=red>onUpdated</font>
            =>
            <font color=red>onBeforeUnmount</font>
            =>
            <font color=red>onUnmounted</font>
        </p>
    </div>
</div>

### vue3写一个计数器
``` javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo2计数器</title>
</head>

<body>
    <div id="app">

    </div>
    <script src="https://unpkg.com/vue@next"></script>
    <script>
        const app = Vue.createApp({
            template: `<div>{{counter}}</div>`,
            data() {
                return {
                    counter: 1
                }
            },
            mounted() {
                setInterval(() => {
                    this.counter++;
                }, 1000);
            },
        });
        app.mount("#app");
    </script>
</body>

</html>
```