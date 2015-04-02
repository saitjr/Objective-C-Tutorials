# 类

##概念

> 对一类物体的抽象描述

可以看出*类* 是一个抽象的存在，如：人、动物、电脑。他们都只是一个名称而已，没有具体的指向某个物体。

##在Xcode中创建OC工程

1.打开Xcode，选择Create a new Xcode project

<image src="./images/class-1.png" width="400px" />

2.选择创建一个OS X的Application -> Commad Line Tool工程

<image src="./images/class-2.png" width="400px" />

3.填写相关工程信息

<image src="./images/class-3.png" width="400px" />

4.选择项目保存路径，然后创建

##main.m

以前创建的C语言程序都是已.c与.h结尾的，但是OC是.m与.h结尾。创建完工程以后，系统在main.m中做了些事情，我们一一解释下：

```objc
#import <Foundation/Foundation.h>           // 引入头文件

int main(int argc, const char * argv[]) {   // main函数
    @autoreleasepool {                      // 自动释放池，将在内存管理章节中讲到
        // insert code here...
        NSLog(@"Hello, World!");            // NSLog输出，字符串使用@""
    }
    return 0;                               // 返回值
}
```

其中`NSLog`也支持像`printf`一样使用占位符来输出，在NSLog进行输出的时候，整型占位符除了`%d`还可以是`%i`。

```objc
NSLog(@"输出一个整型:%i, 浮点型:%f", 10, 10.1);

```

### #import
OC中有三种引入文件的方式，分别是：`#import`，`#include`，`@class`，关于他们之间的区别，详见：
[#include、#import和@class区别](http://www.brighttj.com/ios/oc-include-import-class-difference.html)。

##在Xcode中创建类

1.选中工程目录中的main.m，然后快捷键Command+N（表示在main.m的下面创建一个新文件）；

2.选择OS X -> Source的Cocoa Class

<image src="./images/class-4.png" width="400px" />

3.填写类名，并将NSObject作为父类<font color=red>（注意：类名首字母大写，并采用驼峰命名）</font>

<image src="./images/class-5.png" width="400px" />

4.保存路径不用修改，直接创建

5.创建之后的工程目录为：

<image src="./images/class-6.png" width="400px" />

##类文件的分析

类文件分为两个.h文件与.m文件

.h为类的声明文件，`@interface`表示类的接口，`:`表示继承关系。
> `@interface Person : NSObject`的含义为：声明了一个继承自NSObject类的Person类

.m为类的实现文件，`@implementation`表示类的实现。
> `@implementation Person`的含义为：Person类的实现

两个关键字都必须和`@end`成对出现，表示声明/实现的结束。

```objc
#import <Foundation/Foundation.h>

@interface Person : NSObject

// 内容写在@interface与@end之间

@end

```

```objc
#import "Person.h"

@implementation Person

// 内容写在@implementation与@end之间

@end

```

##类的简介
关于类的简介，有几个概念不得不提：

1. OC只支持单继承（子类只能拥有一个父类）；
2. NSObject<font color=red>几乎</font>是所有类的基类（归根结底的那个类）；
3. 子类能继承父类的<font color=red>公开</font>方法与属性；

##成员变量的定义
之前讲到了结构体中变量的定义，类中成员变量的定义如下（<font color=red>注意：是在.h文件中定义</font>）：

```objc
@interface Person : NSObject {

    NSString *_name; // NSString是OC中的字符串
    NSInteger _age;  // NSInteger是OC中的整型，64位下是long，其他情况下是int
    float _height;
}

@end
```

在写代码的时候，应该时刻注意编码规范。在Cocoa编码规范中，成员变量在定义时，名称前需要加上`_`下划线。

在上面这个例子中，因为`NSString`是OC中的类，name为对象，所以需要写成`*_name`，而`NSInteger`其实是`typedef long NSInteger;`基本类型，所以写为`_age`。
