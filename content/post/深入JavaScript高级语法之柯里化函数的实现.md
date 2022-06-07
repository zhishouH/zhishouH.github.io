---
title: "深入JavaScript高级语法之柯里化函数的实现"
date: 2022-06-07T17:02:52+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之柯里化函数的实现**

#### 自动柯里化函数的实现

```javascript
function myCurrying(fn) {
	function curried1(...args1) {
		// 判断当前接收的参数个数与函数本身需要接收的个数是否一致
        if(args1.length >= fn.length) {
			return fn.apply(this, args1)
        } else {
            function curried2(...args2) {
				return curried1.apply(this, [...args1, ...args2])
            }
            return curried2
        }
    }
    return curried1
}

function add(x, y, z) {
    return x + y + z
}

var curryAdd = myCurrying(add)
console.log(curryAdd(10, 20, 30))  // 60
console.log(curryAdd(10, 20)(30))  // 60
console.log(curryAdd(10)(20)(30))  // 60
```

