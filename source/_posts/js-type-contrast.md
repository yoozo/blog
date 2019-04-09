---
title: js类型比较
tags:
  - ES6
  - javascript
category: javascript
date: 2019-04-09 22:58:51
---


比较数据类型做比较的三种方法typeof\instanceof\Object.prototype.toString.call()
<!-- more -->

## javascript七大类型
javascript的数据类型分为两类：原始类型和对象类型。   
### 原始类型（6个）   
  四个普通类型：数字（number）、字符串（string）、布尔值（bool）、Symbol(ES6新增类型)   
  两个特殊原始值：空（null）、未定义（undefined）
### 对象类型（object）   
  每个属性都由 &lt;key:value&gt;构成，value可以是任意类型（包括对象类型）

## typeof操作符获取类型
typeof 返回值有 `object\boolean\undefined\number\string\symbol\function`
 - 确定不可以判断null，也不可以获取到具体的类型

```js
console.log(typeof 42);
// expected output: "number"

console.log(typeof 'blubber');
// expected output: "string"

console.log(typeof true);
// expected output: "boolean"

console.log(typeof declaredButUndefinedVariable);
// expected output: "undefined";

let aa = null;
console.log(typeof aa);
// expected output: "object"

```

## instanceof操作符
instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。 
[参考资料](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/instanceof)
```js
// 定义构造函数
function C(){} 
function D(){} 

var o = new C();


o instanceof C; // true，因为 Object.getPrototypeOf(o) === C.prototype


o instanceof D; // false，因为 D.prototype不在o的原型链上

o instanceof Object; // true,因为Object.prototype.isPrototypeOf(o)返回true
C.prototype instanceof Object // true,同上

C.prototype = {};
var o2 = new C();

o2 instanceof C; // true

o instanceof C; // false,C.prototype指向了一个空对象,这个空对象不在o的原型链上.

D.prototype = new C(); // 继承
var o3 = new D();
o3 instanceof D; // true
o3 instanceof C; // true 因为C.prototype现在在o3的原型链上
```
- 可以确定当前数据是否是某个对象（Object）
- 缺点：无法确定原始类型是否是[原始类型](#原始类型（6个）)

## 通过Object.prototype.toString.call()判断类型
这种判断算是比较靠谱的，可以判断出数据的七大类型以及内置对象（Date\Json等）
```js
Object.prototype.toString.call(null); // "[object Null]"
Object.prototype.toString.call(undefined); // "[object Undefined]"
Object.prototype.toString.call(“abc”);// "[object String]"
Object.prototype.toString.call(123);// "[object Number]"
Object.prototype.toString.call(true);// "[object Boolean]"
Object.prototype.toString.call(Symbol());// "[object Symbol]"
```