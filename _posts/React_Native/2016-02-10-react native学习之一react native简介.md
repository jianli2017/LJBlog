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

不过我们推荐更易理解的在构造函数中初始化（这样你还可以根据需要做一些计算）：

~~~
//ES6
class Video extends React.Component {
    constructor(props){
        super(props);
        this.state = {
            loopsRemaining: this.props.maxLoops,
        };
    }
}
~~~

### 2.4 把方法作为回调提供

很多习惯于ES6的用户反而不理解在ES5下可以这么做：

~~~
//ES5
var PostInfo = React.createClass({
    handleOptionsButtonClick: function(e) {
        // Here, 'this' refers to the component instance.
        this.setState({showOptionsModal: true});
    },
    render: function(){
        return (
            <TouchableHighlight onPress={this.handleOptionsButtonClick}>
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
});
~~~

在ES5下，React.createClass会把所有的方法都bind一遍，这样可以提交到任意的地方作为回调函数，而this不会变化。但官方现在逐步认为这反而是不标准、不易理解的。

在ES6下，你需要通过bind来绑定this引用，或者使用箭头函数（它会绑定当前scope的this引用）来调用

~~~
//ES6
class PostInfo extends React.Component
{
    handleOptionsButtonClick(e){
        this.setState({showOptionsModal: true});
    }
    render(){
        return (
            <TouchableHighlight 
                onPress={this.handleOptionsButtonClick.bind(this)}
                onPress={e=>this.handleOptionsButtonClick(e)}
                >
                <Text>{this.props.label}</Text>
            </TouchableHighlight>
        )
    },
}
~~~

箭头函数实际上是在这里定义了一个临时的函数，箭头函数的箭头=>之前是一个空括号、单个的参数名、或用括号括起的多个参数名，而箭头之后可以是一个表达式（作为函数的返回值），或者是用花括号括起的函数体（需要自行通过return来返回值，否则返回的是undefined）。


~~~
// 箭头函数的例子
()=>1
v=>v+1
(a,b)=>a+b
()=>{
    alert("foo");
}
e=>{
    if (e == 0){
        return 0;
    }
    return 1000/e;
}
~~~

需要注意的是，不论是bind还是箭头函数，每次被执行都返回的是一个新的函数引用，因此如果你还需要函数的引用去做一些别的事情（譬如卸载监听器），那么你必须自己保存这个引用

~~~
// 错误的做法
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused.bind(this));
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this.onAppPaused.bind(this));
    }
    onAppPaused(event){
    }
}

// 正确的做法
class PauseMenu extends React.Component{
    constructor(props){
        super(props);
        this._onAppPaused = this.onAppPaused.bind(this);
    }
    componentWillMount(){
        AppStateIOS.addEventListener('change', this._onAppPaused);
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this._onAppPaused);
    }
    onAppPaused(event){
    }
}

// 正确的做法
class PauseMenu extends React.Component{
    componentWillMount(){
        AppStateIOS.addEventListener('change', this.onAppPaused);
    }
    componentDidUnmount(){
        AppStateIOS.removeEventListener('change', this.onAppPaused);
    }
    onAppPaused = (event) => {
        //把方法直接作为一个arrow function的属性来定义，初始化的时候就绑定好了this指针
    }
}

~~~

### 2.5 Mixins

在ES5下，我们经常使用mixin来为我们的类添加一些新的方法，譬如PureRenderMixin

~~~
var PureRenderMixin = require('react-addons-pure-render-mixin');
React.createClass({
  mixins: [PureRenderMixin],

  render: function() {
    return <div className={this.props.className}>foo</div>;
  }
});
~~~

然而现在官方已经不再打算在ES6里继续推行Mixin，他们说：Mixins Are Dead. Long Live Composition。

尽管如果要继续使用mixin，还是有一些第三方的方案可以用，譬如这个方案

不过官方推荐，对于库编写者而言，应当尽快放弃Mixin的编写方式，上文中提到Sebastian Markbåge的一段代码推荐了一种新的编码方式：

~~~
//Enhance.js
import { Component } from "React";

export var Enhance = ComposedComponent => class extends Component {
    constructor() {
        this.state = { data: null };
    }
    componentDidMount() {
        this.setState({ data: 'Hello' });
    }
    render() {
        return <ComposedComponent {...this.props} data={this.state.data} />;
    }
};
//HigherOrderComponent.js
import { Enhance } from "./Enhance";

class MyComponent {
    render() {
        if (!this.data) return <div>Waiting...</div>;
        return <div>{this.data}</div>;
    }
}

export default Enhance(MyComponent); // Enhanced component

~~~

用一个“增强函数”，来某个类增加一些方法，并且返回一个新类，这无疑能实现mixin所实现的大部分需求。

结合使用ES6+的解构和属性延展，我们给孩子传递一批属性更为方便了。这个例子把className以外的所有属性传递给div标签：

~~~
class AutoloadingPostsGrid extends React.Component {
    render() {
        var {
            className,
            ...others,  // contains all properties of this.props except for className
        } = this.props;
        return (
            <div className={className}>
                <PostsGrid {...others} />
                <button onClick={this.handleLoadMoreClick}>Load more</button>
            </div>
        );
    }
}
~~~

下面这种写法，则是传递所有属性的同时，用覆盖新的className值：

~~~
<div {...this.props} className="override">
    …
</div>
这个例子则相反，如果属性中没有包含className，则提供默认的值，而如果属性中已经包含了，则使用属性中的值

<div className="base" {...this.props}>
    …
</div>
~~~











### 3 flexBox 模型

任何一个元素都可以指定为flexbox 布局，设置为display:flex或display:inline-flex的元素称为伸缩容器，伸缩容器的子元素称为伸缩项目，下面是伸缩的模型：
![伸缩模型]({{site.url}}/images/reactnative/1.png)

###3.1 伸缩容器属性

1. display
2. flex-directon
3. flex-wrap
4. flex-flow
5. justify-content
6. align-items
7. align-content

display 指定元素是否为伸缩容器，其语法：

~~~
display:flex|inline-flex
~~~

flex-direction 指定主轴方向

~~~
flex-direction:row|row-reverse|column|column-reverse
~~~

flex-wrap 指定伸缩容器的主轴方向空间不足的情况下，是否换行以及如何换行：

~~~
felx-wrap:nowrap|wrap|wrap-reverse
~~~

flex-flow 是flex-direction和flex-wrap的缩写版本，同时定义了伸缩容器的主轴和侧轴，其默认值是row nonwrap

justify-content指定伸缩项目沿主轴线的对齐方式

~~~
justify-content:flex-strat|flex-end|center|space-between|space-around
~~~

其中：space-around 指的是：伸缩项目平均的分布在主轴里，两端保留一般的空间

6. align-items 改属性用来定义伸缩项目在伸缩容器的交叉轴上的对齐方式

~~~
align-items:flex-strat|flex-end|center|baseline|stretch
~~~

align-content 调整伸缩项目出现换行后再交叉轴的对齐方式

~~~
algin-content:flex-start|flex-end|center|space-between|space-around|stretch
~~~

###3.2 伸缩项目属性

1. order
2. flex-grow
3. flex-shrink
4. flex-basis
5. flex
6. align-self

order用于定义项目的排列顺序。数组越小，排列越靠前，默认值为0

~~~
order:integer
~~~

flex-grow定义伸缩项目的放大比例，默认是0，即如果存在剩余空间，也不放大如果所有伸缩项目的flex-grow都为1，每个伸缩项目将设置为一个大小相等的剩余空间，如果你将其中的一个伸缩项目的flex-grow设置为2，那么这个项目所占得剩余空间是其他伸缩项目所占得剩余空间的两倍

flex-shrink用于定义伸缩项目的收缩能力

~~~
flex-shrink:number /*默认值为1*/
~~~

flex-basis 设置伸缩项目的基准值，剩余空间按比率进行伸缩

~~~
flex-basis:length|auto
~~~

flex 是flex-grow、flex-shrink、flex-basis三个属性的缩写

~~~
flex:none|flex-grow flex-shrink flex-basis/*默认值为0 1 auto*/
~~~

align-self 设置单独的伸缩项目在交叉轴上的对齐方式，会复写默认的对齐方式

~~~
align-self:auto|flex-start|flex-end|center|baseline| stretch
~~~

### 2.3 React Native中使用flexBox

1. alignItems
2. alignSelf
3. flex
4. flexDirection
5. flexWrap
6. justifyContent


flexDirection 指定主轴方向

~~~
flexDirection:row|column
~~~

flexWrap 指定伸缩容器的主轴方向空间不足的情况下，是否换行以及如何换行

~~~
flexWrap:wrap|noWrap
~~~

justifyContent指定伸缩项目沿主轴线的对齐方式

~~~
justifyContent:flex-start|flex-end|center|space-between|space-around
~~~

alignItems 该属性用来定义伸缩项目在伸缩容器的交叉轴上的对齐方式

~~~
alignSelf:auto|flex-start|flex-end|center|stretch
~~~

alignSelf

~~~
alignSelf:auto|flex-start|flex-end|center|stretch
~~~

flex

~~~
flex:number
~~~

## 3 React 中的JSX

jsx允许开发者在JavaScript中书写html语法，每个html标签都转化为JavaScript代码来运行，这样对于使用JavaScript来构建组件以及组件之间关系的应用 。而不在用JavaScript操作dom来创建组件以及组件之间的嵌套关系。

jsx中运行JavaScript表达式需要将表达式用{}括起来。

1. 环境  
JSX 必须借助于ReactJS环境才能运行，在编写JSX代码前需要加载ReactJS文件，还需要加载JSXTransformer

2. 载入方式  
内联方式 外联方式

3. 标签  
JSX标签其实就是HTML标签

4. 转化  
JSX为了让我们更直观的看到组件的DOM，她并不能直接在浏览器端运行，只能通过解析器将其转化为JavaScript代码才能在浏览器上运行，其实就是调用  

~~~
React.createElemnet("h1", null, "hello,ReactJS")
~~~

5. 执行JavaScript表达式  
jsx中运行JavaScript表达式需要将表达式用{}括起来。

6. 注释  
和JavaScript相同，用// 或/*   */

7. 属性  
在HTML中，可以通过标签的属性改变当前元素的样式，在JSX中也可以

8. 延伸属性  
"..." 用于遍历对象，...props 是遍历props对象

9. 自定义属性   
凡是以data-开头的自定义属性，在页面渲染后可以显示在页面上。

10. 显示HTML   
有时候我们需要显示HTML字符串，不是节点  ，使用_html 属性

11. 样式使用   

~~~
<h1 style={{color:'#ff0000',fontSize:'14px'}}> hello ,ReacJS!!! </h1>
~~~

JSX样式通过style属性定义，和传统的web不同，不是字符串，而是JavaScript对象，第一个大括号是JSX语法，第二个大括号是JavaScript对象，需要用驼峰法命名，否则需要加引号，也可以通过className方式引入样式。

12. 事件绑定


1. ReactJS 简介  
ReactJS 和核心思想是组件化，即按照功能封装一个一个组件，各个组件维护自己的状态和UI，当状态发生变化时，会自动重新渲染整个组件，多个组件一起协作共同构成了ReactJS应用。

2. 组件的生命周期  
getDefaultProps 创建阶段  
getInitialState 实例化阶段    
componentWillMount  在render 之前调用   
render 渲染并返回一个虚拟的DOM  
componentDidMount  在render 之后调用   
componentWillRecieveProps 在this.props被修改或者父组件调用setProps方法之后   
shouldComponentUpdate  是否需要更新   
componentWillUpdate  将要更新  
componentDidUpdate  更新完毕   
componentWillUnmount  销毁对象是调用  
主要包括四个阶段 创建阶段、实例化阶段、更新阶段、 销毁阶段  
创建阶段  

即在条用React.createClass的时候这个阶段只会触发getDefaultProps方法，该方法返回了一个对象，并缓存下来，然后与父组件指定的props对象合并，最后赋值给this.props作为组件的默认属性，props是一个对象，是组件用来接收外面传来的参数的。组件内部是不允许修改自己的props属性的。

实例化阶段  

就是组件类被调用的时候，执行顺序是 
geiInitialState,返回值赋给了this.state属性
componentWillMount根据业务逻辑对state进行相应的操作
render 根据state的值，生成页面需要的DOM结构，并返回该结构
componentDidMount

state是组件的属性，他的每次改变都会引发组件的跟新，每次组件的更新都是通过修改state属性的值。ReactJS内部会监听state属性的变化，一旦发生变化，就会主动触发组件的render方法来更新DOM的结构。

虚拟DOM 是将真实的DOM结构映射成一个JSON数据结构。

更新阶段  

componentWillReceiveProps（object nextProps） 当组件接收到新的Props时，会触发改函数，在该函数中，通常会调用this.setState方法完成对state的修改。

shouldComponentUpdate（nextProps， nextState），该方法会拦截新的props 和state

componentWillUpdate（nextProps，nextState） 

render 根据一系列的diff算法，生成需要更新的虚拟DOM数据

componentDidUpdate 常在该方法中做一些DOM操作。

销毁阶段 

自组件调用父组件是通过props实现的。

父组件调用子组件， 子组件被设置为ref之后，父组件就可以通过this.ref.xxx 来获取子组件了，其中xxx为子组件的ref值

虚拟DOM 

当组件的state属性发生变化时，会自动执行组件的render方法来实现组件的更新，虚拟DOM就是将组件的DOM结构映射到这个虚拟DOM对象上，并且实现了一套diff算法，当组件需要更新的时候，会通过Diff算法找到变更的内容，然后将变化修改到实际的DOM节点上，所以组件的更新不是真的渲染整个DOM树，只是更新需要修改的DOM节点上 

~~~
console.log(root)
~~~

## 4 样式 

定义样式

~~~
var styles = StyleSheet.create({
  base: {
    width: 38,
    height: 38,
  },
  background: {
    backgroundColor: '#222222',
  },
  active: {
    borderWidth: 2,
    borderColor: '#00ff00',
  },
});
~~~

使用样式

~~~
<Text style={styles.base} />
<View style={styles.background} />
<View style={[styles.base, styles.background]} />
~~~

将样式作为参数传递

~~~
_handleClick = (e) => {
    // 使用箭头函数(arrow function)
    console.log(this);
}
render() {
    return (
        <div>
            <h1 onClick={this._handleClick}>点击</h1>
        </div>
    );
}
~~~

箭头函数的理解：是一个临时函数，返回一个函数引用

## 5. 图片

~~~
<Image source={require('./my-icon.png')} />
~~~

### 6 原生模块

react native 设计为可以在他的基础上编写原生的代码，并且可以访问平台的所有能力  

在react native 中，一个原生模块 就是实现了RCTBridgeModlue协议的OC类 

~~~
// CalendarManager.h
#import "RCTBridgeModule.h"

@interface CalendarManager : NSObject <RCTBridgeModule>
@end
~~~

为了实现RCTBridgeModule 协议，你需要包含RCT_EXPORT_MODULE宏，这个宏可以添加一个参数用来指定JavaScript中访问这个模块的名字。如果不指定，默认会使用这个OC类的名字  

~~~
// CalendarManager.m
@implementation CalendarManager

RCT_EXPORT_MODULE();

@end
~~~

你必须明确的声明给JavaScript到处的方法，否则，react native 不导出任何方法，通过声明RCT_EXPORT_METHOD()宏来实现

~~~
RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location)
{
  RCTLogInfo(@"Pretending to create an event %@ at %@", name, location);
}
~~~

js中调用这个方法

~~~
var CalendarManager = require('react-native').NativeModules.CalendarManager;
CalendarManager.addEvent('Birthday Party', '4 Privet Drive, Surrey');
~~~

桥接到Javascript的方法返回值类型必须是void。React Native的桥接操作是异步的，所以要返回结果给Javascript，你必须通过回调或者触发事件来进行。

### 6.1 参数类型

RCT_EXPORT_METHOD 支持所有标准JSON类型，包括：

string (NSString)
number (NSInteger, float, double, CGFloat, NSNumber)
boolean (BOOL, NSNumber)
array (NSArray) 包含本列表中任意类型
map (NSDictionary) 包含string类型的键和本列表中任意类型的值
function (RCTResponseSenderBlock)

任何RCTConvert类支持的的类型也都可以使用[参见RCTConvert了解更多信息](https://github.com/facebook/react-native/blob/master/React/Base/RCTConvert.h)。RCTConvert还提供了一系列辅助函数，用来接收一个JSON值并转换到原生Objective-C类型或类

### 6.2 回调函数

原生模块还支持一种特殊的参数，回调函数，她提供了一个函数作为返回值，传给JavaScript。

~~~
RCT_EXPORT_METHOD(findEvents:(RCTResponseSenderBlock)callback)
{
  NSArray *events = ...
  callback(@[[NSNull null], events]);
}
~~~

### 6.3 导出常量

原生模块可以导出一些常量，这些常量在JavaScript端随时都可以访问。用这种方法来传递一些静态数据，可以避免通过bridge进行一次来回交互。

~~~
- (NSDictionary *)constantsToExport
{
  return @{ @"firstDayOfTheWeek": @"Monday" };
}
~~~

Javascript端可以随时同步地访问这个数据：

~~~
console.log(CalendarManager.firstDayOfTheWeek);
~~~

### 6.3 枚举常量

用NS_ENUM定义的枚举类型必须要先扩展对应的RCTConvert方法才可以作为函数参数传递。

~~~
@implementation RCTConvert (StatusBarAnimation)
  RCT_ENUM_CONVERTER(UIStatusBarAnimation, (@{ @"statusBarAnimationNone" : @(UIStatusBarAnimationNone),
                                               @"statusBarAnimationFade" : @(UIStatusBarAnimationFade),
                                               @"statusBarAnimationSlide" : @(UIStatusBarAnimationSlide)},
                      UIStatusBarAnimationNone, integerValue)
@end


- (NSDictionary *)constantsToExport
{
  return @{ @"statusBarAnimationNone" : @(UIStatusBarAnimationNone),
            @"statusBarAnimationFade" : @(UIStatusBarAnimationFade),
            @"statusBarAnimationSlide" : @(UIStatusBarAnimationSlide) }
};

RCT_EXPORT_METHOD(updateStatusBarAnimation:(UIStatusBarAnimation)animation
                                completion:(RCTResponseSenderBlock)callback)
~~~


### 6.4 给Javascript发送事件

即使没有被JavaScript调用，本地模块也可以给JavaScript发送事件通知。最直接的方式是使用eventDispatcher:

~~~
#import "RCTBridge.h"
#import "RCTEventDispatcher.h"

@implementation CalendarManager

@synthesize bridge = _bridge;

- (void)calendarEventReminderReceived:(NSNotification *)notification
{
  NSString *eventName = notification.userInfo[@"name"];
  [self.bridge.eventDispatcher sendAppEventWithName:@"EventReminder"
                                               body:@{@"name": eventName}];
}

@end
~~~

在JavaScript中可以这样订阅事件：

~~~
var { NativeAppEventEmitter } = require('react-native');

var subscription = NativeAppEventEmitter.addListener(
  'EventReminder',
  (reminder) => console.log(reminder.name)
);
...
// 千万不要忘记忘记取消订阅, 通常在componentWillUnmount函数中实现。
subscription.remove();
~~~


### 7 原生UI 组件
























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