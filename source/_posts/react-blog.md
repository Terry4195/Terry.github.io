---
title: react+egg.js搭建博客系统
date: 2021-08-04 13:59:39
tags: [react,javascript]
index_img: https://qiniu.zhaoxinchuan.cn/indexedDB/index.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
---
# 技术栈：
## 1 开发环境搭建
### 1.1 全局安装 create-next-app 
``` javascript
    npm i create-next-app -g
    or 
    yarn global add create-next-app
```

### 1.2 生成脚手架
 ```javascript
    npx create-next-app myapp
    or 
    yarn create next-app myapp
```

## 2 搭建博客首页
进入工程目录，删除默认的文件和代码，把首页改为下面的代码
```javascript
import Head from 'next/head'
const Home = () => (
  <>
    <Head>
      <title>Home</title>
    </Head>
 </>
)
export default Home
```