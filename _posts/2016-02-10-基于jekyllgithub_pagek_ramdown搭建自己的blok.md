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

kramdown支持六级标题 ，一级标题使用一个#，二级标题使用两个#，以此类推

~~~

# H1 header

## H2 header

### H3 header

#### H4 header

##### H5 header

###### H6 header
{% endraw %}
~~~

