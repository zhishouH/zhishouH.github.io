---
title: "深入JavaScript高级语法之关于this的练习题"
date: 2022-05-23T14:01:25+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之关于this的练习题**

#### 练习题一

```javascript
var name = 'window'

var person = {
	name: 'person',
    sayName: function () {
		console.log(this.name)
    }
}

function sayName () {
	var test = person.sayName
    test()  // window 默认绑定(独立函数调用)
    person.sayName();  // person 隐式绑定 
    (person.sayName)();  // person 隐式绑定
    (b = person.sayName)()   // window 间接函数调用(独立函数调用)
}

sayName()
```

#### 练习题二

```javascript
var name = 'window'

var person1 = {
    name: 'person1',
    foo1: function () {
		console.log(this.name)
    },
    foo2: () => console.log(this.name),
    foo3: function () {
        return function () {
			console.log(this.name)
        }
    },
    foo4:function () {
		return () => {
			console.log(this.name)
        }
    }
}

var person2 = { name: 'person2' }

person1.foo1() // window (独立函数调用)
person2.foo1.call(person2) // person2 (显示绑定)

person1.foo2() // window (箭头函数不绑定this,上层作用域是全局)
person1.foo2.call(person2) // window (箭头函数不适用this的绑定规则)

person1.foo3()() // window (独立函数调用)
person1.foo3.call(person2)() // window (独立函数调用)
person1.foo3().call(person2) // person2 (最终调用返回函数时，使用的是显示绑定)

person1.foo4()() // person1 (箭头函数不绑定this，上层作用域是person1)
person1.foo4.call(person2) // person2 (上层作用域被显示地绑定为person2)
person1.foo4().call(person2) // peerson1 (上层找到了person1)
```

#### 练习题三

```javascript
var name = 'window'

function Person(name) {
    this.name = name
    this.foo1 = function () {
        console.log(this.name)
    }
    this.foo2 = () => console.log(this.name)
    this.foo3 = function () {
        return function () {
            console.log(this.name)
        }
    }
    this.foo4 = function () {
		return () => {
            console.log(this.name)
        }
    }
}

var person1 = new Person('person1')
var person2 = new Person('person2')

person1.foo1() // person1 (隐式绑定)
person1.foo1.call(person2) // person2 (显示绑定)

person1.foo2() // person1 上层作用域是person1
person1.foo2.call(person2) // person1 call不绑定箭头函数中的this

person1.foo3()() // window (独立函数调用)
person1.foo3.call(person2)() // window (独立函数调用)
person1.foo3().call(person2) // person2 (显示绑定)

person1.foo4()() // person1
person1.foo4.call(person2)() // person2
person1.foo4().call(person2) // person1
```

#### 练习题四

```javascript
var name = 'window'

function Person(name) {
    this.name = name
    this.obj = {
        name: 'obj',
        foo1: function () {
			return function () {
				console.log(this.name)
            }
        },
        foo2: function () {
			return () => {
                console.log(this.name)
            }
        }
    }
}

var person1 = new Person('person1') 
var person2 = new Person('person2') 

person1.obj.foo1()() // window (独立函数调用)
person1.obj.foo1.call(person2)() // window (独立函数调用)
person1.obj.foo1().call(person2) // person2 (显示绑定)

person1.obj.foo2()() // obj
person1.obj.foo2.call(person2)() // person2
person1.obj.foo2().call(person2) // obj
```

