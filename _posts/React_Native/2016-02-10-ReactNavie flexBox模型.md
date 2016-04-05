---
layout: post
title:  ReactNative flexBox 伸缩盒子模型
category: 技术
comments: true
---


##  一、flexBox模型

　　　　
任何一个元素都可以指定为flexbox 布局，设置为display:flex或display:inline-flex的元素称为伸缩容器，伸缩容器的子元素称为伸缩项目，下面是伸缩的模型：
![伸缩模型]({{site.url}}/images/reactnative/1.png)

## 二、React Native中使用flexBox

1. flexDirection（伸缩容器）

2. alignItems（伸缩容器）

3. flexWrap（伸缩容器）
4. justifyContent（伸缩容器）
5. alignSelf（伸缩项目）
6. flex （伸缩项目）


flexDirection 指定主轴方向

~~~
flexDirection:row|column
~~~

效果图如下：
![row]({{site.url}}/images/reatNative FlexBox模型/1.png)

![column]({{site.url}}/images/reatNative FlexBox模型/2.png)


alignItems 该属性用来定义伸缩项目在伸缩容器的交叉轴上的对齐方式

~~~
alignSelf:auto|flex-start|flex-end|center|stretch
~~~

![flex-start]({{site.url}}/images/reatNative FlexBox模型/3.png)

![flex-end]({{site.url}}/images/reatNative FlexBox模型/4.png)

![flex-center]({{site.url}}/images/reatNative FlexBox模型/5.png)



flexWrap 指定伸缩容器的主轴方向空间不足的情况下，是否换行以及如何换行

~~~
flexWrap:wrap|noWrap
~~~

justifyContent指定伸缩项目沿主轴线的对齐方式

~~~
justifyContent:flex-start|flex-end|center|space-between|space-around
~~~


alignSelf

~~~
alignSelf:auto|flex-start|flex-end|center|stretch
~~~

flex

~~~
flex:number
~~~
