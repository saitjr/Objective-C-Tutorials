# 方法的使用与调用

##方法的调用

在初始化Person对象的时候，我们使用到了以下代码：

```objc
Person *person1 = [Person alloc];
person1 = [person1 init];

```

按住command键，点击`alloc`可以进入到NSObject的头文件中，找到`alloc`与`init`方法的声明：

```objc
+ (instancetype)alloc; 	// 开辟内存
- (instancetype)init;	  	// 初始内存

```

1. 方法使用`空格`来调用；
2. `+`方式使用类名进行调用，如这里的`[Person alloc]`；
3. `-`方式使用对象进行调用，如这里的`[person1 init]`。

##对象的初始化

刚才初始化`Person`对象的时候，我们所使用的是`init`方法，但是这样`init`出来的对象没有自身独有的元素。比如，我们的`Person`类中，还有姓名、年龄等成员变量根本体现不出来。如果想要对某个人的姓名、年龄赋值，怎么办呢？

####自定义初始化方法

首先在.h的`@interface`内部声明方法（如果不声明，则外则不可访问）：

```objc
#import <Foundation/Foundation.h>

@interface Person : NSObject {

    NSString *_name;
    NSInteger _age;
    float _height;
}

// 注意这里的编码规范，先定义成员变量，然后换行再声明方法
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

