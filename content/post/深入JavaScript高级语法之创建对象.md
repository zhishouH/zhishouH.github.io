---
title: "深入JavaScript高级语法之创建对象"
date: 2022-06-09T10:10:42+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之创建对象**

#### 工厂模式(工厂函数)

```javascript
function createPerson(name, age, height, address) {
	return {
        name,
        age,
        height,
        address,
        eating() {
			console.log(this.name + '在吃东西')
        },
        running() {
			conosle.log(this.name + '在跑步')
        }
    }
}

var p1 = createPerson('zhishouh', 20, 1.88, '广州市')
console.log(p1)
// {
//   name: 'zhishouh',
//   age: 21,
//   height: 1.88,
//   address: '广州市',
//   eating: [Function: eating],
//   running: [Function: running]
// }
```



#### 构造函数

```javascript
function Person(name, age, height, address) {
	this.name = name
    this.age = age
    this.height = height
    this.address = address
    this.eating = function() {
		console.log(this.name + '在吃东西')
    }
    this.running = function() {
		console.log(this.name + '在跑步')
    }
}

var p1 = new Person('zhishouh', 20, 1.88, '广州市')
console.log(p1) 
// Person {
//   name: 'zhishouh',
//   age: 20,
//   height: 1.88,
//   address: '广州市',
//   eating: [Function (anonymous)],
//   running: [Function (anonymous)]
// }
console.log(p1.__proto__.constructor) // [Function: Person]
console.log(p1.__proto__.constructor.name) //Person
```

