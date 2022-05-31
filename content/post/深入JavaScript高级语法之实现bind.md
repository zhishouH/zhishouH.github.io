---
title: "深入JavaScript高级语法之实现bind"
date: 2022-05-31T11:58:46+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之实现bind**

```javascript
Function.prototype.mybind = function (thisArg, ...argArray) {
  // 获取被执行的函数
  var fn = this

  // 对thisArg转成对象类型(防止传入的是非对象类型)
  thisArg = (thisArg !== null && thisArg !== undefined) ? Object(thisArg) : window

  // 调用被执行的函数
  return function (...args) {
    thisArg.fn = fn
    var finalArgs = [...argArray, ...args]
    var result = thisArg.fn(...finalArgs)
    delete thisArg.fn

    // 将结果返回
    return result
  }
}

function foo() {
  console.log('foo被执行')
}

function sum(num1, num2, num3, num4) {
  console.log(num1 + num2 + num3 + num4)
}

foo.mybind()() // foo被执行
foo.mybind('foo')() // foo被执行

var newSum = sum.mybind('sum', 10, 20, 30, 40)
newSum() // 100
var newSum2 = sum.mybind('sum2', 10, 20)
newSum2(30, 40) // 100
```

