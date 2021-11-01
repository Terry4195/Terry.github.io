---
title: pm2-进程管理器
index_img:  https://qiniu.zhaoxinchuan.cn/pm2/index.webp
date: 2020-02-05 15:04:42
tags: [nodejs,centos]
categories: Node
description: PM2 is a daemon process manager that will help you manage and keep your application online
---
> 官方说明：PM2 is a daemon process manager that will help you manage and keep your application online
> 官方说明：PM2是一个守护进程管理器，可以帮助您管理和保持应用程序在线
>> pm2是node项目的进程、状态管理器

### 1.安装nodejs
[nodejs安装](https://www.zhaoxinchuan.cn/blog/2021/10/25/nodejs)


### 2.查看nodejs、npm版本
```
node -v
npm -v
```
----

### 3.安装pm2
```
npm install -g pm2
```
#### 3.1.查看是否安装成功
```
pm2 list
```
![pm2-list](https://qiniu.zhaoxinchuan.cn/pm2/1.png)

#### 3.2.启动node项目
```
pm2 start 项目路径
pm2 start root/webapp/server/bin/www
```

#### 3.3.查看进程状态
```
pm2 status
```
![pm2-logs-name](https://qiniu.zhaoxinchuan.cn/pm2/3.png)

#### 3.4.查看指定文件的日志
```
pm2 logs www
```
![pm2-logs-name](https://qiniu.zhaoxinchuan.cn/pm2/2.png)

----

# 4.pm2 常用命令
``` javascript
pm2 list // 查看所有进程状态
pm2 logs // 显示所有进程日志
pm2 stop all // 停止所有进程
pm2 restart all // 重启所有进程
pm2 reload all // 重载所有进程
pm2 delete all  // 删除所有进程
pm2 restart [name] // 重启指定进程[对应进程的名称]
pm2 stop [name] // 停止指定进程[对应进程的名称]
pm2 delete [name]  // 删除指定进程[对应进程的名称]
pm2 logs [name]  // 查看指定进程的日志[对应进程的名称]
```
