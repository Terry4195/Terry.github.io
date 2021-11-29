---
title: Array操作方法
date: 2020-03-11 10:30:00
index_img: https://qiniu.zhaoxinchuan.cn/javascript/index.webp 
banner_img: https://qiniu.zhaoxinchuan.cn/bg/category.webp
tags: [JavaScript]
categories: JavaScript
---
## 一.获取数组交集-差集
``` js
// 定义两个数组
const arrA = [1,2,3,4,5,6,7];
const arrB = [2,3,4,5,6,7,8,9];
```
### 获取交集
#### 方式一：filter+some
```js
const intersection = arrA.filter(item => arrB.some(item2 => item2 === item)));
console.log(intersection); // [2, 3, 4, 5, 6, 7]
```
#### 方式二： es6的Set+filter
```js 
const setArrA = new Set(arrA);
const setArrB = new Set(arrB);
const intersection2 = [...new Set([...setArrA].filter(item => setArrB.has(item)))];
console.log(intersection2); // [2, 3, 4, 5, 6, 7]
```

### 获取差集
#### 方式一：es6的Set+filter
```js
const setArrA1 = new Set(arrA);
const setArrB1 = new Set(arrB);
const difference = [...new Set([...[...setArrA1].filter(item => !setArrB1.has(item)),...[...setArrB1].filter(item => !setArrA1.has(item))])];
console.log(difference); // [1, 8, 9]
```

#### 方式二：filter+every
```js
function getDifference(source,target){
   return source.filter(item => {
        return target.every(item1 => {
            return item1 !== item
        });
    });
};
let difference2 = [...getDifference(arrA,arrB),...getDifference(arrB,arrA)];
console.log(difference2); // [1, 8, 9]
```

## 二.数组去重
```js
// 定义一个含有重复值的数组
const repeatArr = [1,2,3,1,2,3,1,2,3,1,2,3];
```
### 方式一：es6的Set方法
```js
const noRepeatArr1 = [...new Set(repeatArr)];
console.log(noRepeatArr1); // [1, 2, 3]
```

### 方式二：forEach + 空数组 + indexOf
```js
let noRepeatArr2 = [];
repeatArr.forEach(item => {
    if(noRepeatArr2.indexOf(item) === -1) noRepeatArr2.push(item);
});
console.log(noRepeatArr2); // [1, 2, 3]
```

### 方式三：reduce + 空数组 + indexOf
```js
let noRepeatArr3= repeatArr.reduce((prev,next) => {
    if(prev.indexOf(next) === -1) prev.push(next);
    return prev;
},[]);
console.log(noRepeatArr3); // [1, 2, 3];
```

### 方式四：for循环 + includes
```js
let noRepeatArr4 = [];
for(var i = 0; i < repeatArr.length; i++ ){
     if(!noRepeatArr3.includes(repeatArr[i])) noRepeatArr3.push(repeatArr[i]);
};
console.log(noRepeatArr4); // [1, 2, 3];
```

### 方式五：es6的Map
```js 
let noRepeatArr5 = [];
let map = new Map();
for(var i = 0; i < repeatArr.length; i++){
    if (map.has(repeatArr[i])) {      // 判断是否存在该key值
      map.set(repeatArr[i], true);
    }else {
      map.set(repeatArr[i], false);
      noRepeatArr5.push(repeatArr[i]);
    }
};
console.log(noRepeatArr5); // [1, 2, 3];
```

## 三.数组值求和
```js
// 定义一个全部值为数字类型的数组
const nums = [1,2,3,4,5];
```

### 方式一：for循环+为0的初始值
```js
let sum1 = 0;
for(var i = 0; i < nums.length;i++){
  sum1 += nums[i];
};
console.log(sum1); // 15
```

### 方式二：reduce方法
```js
const sum2 = nums.reduce((prev,next) => {
  prev+=next;
  return prev;
},0);
console.log(sum2); // 15
```

### 方式三：递归
```js
function sum3Fn (arr) {
  let len = arr.length;
  if(len === 0){
    return 0;
  }else if (len === 1){
    return arr[0]
  }else{
    return arr[0] + sum3Fn(arr.slice(1));
  }
};
const sum3 = sum3Fn(nums); // 15
```

### 方式四：eval
```js
const sum4 = eval(nums.join("+"));
const sum3 = sum3Fn(nums); // 15
```

## 四.数组排序
```js
const sorts = [12,11,7,4,8,3,0];
```
### 方式一：冒泡排序
```js
let sorts1 = sorts;
for(var i = 0; i < sorts1.length; i++){
  for(var j = 0; j < sorts1.length; j++){
    if(sorts1[j] > sorts1[j+1]){
      let temp  = sorts1[j];
      sorts1[j] = sorts1[j +1];
      sorts1[j +1] = temp;
    }
  };
};
console.log(sorts1); // [0, 3, 4, 7, 8, 11, 12]
```

### 方式二：选择排序
```js
let sorts2 = sorts;
let temp;//交换变量标识
// 两层for分别表示当前项与第二项
for(let i = 0; i < sorts2.length - 1; i++) {
  for(let j = i + 1; j < sorts2.length; j++) {
  // 假设第二项是最小值(是则交换/否则继续比较)
    if(sorts2[i] > sorts2[j]) {
      temp = sorts2[i];
      sorts2[i] = sorts2[j];
      sorts2[j] = temp;
    }
  }
}
console.log(sorts2); // [0, 3, 4, 7, 8, 11, 12]
```

### 方式三：插入排序
```js
let sorts3 = sorts;
for(var i = 0; i < sorts3.length; i++) {
 var n = i;
 while(sorts3[n] > sorts3[n+1] && n >= 0) {
     let temp = sorts3[n];
     sorts3[n] = sorts3[n+1];
     sorts3[n+1] = temp;
     n--;
  };
};
console.log(sorts3); // [0, 3, 4, 7, 8, 11, 12]
```

### 方式四：sort排序 
```js
let sorts4= sorts;
sorts4.sort((a,b) => {
  return a-b;
});
console.log(sorts4); // [0, 3, 4, 7, 8, 11, 12]
```