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

#### 水平指标符  （这个效果没有实现）
It is easy to insert a horizontal rule in kramdown: just use three or more asterisks, dashes or underscores, optionally separated by spaces or tabs, on an otherwise blank line  
使用三个或者更多的星号（*）、破折号（-）、下划线（_）。后面跟随可选分割符，包括tab、空行，下面是具体的例子：  

 
#### 列表（lists）

kramdown supports ordered and unordered lists. Ordered lists are started by using a number followed by a period, a space and then the list item text. The content of a list item consists of block-level elements. All lines which have the same indent as the text of the line with the list marker belong to the list item。  

kramdown支持两种风格的列，有序和无序。有序列表用数字开始，后面跟随period（.），接着是空格和列表的内容。 列表的内容可以包含其他类型的块元素。

~~~
1. Item one
    1. sub item one
    2. sub item two
    3. sub item three  
2. Item two
~~~~

1. Item one
    1. sub 1
    2. sub 2 
1. item Two


Unordered lists are started by using an asterisk, a dash or a plus sign (they can be mixed) and a space. Apart from that unordered lists follow the same rules as ordered lists

使用星号、破择号、加号开始，创建无序列，例如代码和效果

~~~
* item
+ item
- item  
~~~~

* item
+ item
- item

#### 定义列表（Definition Lists）  
A definition list works similar to a normal list and is used to associate definitions with terms. Definition lists are started when a normal paragraph is followed by a line starting with a colon and then the definition text. One term can have many definitions and multiple terms can have the same definition. Each line of the preceding paragraph is assumed to contain one term, for example。
定义列表：用于术语相关的定义，他的工作方式类似于常规的列表。定义列表的格式：开始于正常的段落，后面跟随一行，这行以冒号（：）开始，后面是定义内容。  

~~~~
term
: defination
: defination2
~~~~~

term  
: defination
: defination2

If you insert a blank line before a definition (note: there must only be one blank line between the terms and the first definition), the definition will be wrapped in a paragraph  

如果在定义前面插入一个空行，那么定义被打包到一个段落中。  

Each term can be styled using span-level elements and each definition is parsed as block-level elements, i.e. you can use any block-level in a definition. Just use the same indent for the lines following the definition line  

每个术语可以使用span-level elements定制分割，每个定义被解析为一个block-level elements，你可以在定义中使用任何的block-level elements。  

#### 表（tables） 
 
kramdown supports a syntax for creating simple tables. A line starting with a pipe character (|) starts a table row. However, if the pipe characters is immediately followed by a dash (-), a separator line is created. Separator lines are used to split the table header from the table body (and optionally align the table columns) and to split the table body into multiple parts. If the pipe character is followed by an equal sign (=), the tables rows below it are part of the table footer.  

kramdown具有创建表的语法。 表的每行使用竖线（|）开始，如果竖线后面紧跟着的是破折号，那么会创建分隔符。分隔符用于分离表头和表体或者将表体分割为多个部分。如果竖线后面紧跟着的是等号，那么后面的行是表的尾部。  

~~~
| Header1 | Header1 |  Header3|  
|:       :|:       :|:       :|  	
| cell1   |  cell2  | cell3   |  
| cell4   |  cell5  | cell6   |  
|———  
| cell1   |  cell2  | cell3   |  
| cell4   |  cell5  | cell6   |  
|=====
| Foot1   |  Foot2  | Foot3   |  
~~~~

| Header1 | Header1 |  Header3|  
|:       :|:       :|:       :|  	
| cell1   |  cell2  | cell3   |  
| cell4   |  cell5  | cell6   |  
|———  
| cell1   |  cell2  | cell3   |  
| cell4   |  cell5  | cell6   |  
|=====
| Foot1   |  Foot2  | Foot3   | 

#### HTML elements  

kramdown allows you to use block-level HTML tags (div, p, pre, …) to markup whole blocks of text – just start a line with a block-level HTML tag. kramdown syntax is normally not processed inside an HTML tag but this can be changed with the parse_block_html option. If this options is set to true, then the content of a block-level HTML tag is parsed by kramdown either as block level or span-level text, depending on the tag 
 
kramdown支持用html标记标识文本块。 语法： 新起一行，添加html标记。一般，在html标记中的kramdown原始是不被kramdown处理的。你可以设置parse_block_html为true，这样包含在html标记中的kramdown原始可以被kramdown处理。更过关于html标记的学习，可以参考[这里](http://www.w3school.com.cn/tags/tag_div.asp)
 
~~~ 
<div style="float: right">
Something that stays right and is not wrapped in a para.
</div>

{::options parse_block_html="true" /}

<div>
This is wrapped in a para.
</div>
<p>
This can contain only *span* level elements.
</p>  
~~~

<div style="float: right">
Something that stays right and is not wrapped in a para.
</div>

{::options parse_block_html="true" /}

<div>
This is wrapped in a para.
</div>
<p>
This can contain only *span* level elements.
</p>  

#### Block Attributes  

You can assign any attribute to a block-level element. Just directly follow the block with a block inline attribute list (or short: block IAL). A block IAL consists of a left curly brace, followed by a colon, the attribute definitions and a right curly brace. Here is a simple example which sets the title attribute of a block quote.

在元素的后面紧跟着元素的属性 可以设置元素的属性。属性元素的语法包括：左大括号开始，跟随冒号、属性定义、右大括号。

## Span-Level Elements - Text Modifiers

#### （强调或加粗）Emphasis  

Emphasis can be added to text by surrounding the text with either asterisks or underscores

加粗可以通过在文本的前后添加星号或者下划线  

~~~
This is *emphasized*,_this_ too!
~~~~  

This is *emphasized*,_this_ too! 

Strong emphasis can be done by doubling the delimiters  
进一步强调可以通过加倍分隔符实现  
 
~~~
This is **strong**,
__this__ too!
~~~~

This is **strong**,
__this__ too!

#### Links and Images

A simple link can be created by surrounding the text with square brackets and the link URL with parentheses  

简单的link语法： 创建一段用中括号包括的文字，后面跟随url，url使用小括号括起来。

~~~
A [link](http://kramdown.gettalong.org)
to the kramdown homepage.
~~~~

A [link](http://kramdown.gettalong.org)
to the kramdown homepage.









## liquid用法笔记

下面是[liquid](http://blog.csdn.net/dont27/article/details/38097581)用法的说明。

## jekyll 使用指南

下面是[jekyll](http://jekyllcn.com/docs/configuration/)的使用指南  

下面是参考的博文：
[采用Jekyll + github + pygments构建个人博客的最终说明](http://www.jianshu.com/p/609e1197754c)
































