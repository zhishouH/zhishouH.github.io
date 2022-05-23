---
title: "深入JavaScript高级语法之箭头函数的使用"
date: 2022-05-23T13:36:17+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之箭头函数的使用**

#### 编写箭头函数

```javascript
var foo = () => { }

//在高阶函数中使用箭头函数
var nums = [10, 20, 30]
var result = nums.filter(item => item % 2 === 0)
				 .map(item => item * 10)
				 .reduce((prevValue, item) => prevValue + item)
console.log(result) // 600
```

#### 箭头函数的简写规则

```javascript
// 1、参数只有一个时，()可以省略
// 2、函数体只有一行代码时，{}可以省略，并且会将这行代码的结果作为返回值
// 3、如果箭头函数只有一行代码，并且返回一个对象是 + ()

var bar = () => ({ name: 'bar' })
console.log(bar()) // { name: 'bar' }
```

#### 箭头函数中的this

```javascript
// 箭头函数不使用this的四个规则(也就是不绑定this),而是根据外层作用域来决定this
var foo = () => {
    console.log(this)
}
foo() // window

var obj = {
    data: [],
    getData: function () {
        // 普通函数写法
        // var _this = this
        // setTimeout(function () {
        //    var result = [100, 200, 300]
        //    _this.data = result
        //    console.log(_this.data)
        // }, 2000)
        
        // 箭头函数写法
        setTimeout(() => {
            var result = [100, 200, 300]
            this.data = result
            console.log(this.data)
        }, 2000)
    }
}
obj.getData() // [100, 200, 300]
```

