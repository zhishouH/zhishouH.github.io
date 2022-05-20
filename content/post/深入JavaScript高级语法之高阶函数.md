---
title: "深入JavaScript高级语法之高阶函数"
date: 2022-05-20T10:04:09+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之高阶函数**

#### 高阶函数的定义

- 函数接受另一个函数作为参数
- 函数返回另一个函数作为返回值



#### 函数接受另一个函数作为参数

```javascript
function foo(fn) {
    fn()
}
function bar() {
	console.log('bar')
}
foo(bar)

// bar
```

```javascript
function calc(num1,num2,calcFn) {
    console.log(calcFn(num1,num2))
}
function add(num1,num2) {
    return num1 + num2
}
function sub(num1,num2) {
	return num1 - num2
}
function mul(num1,num2) {
	return num1 * num2
}

var a = 10
var b = 20

calc(a,b,add)
calc(a,b,sub)
calc(a,b,mul)

// 30
// -10
// 200
```



#### 函数返回另一个函数作为返回值

```javascript
function foo() {
    return function bar() {
        console.log('bar')
    }
}
var fn = foo()
fn()

// bar
```

```javascript
function foo(num1) {
    return function bar(num2) {
        return num1 + num2
    }
}
var add = foo(10)
console.log(add(10))
console.log(add(20))

// 20
// 30
```

