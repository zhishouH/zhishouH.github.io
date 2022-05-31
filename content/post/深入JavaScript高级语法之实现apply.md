---
title: "深入JavaScript高级语法之实现apply"
date: 2022-05-31T10:49:19+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之实现apply**

#### 实现一个apply

```javascript
Function.prototype.myapply = function (thisArg, argArray) {
  // 获取被执行的函数
  var fn = thisx

  // 对thisArg转成对象类型(防止传入的是非对象类型)
  thisArg = (thisArg !== null && thisArg !== undefined) ? Object(thisArg) : window

  // 调用被执行的函数
  thisArg.fn = fn
  argArray = argArray || []
  var result = thisArg.fn(...argArray)
  delete thisArg.fn

  // 将结果返回
  return result
}

function foo() {
  console.log('foo被执行了')
}

function sum(num1, num2) {
  console.log('sum被执行了')
  return num1 + num2
}

foo.myapply() // foo被执行了
foo.myapply('foo') // foo被执行了

sum.myapply() // sum被执行了
sum.myapply('sum') // sum被执行了
var result = sum.myapply('sum', [10, 20]) // sum被执行了
console.log(result) // 30
```

