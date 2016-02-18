---
layout: post
title:  基于jekyll、github page、kramdown搭建自己的博客
category: 技术
comments: true
---


# kramdown语法学习  

 kramdown是有ruby些的library，是markdown的超级（superset）。想了解关于kramdown的详细信息，可以到[kramdown的官网](http://kramdown.gettalong.org/index.html)  

下面是自己学习kramdown是的一点中文笔记，方便自己以后查找。  

kramdown has two main classes of elements: block and span-level elements. Block-level elements are used to create paragraphs, headers, lists and so on whereas span-level elements are used to markup text phrases as emphasized, as a link and so on.  

kramdown主要有两类元素：块元素、span-level elements。block元素用于创建段落、标题、列表等待，span-level elements主要用来标记文本为连接等。 

## Block-level Elements - Main Structural Elements  

#### 标记段落   
Consecutive lines of text are considered to be one paragraph. As with other block level elements you have to add a blank line to separate it from the following block-level element:

通过在段落的末尾添加一个空行，将段落和其他block分割开。 （这个觉得比较有用，）

Explicit line breaks in a paragraph can be made by using two spaces or two backslashes at the end of a line:

在行的末尾添加两个空格或两个反斜杠，将在段落中显示的创建新行

#### 标题

kramdown supports Setext style headers and atx style headers. A header must always be preceded by a blank line except at the beginning of the document

kramdown支持六级标题 ，一级标题使用一个#，二级标题使用两个#，以此类推,写法如下：  

~~~

# H1 header

## H2 header

### H3 header

#### H4 header

##### H5 header

###### H6 header
~~~  

#### 引用  
A blockquote is started using the > marker followed by an optional space; all following lines that are also started with the blockquote marker belong to the blockquote. You can use any block-level elements inside a blockquote  

使用>和可选的空格 标记，创建一个引用block。所有后续的引用中的行都包含>,你可以在引用元素中添加任意其他的元素。下面是具体的例子  

~~~
> This is a blockquote
continued on this
and this line.  

But this is a separate paragraph.
~~~

#### 代码段  
kramdown supports two different code block styles. One uses lines indented with either four spaces or one tab whereas the other uses lines with tilde characters as delimiters – therefore the content does not need to be indented。  
kramdown 支持两种风格的代码段，一种是用四个空格或一个tab制表符，另一种使用多个波浪线开始，后面跟代码（代码中不需要添加波浪线），并以多个波浪线结束（个数多余开始波浪线的个数）。下面是示例代码：  
~~~~~~
This is also a code block.
~~~
Ending lines must have at least as
many tildes as the starting line.
~~~~~~~~~~~~  

#### 水平指标符  
It is easy to insert a horizontal rule in kramdown: just use three or more asterisks, dashes or underscores, optionally separated by spaces or tabs, on an otherwise blank line  
使用三个或者更多的星号（*）、破折号（-）、下划线（_）。后面跟随可选分割符，包括tab、空行，下面是具体的例子：  
~~~
* * *

---

_  _  _  _

---------------
~~~~ 

* * *  你好 

***  你好

---  你好

_  _  _  _ 你好

--------------- 你好 

