---
title: "深入JavaScript高级语法之with Eval Strict"
date: 2022-06-09T09:11:10+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之with Eval Strict**

#### with语句

- with语句会形成作用域
- 是混淆错误和兼容性问题的根源

```javascript
var message = 'window hello'

var obj = { message: 'obj hello' }

function foo() {
	function bar() {
		with(obj) {
			console.log(message)
        }
    }
    bar()
}

foo() // obj hello
```



#### eval函数

- 将传入的字符串当作JavaScript代码运行
- 可读性差
- 执行过程可能被可以篡改，造成风险
- eval的执行必须经过js解释器，不能被js引擎优化

```javascript
var jsString = 'var message = "hello world" console.log(message); '

eval(jsString)  // hello world
```



#### strict

```javascript
// 全局开启
"use strict";
message = 'hello world'
conosle.log(message)  // ReferenceError: message is not defined
```

```javascript
// 函数内部开启
function foo() {
	"use strict";
    message = 'hello world'
    console.log(message)
}

foo() // ReferenceError: message is not defined
```

