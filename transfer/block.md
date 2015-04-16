# Block

关于block的基本使用与介绍，请参考文章：

> [block的使用](http://www.brighttj.com/ios/ios-block-foundation.html)

##内存

对于block来说，除了要注意怎么使用，还需要注意它的内存管理。首先需要明白几个概念：

全局区：对于全局变量来说（包括全局block变量），都是存储在全局区的。

栈区(stack)：block直接定义(没有进行copy时)，基本数据类型(int, double等)，均存储在栈区。

堆区(heap)：对象alloc、block在copy后，存储在堆区。

##__block

要引入`__block`修饰符，我们需要先看下面这个例子：

```objc
typedef void(^Block)(void);

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        
        int a = 10;
        
        // 定义block并赋值
        Block block = ^{
        
            NSLog(@"%d", a);
        };
        
        // 改变a的值
        a = 20;
        block();
    }
    return 0;
}
```

在上面的例子中，按照我们的思维逻辑，应该输出20，但控制台输出的是10。

原因：

对于基本数据类型，存储在栈上，如果block当中需要使用到该变量，则会对该变量的值进行赋值，然后传给block中的变量（类似于函数的实参传值给形参）。所以，我们看到在block外部定义与赋值的a，与block内部输出的a，不在同一块地址。那么改变a的值，当然不会影响到block内部a的值。

解决方案：

还记得在学习C语言时，想要用函数交换两个变量的值吗？直接将变量名传过去是不行的，这样实参与形参的地址不同。最后我们采用的方法是传指针，这样就可以直接修改指针指向的变量的值。其实，block也是一样的，如果我们需要在block当中，使用a时，使用的是a的地址，那么就需要在定义变量a时，对变量a进行`__block`修饰。

```objc
__block int a = 10; // 注意有两根下划线
```

##copy

在声明block属性的时候，写法如下：

```objc
#import <Foundation/Foundation.h>

typedef void(^RentOutCallback)(NSInteger money);

@interface Agent : NSObject

@property (copy, nonatomic) RentOutCallback callback; // 注意，这里使用的是copy

@end
```
为什么这里声明属性，参数要填写copy，而不能是retain。因为block只有`Block_copy()`函数，没有对应的`retain`函数。

对block使用copy操作，有以下特点：

