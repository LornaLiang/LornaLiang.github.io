---
layout: post
title:  "面试总结01"
date:   2018-05-04
tag: interview summary
---

# 面试题总结
本菜鸟最近在找前端开发的相关工作，现在把之前面试遇到的问题整理一下，感觉自己真的是太弱了，还学要多练习写项目，加深理解。


------
### 1.解释一下CSS 3的flexible盒子模型，并说明该模型是用来解决什么问题。

<p>flexible box 或flexbox，指弹性盒子，是CSS3的一种新的布局模式。弹性盒子模型由弹性容器(flex container)和弹性子元素(flex item)组成。弹性容器通过设置display属性的值为flex或inline-flex将其定义为弹性容器。弹性容器内包含了一个或多个弹性子元素。</p>
<p>弹性盒子模型提供了一种更加有效的方式来对一个容器中的子元素进行排列、对齐和分配空白空间，是一种当页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。（说人话：解决浏览器和设备的兼容问题。）</p>
**补充：其他盒子模型**
<p>标准模型：一个块的总宽度=width+margin(左右)+padding(左右)+border(左右)</p>
![standar](/images/post/interview01/standar.png)
<p>怪异盒子模型：一个块的总宽度=width+margin(左右)(width已经包含了padding和border的值)</p>
![unstandar](/images/post/interview01/un-standar.png)

<br>

### 2.style标签放在body之前和body之后的区别。

<p>浏览器自上而下对HTML文档进行解析，style标签放在之前就意味着当整个文档加载完成以后样式已经渲染完成了。如果style放在body之后，当浏览器解析到尾部的样式表的时候，会停止之前的渲染，继续等待解析样式表完成之后再重新渲染。在IE浏览器下可能出现FOUC(文档样式短暂失效)现象，即短暂的花屏现象。</p>
<br>

### 3.简单谈一谈JS引擎的执行机制。

JS引擎读取网页中的JavaScript代码，对其进行处理后运行。
<p>网页中嵌入JavaScript代码的方式有两种,通过&lt;script&gt;&lt;/script&gt 嵌入或者指定外部的脚本文件。脚本的执行顺序由它们在页面中出现的位置决定。第二个问题说了，浏览器会自找不着自上而下的顺序对HTML文档进行解析。
</p>
（1）首先，JS是单线程的。
<p>进程：一个程序及其数据在处理机上顺序执行时发生的活动，是系统进行资源分配和调度的一个独立单位。它由一组机器指令、数据和堆栈组成。<br>
线程：程序执行流的最小单元。一个进程中包含了多个线程，它们可以利用进程所拥有的所有资源，通常把线程作为独立运行和独立调度的基本单位。 </p>
为什么是单线程？<br>
JS要操作DOM结点，如果同时有两个线程，对于同一个结点，一个要给这个结点添加新内容，另一个要删除这个结点，岂不是要打起来~

（2）Event Loop（事件循环）<br>
先来明确两个概念，同步和异步，以及为什么JS需要异步执行。<br>
<b>同步任务</b>：在主线程上排队执行的任务，只有当一个任务执行完毕的时候才能顺序执行下一个任务。<br>
<b>异步任务</b>：任务进入任务队列中，任务队列通知主线程某个异步任务可以执行的时候，该异步任务才会进入主线程执行。<br>
<b>为什么要异步？</b><br>
如果一段代码解析起来需要很长的时间，那么下面的代码就会阻塞，卡在那里无法执行，用户体验很差。<br>
还要明确<b>任务队列</b>的类型<br>
microtask queue(微任务队列)：同一个事件循环中，微任务按队列顺序，串行执行。<br>
macrotask queue（宏任务队列）：宏任务存在优先级，同一个事件循环中只执行一个。<br>
![jschart](/images/post/interview01/jschart.png)

### 4.JS是如何判断一个变量是String型的变量，写出实现函数。

就是JavaScript的类型检测，有很多方法。<br>
(1)<b>typeof运算符</b><br>
```JavaScript
console.log("123是什么类型:"+typeof 123);
console.log("success是什么类型:"+typeof "success");
console.log("false是什么类型:"+typeof false);
console.log("null是什么类型:"+typeof null);
```
![typeof](/images/post/interview01/typeof.png)

(2)<b>instanceof运算符判断数组</b><br>
instanceof实质上是一个三目运算符a instanceof b?alert("true"):alert("false")<br>

```JavaScript
 var a=[];
 console.log(a instanceof Array);//结果为true		
``` 
(3)<b>Object.prototype.toString.call方法</b><br>
```JavaScript
 var a=[];
 console.log(Object.prototype.toString.call(a));//结果为[object Array]
```
### 5.将数组[1,2,3,4,5,6,7,8,9,10,11]分割成[[1,2,3],[4,5,6],[7,8,9],[10,11]]

### 6.统计字符串"aaaabbbccddfgh"中出现次数最多的字符的次数。

```JavaScript
 var str="accccddfgh";
 var obj={};
 for(var i=0;i<str.length;i++){
		var k=str.charAt(i);
		if(obj[k]){
			obj[k]++;
		}else{
			obj[k]=1;
		}
		}
		var m=0;
		var i=null;
		for(var k in obj){
			if(obj[k]>m){
				m=obj[k];
				i=k;
			}
		}
		document.write(i+':'+m);
```
统计出现次数最多的字符<br>
```JavaScript
 var str="accccddfgh";
 var obj={};
  for(var i=0;i<str.length;i++){
	var v=str.charAt(i);
	if(obj[v]&&obj[v].value==v){
    	obj[v].count=++obj[v].count;
	}else{
		obj[v]={};
		obj[v].count=1;
		obj[v].value=v;
			}
	}
 for(key in obj){
//循环打印各个字符出现的次数
  document.write(obj[key].value+':'+obj[key].count+' ');
	}
```
### 7.如何让div垂直水平居中？

方法很多，这个应该不难。举个栗子~<br>
<b>直接在浏览器中垂直水平居中</b><br>

```HTML
<style>
		.a{
       position: relative;
		}
		.b{
			width:200px ;
			height: 200px;
			border: solid 1px chocolate;
			position: absolute;
			top:50%;
			left: 50%;
		 margin-top: 100px;
		 margin-left: -100px;
		}
	</style>
<body>
<div class="a">
	<div class="b">			
	</div>			
</div>
</body>
 
```
<b>一个div在另一div中垂直水平居中</b><br>

```HTML
    .parent {
          width:800px;
          height:500px;
          border:2px solid #000;
          position:relative;
}
 .child {
            width:200px;
            height:200px;
            margin: auto;  
            position: absolute;  
            top: 0; left: 0; bottom: 0; right: 0; 
            background-color: red;
}
```

