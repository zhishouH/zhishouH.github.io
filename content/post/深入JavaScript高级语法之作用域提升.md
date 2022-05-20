---
title: "深入JavaScript高级语法之作用域提升"
date: 2022-05-20T09:12:18+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之作用域提升**

#### 理解

1. 函数执行
2. 作用域链



#### 示例一

```javascript
var n = 10
function foo() {
    n = 20
}
foo()
console.log(n)

// 20
```



#### 示例二

```javascript
function foo() {
    console.log(n)
    var n = 10
    console.log(n)
}
var n = 20
foo()

// undefined
// 10
```



#### 示例三

```javascript
var n = 100
function foo1() {
    console.log(n)
}
function foo2() {
    var n = 200
	console.log(n)
    foo1()
}
foo2()
console.log(n)

// 200
// 100
// 100
```



#### 示例四

```javascript
var n = 100
function foo() {
    console.log(n)
    return
    var a = 20
}
foo()

// undefined
```



#### 示例五

```JavaScript
function foo() {
    var a = b = 100
}
foo()
console.log(a)
console.log(b)

// a报引用错误
// 100
```



#### 示例六

```javascript
var x = [12, 23]
function foo(y) {
    y[0] = 100
    y = [100]
    y[1] = 200
    console.log(y)
}
foo(x)
console.log(x)

// [100,200]
// [100,23]
```

