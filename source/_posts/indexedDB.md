---
title: indexedDB
date: 2021-08-02 16:37:26
tags: [javascript]
index_img: https://qiniu.zhaoxinchuan.cn/indexedDB/index.webp
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
---
# IndexedDB 入门教程

## 1. 说明
随着浏览器的功能不断增强，更多的网站考虑将大量数据储存在客户端，这样可以减少从服务器获取数据，直接从本地获取数据。

* Cookie：存储的大小不超过4kb，且每次请求接口都会将cookie发送到服务器。
* LocalStorage：存储大小在2.5MB-10MB之间，且不提供搜索功能，不能建立自定义的索引。
* IndexedDB：IndexedDB 就是浏览器提供的本地数据库，它可以被网页脚本创建和操作。IndexedDB 允许储存大量数据，提供查找接口，还能建立索引。这些都是 LocalStorage 所不具备的。就数据库类型而言，IndexedDB 不属于关系型数据库（不支持 SQL 查询语句），更接近 NoSQL 数据库。
  * **键值对储存**。 IndexedDB 内部采用对象仓库（object store）存放数据。所有类型的数据都可以直接存入，包括 JavaScript 对象。对象仓库中，数据以"键值对"的形式保存，每一个数据记录都有对应的主键，主键是独一无二的，不能有重复，否则会抛出一个错误。
  * **异步**。 IndexedDB 操作时不会锁死浏览器，用户依然可以进行其他操作，这与 LocalStorage 形成对比，后者的操作是同步的。异步设计是为了防止大量数据的读写，拖慢网页的表现。
  * **支持事务**。 IndexedDB 支持事务（transaction），这意味着一系列操作步骤之中，只要有一步失败，整个事务就都取消，数据库回滚到事务发生之前的状态，不存在只改写一部分数据的情况。
  *  **同源限制**IndexedDB 受到同源限制，每一个数据库对应创建它的域名。网页只能访问自身域名下的数据库，而不能访问跨域的数据库。*
  *  **储存空间大** IndexedDB 的储存空间比 LocalStorage 大得多，一般来说不少于 250MB，甚至没有上限。
  *  **支持二进制储存**。 IndexedDB 不仅可以储存字符串，还可以储存二进制数据（ArrayBuffer 对象和 Blob 对象）。

## 2. 基本概念
IndexedDB 是一个比较复杂的 API，涉及不少概念。它把不同的实体，抽象成一个个对象接口。学习这个 API，就是学习它的各种对象接口。

> * 数据库：IDBDatabase 对象
> * 对象仓库：IDBObjectStore 对象
> * 索引： IDBIndex 对象
> * 事务： IDBTransaction 对象
> * 操作请求：IDBRequest 对象
> * 指针： IDBCursor 对象
> * 主键集合：IDBKeyRange 对象


#### （1）数据库
数据库是一系列相关数据的容器。每个域名（严格的说，是协议 + 域名 + 端口）都可以新建任意多个数据库。

IndexedDB 数据库有版本的概念。同一个时刻，只能有一个版本的数据库存在。如果要修改数据库结构（新增或删除表、索引或者主键），只能通过升级数据库版本完成。

#### （2）对象仓库
每个数据库包含若干个对象仓库（object store）。它类似于关系型数据库的表格。 

#### （3）数据记录
对象仓库保存的是数据记录。每条记录类似于关系型数据库的行，但是只有主键和数据体两部分。主键用来建立默认的索引，必须是不同的，否则会报错。主键可以是数据记录里面的一个属性，也可以指定为一个递增的整数编号。
> { id: 1,content: "测试" } 

上面的对象，id可以为主键/索引，数据体可以是任意数据类型，不限于对象。

#### （4）索引
为了加速数据的检索，可以在对象仓库里面，为不同的属性建立索引。

#### （5）事务
数据记录的读写和删改，都要通过事务完成。事务对象提供 <font color=red>error</font>、<font color=red>abort</font>和<font color=red>complete</font>三个事件，用来监听操作结果。

## 3. 操作流程
IndexedDB 数据库的各种操作，一般是按照下面的流程进行的。这个部分只给出简单的代码示例，用于快速上手，详细的各个对象的 API 请看这里。

 #### 3.1. 打开数据库
 使用 IndexedDB 的第一步是打开数据库，使用indexedDB.open()方法。
 ``` javascript
    const request = indexedDB.open(databaseName, version);
 ```
 * databaseName：数据库名称，如果没有当前数据库，会创建当前数据库
 * version：指定数据库版本，当你想要更改数据库格式（比如增加对象存储，非增加记录），必须指定更高版本，通过 versionchange 来更改
  
(1) error
        error事件表示打开数据库失败。
    ``` javascript
    request.error = (e) => {
        console.log(e,"数据库打开错误")
    }
    ```
(2) success 
    ``` javascript
    let db;
    request.success  = (e) => {
        db = request.result; 
        // 通过request的result对象获取数据库对象
        console.log(e,"数据库打开成功")
    }
    ```
(3) upgradeneeded 
    如果指定的版本号，大于数据库的实际版本号，就会发生数据库升级事件 <font color=red>upgradeneeded</font>
     ``` javascript
    let db;
    request.success  = (event) => {
        db = event.target.result; 
        // 通过event的target.result对象获取数据库实例
        console.log(event,"数据库升级")
    }
    ```
#### 3.2. 创建数据库




