---
title: js原型与原型链的理解
date: 2019-04-20 20:57:31
tags:
 - javascript
category:
 - javascript
---

>JavaScript 常被描述为一种基于原型的语言 (prototype-based language)——每个对象拥有一个**原型对象**，对象以其原型为模板、从原型继承方法和属性。**原型对象**也可能拥有原型，并从中继承方法和属性，一层一层、以此类推。这种关系常被称为原型链 (prototype chain)，它解释了为何一个对象会拥有定义在其他对象中的属性和方法。

prototype 函数特有属性，指向**原型对象**
\_\_proto\_\_ 对象属性，指向**原型对象**
constructor 构造函数
instance 实例
> 每个构造函数(constructor)都有一个指向**原型对象**的属性prototype,**原型对象**都包含一个指向构造函数(constructor)的指针,而实例(instance)都包含一个指向**原型对象**的属性\_\_proto\_\_ .

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
> 当使用new A()的时候，A就是构造函数，直接使用A()的时候就是一个普通函数

为了更好区分普通函数和构造函数，一般约定了构造函数有三大特点：
 - 构造函数的函数名的第一个字母通常大写。
 - 函数体内使用this关键字，代表所要生成的对象实例。
 - 生成对象的时候，必须使用new命令来调用构造函数。


## 原型对象
前面多次出现**原型**，那么原型到底是指什么？
原型其实就是一个对象，当你定义一个构造函数(constructor)的时候，默认就会为你创建一个对象，这个对象就是你使用new关键字创建的对象的**原型**。
```js
// 定义一个函数
function Test(){}

// 函数的prototype属性是指向Test类的的原型对象
let test = new Test()
console.log(Test.prototype)
console.log(test)
console.log(Test.prototype ==== test)
console.log(Test.prototype === test.__proto__)


```

## \_\_proto\_\_
> 每个对象都有一个\_\_proto\_\_属性的值指向他的**原型**，每一个**原型**都有\_\_proto\_\_属性。

## prototype
> prototype是函数的特有属性，指向**原型对象**。

设想一下，如果没有该字段，那创建一个实例


## new
> 根据前面的分析，那么创建实例new Object()，js到底做了什么？


## 原型链
![原型链](/images/prototype-chain.jpg)