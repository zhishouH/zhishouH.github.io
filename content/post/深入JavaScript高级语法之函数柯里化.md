---
title: "深入JavaScript高级语法之函数柯里化"
date: 2022-06-01T14:14:29+08:00
draft: false
tags: [JavaScript]
categories: [JavaScript]
---

> **深入JavaScript高级语法之函数柯里化**

#### 函数柯里化

```javascript
function sum(x) {
	return function(y) {
		return function(z) {
            return x + y + z
        }
    }
}

var result = sum(10)(20)(30)
console.log(result) // 60

// 简化柯里化函数
function sum2 = x => y => z => x + y + z
console.log(sum2(10)(20)(30)) // 60

```

#### 函数柯里化 —— 单一职责的原则

```javascript
function add(x, y, z) {
	x = x + 2
    y = y + 2
    z = z ** 2    
    return x + y + z
}
console.log(add(10, 20, 30)) // 952

function sum(x) {
	x = x + 2
    return function(y) {
        y = y * 2
        return function(z) {
			z = z ** 2
            return x + y + z
        }
    }
}
console.log(sum(10)(20)(30)) // 952
```

#### 函数柯里化 —— 逻辑的复用

```javascript
function makeAdder(count) {
  count = count ** 2
  return function (num) {
    return count + num
  }
}
var result = makeAdder(5)
console.log(result(10))  // 35
console.log(result(20))  // 45
console.log(result(30))  // 55
```

```javascript
const log = date => type => message => {
  console.log(`[${date.getHours()}:${date.getMinutes()}][${type}]:[${message}]`)
}

var nowLog = log(new Date())
nowLog('DEBUG')('nowLog-xxx')  // [16:6][DEBUG]:[nowLog-xxx]

var nowAndDebugLog = log(new Date())('DEBUG')
nowAndDebugLog('nowAndDebugLog-xxx')  // [16:6][DEBUG]:[nowAndDebugLog-xxx]
```

