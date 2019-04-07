---
title: js类型比较
tags: 
 - ES6
 - javascript
category: javascript
---


<!-- more -->

## javascript七大类型
javascript的数据类型分为两类：原始类型和对象类型。   
- 原始类型（6个）   
  三个普通类型：数字（number）、字符串（string）、布尔值（bool）、Symbol(ES6新增类型)   
  两个特殊原始值：空（null）、未定义（undefined）
- 对象类型（object）   
  每个属性都由 &lt;key:value&gt;构成，value可以是任意类型（包括对象类型）

## typeof操作符获取类型
typeof 返回值有 `object\boolean\undefined\number\string\symbol\function`
 - 可以简单获取到上述返回类型
 - 但是不可以判断null，也不可以获取到具体的类型

## instanceof操作符

## 通过Object.prototype.toString.call()判断类型