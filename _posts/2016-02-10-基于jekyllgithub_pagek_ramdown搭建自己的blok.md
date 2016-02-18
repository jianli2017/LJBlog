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


