# NSArray

不可变数组。OC中的集合不再是单纯的数组，而范围了三大类：数组、字典、集。

学习数组，首先明白一下几个内容：

- 数组分为不可变数组(NSArray)与可变对象(NSMutableArray)；
- 只能装对象，基本数据类型包装成NSNumber，复杂类型包装成NSValue；
- nil作为结束标示；
- 下标从0开始；
- 数组中的元素不一定为一个类型，可以存在`NSString`，也可以存在`NSNumber`。

##常用方法

与不可变字符串`NSString`类似，不可变数组`NSArray`操作也不在原数组上进行，而是通过返回一个新的数组来操作。

- [初始化](#init)
- [获取数组元素个数](#count)
- [添加元素](#append)
- [查找元素](#search)
- [获取元素](#objectAtIndex)
- [截取部分元素](#delete)
- [数组排序](#sort)

<span id='init'></span>
##初始化

###简化操作

```objc
NSArray *array1 = @[@"1", @"2", @"3"];
```

###实例方法

```objc
// 按元素初始化（常用）
NSArray *array2 = [[NSArray alloc] initWithObjects:@"1", @"2", @"3", nil];

// 按已有的数组进行初始化（初始化出来和array1的元素相同）
NSArray *array3 = [[NSArray alloc] initWithArray:array1];
```

###遍历构造

```objc
NSArray *array4 = [NSArray arrayWithObjects:@"1", @"2", @"3", nil];
NSArray *array5 = [NSArray arrayWithArray:array1];
```

<span id='count'></span>
##获取数组元素个数

获取数组元素个数的方法与`NSString`获取长度有区别，使用的是`count`，而不是`length`。

```objc
NSUInteger count1 = [array1 count];
NSUInteger count2 = array1.count;
```

<span id='append'></span>
##添加元素

```objc
// 从尾部追加一个元素
NSArray *array6 = [array1 arrayByAddingObject:@"4"];

// 从尾部依次追加array2中的元素
NSArray *array7 = [array1 arrayByAddingObjectsFromArray:array2];
```

<span id='search'></span>
##查找元素

###是否包含某元素

```objc
BOOL isContain = [array2 containsObject:@"1"];
```
###元素具体位置

查找并返回元素的具体位置，如果没找到，返回NSNotFound。

```objc
NSUInteger index = [array2 indexOfObject:@"2"];
NSLog(@"是否找到 = %d", index == NSNotFound);
```

<span id='objectAtIndex'>
##获取元素

<font color=red>存入的是什么类型，取出的时候，就需要什么类型去接收</font>。

###根据下标获取元素

```objc
// 两种取值方式等价
NSString *string1 = array2[0];
NSString *string2 = [array2 objectAtIndex:0];
```

```objc
// 取出一个与最后一个元素
NSString *string3 = [array2 firstObject]; // 第一个元素
NSString *string4 = [array2 lastObject];  // 最后一个元素
```

<span id='sub'></span>
##截取部分元素

通过给定范围，截取数组元素中的部分元素，存入新数组。

```objc
NSArray *array8 = [array2 subarrayWithRange:NSMakeRange(0, 2)];
```

<span id='sort'></span>
##数组排序

一般的<font color=red>字符串</font>数组排序会使用到`NSString`提供的`compare:`或`caseInsensitiveCompare:`方法，然后调用`sortedArrayUsingSelector`达到对`array2`中，存储的<font color=red>字符串</font>进行排序的目的。

```objc
NSArray *array9 = [array2 sortedArrayUsingSelector:@selector(caseInsensitiveCompare:)];
```

注意上面写法的几点要求：

1. array2数组中存储的全是字符串；
2. 比较大小需要传的@selector类型中，`caseInsensitiveCompare`是字符串中的方法；
3. 这里选择器`@selector`返回值类型必须是`NSComparisonResult`。

根据这几点要求，我们可以写出自己的比较大小的方法，练习如下：

1. 创建一个`Person`类；
2. `Person`类有一个成员变量`name`；
3. 初始化多个`Person`，并给出不同的`name`值；
4. 将初始化出来的`Person`对象存入`NSArray`；
5. 根据`name`的大小，对`Person`进行升序排列。

实现如下：

1.创建`Person`类，并给出成员变量`name`，并实现响应的`getter` / `setter`方法；

2.为了输出方便，重写`description`方法，返回`name`；
3. 