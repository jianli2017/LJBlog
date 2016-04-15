---
layout: post
title:  JavaScript权威指南 学习笔记（1）
category: 技术
comments: true
---


# JavaScript概述  

　　　　
本书的示例代码在：http://oreilly.com/catalog/9780596805531

前端三种技能：  
* 描述网页内容的HTML
* 描述网页样式的CSS
* 描述网页行为的JAVAScript  
  
ECMAScript是JavaScript的规范

Firebug 运行一小段代码

## 1. JavaScript 语言核心

通过var关键字声明变量

~~~
var x;
x = 0;
~~~

对象是名值对的集合

~~~
var book = {
topic:"javaScript",
fat:true
}
~~~

可以通过. 或者[]来访问对象的属性

~~~
book.topic
book["fat"]
book.author = "flanagan"  //通过赋值创建一个新属性
~~~

数组：JavaScript同样支持数组（以数字为索引的列表）

~~~
var primes = [2,3,5,7];
primes[0]
primes.length
primes[4] = 9 //通过赋值来添加新的元素
~~~

表达式仅仅计算出一个值，但并不作任何操作，不改变程序的运行状态。

语句改变程序的运行状态

函数是带有参数的JavaScript代码段，可以多次调用。

~~~
fuction plus(x)
{
	return x+ 1;
}
plus(y)

var square = fuction(x){ return x*x;} /// 函数是一种值，可以赋值给变量
~~~

当函数赋值给对象的属性，我们称为方法。this关键字是对定义方法的对象的引用。构造函数以大写字母开头，使用new 关键字和构造函数创建一个实例

~~~
fuction Point(x,y)
{
this.x= x;
this.y = y;
}

var p = new Point(1,1);
~~~

通过给构造函数的prototype对象赋值来给Point对象定义方法

~~~
Point.prototype.r = fuction(){
 return Math.sqrt(
 this.x *this.x + this.y*this.y);
}
p.r();
~~~

## 2. 客户端JavaScript

JavaScript代码可以通过<script> 标签切入到HTML文件中 
