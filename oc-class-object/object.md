# 对象

[上一讲](./class.md)我们讲到了类，说类是一个抽象的描述。有抽象就有具体，对象就是类的一个具体的表现。

在网上有很多关于程序员的段子，出现频率最高的是：

> 程序员从来不缺少对象，因为程序里到处都是对象

当然，这种幽默只有程序员，也只有知道面向对象的程序员才懂。

##main.m
创建完工程以后，系统在main.m中做了些事情，我们一一解析下：

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

其中`NSLog`也支持像`printf`一样使用占位符来输出，需要注意的是整型的占位符不再是`%d`而是`%i`。

```objc

NSLog(@"输出一个整型:%i, 浮点型:%f", 10, 10.1);

```

##实例化对象

从类到对象这个转变，我们有一个专业术语，叫做*实例化*。

1. 打开[上一讲的工程](https://github.com/saitjr/Objective-C-Tutorials-Demo/tree/master/1-OC-Class-Object/Class/ClassDemo)；
2. 在main.m文件中引入person类的头`#import "Person.h"`（为什么使用`#import`而不使用`#include`，请见文章[#include、#import和@class区别](http://www.brighttj.com/ios/oc-include-import-class-difference.html)）；
3. 然后实例化Person类，并用临时变量person1去接收，最终代码如下：

```objc

#import <Foundation/Foundation.h>
#import "Person.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...

        // 实例化Person，实例化的对象为person1
        // 首先需要使用alloc方法，开辟一块内存
        // 然后使用init方法对这块内存进行初始化
        Person *person1 = [[Person alloc] init];
    }
    return 0;
}

```

##方法的书写

1. 在OC中有两种方法，一种以`-`开头，一种以`+`开头。`-`开头为实例方法，用对象来进行调用；`+`为类方法（静态方法），用类名调用；
2. 方法使用`空格`来调用；
3. 参数的传递使用`:`来传递；
4. 方法名和参数描述之间一般用`with`来进行连接（这只是编码规范）；
5. 多个参数用`空格`隔开，然后添加第二个参数描述与参数名；
6. 方法名一般采用驼峰命名。

```
方法类型 (返回值类型)方法名With参数描述:(参数类型)参数名 参数描述:(参数类型)参数名;

```

方法的声明：

```objc
- (instancetype)initWithName:(NSString *)name age:(NSInteger)age;

```

方法的实现：

```objc
- (instancetype)initWithName:(NSString *)name age:(NSInteger)age {

}

```

##对象的初始化
刚才初始化Person对象的时候，我们所使用的是`init`方法，但是这个`init`方法是属于`NSObject`的，对于Person来讲，它有姓名、年龄这些独有的成员变量，那么我们想要在初始化它的时候，就给这个对象相应的姓名、年龄应该怎么办呢？

####自定义初始化方法

首先在.h的`@interface`内部声明方法（如果不声明，则外则不可访问）：

```objc
#import <Foundation/Foundation.h>

@interface Person : NSObject {

    NSString *_name;
    NSInteger _age;
    float _height;
}

- (instancetype)initWithName:(NSString *)name age:(NSInteger)age height:(float)height;

@end

```

然后在.m中进行实现：

```objc
#import "Person.h"

@implementation Person

- (instancetype)initWithName:(NSString *)name age:(NSInteger)age height:(float)height {

    self = [super init];

    if (self) {

        // 需要添加的特性
        _name = name;
        _age = age;
        _height = height;
    }

    return self;
}

@end

```

那么这个时候，我们在main.m中的Person初始化方法也需要修改：

```objc
Person *person2 = [[Person alloc] initWithName:@"tangjr" age:10 height:100];

```

##description方法

当使用NSLog打印对象信息的时候，系统会走该对象的description方法。

比如这里，我们想要输出`person2`这个人的信息，就可以通过重写description来实现。
