---
title: mysql
date: 2021-07-05 10:32:48
index_img: http://qwlbyw52x.hn-bkt.clouddn.com/mysql/index.webp
tags: [数据库安装]
description: mysql在windows中安装教程
---

## 1.下载mysql
[点击下载免安装版](https://pan.baidu.com/s/1-53ZhX1XORZ2GG_nwte1cw)
提取码：come

## 2.解压到本地目录
![解压目录](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/1.webp)
*由于使用的免安装版，所以在解压目录中并没有my.ini配置文件。这里我们手动创建my.ini文件,复制下方配置*
```
# 
#此数据库没有my.ini文件，当前文件为后来增加的
#
#
[client]
default-character-set = utf8mb4
[mysql]
default-character-set = utf8mb4
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_bin
init_connect='SET NAMES utf8mb4'
# Remove leading # and set to the amount of RAM for the most important data
# cache in MySQL. Start at 70% of total RAM for dedicated server, else 10%.
innodb_buffer_pool_size = 128M
# Remove leading # to turn on a very important data integrity option: logging
# changes to the binary log between backups.
# log_bin
# These are commonly set, remove the # and set as required.

#该参数指定了安装 MySQL 的安装路径，填写全路径可以解决相对路径所造成的问题。
basedir = E:/mysql-5.7.29-winx64
#该参数指定了 MySQL 的数据库文件放在什么路径下。数据库文件即我们常说的 MySQL data 文件。
datadir = E:/MySQL/Data


port = 3306
# server_id = .....
# Remove leading # to set options mainly useful for reporting servers.
# The server defaults are faster for transactions and fast SELECTs.
# Adjust sizes as needed, experiment to find the optimal values.
join_buffer_size = 128M
sort_buffer_size = 16M
read_rnd_buffer_size = 16M 

#定义应该支持的sql语法，对数据的校验等等
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES


max_allowed_packet=300M
```
* 参数说明
* basedir:输入当前mysql的解压目录
* datadir：数据库文件放在哪里
* port：在什么端口启动

## 3.命令行启动mysql服务
* *由于mysql没有配置环境变量，所以输入mysql后，提示无法识别*
1. 此电脑，右键属性
    ![属性](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/2.webp)

2. 高级系统设置-环境变量-系统变量-Path(编辑-新建)-mysql安装目录-一路确定，在输入mysql就不会提示无法识别了
    ![高级系统设置](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/3.webp)
    ![环境变量](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/4.webp)
    ![新增变量](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/5.webp)

3. 安装mysqld服务
    ```
    mysqld --install
    ```
    安装成功提示：<font color=red>Service successfully installed.</font>

4. 初始化mysql
    ```
    mysqld --initialize --console
    ```
    **初始化成功后会产生一个随机密码，请记住，待会儿会用到**
    ![初始化mysql](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/6.webp)

5. 启动mysql
    ```
    # 启动命令
    net start mysql
    # 停止命令
    net stop mysql
    ```
     
6. 修改密码
   *由于随机密码过于繁琐，所以我们将密码修改为自定义的密码*
   ```
   # 登录mysql
   mysql -p root -u
   ```
   * root:初始化的默认名称
    回车后会输入登录密码(初始化产生的随机密码)
    ![登录](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/7.webp)
    ```
    # set password for 用户名(默认为root)@localhost = password('新密码');
    set password for root@localhost = password('新密码');
    ```
    ![修改成功](http://qwlbyw52x.hn-bkt.clouddn.com/mysql/8.webp)

    <font color=red>**有时候，在命令行会出现各种各样的问题，所以尽量使用 以管理员身份打开**</font>

