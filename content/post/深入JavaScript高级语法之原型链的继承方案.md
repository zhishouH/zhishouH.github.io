---
title: "深入JavaScript高级语法之原型链的继承方案"
date: 2022-06-17T17:59:00+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之原型链的继承方案**

```javascript
// 父类
function Person(name) {
    this.name = name
}
Person.prototype.eating =  function(){
    console.log(this.name + ' eating~')
}

// 子类
function Student(name,sno) {
    Person.call(this, name)
    this.sno = sno
}
Student.prototype = new Person()
Student.prototype.studying = function() {
	console.log(this.name + ’ studying~‘)
}

var s1 = new Student('hn')
s1.eating() // hn eating~
s1.studying() // hn studying~

// 弊端
// 1、Person函数被调用了两次
// 2、Student原型上多出了重复的属性存在

```

