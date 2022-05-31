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
Function.prototype.mycall = function (thisArg, ...args /*剩余参数*/) {
  // 获取被执行的函数
  var fn = this

  // 对thisArg转成对象类型(防止传入的是非对象类型)
  thisArg = (thisArg !== null && thisArg !== undefined) ? Object(thisArg) : window

  // 调用被执行的函数
  thisArg.fn = fn
  var result = thisArg.fn(...args /* 展开运算符 */)
  delete thisArg.fn

  // 将结果返回
  return result
}

var name = 'window'

function foo() {
  console.log('foo函数被执行了', this)
}

function sum(num1, num2) {
  console.log('sum函数被执行了', this)
  return num1 + num2
}

foo.mycall() // foo函数被执行了, window
foo.mycall('foo') // foo函数被执行了, String{ 'foo', fn: f }

sum.mycall() // sum函数被执行了, window
sum.mycall('sum') // sum函数被执行了, String{ 'sum', fn: f }
var result = sum.mycall('sum', 20, 30) // sum函数被执行了, String{ 'sum', fn: f }
console.log(result) // 50
```

