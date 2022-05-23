---
title: "深入JavaScript高级语法之闭包"
date: 2022-05-23T09:33:38+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之闭包**

#### 闭包 = 函数 + 可以访问的自由变量

```javascript
function foo() {
	var fnName = 'foo'
    function bar() {
		console.log('bar',fcName)
    }
    return bar
}
var fn = foo()
fn()

// bar foo
```

#### 总结

- 一个普通的函数function，如果可以访问外层作用域的自由变量，那么该函数就是一个闭包
- 从广义上：JavaScript的函数都是闭包
- 从狭义上：JavaScript中的函数，如果访问了外层作用域的变量，那么它就是一个闭包

#### 闭包的内存泄露

```javascript
function foo() {
    var foName = 'foo'
    function bar() {
		return foName
    }
    return bar
}
var fn = foo()
console.log(fn())
// foo
// 释放内存
fn = null
foo = null
```

