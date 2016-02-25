---
layout: post
title:  javascript学习记录
category: 技术
comments: true
---


# 学习记录

[js的简单学习网址 ](http://www.w3school.com.cn/js/)

前端开发工程师必须掌握的三个技能：  

*描述网页内容的HTML   

*描述网页样式的CSS  

*描述网页行为的JavaScript    

可以在html文件中写一个<script>标签来嵌入javaScript代码。当浏览器加载html文件的时候，会自动执行这段代码。可以通过firebug这个工具来调试。现代的浏览器可能实现了一个简单的控制台API，可以通过使用console.log 来向控制体输出消息，同样也可以使用alert()函数传入一段文本来弹出一个对话框。

JavaScript 可以通过//来注释，JavaScript两个非常重要的数据类型是对象和数组。对象是名/值得集合或者字符串到值得映射的集合。

~~~
var   book = 
{
	topic：“JavaScript”，
	fat：ture
}
~~~~ 

可以通过.或者[]来访问对象的属性。

~~~
book.topic
book["fat"]
book.author = "flan"  //通过赋值创建一个新的属性

var primes = [2,3,4,5];
primes[0];
~~~~

## 第三章 类型、值变量

JavaScript的数值类型分为两类：原始类型和对象类型。原始类型有数字、字符串、布尔值、null、undefined。对象是属性的集合，数组是特殊的对象（Array），函数也是特殊的对象（function）。

### 3.1数字

JavaScript溢出和被零整除不会报错，溢出使用Infinity无穷大表示。下溢出是当运算结果无限接近零并比JavaScript能表示的最小值还小的时候发生的情形，这种情况会返回0. NAN（not a number）

### 3.2 文本

字符串（string） 是一组16位值组成的不可变的有序序列，每个字符通常是来自原Unicode字符集。字符串的长度（length），js中没有表示单个字符的字符型，要表示字符，只需要将其赋值给字符串即可，长度为1.字符串可以当做只读数组。

~~~
var s = “hello world”
s.charAt(0)  ///s的第一个字符
s.charAt(s.length -1 )   ///s 的最后一个字符
s.substring(1,4)   //s的第2~4个字符
s.slice(1,4)
s.slice(-3)   ////最后三个字符
s.indexOf("l")  ///l首次出现的位置
~~~~

<!-- 这是html 注释 -->

javascript 允许程序直接对变量赋值，而无需事先声明。变量和其他语法元素的名字是区分大小写的 。

数组的声明

~~~
var beatles = Array(4);
var beatles = Array();
var beatle = Array("john","paul","george","ringo");
var bealtes  = ["john","paul","george","ringo"];
~~~~

关联数组

~~~
var lennon = Array();
lennon["name"] = "john";
lennon["year"] = 1940;
lennon["living"] = false;
~~~~

对象

~~~
var lennon = Object();
lennon.name = "join"
lennon.year = 1940;
lennon.living = false;

var lennon  = {"john","paul","george","ringo"};

~~~~

函数

~~~
function name(arguments)
{
	statements;
}
~~~~

#第三章  DOM

5个常用DOM方法：getElementById、getElementByTagName、getElementByClassName、getAttribute、setAttribute。

