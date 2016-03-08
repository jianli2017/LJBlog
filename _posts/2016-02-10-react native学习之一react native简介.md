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

###1.2 使用ruby安装brew

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### 1.3 使用home 安装 watchman 和 flow

brew install watchman
brew install flow

### 1.4 使用npm 安装 react-native-cli 命令行工具

install -g react-native-cli

npm install -g n

n

node server node.js

node index.js

### 1.5 创建一个项目 

在终端中输入 react-native init hello  这样就创建一个项目 

下面是react-native init 慢的解决方法；

1.通过config命令

npm config set registry https://registry.npm.taobao.org 
npm info underscore （如果上面配置正确这个命令会有字符串response）

2.命令行指定

npm --registry https://registry.npm.taobao.org info underscore 

3.编辑 ~/.npmrc 加入下面内容

registry = https://registry.npm.taobao.org


### 1.6 从react到react Native

react 的github [地址](https://facebook.github.io/react/), React 的官方介绍是： a javascript library for building user interface   

react 的特点：

1.作为UI
2.虚拟dom
3.数据流

需要掌握的内容：

jsx 语法类似xml
ES6
前端基础知识（js 和css）

react 的IDE 可以使用 WebStorm 

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
