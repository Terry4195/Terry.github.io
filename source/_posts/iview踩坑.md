---
title: iview踩坑
date: 2022-02-26 22:27:53
tags:
---
### 这里记录的都是一些在使用Iview的坑,主要是vue2
### 1.Table中遇到的坑
使用Table，并且配置了操作栏。
![table-action配置](https://qiniu.zhaoxinchuan.cn/iview/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220226222614.png)
如果使用了fixed属性,在自定义组件中,打印初始化情况,会打印两次!
![fixed](https://qiniu.zhaoxinchuan.cn/iview/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220226222637.png)
![console结果](https://qiniu.zhaoxinchuan.cn/iview/%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20220226222649.png)