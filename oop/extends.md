# 继承

> 继承是面向对象最显著的一个特性。继承是从已有的类中派生出新的类，新的类能吸收已有类的数据属性和行为，并能扩展新的能力。

##为什么有继承

假设现在有两个类，分别是教师类与学生类，定义如下：

```objc
#import <Foundation/Foundation.h>

@interface Teacher : NSObject {

    NSString *_name;
    NSInteger _age;
    float _height;
    float _salary;
}

@end

```

```objc
#import <Foundation/Foundation.h>

@interface Student : NSObject {

    NSString *_name;
    NSInteger _age;
    float _height;
    float _score;
}

@end

```
不难看出，学生类与教师类都有姓名、年龄与身高。那么，可不可以想一个办法，把这些都有的成员提取（抽象）出来，作为一个类，然后让学生和教师都引入就行了呢？答案是，可以的，使用继承就行。

##怎么继承

对于上面的问题，我们需要使用到继承。

1. 对于`Student`与`Teacher`两个类来说，首先要找到共有的部分（即姓名、年龄、身高）；
2. 然后他们都是属于`人类`的；
3. 那么我们就可以<font color=red>抽象</font>出一个人类，然后让`Teacher`与`Student`来继承它。

首先，人类的定义：

```objc
#import <Foundation/Foundation.h>

@interface Person : NSObject {

    NSString *_name;
    NSInteger _age;
    float _height;
}

@end
```

然后，学生有自己独有的成员变量，叫做`_score`，写法如下：

```objc
#import <Foundation/Foundation.h>
#import "Person.h"

// 注意：继承关系变成了Student继承自Person
@interface Student : Person {

    float _score;
}

@end
```

教师类也有独有的成员变量，叫做`_salary`，写法如下：

```objc
#import <Foundation/Foundation.h>
#import "Person.h"

// 注意：继承关系变成了Teacher继承自Person
@interface Teacher : Person {

    float _salary;
}

@end
```

##继承与方法

与上面使用继承的原因相同，对于人类来说，有自己的初始化方法，比如直接自定义init方法来初始化成员变量，Person类中的定义与实现如下：

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

```objc
#import "Person.h"

@implementation Person

- (instancetype)initWithName:(NSString *)name age:(NSInteger)age height:(float)height {

    self = [super init];

    if (self) {

        _name = name;
        _age = age;
        _height = height;
    }

    return self;
}

@end
```
同样，因为`Student`与`Teacher`继承自`Person`，所以他们也可以直接调用自定义init方法来进行对象的初始化。

```objc
#import <Foundation/Foundation.h>
#import "Person.h"
#import "Student.h"
#import "Teacher.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...

        Person *person = [[Person alloc] initWithName:@"A" age:0 height:10];
        Teacher *teacher = [[Teacher alloc] initWithName:@"B" age:3 height:12];
        Student *student = [[Student alloc] initWithName:@"C" age:5 height:16];
    }
    return 0;
}
```

##访问权限修饰符

> 权限修饰符是用来修饰实例变量的，用来控制实例变量的访问权限。

常用的访问权限修饰符有：`@public`，`@protected`，`@private`，区别如下：

| 修饰符名称 | 修饰后的变量作用域 | 其他说明 |
| -- | -- | -- |
| @public | 所有地方都能访问 | 少用，容易破坏封装性 |
| @protected | 在本类中与子类中可以访问 | 系统默认为@protected权限 |
| @private | 只能在本来中访问，不能继承给子类 |  ||

###修饰符的使用

```objc
#import <Foundation/Foundation.h>

@interface Person : NSObject {
    
    // 表示_name与_age两个成员变量是公开的，任何地方都可以访问
    @public
    NSString *_name;
    NSInteger _age;
    
    // 表示_height成员变量是私有的，只有自己访问，不能被继承
    @private
    float _height;
}

@end
```

##继承注意事项

1. OC中的继承为<font color=red>单继承</font>，也就是说，一个子类，只能有一个父类；
2. 被继承的类成为<font color=red>父类（或超类）</font>，继承其他类的类，称为<font color=red>子类</font>。

