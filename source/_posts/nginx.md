---
title: linux下部署nginx
date: 2021-06-02 14:34:13
index_img:  https://qiniu.zhaoxinchuan.cn/nginx/index.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags:
---

> nginx 部署 web 项目

1. 环境安装

```javascript
yum -y install gcc gcc-c++ autoconf pcre-devel make automake
yum -y install wget httpd-tools vim
```

2. 创建基础目录

   > > > html
   > > >
   > > > > app
   > > > > backup
   > > > > download
   > > > > logs
   > > > > work

3. Nginx 搭建
   配置 yum 源

```javascript
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/OS/OSRELEASE/$basearch/
gpgcheck=0
enabled=1
```

创建 nginx.repo 文件,把上面的源代码复制进去

```c++
vim / etc / yum.repos.d / nginx.repo;

```

启动命令

```javascript
nginx - c / etc / nginx / nginx.conf;
```
