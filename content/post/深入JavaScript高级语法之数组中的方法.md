---
title: "深入JavaScript高级语法之数组中的方法"
date: 2022-05-20T10:29:01+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之数组中的方法**

#### 函数与方法的定义

- 函数function：独立的function称之为函数，例：function foo() {}
- 方法method：当一个函数存在于某一个对象时，称之为这个函数是该对象的方法，例：var obj = {foo: function(){}} obj.foo()



#### 数组中的方法(高阶函数)

##### filter方法—过滤

```javascript
var nums = [10, 15, 20, 25, 30, 35]
var newNums = nums.filter(function (item,index,arr) {
    return item % 2 === 0
})
console.log(newNums)

// [10, 20, 30]
```

##### map方法—映射

```javascript
var nums = [10, 15, 20, 25, 30, 35]
var newNums = nums.map(function(item) {
    return item * 10
})
console.log(newNums)

// [100, 150, 200, 250, 300, 350]
```

##### forEach方法—迭代(没有返回值)

```javascript
var nums = [10, 15, 20, 25, 30, 35]
var newNums = nums.forEach(function (item,index) {
	console.log(item,index)
})

// 10 0
// 15 1
// 20 2
// 25 3
// 30 4
// 35 5
```

##### find/findIndex方法—查找

```javascript
var friends = [
    {name: 'tom', age: 20},
    {name: 'tim', age: 21},
    {name: 'jay', age: 22},
    {name: 'amy', age: 23},
]
var findFriend = friends.find(function(item) {
    return item.name === 'tom'
})
var findIndexFriend = friends.findIndex(function(item) {
		return item.name === 'tom'
})
console.log(findFriend)
console.log(findIndexFriend)

// {name: 'tom', age: 20}
// 0
```

##### reduce方法—累加

```javascript
var nums = [10, 15, 20, 25, 30, 35]
var newNums = nums.reduce(function(prevValue,item) {
    return prevValue + item
},0)
console.log(newNums)

// 135
```

