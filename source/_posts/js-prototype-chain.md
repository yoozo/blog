---
title: js原型与原型链的理解
date: 2019-04-20 20:57:31
tags:
 - javascript
category:
 - javascript
---

prototype 原型
\_\_proto\_\_ 原型链
constructor 构造函数
> 每个构造函数(constructor)都有一个原型对象(prototype),原型对象都包含一个指向构造函数的指针,而实例(instance)都包含一个指向原型对象的内部指针.

<!-- more -->
*下面的代码是在严格模式下的运行*

## 构造函数
先看下例子
```js
function A(){
    if(this.getConstructorName)
        console.log('这是一个构造函数：' + this.getConstructorName,`执行model方法：${this.getConstructorName()}`)
    else
        // 这里再严格模式下 this.w = undefined
        console.log('这是一个函数,使用：' + this.getConstructorName)
}

A.prototype.getConstructorName = function(){ return this.constructor.name }
// 这样使用代表这是一个普通函数
A()
// 使用new关键字表示这是一个构造函数
new A()
```
