---
layout: post
title:  "JavaScript篇"
date:   2018-05-31
tag: 前端
---

# JavaScript篇
面试高频必问的问题
------
### 1.js的基本类型有哪些？引用类型有哪些？null和undefined的区别。
<p>基本类型：Number，String，Boolean，Null，undefined。</p>
<p>引用类型:Object，Array，Function。</p>
区别：<br>
**null表示“没有对象”，即不应该有值。**有两种常见用法:<br>
1.作为函数的参数，表示该函数的参数不是对象。<br>
2.作为对象原型链的终点。<br>
**undefined表示“缺少值”，此处应该有一个值但是还没有定义。**常见用法有：<br>
1.变量被声明但没有赋值。<br>
![js_1](/images/post/JavaScript/js_1.png)
<p>2.函数被调用时，应该提供的参数没有提供。</p>
![js_2](/images/post/JavaScript/js_2.png)
<p>3.对象没有赋值的属性。</p>
4.函数 没有返回值时，默认返回undefined。<br>
### 2.解释一下事件冒泡和事件捕获。

### 3.js的作用域问题。
### 4.原型链是什么？为什么要有原型链？
### 5.创建对象的方式有哪些？
### 6.实现继承的方式有哪些？
### 7.JS都有哪些内置对象和内置函数？
### 8.如何实现图片滚动懒加载？
### 9.讲一讲promise。
### 10.