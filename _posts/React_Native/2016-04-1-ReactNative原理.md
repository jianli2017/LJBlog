---
layout: post
title:  native原理
category: 技术
comments: true
---


# 一、 简介

React Native 的详细内容可以参考[中文官方文档](http://reactnative.cn)。 React Native 简介可以参考 [《把现代web科技带给移动开发者》](http://bbs.reactnative.cn/topic/14/react-native-把现代web科技带给移动开发者)、 [《唐巧：谈谈React Native》](http://www.csdn.net/article/1970-01-01/2823790) 、[《一个资深iOS开发者对于React Native的看法》](http://www.linuxidc.com/Linux/2015-09/123239.htm) 、[《如何评价 React Native？》](http://www.zhihu.com/question/27852694),下面是自己参考《把现代web科技带给移动开发者》自己的一点总结：

### 1.1 开发原生的APP 比较困难

开发成本高，耗时，每次发版受apple的限制。

### 1.2 开发原生开发非常必要 

1. 原生APP 的用户体验比web、Hybird APP 的用户体验好 
2. 在web上，我们也没有一个足够完善的线程模型，很难利用多线程并行执行工作

### 1.3 将两个世界合二为一？

 用脚本封装原生，即用JavaScript去调用原生API，优点：

1. 能获得原生平台的所有强大之处
2. 同时还能享受快速迭代和使用我们现有JavaScript上基础设施的好处
3. 因为基于JavaScript构建，我们应当能使得这样技术栈跨平台。

### 1.4 用脚本封装原生是一件需要技巧的事情

1. 同步执行JS阻塞UI。  
如果我们只是同步的在原生环境和解释环境之间调用，我们的UI线程很可能会被JavaScript执行阻塞住。
2. 异步执行JS会资源竞争、加锁开销大。  
 要提升界面的响应效率，我们知道我们必须把JavaScript放到主线程之外执行，但这么做其实很困难。最直接的困难就是资源访问竞争。如果我们的JavaScript访问什么正好在被别的线程用的东西（譬如一个渲染的View的尺寸），系统就只能加锁来确保方案安全，而这又会导致UI线程的卡顿。还有一个问题在于每次原生和JavaScript虚拟机之间互相访问，在访问过程中都会带来极大的开销。如果我们要经常跨线程访问，我们不得不一次又一次的经历这种开销。

### 1.5 引入React Native

react native 来源于React，React组件本来就被设计为一个纯粹的、无副作用的函数，函数返回每一个时刻当时的View状态，这样我们无需读取底层View的状态就可以为它写入新的状态。能解决上面提出的问题。

1. React Native使你能够在Javascript和React的基础上获得完全一致的开发体验，构建世界一流的原生APP。

2. React Native着力于提高多平台开发的开发效率 —— 仅需学习一次，编写任何平台。(Learn once, write anywhere)
3. 写界面的时候，不需要重新编译，直接刷新界面就可以了，这点感觉会大幅提高开发效率。


### 1.6 使用React Native 需要了解的知识

1. 前端开发工程师必须掌握的三个技能：

* 描述网页内容的HTML     

* 描述网页样式的CSS ，[html 和css 的学习地址](http://www.imooc.com/learn/9)

* 描述网页行为的JavaScript, [java 学习地址](http://www.w3school.com.cn/js/)

2. JavaScript的语法规范 [ES5和ES6写法对照表](http://bbs.reactnative.cn/topic/15/react-react-native-的es5-es6写法对照表)

3.  ReactNative在CSS基础上使用的布局模型：[伸缩盒子模型flexBox](http://jianli2017.github.io/LJBlog/技术/2016/02/10/ReactNavie-flexBox模型.html)

4.JSX ，这个一直没有找到好点的资料，可以参考[JSX在React-Native中的应用](http://www.tuicool.com/articles/byiay2N) 、或者[深入浅出React系列文章](http://www.infoq.com/cn/react1/)


# 二、搭建开发环境

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


# 三、 植入原生的应用


可以通过cocoaPod安装 React Native，只需要在Podfile中添加一下内容即可

~~~
# 取决于你的工程如何组织，你的node_modules文件夹可能会在别的地方。
# 请将:path后面的内容修改为正确的路径。
pod 'React', :path => './node_modules/react-native', :subspecs => [
  'Core',
  'RCTImage',
  'RCTNetwork',
  'RCTText',
  'RCTWebSocket',
  # 添加其他你想在工程中使用的依赖。
]
~~~

# 四、 react Native 通信原理

React Native 的通信原理可以参照[使用 JS 构建跨平台的原生应用：React Native iOS 通信机制初探](http://www.open-open.com/lib/view/open1451460443901.html),这篇文章的作者应该是做前端的，分析了部分JS通信过程中的JS部分。下面我是分析的Native部分（IOS部分）。

## 4.1 初始化的原理

React Native 的基本原理是使用js脚本封装原生的模块，可以访问原生平台的所用特性。具体封装原生模块的原理如下：

![初始化原理]({{site.url}}/images/react Native 原理/Native 初始化.png)

## 4.2 原生模块的约定

原生模块需要RCTBridgeModule协议，或者说遵循了RCTBridgeModule协议的模块称为原生模块，遵循RCTBridgeModule协议只需要在类中包含RCT_EXPORT_MODULE()宏。

~~~
@implementation CalendarManager

RCT_EXPORT_MODULE();

@end
~~~

RCT_EXPORT_MODULE的作用是将原生模块导入到配置文件中，使JS 可以调用到，这个红的原理如下

~~~
#define RCT_EXPORT_MODULE(js_name) \
RCT_EXTERN void RCTRegisterModule(Class); \
+ (NSString *)moduleName { return @#js_name; } \
+ (void)load { RCTRegisterModule(self); }
~~~

下面是RCTRegisterModule的实现

~~~
static NSMutableArray<Class> *RCTModuleClasses;
void RCTRegisterModule(Class moduleClass)
{
  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    RCTModuleClasses = [NSMutableArray new];
  });

  RCTAssert([moduleClass conformsToProtocol:@protocol(RCTBridgeModule)],
            @"%@ does not conform to the RCTBridgeModule protocol",
            moduleClass);

  // Register module
  [RCTModuleClasses addObject:moduleClass];

  objc_setAssociatedObject(moduleClass, &RCTBridgeModuleClassIsRegistered,
                           @NO, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
}
~~~

即在load的时候将原生模块添加到RCTModuleClasses数组中，jsBridge初始话的时候，读取RCTModuleClasses内容，自动构造配置文件，设置到JS执行器中。

#### 4.2.1导出方法

导出方法 指的是导出方法给JavaScript调用，否则React Native不会导出任何方法。通过RCT_EXPORT_METHOD()宏来实现：

~~~
RCT_EXPORT_METHOD(addEvent:(NSString *)name location:(NSString *)location)
{
  RCTLogInfo(@"Pretending to create an event %@ at %@", name, location);
}
~~~

在JavaScript中条用这个方法：

~~~
var CalendarManager = require('react-native').NativeModules.CalendarManager;
CalendarManager.addEvent('Birthday Party', '4 Privet Drive, Surrey');
~~~

导出方法原理如下：

~~~
#define RCT_EXPORT_METHOD(method) \
  RCT_REMAP_METHOD(, method)
  
  #define RCT_REMAP_METHOD(js_name, method) \
  RCT_EXTERN_REMAP_METHOD(js_name, method) \
  - (void)method

  #define RCT_EXTERN_REMAP_METHOD(js_name, method) \
  + (NSArray<NSString *> *)RCT_CONCAT(__rct_export__, \
    RCT_CONCAT(js_name, RCT_CONCAT(__LINE__, __COUNTER__))) { \
    return @[@#js_name, @#method]; \
  }
  
  #define RCT_CONCAT2(A, B) A ## B
#define RCT_CONCAT(A, B) RCT_CONCAT2(A, B)

~~~

其实相当于声明了两个方法，一个类方法，供自动生成配置文件使用，一个是实例方法，即导出的方法

~~~
+(NSArray<NSString *> *) __rct_export__ js_name __LINE__ __COUNTER__
{
     return @[@#js_name, @#method];
}
-(void)addEvent:(NSString *)name location:(NSString *)location;
~~~

#### 4.2.2导出常量

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

#### 4.2.3导出枚举

用NS_ENUM定义的枚举类型必须要先扩展对应的RCTConvert方法才可以作为函数参数传递。

~~~
typedef NS_ENUM(NSInteger, UIStatusBarAnimation) {
    UIStatusBarAnimationNone,
    UIStatusBarAnimationFade,
    UIStatusBarAnimationSlide,
};
~~~

你需要这样来扩展RCTConvert类：

~~~
@implementation RCTConvert (StatusBarAnimation)
  RCT_ENUM_CONVERTER(UIStatusBarAnimation, (@{ @"statusBarAnimationNone" : @(UIStatusBarAnimationNone),
                                               @"statusBarAnimationFade" : @(UIStatusBarAnimationFade),
                                               @"statusBarAnimationSlide" : @(UIStatusBarAnimationSlide)},
                      UIStatusBarAnimationNone, integerValue)
@end
~~~

接着你可以这样定义方法并且导出enum值作为常量：

~~~
- (NSDictionary *)constantsToExport
{
  return @{ @"statusBarAnimationNone" : @(UIStatusBarAnimationNone),
            @"statusBarAnimationFade" : @(UIStatusBarAnimationFade),
            @"statusBarAnimationSlide" : @(UIStatusBarAnimationSlide) }
};

RCT_EXPORT_METHOD(updateStatusBarAnimation:(UIStatusBarAnimation)animation
                                completion:(RCTResponseSenderBlock)callback)
~~~

js 调用原生方法的时候，可以使用这些常量的原理是，初始化的时候将这些常量添加到配置信息中，然后设置到JS执行器中，执行JS的时候，JS通过配置信息，取到key value的JSON，通过TCTConvert转化为本地的值。

#### 4.2.4 多线程

React Native在一个独立的串行GCD队列中调用原生模块的方法，通过实现方法- (dispatch_queue_t)methodQueue，原生模块可以指定自己想在哪个队列中被执行。具体来说，如果模块需要调用一些必须在主线程才能使用的API，那应当这样指定：

~~~
- (dispatch_queue_t)methodQueue
{
  return dispatch_get_main_queue();
}
~~~

类似的，如果一个操作需要花费很长时间，原生模块不应该阻塞住，而是应当声明一个用于执行操作的独立队列。举个例子，RCTAsyncLocalStorage模块创建了自己的一个queue，这样它在做一些较慢的磁盘操作的时候就不会阻塞住React本身的消息队列：

~~~
- (dispatch_queue_t)methodQueue
{
  return dispatch_queue_create("com.facebook.React.AsyncLocalStorageQueue", DISPATCH_QUEUE_SERIAL);
}
~~~

指定的methodQueue会被你模块里的所有方法共享。如果你的方法中“只有一个”是耗时较长的（或者是由于某种原因必须在不同的队列中运行的），你可以在函数体内用dispatch_async方法来在另一个队列执行，而不影响其他方法：

~~~
RCT_EXPORT_METHOD(doSomethingExpensive:(NSString *)param callback:(RCTResponseSenderBlock)callback)
{
  dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
    // 在这里执行长时间的操作
    ...
    // 你可以在任何线程/队列中执行回调函数
    callback(@[...]);
  });
}
~~~

## 4.3 管理原生模块类 RCTModuleData

RCTModuleData 管理原生模块的类，RCTBridge持有该类的实例 。RCTBridge初始化该类的时候，会将所有的原生模块都初始化为一个RCTModuleData的实例，每个实例包括原生模块的导出方法、导出常量、配置信息、原生模块的实例，最后将所有的RCTModuleData 实例保存到RCTBridge的下面三个成员变量中。JS调用原生方法的时候，就会从这三个实例中查找对应的模块、方法，然后invoke 方法。

~~~
NSMutableDictionary<NSString *, RCTModuleData *> *_moduleDataByName;
NSArray<RCTModuleData *> *_moduleDataByID;
NSArray<Class> *_moduleClassesByID;
~~~

#### 4.3.1 方法列表 

方法列表method 返回原生模块的所有导出方法

~~~
- (NSArray<id<RCTBridgeMethod>> *)methods
{
    ///获取类的 类方法
    unsigned int methodCount;
    Method *methods = class_copyMethodList(object_getClass(_moduleClass), &methodCount);

    ///如果有 方法名中包含__rct_export__ ，则保存 导出方法
    for (unsigned int i = 0; i < methodCount; i++) {
      Method method = methods[i];
      SEL selector = method_getName(method);
      if ([NSStringFromSelector(selector) hasPrefix:@"__rct_export__"]) {
        IMP imp = method_getImplementation(method);
        NSArray<NSString *> *entries =
          ((NSArray<NSString *> *(*)(id, SEL))imp)(_moduleClass, selector);
        id<RCTBridgeMethod> moduleMethod =
          [[RCTModuleMethod alloc] initWithMethodSignature:entries[1]
                                              JSMethodName:entries[0]
                                               moduleClass:_moduleClass];

        [moduleMethods addObject:moduleMethod];
      }
    }
    free(methods);
    _methods = [moduleMethods copy];
  return _methods;
}
~~~

#### 4.3.2 常量列表

常量列表是调用原生模块的 constantsToExport 方法获取常量列表

~~~
- (void)gatherConstants
{
  if (_hasConstantsToExport && !_constantsToExport) {
    (void)[self instance];
    RCTExecuteOnMainThread(^{
      _constantsToExport = [_instance constantsToExport] ?: @{};
    }, YES);
  }
}
~~~

#### 4.3.3 原生模块的实例

包括实例化原生模块和 获取原生模块的实例

~~~
- (id<RCTBridgeModule>)instance
{
  [self setUpInstanceAndBridge];
  return _instance;
}

- (void)setUpInstanceAndBridge
{
	/// 实例化原生模块
	_instance = [_moduleClass new];
	
	///设置原生模块的桥
	[self setBridgeForInstance];
}
~~~

#### 4.3.4 原生模块的配置信息

原生模块的配置信息包括 导出方法和导出常量

~~~
- (NSArray *)config
{
	/// 收集常量
  [self gatherConstants];
  
  ///收集方法
  NSMutableArray<NSString *> *methods = self.methods.count ? [NSMutableArray new] : nil;
  NSMutableArray<NSNumber *> *asyncMethods = nil;
  for (id<RCTBridgeMethod> method in self.methods) 
  {
    [methods addObject:method.JSMethodName];
  }

   ///组装配置信息
  NSMutableArray *config = [NSMutableArray new];
  [config addObject:self.name];
  if (constants.count) {
    [config addObject:constants];
  }
  if (methods) {
    [config addObject:methods];
    if (asyncMethods) {
      [config addObject:asyncMethods];
    }
  }
  return config;
}
~~~

## 4.4 初始化桥 （RCTBride）

初始化桥 主要完成初始化原生模块、 原生模块的配置信息、 设置JS执行器，并初始化（RCTJSCExecutor） ，最后将配置信息设置到 JS执行器中。

### 4.4.1 如果引入React Native ,需要先使用你的index.ios.bundle的URI来初始化RCTRootView

~~~
    jsCodeLocation = [NSURL URLWithString:@"http://localhost:8081/index.ios.bundle?platform=ios&dev=true"];
    //   jsCodeLocation = [[NSBundle mainBundle] URLForResource:@"main" withExtension:@"jsbundle"];
    
    RCTRootView *rootView = [[RCTRootView alloc] initWithBundleURL:jsCodeLocation
                                                        moduleName:@"PanApp"
                                                 initialProperties:nil
                                                     launchOptions:nil];
~~~

### 4.4.2 RCTRootView 的初始化会触发 RCTBridge 的初始化 

~~~
- (instancetype)initWithBundleURL:(NSURL *)bundleURL
                       moduleName:(NSString *)moduleName
                initialProperties:(NSDictionary *)initialProperties
                    launchOptions:(NSDictionary *)launchOptions
{
  RCTBridge *bridge = [[RCTBridge alloc] initWithBundleURL:bundleURL
                                            moduleProvider:nil
                                             launchOptions:launchOptions];

  return [self initWithBridge:bridge moduleName:moduleName initialProperties:initialProperties];
}
~~~

### 4.4.3 RCTBridge的初始化会 触发实际干活的batchedBridge 的初始化 

~~~
- (instancetype)initWithBundleURL:(NSURL *)bundleURL
                   moduleProvider:(RCTBridgeModuleProviderBlock)block
                    launchOptions:(NSDictionary *)launchOptions
{
  if ((self = [super init])) {
    RCTPerformanceLoggerStart(RCTPLTTI);

    _bundleURL = bundleURL;
    _moduleProvider = block;
    _launchOptions = [launchOptions copy];
    [self setUp];
  }
  return self;
}

- (void)setUp
{
	...
  // Sanitize the bundle URL
  _bundleURL = [RCTConvert NSURL:_bundleURL.absoluteString];

  [self createBatchedBridge];
}

- (void)createBatchedBridge
{
  self.batchedBridge = [[RCTBatchedBridge alloc] initWithParentBridge:self];
}
~~~

### 4.4.4 batchedBridge的初始化 

batchedBridge 的初始化，会初始化原生模块、 原生模块的配置信息、 设置JS执行器，并初始化（RCTJSCExecutor） ，最后将配置信息设置到 JS执行器中。

~~~
- (void)start
{
  ...
  ///1 . 加载JS 代码 
  __weak RCTBatchedBridge *weakSelf = self;
  __block NSData *sourceCode;
  [self loadSource:^(NSError *error, NSData *source) {
    }
    sourceCode = source;
  }];

  ///2   初始化本地模块，本地模块指的是遵循了桥协议的模块  RCTBridgeModule  
  [self initModulesWithDispatchGroup:initModulesAndLoadSource];

 
  /// 3 js 执行器相关的
  NSString *config;
  [weakSelf setUpExecutor];
  
  config = [weakSelf moduleConfig];
  RCTPerformanceLoggerEnd(RCTPLNativeModulePrepareConfig);
  
  [weakSelf injectJSONConfiguration:config onComplete:^(NSError *error) {
        RCTPerformanceLoggerEnd(RCTPLNativeModuleInjectConfig);
        if (error) {
          
        }
  /// 4 执行JS代码 
  [strongSelf executeSourceCode:sourceCode];
}
~~~

初始化原生模块，主要的工作就是初始化所有的原生模块 ，保存到_moduleDataByID、_moduleDataByName、_moduleClassesByID中

~~~
- (void)initModulesWithDispatchGroup:(dispatch_group_t)dispatchGroup
{
  NSMutableArray<Class> *moduleClassesByID = [NSMutableArray new];
  NSMutableArray<RCTModuleData *> *moduleDataByID = [NSMutableArray new];
  NSMutableDictionary<NSString *, RCTModuleData *> *moduleDataByName = [NSMutableDictionary new];
  /// 1 安装自动导出的模块
  for (Class moduleClass in RCTGetModuleClasses()) {
    NSString *moduleName = RCTBridgeModuleNameForClass(moduleClass);
    moduleData = [[RCTModuleData alloc] initWithModuleClass:moduleClass
                                                     bridge:self];
    moduleDataByName[moduleName] = moduleData;
    [moduleClassesByID addObject:moduleClass];
    [moduleDataByID addObject:moduleData];
  }

  ///2. 存储
  _moduleDataByID = [moduleDataByID copy];
  _moduleDataByName = [moduleDataByName copy];
  _moduleClassesByID = [moduleClassesByID copy];

  //3. 在实例初始化前 设置js 执行器
  _javaScriptExecutor = [self moduleForClass:self.executorClass];

  ///4. 实例化本地模块，并设置 实例的桥 （bridge）
  for (RCTModuleData *moduleData in _moduleDataByID) {

      (void)[moduleData instance];
      [moduleData gatherConstants];
  }
}
~~~

获取原生模块的配置信息

~~~
- (NSString *)moduleConfig
{
  NSMutableArray<NSArray *> *config = [NSMutableArray new];
  for (RCTModuleData *moduleData in _moduleDataByID) {
    if (self.executorClass == [RCTJSCExecutor class]) {
      [config addObject:@[moduleData.name]];
    } else {
      [config addObject:RCTNullIfNil(moduleData.config)];
    }
  }

  return RCTJSONStringify(@{
    @"remoteModuleConfig": config,
  }, NULL);
}
~~~


将配置文件注入到JS执行器中

~~~
- (void)injectJSONConfiguration:(NSString *)configJSON
                     onComplete:(void (^)(NSError *))onComplete
{
  if (!_valid) {
    return;
  }

  [_javaScriptExecutor injectJSONText:configJSON
                  asGlobalObjectNamed:@"__fbBatchedBridgeConfig"
                             callback:onComplete];
}
~~~

### 4.4.5 JS 调用原生方法 

![JS调用 原生方法]({{site.url}}/images/react Native 原理/JS 调用Native.png)

JS调用RCTBridge的enqueueJSCall方法，传入代码和参数，例如JSTimersExecution.callTimers

~~~
- (void)enqueueJSCall:(NSString *)moduleDotMethod args:(NSArray *)args
{
  [self.batchedBridge enqueueJSCall:moduleDotMethod args:args];
}
~~~

上面触发了实际干活的桥（batchedBridge） 的enqueueJSCall方法，该方法 在JS执行线程执行JS代码。

~~~
- (void)enqueueJSCall:(NSString *)moduleDotMethod args:(NSArray *)args
{
  NSArray<NSString *> *ids = [moduleDotMethod componentsSeparatedByString:@"."];

  NSString *module = ids[0];
  NSString *method = ids[1];

  RCTProfileBeginFlowEvent();
  __weak RCTBatchedBridge *weakSelf = self;
  [_javaScriptExecutor executeBlockOnJavaScriptQueue:^{

  [strongSelf _actuallyInvokeAndProcessModule:module method:method arguments:args ?: @[]];
  }];
}
~~~

 JS执行器执行JS代码，js执行器会根据配置文件返回模块ID，方法ID。格式是json格式，JS执行成功会回调handleBuffer方法

~~~
- (void)_actuallyInvokeAndProcessModule:(NSString *)module
                                 method:(NSString *)method
                              arguments:(NSArray *)args
{
  RCTJavaScriptCallback processResponse = ^(id json, NSError *error) {
///根据返回的json，执行本地方法
    [self handleBuffer:json batchEnded:YES];
  };

/// 执行js 代码，有JavaScript core 执行，返回json类型的 原生模块ID、方法ID
  [_javaScriptExecutor callFunctionOnModule:module
                                     method:method
                                  arguments:args
                                   callback:processResponse];
}

- (void)handleBuffer:(id)buffer batchEnded:(BOOL)batchEnded
{
  [self handleBuffer:buffer];
}
~~~

根据模块ID、方法ID、参数执行 原生方法。

~~~
- (void)handleBuffer:(NSArray *)buffer
{

///JS类型转native类型
 NSArray *requestsArray = [RCTConvert NSArray:buffer];
/// 原生模块类名
  NSArray<NSNumber *> *moduleIDs = [RCTConvert NSNumberArray:requestsArray[RCTBridgeFieldRequestModuleIDs]];
///方法名
  NSArray<NSNumber *> *methodIDs = [RCTConvert NSNumberArray:requestsArray[RCTBridgeFieldMethodIDs]];
///参数
  NSArray<NSArray *> *paramsArrays = [RCTConvert NSArrayArray:requestsArray[RCTBridgeFieldParams]];

[self _handleRequestNumber:index
                            moduleID:[moduleIDs[index] integerValue]
                            methodID:[methodIDs[index] integerValue]
                              params:paramsArrays[index]];
}

- (BOOL)_handleRequestNumber:(NSUInteger)i
                    moduleID:(NSUInteger)moduleID
                    methodID:(NSUInteger)methodID
                      params:(NSArray *)params
{
	/// 根据模块ID、 方法ID 获取原生模块的的模块名、方法名
  RCTModuleData *moduleData = _moduleDataByID[moduleID];
  id<RCTBridgeMethod> method = moduleData.methods[methodID];

 ///分发消息
  @try {
    [method invokeWithBridge:self module:moduleData.instance arguments:params];
  }
  return YES;
}
~~~

分发消息 ，分发消息使用了[invocation] (http://blog.csdn.net/yhawaii/article/details/8306637)

~~~
- (void)invokeWithBridge:(RCTBridge *)bridge
                  module:(id)module
               arguments:(NSArray *)arguments
{
  ///处理方法签名
  [self processMethodSignature];

  /// 消息分发
  [_invocation invokeWithTarget:module];

  /// 
  [_invocation getArgument:&value atIndex:index];
~~~

# 五、 ReactJS 组件的生命周期 

React Native 继承于（来源于ReactJS），所以ReactJS 的核心思想，在React Native中也体现出来了。React 主要的有点有两个：

1. 组件化
2. 虚拟DOM

ReactJS 和核心思想是组件化，即按照功能封装一个一个组件，各个组件维护自己的状态和UI，当状态发生变化时，会自动重新渲染整个组件，多个组件一起协作共同构成了ReactJS应用。

## 5.1  组件的生命周期 
 
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

### 5.1.1  创建阶段  

即在条用React.createClass的时候这个阶段只会触发getDefaultProps方法，该方法返回了一个对象，并缓存下来，然后与父组件指定的props对象合并，最后赋值给this.props作为组件的默认属性，props是一个对象，是组件用来接收外面传来的参数的。组件内部是不允许修改自己的props属性的。

## 5.1.2  实例化阶段  

就是组件类被调用的时候，执行顺序是 
geiInitialState,返回值赋给了this.state属性
componentWillMount根据业务逻辑对state进行相应的操作
render 根据state的值，生成页面需要的DOM结构，并返回该结构
componentDidMount

state是组件的属性，他的每次改变都会引发组件的跟新，每次组件的更新都是通过修改state属性的值。ReactJS内部会监听state属性的变化，一旦发生变化，就会主动触发组件的render方法来更新DOM的结构。

虚拟DOM 是将真实的DOM结构映射成一个JSON数据结构。

### 5.1.2  更新阶段  

componentWillReceiveProps（object nextProps） 当组件接收到新的Props时，会触发改函数，在该函数中，通常会调用this.setState方法完成对state的修改。

shouldComponentUpdate（nextProps， nextState），该方法会拦截新的props 和state

componentWillUpdate（nextProps，nextState） 

render 根据一系列的diff算法，生成需要更新的虚拟DOM数据

componentDidUpdate 常在该方法中做一些DOM操作。

### 5.1.3  销毁阶段 

自组件调用父组件是通过props实现的。

父组件调用子组件， 子组件被设置为ref之后，父组件就可以通过this.ref.xxx 来获取子组件了，其中xxx为子组件的ref值

### 5.2 虚拟DOM 

当组件的state属性发生变化时，会自动执行组件的render方法来实现组件的更新，虚拟DOM就是将组件的DOM结构映射到这个虚拟DOM对象上，并且实现了一套diff算法，当组件需要更新的时候，会通过Diff算法找到变更的内容，然后将变化修改到实际的DOM节点上，所以组件的更新不是真的渲染整个DOM树，只是更新需要修改的DOM节点上 


# 六. 微店的例子

具体的看代码
