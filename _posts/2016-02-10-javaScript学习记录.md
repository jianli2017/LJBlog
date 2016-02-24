---
layout: post
title:  javascript学习记录
category: 技术
comments: true
---


# 主要的思想

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

JavaScript的数值类型分为两类：原始类型和对象类型。原始类型有数字、字符串、布尔值、null、undefined。对象是属性的集合，数组是特殊的对象（Array），函数也是特殊的对象（function）。