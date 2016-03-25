---
layout: post
title:  react native简介
category: 技术
comments: true
---


##  一、搭建开发环境

reactive Native 的中文[网址](http://reactnative.cn),目前我研究ios 的native ，所以基于mac系统。需要的工具包括：

1.xocde  
2.Node.js 4.0  
3.使用HomeBrew安装wathman 和flow  

### 1.1 安装Node.js

前往node.js 的[官网 英文](https://nodejs.org) [官网中文](http://nodejs.cn)下载pkg安装包

Node.js是javascript的运行环境，JavaScript作为前端语言，在浏览器中解释执行，而Node.js 是后端JavaScript运行环境，可以在mac、window、linux上执行JavaScript代码。

### 1.2 使用ruby安装brew

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### 1.3 使用home 安装 watchman 和 flow

brew install watchman   
如果你希望使用flow来为js代码加上类型检查，那么在命令行中输入brew install flow来安装flow

### 1.4 使用npm 安装 react-native-cli 命令行工具

安装react-native-cli 命令行工具，在终端中输入： npm install -g react-native-cli

执行成功，会有如下的显示：  

~~~
/usr/local/bin/react-native -> /usr/local/lib/node_modules/react-native-cli/index.js
- pkginfo@0.3.1 node_modules/react-native-cli/node_modules/winston/node_modules/pkginfo
/usr/local/lib
└─┬ react-native-cli@0.2.0 
  ├── minimist@1.2.0 
  └─┬ prompt@0.2.14
    ├── pkginfo@0.3.1 
    └─┬ utile@0.2.1
      └─┬ mkdirp@0.5.1
        └── minimist@0.0.8 

~~~

安装n 工具，在命令行中输入：npm install -g n,安装成功，会有如下的提示：  

~~~
/usr/local/bin/n -> /usr/local/lib/node_modules/n/bin/n
/usr/local/lib
└── n@2.1.0 
~~~

~~~
/* 这个目前不知道做什么*、
n

node server node.js

node index.js
~~~

### 1.5 创建一个项目 

在终端中输入想创建工程的目录，然后输入 react-native init weidian 命令，其中weidian 是应用的名称。例如：

~~~
cd /Users/gome/GitHub/native_sample 
react-native init weidian
~~~

如果创建成功，终端会有如下输出：

~~~
This will walk you through creating a new React Native project in /Users/gome/GitHub/native_sample/weidian
Installing react-native package from npm...
Setting up new React Native app in /Users/gome/GitHub/native_sample/weidian
weidian@0.0.1 /Users/gome/GitHub/native_sample/weidian
└─┬ react@0.14.7 
  ├─┬ envify@3.4.0 
  │ └─┬ jstransform@10.1.0 
  │   ├── base62@0.1.1 
  │   ├── esprima-fb@13001.1001.0-dev-harmony-fb 
  │   └── source-map@0.1.31 
  └─┬ fbjs@0.6.1 
    └── whatwg-fetch@0.9.0 

To run your app on iOS:
   cd /Users/gome/GitHub/native_sample/weidian
   react-native run-ios
   - or -
   Open /Users/gome/GitHub/native_sample/weidian/ios/weidian.xcodeproj in Xcode
   Hit the Run button
~~~

创建完的目录结构如下：

~~~
weidian
   ├── index.ios.js
   ├── node_modules 
   └── package.json
   ├── ios   
        ├── weidian
        ├── weidian.xcodeproj 
~~~

下面是react-native init 慢的解决方法， 替换为淘宝的镜像源，在终端中输入如下命令：

~~~
npm config set registry https://registry.npm.taobao.org 
npm config set disturl https://npm.taobao.org/dist
npm info underscore //（如果上面配置正确这个命令会有字符串response）
~~~

或者前往~/.npmrc 修改内容为如下，也可以使用命令 cat  ~/.npmrc 先查看下这个文件的内容。

~~~
registry = https://registry.npm.taobao.org
~~~

### 1.6 简单修改界面

修改index.ios.js可以简单修改界面，下面是index.ios.js的内容：

~~~
import React, {
  AppRegistry,
  Component,
  StyleSheet,
  Text,
  View
} from 'react-native';

class weidian extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
        <Text style={styles.instructions}>
          To get started, edit index.ios.js
        </Text>
        <Text style={styles.instructions}>
          Press Cmd+R to reload,{'\n'}
          Cmd+D or shake for dev menu
        </Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

AppRegistry.registerComponent('weidian', () => weidian);

~~~

##  二、ES6的学习

React Native从0.18之后，新建项目默认已经采用了ES6语法，故我们推荐不熟悉ES6与ES5区别的朋友先读读这篇文章：[React/React Native 的ES5 ES6写法对照表](http://bbs.reactnative.cn/topic/15/react-react-native-的es5-es6写法对照表),下面是我边学习中方便记忆，又重新写了一遍。

### 2.1  模块

#### 2.1.1 引用

在ES5里，如果使用CommonJS标准，引入React包基本通过require进行，代码类似这样：

~~~
//ES5
var React = require("react-native");
var {
    Image,
    Text,
    PropTypes
} = React;  //引用不同的React Native组件
~~~

在ES6里，import写法更为标准

~~~
//ES6
import React, {
    Image, 
    Text,
    PropTypes
} from 'react-native';
~~~

#### 2.1.2 导出单个类

在ES5里，要导出一个类给别的模块用，一般通过module.exports来导出

~~~
//ES5
var MyComponent = React.createClass({
    ...
});
module.exports = MyComponent;
~~~

在ES6里，通常用export default来实现相同的功能：

~~~
export default class MyComponent externds React.Component{
...
}
~~~

### 2.2 定义组件

在ES5里，通常通过React.createClass来定义一个组件类，像这样：

~~~
//ES5
var Photo = React.createClass({
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});
~~~

在ES6里，我们通过定义一个继承自React.Component的class来定义一个组件类，像这样：

~~~
//ES6
class Photo extends React.Component {
    render() {
        return (
            <Image source={this.props.source} />
        );
    }
}
~~~

#### 2.2.1 给组件定义方法

从上面的例子里可以看到，给组件定义方法不再用 名字: function()的写法，而是直接用名字()，在方法的最后也不能有逗号了。

~~~
//ES5 
var Photo = React.createClass({
    componentWillMount: function(){

    },
    render: function() {
        return (
            <Image source={this.props.source} />
        );
    },
});
~~~

~~~
class Photo extends React.Component{
	compnentWillMount(){
	}
	render(){
		return(
			<Image Source={this.props.source}/>
		);
	}
}
~~~

#### 2.2.2 定义组件的属性类型和默认属性

在ES5里，属性类型和默认属性分别通过propTypes成员和getDefaultProps方法来实现

~~~
//ES5 
var Video = React.createClass({
    getDefaultProps: function() {
        return {
            autoPlay: false,
            maxLoops: 10,
        };
    },
    propTypes: {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    },
    render: function() {
        return (
            <View />
        );
    },
});
~~~

在ES6里，可以统一使用static成员来实现

~~~
//ES6
class Video extends React.Component {
    static defaultProps = {
        autoPlay: false,
        maxLoops: 10,
    };  // 注意这里有分号
    static propTypes = {
        autoPlay: React.PropTypes.bool.isRequired,
        maxLoops: React.PropTypes.number.isRequired,
        posterFrameSrc: React.PropTypes.string.isRequired,
        videoSrc: React.PropTypes.string.isRequired,
    };  // 注意这里有分号
    render() {
        return (
            <View />
        );
    } // 注意这里既没有分号也没有逗号
}
~~~

也有人这么写，虽然不推荐，但读到代码的时候你应当能明白它的意思

~~~
//ES6
class Video extends React.Component {
    render() {
        return (
            <View />
        );
    }
}
Video.defaultProps = {
    autoPlay: false,
    maxLoops: 10,
};
Video.propTypes = {
    autoPlay: React.PropTypes.bool.isRequired,
    maxLoops: React.PropTypes.number.isRequired,
    posterFrameSrc: React.PropTypes.string.isRequired,
    videoSrc: React.PropTypes.string.isRequired,
};
~~~

### 2.3 初始化STATE

ES5下情况类似

~~~
//ES5 
var Video = React.createClass({
    getInitialState: function() {
        return {
            loopsRemaining: this.props.maxLoops,
        };
    },
})
~~~

ES6下，有两种写法：

~~~
//ES6
class Video extends React.Component {
    state = {
        loopsRemaining: this.props.maxLoops,
    }
}
~~~











































~~~

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
~~~