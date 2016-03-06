---
layout: post
title:  react native简介
category: 技术
comments: true
---


##  一、搭建开发环境

目前我研究ios 的native ，所以基于mac系统。需要的工具包括：

1.xocde  
2.Node.js 4.0  
3.使用HomeBrew安装wathman 和flow  

###1.1 安装Node.js

前往node.js 的[官网 英文](https://nodejs.org) [官网中文](http://nodejs.cn)下载pkg安装包

Node.js是javascript的运行环境，JavaScript作为前端语言，在浏览器中解释执行，而Node.js 是后端JavaScript运行环境，可以在mac、window、linux上执行JavaScript代码。

brew.sh
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew install node

npm install -g n

n

node server node.js

node index.js

sublime  一个有用的文本编辑器

commonjs  一个规范

鱼摆摆  一个翻墙软件 

创建模块的流程

创建模块   teacher.js

导出模块   export.add = fuction(){}

加载模块    var teacher = require(./teacher.js)

使用模块   teacher.add(“lijian”)

慕课网  可以学习nodejs


终端中看node.js的方法

在终端中输入 node

url

url.parse(“sdfsdff”);
