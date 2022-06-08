---
title: "深入JavaScript高级语法之组合函数"
date: 2022-06-08T10:52:29+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之组合函数**

#### 组合函数

```javascript
function double(x) {
	return x * 2
}

function square(y) {
	return y ** 2
}

function composFn(m, n) {
	return function(count) {
		return n(m(count))
    }
}

var newFn = composFn(double, square)
console.log(newFn(10))  // 400
```



#### 实现自动化组合函数

```javascript
function myCompose(...fns) {
    var length = fns.length
    for(var i = 0; i < length; i++) {
		if(typeof fns[i] !== 'function') {
            throw new TypeError("Expected arguments are functions")
        }
    }
    function compose(...args) {
        var index = 0
        var result = length ? fns[index].apply(this, args) : args
       	while(++index < length) {
			result = fns[index].call(this, result)
        }
        return result
    }
    result compose
}

function double(x) {
	return x * 2
}

function square(y) {
	return y ** 2
}

var newFn = myCompose(double, square)
console.log(newFn(10)) // 400
```

