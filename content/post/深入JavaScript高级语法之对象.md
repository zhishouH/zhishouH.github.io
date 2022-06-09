---
title: "深入JavaScript高级语法之对象"
date: 2022-06-09T09:28:06+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之对象**

#### 对象写法

##### 写法一

```javascript
var obj = new Object()
obj.name = 'zhishouh'
obj.age = 20
obj.address = '广州市'

console.log(obj) // { name: 'zhishouh', age: 20, address: '广州市' }
```

##### 写法二

```javascript
var obj = {
    name: 'zhishouh',
    age: 20,
    address: '广州市'
}

console.log(obj) // { name: 'zhishouh', age: 20, address: '广州市'}
```



#### 数据属性描述符

```javascript
var obj = { }

Object.defineProperty(obj, 'name', {
    value: 'zhishouh',
    configurable: true, // 表示是否可配置(如删除该属性)
    enumerable: true, // 表示是否可枚举
    writable: true // 表示是否可写入值
})

console.log(obj) // name: 'zhishouh'
```



#### 存取属性描述符

```javascript
var obj = { _name: 'zhishouh' }

Object.defineProperty(obj, 'name', {
	configurable: true,
    enumerable: true,
    get: function() {
		return this._name
    },
    set: function(value) {
		this._height = value
    }
})

conosle.log(obj.name) // zhishouh

obj.name = 'hn'
console.log(obj.name) // hn
```



#### 定义多个属性描述符

```javascript
var obj = {
    // 私有属性(js里没有严格意义上的私有属性)
    _age: 20
}

Object.defineProperty(obj,{
    _age: {
        enumerable: false
    },
    name: {
        configurable: true,
        enumerable: true,
        writable: true,
        value: 'zhishouh'
    },
    age: {
		configurable: true,
        enumerable: true,
        get: function() {
			return this._age
        },
        set: function(value) {
			this._age = value
        }
    }
})

console.log(obj) // { name: 'zhishouh', age: [Getter/Setter] }
obj.age = 21
console.log(obj.age) // 21
conosle.log(obj._age) // 21
```



#### 获取某一个属性的属性描述符

```javascript
var obj = { name: 'zhishouh', age: 20 }

console.log(Object.getOwnPropertyDescriptor(obj, 'name'))
// { value: 'zhishouh', writable: true, enumerable: true, configurable: true }
console.log(Object.getOwnPropertyDescriptor(obj, 'age'))
// { value: 20, writable: true, enumerable: true, configurable: true }
```



#### 获取对象的所有属性描述符

```javascript
var obj = { name: 'zhishouh', age: 20 }

console.log(Object.getOwnPropertyDescriptors(obj))

// { 
//    name: { value: 'zhishouh', writable: true, enumerable: true,onfigurable: true },
// 	  age: { value: 20, writable: true, enumerable: true, configurable: true }
// }
```



#### 禁止对象配置/删除里面的属性

```javascript
var obj = { name: 'zhishouh', age: 20 }

// 方法一
for (var key in obj) {
	Object.defineProperty(obj, key, {
        configurable: false,
        enmunerable: true,
        writable: true,
        value: obj[key]
    })
}

delete obj.name
console.log(obj) // { name: 'zhishouh', age: 20 }

// 方法二
Object.seal(obj)
delete obj.name
console.log(obj) // { name: 'zhishouh', age: 20 }
```



#### 禁止对象修改属性

```javascript
var obj = { name: 'zhishouh', age: 20 }

// 方法一
for (var key in obj) {
	Object.defineProperty(obj, key, {
        configurable: true,
        enmunerable: true,
        writable: false,
        value: obj[key]
    })
}
console.log(obj) // { name: 'zhishouh', age: 20 }

// 方法二
Object.freeze(obj)
obj.name = 'hn'
console.log(obj) // { name: 'zhishouh', age: 20 }
```

