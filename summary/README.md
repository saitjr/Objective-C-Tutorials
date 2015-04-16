# OC总结与复习

##面向对象

1. 面向对象的特点
2. 定义类与对象
3. 方法的定义(+/-，返回值，方法名，参数的写法)
4. 方法的重写(init，description)
5. self与super
6. 类、对象、方法的命名规范

##字符串

`NSString`、`NSMutableString`

1. 字符串初始化（init与遍历构造）
2. 拼接
3. 截取
4. 查找

##数值类型

`NSValue`、`NSNumber`

1. NSNumber与NSValue对基本类型的装包与拆包
2. NSString，NSNumber，基本类型之间的转换
3. NSNumberFormatter的使用（将1234转为1,234）

##集合

`NSArray`、`NSmutableArray`、`NSDictionary`、`NSMutableDictionary`、`NSSet`

1. 有序集合与无序集合区别
2. 初始化
3. 添加
4. 查找
5. 删除
6. 多层取值

##内存管理

1. 内存管理原则
2. 循环引用如何处理
3. OC中是否有垃圾回收机制？iOS中呢？

##属性

1. 属性的写法
2. 属性的优势
3. 参数与其用法
4. 非ARC下，重写setter方法
5. 点语法的理解
6. copy与mutableCopy

##常用设计模式

1. 单例模式的特点（初始化、生命周期、写法、常见的系统单例）
2. KVC
3. 观察者模式（KVO、NSNotification）
4. 代理模式（代理的写法，为什么用assgin）

##类目与延展

1. 写法
2. 用来干啥么
3. 区别
4. 特点

##block代码块

1. block的定义
2. `__block`
3. `__weak`与`__unsafe_unretained`
4. `typeof`
5. 定义属性使用的参数