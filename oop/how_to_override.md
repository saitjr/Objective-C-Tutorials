# 方法的重写

在对象初始化的时候，我们提到一个疑问：

> 初始化`Person`对象的时候，我们所使用的是`init`方法，但是这样`init`出来的对象没有自身独有的元素。比如，我们的`Person`类中，还有姓名、年龄等成员变量根本体现不出来。如果想要对某个人的姓名、年龄赋值，怎么办呢？

当时给出的解决方案是：[自定义一个新的init方法，将姓名与年龄当成参数传进去](./how_to_use.md)。

这一节，将提到另一种解决方案：重写init方法。

##重写init方法

讲到方法的时候，我们就说过，方法是某个对象或者某个类的行为。要有，才能进行调用。我们的`Person`类并没有定义过`alloc`与`init`方法，那为什么可以调用呢？

其实，是因为这两个方法都是`NSObject`的，即系统给我们的。因为`Person`类继承自`NSObject`，所以它也有了这两个方法。（关于继承，将在下一讲中讲到）。

系统提供了`init`方法，那可以不可以改呢？答案是可以的。但是呢不在`NSObject`里面改，哪个类觉得不够用，哪个类来改。比如，我们这里的`Person`类觉得，`init`方法不能初始化姓名、年龄这两个成员，那就由`Person`类来改。那么这个在子类中修改父类的方法，我们称之为<font color=red>*重写*</font>。

1. <font color=red>重写方法，不需要再在.h文件中进行声明，直接在.m文件中实现即可；</font>
2. <font color=red>既然是重写，父类必须要有这个方法，而且必须公开（即方法在父类的.h中声明过）；</font>
3. <font color=red>重写时，只能修改方法的实现。方法类型、返回值、方法名、参数全都不能修改。</font>

```objc
- (instancetype)init {
    
    self = [super init];
    
    if (self) {
        
        _name = @"Karen";
        _age = 1;
        _height = 0.5;
    }
    return self;
}

```

这时，我们再调用`init`方法，就不仅仅是走`NSObject`的方法了，还会走重写过后的`init`方法。所以，输出`_age`与`_height`的值就是1与0.5。

```objc
Person *person1 = [[Person alloc] init];

```
##重写description方法

之前讲解到，要打印对象，`NSLog`中需要使用`%@`。既然如此，`person1`也是对象，也可以使用`%@`输出。

```objc
NSLog(@"%@", person1);

```
控制台打印了对象的地址：

```
2015-04-02 22:48:42.890 test2[422:10156] <Person: 0x10020da60>

```
现在我想要`NSLog`对象的时候，控制台输出这个人的名字，就需要重写description方法，实现如下：

```objc
- (NSString *)description {
    
    // 注意：_name这里的参数，一定不能换成self，会造成循环调用
    return [NSString stringWithFormat:@"姓名：%@", _name];
}

```

这时再输出，控制台打印：

```
2015-04-02 22:54:15.527 test2[473:12684] 姓名：Karen

```