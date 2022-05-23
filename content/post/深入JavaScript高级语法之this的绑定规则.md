---
title: "深入JavaScript高级语法之this的绑定规则"
date: 2022-05-23T09:46:29+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之this的绑定规则**

#### this的四个绑定规则

##### 默认绑定

```javascript
function foo() {
    return function bar() {
		console.log(this)
    }
} 

var fn = foo()

fn() // window
```

##### 隐式绑定

```javascript
var foo1 = {
    name: 'foo1',
    fn: function() {
        console.log(this.name)
    }
}

var foo2 = {
    name: 'foo2',
    fn: foo1.fn
}

foo2.fn() // foo2
```

##### **显示绑定**

```javascript
// 1、call / apply
function foo1() {
    console.log('函数被调用了',this)
}

var obj = { name: 'obj' }

// foo直接调用和call/apply调用的不同在于this绑定的不同
// 函数直接调用指向的是全局对象
// call/apply是可以指向this的绑定对象
foo1()  // 函数被调用了，window
foo1.call(obj) // 函数被调用了，{ name: 'obj' }
foo1.apply(obj) // 函数被调用了，{ name : 'obj' }

// call和apply的区别：参数传递的方式不同
// call和apply在执行函数时可以明确绑定this
function foo2(num1,num2,num3) {
    console.log(num1 + num + num3,this)
}
foo.call('call', 10, 20, 30) // 60, { String: 'call' }
foo.apply('apply',[10, 20, 30]) // 60, { String: 'apply' }

// 2、bind
function foo3() {
    console.log(this)
}
var newFoo3 = foo3.bind('bind') 
newFoo3() // { String: 'bind' }
```

##### **new绑定**

```javascript
// 通过new调用函数时，this绑定在这个函数创建出来的对象
function Person(name, age) {
	this.name = name
    this.age = age
}

var p1 = new Person('person1',20)
console.log(p1.name, p1.age) // person1，20
```

#### 规则优先级

##### 默认绑定优先级最低（直接调用函数）

##### 显示绑定优先级高于隐式绑定

```javascript
var obj = {
    name: 'obj',
    foo: function () {
		console.log(this)
    }
}
obj.foo() // { name: 'obj', foo: f }
obj.foo.call('call') // { String: 'call' }
obj.foo.apply('apply') // { String: 'apply' }
var bar = obj.foo.bind('bind') 
bar() // { String: 'bind' }
```

##### bind优先级高于隐式绑定

```javascript
function foo() {
	console.log(this)
}

var obj = {
	name: 'obj',
    foo: foo.bind('obj.foo')
}

obj.foo() // { String: 'obj.foo' }
```

##### new不能与call / apply一起使用

```javascript
// new优先级高于bind
function foo() {
    console.log(this)
}

var bar = foo.bind('bar')
bar() // { String: 'bar' }

var fn = new bar() // foo {}

foo.bind('bind').call('call') { String: 'bind' }
```

##### 总结

1. new绑定 > 显示绑定(bind > call、apply) > 隐式绑定(obj.foo()) > 默认绑定(独立函数调用)
2. bing优先级高于call、apply

#### 特殊绑定

##### 忽略显示绑定

```JavaScript
// call、apply、bind: 当传入null / undefined时，自动将this绑定为全局对象
function () {
    console.log(this)
}
foo.call(null) // window
foo.call(undefined) // window
foo.apply(null) // window
foo.apply(undefined) // window
var bar1 = foo.bind(null) 
var bar2 = foo.bind(undefined)
bar1() // window
bar2() // window
```

##### 间接函数引用

```javascript
var obj1 = {
    name: 'obj1',
    foo: function () {
		console.log(this)
    }
}

var obj2 = {
	name: 'obj2',
}

obj2.bar = obj1.foo
obj2.bar() // { name: 'obj2', bar: f }
(obj2.bar = obj1.foo)() // window
```

