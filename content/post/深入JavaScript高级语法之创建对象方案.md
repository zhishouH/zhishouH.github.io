---
title: "深入JavaScript高级语法之创建对象方案"
date: 2022-06-17T11:41:39+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之创建对象方案**

#### 原型与构造函数

```javascript
function Person(name, age, height, address) {
	this.name = name 
    this.age = age
    this.height = height
    this.address = address
}
Person.prototype.eating = function() {
	console.log(this.name + '在吃东西')
}
Person.prototype.running = function() {
	console.log(this.name + '在跑步')
}

var p1 = new Person('zhishouh', 20, 1.88, '广州市')
var p2 = new Person('hn', 21, 1.98, '深圳市' )

p1.eating() // zhishouh在吃东西
p2.eating() // hn在吃东西

p1.running() // zhishouh在跑步
p2.running() // hn在跑步
```

