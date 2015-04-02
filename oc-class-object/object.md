# 对象

[上一讲](./class.md)我们讲到了类，说类是一个抽象的描述。有抽象就有具体，对象就是类的一个具体的表现。

在网上有很多关于程序员的段子，出现频率最高的是：

> 程序员从来不缺少对象，因为程序里到处都是对象

当然，这种幽默只有程序员，也只有知道面向对象的程序员才懂。

##实例化对象

从类到对象这个转变，我们有一个专业术语，叫做*实例化*。

1. 打开[上一讲的工程](https://github.com/saitjr/Objective-C-Tutorials-Demo/tree/master/1-OC-Class-Object/Class/ClassDemo)；
2. 在main.m文件中引入Person类的头`#import "Person.h"`（自定义头文件使用`""`引入）；
3. 然后实例化Person类，并用临时变量person1去接收，最终代码如下：

```objc
#import <Foundation/Foundation.h>
#import "Person.h"

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...

        // 实例化Person，实例化的对象为person1
        // 关于方法的书写与调用，将在Function一讲中讲到
        
        // 首先需要使用alloc方法，开辟一块堆内存
        Person *person1 = [Person alloc];
        
        // 然后使用init方法对这块内存进行初始化
        person1 = [person1 init];
        
        // 上面两个步骤合并到一起：开辟并初始化内存
        Person *person1 = [[Person alloc] init];
    }
    return 0;
}

```