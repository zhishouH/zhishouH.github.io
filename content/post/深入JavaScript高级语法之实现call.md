---
title: "深入JavaScript高级语法之实现call"
date: 2022-05-24T17:38:08+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之实现call**

#### 实现一个call

```javascript
Function.prototype.mycall = function (thisArg, ...args) {
	// 1、获取被执行的函数
    var fn = this
    
    // 2、对thisArg转换成对象类型(防止传入非对象类型)
    thisArg = thisArg ? Object(thisArg) : window
    
    // 3、调用被执行的函数
    thisArg.fn = fn
    var result = thisArg.fn(...args)
    delete thisArg.fn
    
    // 4、将结果返回
    return result
}

function foo() {
    console.log('foo函数被调用了',this)
}

function sum(num1, num2) {
    return num1 + num2
}

foo.mycall() // foo函数被调用了，window {}
console.log(sum.mycall('sum', 10, 20)) // 30 
```

