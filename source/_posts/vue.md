---
title: vue
author: Terry
date: 2019-10-26 20:20:57
index_img: /lib/images/vue/webp/index.webp
tags: [Html,css,JavaScript,vue]
categories: web
---

### 初识Vue
[官方文档](https://cn.vuejs.org/)
Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

打开文档,映入眼帘的就是一句简单的介绍-<font color=green>渐进式JavaScript框架</font>,我自己的理解很简单,就是用你想用或者能用的功能特性，你不想用的部分功能可以先不用。Vue不强求你一次性接受并使用它的全部功能特性。

### Hello world
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>初识Vue-Hello world</title>
</head>
<style>
  /* 由于js未加载完成,导致vue无法初始化,导致页面闪烁.可以添加 v-cloak 指令,等到初始化完后在进行显示 */
  [v-cloak] {
    display: none
  }
</style>

<body>
  <div id="app" v-cloak>
    {{say}}
  </div>
  <!-- 引入vue.js -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    // el: 将应用挂载到id为app的dom上,这样在这个dom内的所有元素都可以使用data中的数据
    let vm = new Vue({
      el: "#app",
      data: {
        say: "Hello world"
      }
    })
  </script>
</body>

</html>
```

----

### 循环渲染
**css:**
```css
  [v-cloak] {
    display: none
  }

  .shadow {
    padding: 10px 0;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  }
```
**html:**
```html
<div id="app1" v-cloak>
    <!-- ######################### 对象的渲染 start ######################### -->
  <div class="renderObj shadow">
    <h2>
      对象的渲染
    </h2>
    <div v-for="(item,key,index) in renderObj" :key="key">
      <p v-if="key === 'name'">
        姓名：{{item}}
      </p>
      <p v-else>
        年龄：{{item}}
      </p>
    </div>
  </div>
  <!-- ######################### 对象的渲染 end ######################### -->

  <!-- ######################### 数组的渲染 start ######################### -->
  <div class="renderArr shadow">
    <h2>
      数组的渲染
    </h2>
    <div v-for="(item,index) in renderArr" :key="item.id">
      <p>
        {{item.title}}
      </p>
    </div>
  </div>
  <!-- ######################### 数组的渲染 end ######################### -->
</div>
```
**js:**
```js
  let vm1 = new Vue({
    el: "#app1",
    data: {
      renderObj: {
        name: "小明",
        age: 18
      },
      renderArr: [{
        id: 1,
        title: "标题1"
      }, {
        id: 2,
        title: "标题2"
      }]
    }
  })
```

----

### v-model
**html:**
```html
<div id="app2">
  <input type="number" v-model="val">
  {{val}}
</div>
```
**js:**
```js
let vm2 = new Vue({
  el: "#app2",
  data: {
    val: ""
  }
})
```
### demo
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>demo</title>
</head>
<style>
  /* 由于js未加载完成,导致vue无法初始化,导致页面闪烁.可以添加 v-cloak 指令,等到初始化完后在进行显示 */
  [v-cloak] {
    display: none
  }

  .green {
    color: green;
  }

  .red {
    color: red;
  }
</style>

<body>
  <div id="app" v-cloak>
    <add-fruit :fruits="fruits" @addfruit="handleParentAddFruit"></add-fruit>
    <check-fruits :fruits="fruits" @parentfruit="handleParentFruitChange"></check-fruits>
  </div>
  <!-- 引入vue.js -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    // 自定义组件-水果列表
    Vue.component("check-fruits", {
      template: `
        <div>
          <label  v-for="item in fruits" :key="item.id" :class="item.checked?'green':'red'">
            {{item.name}}
            <input type="checkbox" :value="item.id" :checked="item.checked" @change="handleFruitChange(item.id)"/>
          </label>
          <dl>
            <dt>您喜欢的水果：</dt>
            <dd v-for="(item,index) in checkedList" class="green">
              {{index+1}}:{{item.name}}  <button @click="handleFruitChange(item.id)">删除</button>
            </dd>
          </dl>
        </div>
      `,
      props: {
        fruits: {
          default: [],
          type: Array
        }
      },
      methods: {
        handleFruitChange(id) {
          this.$emit("parentfruit", id)
        }
      },
      computed: {
        checkedList: function () {
          return this.fruits.filter(item => {
            return item.checked
          })
        }
      }
    });
    // 自定义组件-添加水果
    Vue.component("add-fruit", {
      template: `
        <form @submit="submit">
          <label>
            水果名称：
            <input type="text" name="name"  v-model="name"  placeholder="请输入要添加的水果">
          </label>
          <input type="submit" value="添加">
        </form>
      `,
      props: {
        fruits: {
          default: [],
          type: Array
        }
      },
      data: function () {
        return {
          name: null
        }
      },
      methods: {
        submit(e) {
          if (!this.name) return;
          this.$emit("addfruit", {
            name: this.name,
            id: this.fruits.length + 1,
            checked: false
          });
          this.name = null;
          e.preventDefault();
        }
      },
    });
    // el: 将应用挂载到id为app的dom上,这样在这个dom内的所有元素都可以使用data中的数据
    let vm = new Vue({
      el: "#app",
      data: {
        fruits: [{
          id: 1,
          name: "苹果",
          checked: false
        }, {
          id: 2,
          name: "梨",
          checked: false
        }, {
          id: 3,
          name: "枇杷",
          checked: true
        }, {
          id: 4,
          name: "樱桃",
          checked: false
        }]
      },
      methods: {
        handleParentFruitChange(id) {
          let fruits = this.fruits;
          let idx = this.fruits.findIndex((item) => {
            return item.id === id;
          });
          fruits[idx].checked = !fruits[idx].checked;
          this.fruits = fruits;
        },
        handleParentAddFruit(fruit) {
          this.fruits = [...this.fruits, ...[fruit]];
        }
      },
    });
  </script>
</body>

</html>
```

### 计算属性


