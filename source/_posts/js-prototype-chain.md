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
> 每个构造函数(constructor)都有一个指向**原型对象**的属性prototype，**原型对象**都包含一个指向构造函数(constructor)的指针，而实例(instance)都包含一个指向**原型对象**的属性\_\_proto\_\_ 。

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
当使用new A()的时候，A就是构造函数，直接使用A()的时候就是一个普通函数

> 为了更好区分普通函数和构造函数，一般**约定**了构造函数有三大特点：
>  - 构造函数的函数名的**首字母大写**。
>  - 函数体内使用this关键字，代表所要生成的对象实例。
>  - 生成对象的时候，必须使用new关键字来调用构造函数。


## \_\_proto\_\_和prototype
\_\_proto\_\_和prototype都指向**原型对象**
 - \_\_proto\_\_
   > 每个对象都有一个\_\_proto\_\_属性，它指向这个对象的**原型**。

 - prototype
   > prototype是函数对象(Function)的特有属性，它指向用该函数(Function)创建的对象的**原型**。

所以，Function对象都有2个属性\_\_proto\_\_和prototype，而普通对象只有2个属性中的\_\_proto\_\_


## 原型对象
先看下下面的例子：
```js
// 定义一个函数,Test.prototype指向的对象就是Test类的实例的原型
function Test(){}
// 默认创建了一个Test类的原型对象
let proto = Test.prototype
console.log(proto)
// 可以看出来原型对象默认有2个属性constructor、__proto__

let test = new Test()
// 判断对象test 和 Test类的原型对象的关系
console.log(proto === test)
// false 
console.log(proto === test.__proto__)
// true 说明属性__proto__指向原型就是该类的原型对象
```
 - 前面多次出现**原型**，那么原型到底是指什么？
   > 原型其实就是一个对象，当你定义一个构造函数(constructor)的时候，默认就会为你创建一个对象，此时这个对象就是你使用new关键字创建出来的对象的**原型**。
 - 根据上面的例子分析
   > test的**原型**就是proto(引用类型的变量)所指向的对象，此时这个对象就是test对象的**原型**，test.\_\_proto\_\_指向这个**原型对象**。可以认为proto就是test对象的原型。


## 原型链
下面来一张的经典的原型链图
![原型链](/images/prototype-chain.jpg)