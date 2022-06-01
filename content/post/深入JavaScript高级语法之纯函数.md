---
title: "深入JavaScript高级语法之纯函数"
date: 2022-06-01T14:05:33+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之纯函数**

#### 纯函数

1. 确定的输入，一定会产生确定的输出
2. 函数在执行过程中，不能产生副作用

```javascript
var names = ['abc', 'bbc', 'cbc', 'dbc']

// 纯函数 slice 截取，不会对原数组有所改动
var newNames = names.slice(0, 2)
console.log(newNames)  // ['abc', 'bbc']
console.lgo(names)  // ['abc', 'bbc', 'cbc', 'dbc']

// 非纯函数 splice 截取并删除
var newNames2 = names.splice(2,1)
console.log(newNames2)  // ['cbc']
console.log(names)  // ['abc', 'bbc', 'dbc']
```

```javascript
// 举例
function demo(info) {
	return {
		...info,
        age: 20
    }
}
var result = demo({name: 'zhishouh', age: 19})
console.log(result) // {name: 'zhishouh', age: 20}
```

