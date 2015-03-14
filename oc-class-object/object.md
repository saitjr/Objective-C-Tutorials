# 对象

[上一讲](./class.md)我们讲到了类，说类是一个抽象的描述。有抽象就有具体，对象就是类的一个具体的表现。

在网上有很多关于程序员的段子，出现频率最高的是：

> 程序员从来不缺少对象，因为程序里到处都是对象

当然，这种幽默只有程序员，也只有知道面向对象的程序员才懂。 

##实例化对象

从类到对象这个转变，我们有一个专业术语，叫做*实例化*。

1. 打开[上一讲的工程](https://github.com/saitjr/Objective-C-Tutorials-Demo/tree/master/1-OC-Class-Object/Class/ClassDemo)；
2. 在main.m文件中引入person类的头`#import "Person.h"`；
3. 然后实例化Person类，并用临时变量person1去接收`Person *person1 = [[Person alloc] init];`

在实例化这一步中，`alloc`表示开辟一块内存，`init`表示初始化这一块内存，然后将初始化完的这块内存的指针，交给指针`*person1`。`person1`就是Person类的一个对象。

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

```
- (instancetype)initWithName:(NSString *)name age:(NSInteger)age;

```

方法的实现：

```
- (instancetype)initWithName:(NSString *)name age:(NSInteger)age {
    
}

```


##对象的初始化
刚才初始化Person对象的时候，我们所使用的是`init`方法，但是这个`init`方法是属于`NSObject`的，对于Person来讲，它有姓名、年龄这些独有的成员变量，那么我们想要在初始化它的时候，就给这个对象相应的姓名、年龄应该怎么办呢？

对于这个需求，有两种解决方案：

1. 重写`init`方法；
2. 自定义初始化方法；

####重写`init`方法：

重写方法有一个几乎固定的格式，打开.m文件：

```
- (instancetype)init {
    
    self = [super init]; // 通过父类的init方法，去初始化一个对象
    
    if (self) {
        
        // 需要添加的特性
        _name = @"tangjr"; // @""表示字符串对象
        _age = 10;
        _height = 160.2;
    }
    
    return self;
}

```

####自定义初始化方法

重写`init`方法的弊端是：每一个对象的信息都一样。这明显不是我们想要的，所以，对于每个对象都不同的信息，我们给出一个能自定义信息的初始化方法。

首先在.h的`@interface`内部声明方法（如果不声明，则外则不可访问）：

```
- (instancetype)initWithName:(NSString *)name age:(NSInteger)age height:(float)height;

```

然后在.m中进行实现：

```
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

```

那么这个时候，我们在main.m中的Person初始化方法也需要修改：

```
Person *person2 = [[Person alloc] initWithName:@"tangjr" age:10 height:100];

```