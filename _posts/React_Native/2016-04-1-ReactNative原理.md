---
layout: post
title:  native原理
category: 技术
comments: true
---


## 一、 简介

reactnative 引入的原理可以参考 [把现代web科技带给移动开发者](http://bbs.reactnative.cn/topic/14/react-native-把现代web科技带给移动开发者),下面是自己的一点总结：

## 1.1 开发原生的APP 比较困难

开发成本高，耗时，每次发版受apple的限制。

## 1.2 开发原生开发非常必要 

1. 原生APP 的用户体验比web Hybird APP 的用户体验好 
2. 在web上，我们也没有一个足够完善的线程模型，很难利用多线程并行执行工作

## 1.3 将两个世界合二为一？

 用脚本封装原生，即用JavaScript去调用原生API，优点：

1. 能获得原生平台的所有强大之处
2. 同时还能享受快速迭代和使用我们现有JavaScript上基础设施的好处
3. 因为基于JavaScript构建，我们应当能使得这样技术栈跨平台。

## 1.4 用脚本封装原生是一件需要技巧的事情

1. 如果我们只是同步的在原生环境和解释环境之间调用，我们的UI线程很可能会被JavaScript执行阻塞住。
2. 要提升界面的响应效率，我们知道我们必须把JavaScript放到主线程之外执行，但这么做其实很困难。最直接的困难就是资源访问竞争。如果我们的JavaScript访问什么正好在被别的线程用的东西（譬如一个渲染的View的尺寸），系统就只能加锁来确保方案安全，而这又会导致UI线程的卡顿。还有一个问题在于每次原生和JavaScript虚拟机之间互相访问，在访问过程中都会带来极大的开销。如果我们要经常跨线程访问，我们不得不一次又一次的经历这种开销。

## 1.5 引入React Native

react native 来源于React，React组件本来就被设计为一个纯粹的、无副作用的函数，函数返回每一个时刻当时的View状态，这样我们无需读取底层View的状态就可以为它写入新的状态。能解决上面提出的问题。

1. React Native使你能够在Javascript和React的基础上获得完全一致的开发体验，构建世界一流的原生APP。

2. React Native着力于提高多平台开发的开发效率 —— 仅需学习一次，编写任何平台。(Learn once, write anywhere)


## 1.6 使用React Native 需要了解的知识

1. 前端开发工程师必须掌握的三个技能：

* 描述网页内容的HTML     

* 描述网页样式的CSS ，[html 和css 的学习地址](http://www.imooc.com/learn/9)

* 描述网页行为的JavaScript, [java 学习地址](http://www.w3school.com.cn/js/)

2. JavaScript的语法规范 [ES5和ES6写法对照表](http://bbs.reactnative.cn/topic/15/react-react-native-的es5-es6写法对照表)

3.  ReactNative在CSS基础上使用的布局模型：[伸缩盒子模型flexBox](http://jianli2017.github.io/LJBlog/技术/2016/02/10/ReactNavie-flexBox模型.html)

4.[ JSX ](https://segmentfault.com/a/1190000002646155)

~~~
native 的目标是“一处学习，处处编写”，为了实现这个目标，mvc 模块的view 使用jsx（jsx 是js 和xml 混合编写代码的方式，是个语法糖，简化了js处理DOM的过程 ）编写。 ios 端和android端都在自己的平台上实现自己的原生模块的功能，然后暴露出统一的接口， jsx就可以不分平台的控制界面 。
~~~

##  二、搭建开发环境

reactive Native 的中文[网址](http://reactnative.cn),基于IOS的react Native需要的工具包括：
1.xocde  
2.Node.js 4.0  
3.使用HomeBrew安装wathman 和flow  

### 2.1 安装Node.js

前往node.js 的[官网 英文](https://nodejs.org) [官网中文](http://nodejs.cn)下载pkg安装包

Node.js是javascript的运行环境，JavaScript作为前端语言，在浏览器中解释执行，而Node.js 是后端JavaScript运行环境，可以在mac、window、linux上执行JavaScript代码。

### 2.2 使用ruby安装home brew

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

### 2.3 使用home brew安装 watchman 和 flow

brew install watchman   
如果你希望使用flow来为js代码加上类型检查，那么在命令行中输入brew install flow来安装flow

### 2.4 使用npm 安装 react-native-cli 命令行工具

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


### 2.5 创建一个项目 

在终端中cd到想创建工程的目录，然后输入 react-native init weidian 命令，其中weidian 是应用的名称。例如：

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

### 2.6 简单修改界面

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



为了能让js调用原生的方法或者认识原生的方法，原生模块需要遵守一定的协议。


## 3. 植入原生的应用





## 3. 微店的例子

具体的看代码


## 4. react Native 通信原理


# 原生模块的规范约定

RCTBridgeModule 桥协议

~~~
#define RCT_EXPORT_MODULE(js_name) \
RCT_EXTERN void RCTRegisterModule(Class); \
+ (NSString *)moduleName { return @#js_name; } \
+ (void)load { RCTRegisterModule(self); }
~~~

可选的协议

~~~
#define RCT_EXPORT_METHOD(method) \
  RCT_REMAP_METHOD(, method)
~~~

　　　　   UIView *subVIew = [[UIView alloc] initWithFrame:CGRectMake(100, 300, 50, 50)];
subVIew.backgroundColor = [UIColor grayColor];
[self.view addSubview:subVIew];
CAShapeLayer *shaper = [CAShapeLayer layer];
//    UIBezierPath *base = [UIBezierPath bezierPathWithArcCenter:CGPointMake(25, 25)
//                                                                  radius:10
//                                                              startAngle:0
//                                                                endAngle:2 * M_PI
//                                                               clockwise:YES];
//    shaper.path = base.CGPath;

shaper.strokeColor   = [UIColor greenColor].CGColor;   // 边缘线的颜色
shaper.lineWidth = 2.0;
shaper.fillRule = kCAFillRuleEvenOdd;
shaper.fillColor     = [UIColor redColor].CGColor;   // 闭环填充的颜色
shaper.lineCap       = kCALineCapSquare;               // 边缘线的类型
[subVIew.layer addSublayer:shaper];

CGMutablePathRef muPath = CGPathCreateMutable();

CGPathAddRect(muPath, nil, CGRectMake(5, 5, 40, 40));

CGPathAddRoundedRect(muPath, nil, CGRectMake((50-10)/2,(50-10)/2, 10, 10), 5, 5);


UIBezierPath *pazPath = [UIBezierPath bezierPathWithCGPath:muPath];
//    [pazPath closePath];
shaper.path = pazPath.CGPath;



CGMutablePathRef muPathEnd = CGPathCreateMutable();

CGPathAddRect(muPathEnd, nil, CGRectMake(5, 5, 40, 40));

CGPathAddRoundedRect(muPathEnd, nil, CGRectMake((50-40)/2,(50-40)/2, 40, 40), 20, 20);


UIBezierPath *pazPathEnd = [UIBezierPath bezierPathWithCGPath:muPathEnd];


CABasicAnimation *animation = [CABasicAnimation animationWithKeyPath:@"path"];
animation.removedOnCompletion = NO;
animation.repeatCount = 100;
animation.autoreverses = YES;
animation.fillMode = kCAFillModeForwards;
animation.duration = 2.0;
animation.fromValue = (__bridge id _Nullable)(muPath);
animation.toValue = (__bridge id _Nullable)(muPathEnd);

[shaper addAnimation:animation forKey:@"aa"];



http://www.open-open.com/lib/view/open1451460443901.html