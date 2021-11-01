---
title: nodejs
index_img:  https://qiniu.zhaoxinchuan.cn/nginx/index.webp
date: 2021-10-25 15:04:42
tags: [nodejs,centos]
categories: Node
description: centos中安装nodejs
---
> 我们使用nodejs开发服务端并部署到服务器时，会在服务器中安装nodejs应用，windows基于可视化操作安装(不过多赘述)。现在主要是基于linux的centos服务器安装nodejs。

### 1.安装nodejs依赖
``` code
yum install gcc gcc-c++
<!-- 这里使用centos的yum命令 -->
```

### 2.下载nodejs压缩包
[下载地址](https://nodejs.org/en/download/)
#### 在服务器根目录或者自定义位置新建node文件夹，方便我们把压缩包下载到当前位置，
```
mkdir nodejs
cd nodejs
wget https://nodejs.org/dist/v14.18.1/node-v14.18.1.tar.gz
```

![下载安装包](https://qiniu.zhaoxinchuan.cn/node/1.png)


### 3.解压下载的安装包
```
tar -xvf node-v14.18.1.tar.gz
mv node-v14.18.1 node
```
![解压安装包](https://qiniu.zhaoxinchuan.cn/node/2.png)
![解压后的文件](https://qiniu.zhaoxinchuan.cn/node/3.png)

### 4.将node添加到环境变量中
找到/etv/profile
``` javascript
vim /etc/profile //编辑
// 在文本中添加
export NODE_HOME=/nodejs/node-v14.18.1  // 刚刚解压的文件路径
export PATH=$NODE_HOME/bin:$PATH
```
![解压后的文件](https://qiniu.zhaoxinchuan.cn/node/4.png)

### 5.查看node,npm版本
![解压后的文件](https://qiniu.zhaoxinchuan.cn/node/5.png)