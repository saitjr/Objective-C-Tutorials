# BOOL

布尔类型

很多语言都有布尔值类型，有的关键字为`boolean`、有的为`bool`，表示方式为`true`、`false`。

在OC中，布尔类型的关键字为<font color=red>大写</font>的`BOOL`，表示方式为`YES`、`NO`。

##使用方式

BOOL类型一般用于表示真假、是否这种情况，如iOS开发中的按钮是否选中、排序是否提前完成等。表示方式如下：

```objc
BOOL isSelected = NO;

// 判断方式
if (isSelected) {

	NSLog(@"选中");
}

```

##深入理解

当在xcode中输入BOOL时，编译器还联想出了`BOOL`、`bool`、`Boolean`、`boolean_t`等类型，我们来一一分析下。

###BOOL

头文件：`objc.h`

实际类型：`signed char`

表示方式：`YES` \ `NO`

注意点：<font color=red>当`BOOL a == 1`的时候，才是YES，其他情况均为NO</font>，所以在使用时，慎用`a == YES`这种方式。

```objc
BOOL a = 3;
NSLog(@"%d", a == YES); // 输出0
```

###bool

头文件：`stdbool.h`

实际类型：`_Bool (int)`

表示方式：`true` \ `false`

```objc
bool a = 3;
NSLog(@"%d", a == true); // 输出1
```

###Boolean

头文件：`MacTypes.h`

实际类型：`unsigned char`

表示方式：`TRUE` \ `FALSE`

注意：<font color=red>与BOOL的情况相同，仅当a == 1时为TRUE</font>

```objc
Boolean a = 1;
NSLog(@"%d", a == TRUE);
```

###boolean_t

头文件：`boolean.h`

实际类型：`unsigned int`

关于在OC中几种布尔值的区别，可查看这篇在stackoverflow上的回答：

> [http://stackoverflow.com/questions/14464671/all-kinds-of-booleans-in-objectivec](http://stackoverflow.com/questions/14464671/all-kinds-of-booleans-in-objectivec)

