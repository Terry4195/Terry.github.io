---
title: reduce
date: 2020-03-14 19:54:44
index_img: https://qiniu.zhaoxinchuan.cn/javascript/index.webp 
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags: [JavaScript, es5]
categories: JavaScript
---
### 初识reduce
``` javascript
    array.reduce(function(total, currentValue, currentIndex, arr), initialValue);
```
| <font color=red>total</font>                           | <font color=red>currentValue</font> |  currentIndex   |           arr           |                          initialValue                          |
| :----------------------------------------------------- | ----------------------------------: | :-------------: | :---------------------: | :------------------------------------------------------------: |
| <font color=red>初始值</font>, 或者计算结束后的返回值. |                           当前元素. | 当前元素的索引. | 当前元素所属的数组对象. | 传递给函数的<font color=red>初始值</font>,相当于total的初始值. |
### reduce的高级用法

#### 数组去重
``` javascript
    const arr = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5, 5, 6, 9];
    const noRepeat1 = arr.reduce((prev, next) => {
        prev.indexOf(next) === -1 && prev.push(next);
        return prev;
    }, []);
    console.log(noRepeat1); // [1, 2, 3, 4, 5, 6, 9]
```

#### 求最大值
``` javascript
    const arr = [33,44,66,11,88,99,111];
    const max = arr.reduce((prev,next) => {
        return Math.max(prev,next);
    },arr[0]);
    console.log(max); // 111
```

#### 求最小值
``` javascript
    const arr = [33,44,66,11,88,99,111];
    const min = arr.reduce((prev,next) => {
        return Math.min(prev,next);
    },arr[0]);
    console.log(min); // 11
```

#### 求元素出现的次数
``` javascript
    const tomAndJerry = ["Tom", "Jerry", "Tom", "Speike", "Tom", "Jerry"];
    const result = tomAndJerry.reduce((prev, next) => {
        if (next in prev) {
            prev[next]++
        } else {
            prev[next] = 1
        };
        return prev;
    }, {});
    console.log(result); // {Tom: 3, Jerry: 2, Speike: 1}
```

#### 二维数组转一维数组
``` javascript
    const arr = [
            [1, 2, 3],
            [4, 5]
        ];
    const result = arr.reduce((prev, next) => {
        return prev.concat(next)
    }, []);
    console.log(result); // [1, 2, 3, 4, 5]
```

#### 多维数组转一维数组
``` javascript
    const arr = [1, 2, 3, [4, 5],
        [6, 7, [8, 9]]
    ];
    let _concat;
    const getResult = (arr) => {
        return arr.reduce((prev, next) => {
            if (Array.isArray(next)) {
                _concat = getResult(next);
            } else {
                _concat = next;
            }
            return prev.concat(_concat);;
        }, [])
    };
    console.log(getResult(arr)); //  [1, 2, 3, 4, 5, 6, 7, 8, 9]
```
#### 对象属性求和
``` javascript
    const shops = [{
        title: "牙膏",
        price: 18,
        count: 2
    }, {
        title: "牙刷",
        price: 15,
        count: 4
    }, {
        title: "香皂",
        price: 8,
        count: 1
    }];
    const totalPrice = shops.reduce((prev, next) => {
        return prev + next.price * next.count
    }, 0);
    console.log(totalPrice); // 104
```