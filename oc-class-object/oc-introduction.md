#OC简介

###苹果与OC

1. 1980年，Brad Cox设计了Objective-C，而<font color=red>不是</font>苹果设计的；
2. 1985年，乔布斯离开苹果，创建了NeXT，并开发了NextSTEP；
3. 1996年，乔布斯回到苹果，收购NeXT，将NextSTEP更名为Cocoa，将它作为Mac OS X的基础，所以我们看到的Cocoa库，几乎都是以`NS`开头的。


###OC的特点

1. 不开源；
2. 动态语言；
3. 面向对象；

###面向对象

之前我们学到的C语言，是一门面向过程的语言，但是OC是面向对象的。直接这样阐述可能会显得很抽象也显得很苍白，那么，举一个例子（事实上，这也是OC的原理）：

在我们学习C语言的时候，我们接触到了一个概念，叫做结构体。现在假设有一个名为学生的结构体，我们可以将它定义为：
```
typedef struct {

    char name[20];
    int age;
    float height;
} Student;```

可以看到，这个学生有姓名、年龄、身高。
1. 那么在OC中，我们将它称为**<font color=red>类</font>**；
2. 姓名、年龄、身高等信息，称为**<font color=red>属性</font>**；
3. 将声明新的结构体变量`Student *student1;`，称为**<font color=red>对象</font>**。
