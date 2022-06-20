---
title: "深入JavaScript高级语法之寄生组合式继承"
date: 2022-06-20T09:23:11+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> ​	**深入JavaScript高级语法之寄生组合式继承**

```javascript
function inheritPrototype(subType, SuperType) {
    subType.prototype = Object.create(SuperType.prototype)
    Object.defineProperty(subType.prototype, 'constructor', {
		enumerable: false,
        configurable: true,
        writable: trur,
        value: subType
    })
}
// 父类
function Person(name, age) {
	this.name = name
    this.age = age
}
Person.prototype.eating = function() {
	console.log(this.name + ' eating~')
}
Person.prototype.running = function() {
	console.log(this.name + ' running~')
}

// 子类
function Student(name, age, sno) {
    Person.call(this, name, age)
    this.sno = sno
}
inheritPrototype(Student, Person)
Student.prototype.studying = function() {
	console.log(`姓名：${this.name} - 年龄：${this.age} - 学号：${this.sno} --- 正在学习`)
}

var stu = new Student('hn', 20, 1930316)
console.log(stu)  // Student { name: 'hn', age: 20, sno: 1}
stu.eating()  // hn eating~
stu.running() // hn running~
stu.studying()// 姓名：hn - 年龄：20 - 学号：1 --- 正在学习
```