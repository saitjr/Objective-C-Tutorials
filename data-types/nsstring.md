# NSString

字符串类型

NSString为类，它实例化后即是字符串对象。在OC中，NSString表示不可变字符串，可变字符串用[NSMutableString](./nsmutablestring.md)表示。

##NSString与char *的区别

|  | NSString对象 | char * |
| -- | -- | -- |
| 结束符 | 不以\0作为结束标示 | \0 |
| 运算 | 通过方法进行运算 | 通过函数或当成字符数组进行运算 |

##字符串的常用方法

因为NSString为不可变字符串，所以所有的操作都不会对原字符串进行修改，而是返回新的字符串。

- [初始化](#init)
- [拼接](#append) / [截取](#sub) / [查找](#search) / [替换](#replace)
- [获得长度](#length)
- [字符串比较](#compare)
- [转换类型](#transform)
- [转大小写](#upper-lower)

##常量字符串

```objc
NSString *string = @"This is a string";
```

<span id='init'></span>
##初始化

```objc
// 实例方法
NSString *string1 = [[NSString alloc] initWithString:string];
NSString *string2 = [[NSString alloc] initWithFormat:@"格式化初始化%d", 5];

// 类方法（便利构造）
NSString *string3 = [NSString stringWithString:string]; // 与initWithString类似
NSString *string4 = [NSString stringWithFormat:@"%d", 5]; // 这种方式用得最多
```

<span id='append'></span>
##拼接

可直接利用`stringWithFormat`初始化方法来进行拼接。

```objc
NSString *string5 = [NSString stringWithFormat:@"%@%@", string3, string4];
```
使用NSString拼接方法进行拼接，两种拼接方法都会返回拼接好了字符串：

```objc
// 系统声明
- (NSString *)stringByAppendingString:(NSString *)aString;

// 使用方式：
NSString *string6 = [string1 stringByAppendingString:string2];
```

```objc
// 系统声明
- (NSString *)stringByAppendingFormat:(NSString *)format, ...;

// 使用方法：
NSString *string7 = [string1 stringByAppendingFormat:@"%@%d", string2, 123];
```

<span id='sub'></span>
##截取

使用NSString的截取方法，只需记住截取的关键字`sub`即可，几乎在所有语言中，截取方法都是以`sub`开头的。截取时，需要注意<font color=red>越界</font>。

```objc
NSString *string8 = [string4 substringFromIndex:2]; // 从下标2开始截取到最后
NSString *string9 = [string4 substringToIndex:5]; // 从开头截取到下标5

// 按范围截取，NSMakeRange需要两个参数，一个是起始位置，一个是长度
NSString *string10 = [string4 substringWithRange:NSMakeRange(1, 4)];
```

<span id='search'></span>
##查找

查询分为三种：

1. 查看字符串是否以xxx开头，或是否以xxx结尾，这种方式多用于网络请求。如：如果要跳转的链接以http://www.baidu.com开头，则跳转，否则不予跳转。
2. 查找字符串中是否包含某字符串
3. 获得字符串中，某个位置的字符

```objc
BOOL isSuffix = [string10 hasSuffix:@"com"]; // 后缀是否是com
BOOL isPrefix = [string10 hasPrefix:@"www"]; // 前缀是否是www
```

```objc
NSRange range = [string10 rangeOfString:@"23"]; // 查找@"23"在string10中的位置

// NSRange是一个结构体，不属于OC对象类型，不是很方便输出，可采用以下两种形式:
NSLog(@"%ld, %ld", range.location, range.length); // 分开输出
NSLog(@"%@", NSStringFromRange(range)); // 将range转为NSString进行输出
```

```objc
char a = [@"abcSeW" characterAtIndex:3];
```

<span id='replace'></span>
##替换

替换分为两种：

1. 按字符串替换；
2. 按范围替换；

```objc
// 将string10中所有的@"2"替换为@"7"
NSString *string11 = [string10 stringByReplacingOccurrencesOfString:@"2" withString:@"7"];

// 将string10中的0~2范围字符串，替换为@"33"
NSString *string12 = [string10 stringByReplacingCharactersInRange:NSMakeRange(0, 2) withString:@"33"];
```

<span id='length'></span>
##获得长度

```objc
NSInteger length1 = [string12 length]; // 可以使用方法访问
NSInteger length2 = string12.length; // 也可以使用点语法，直接访问(点语法会在属性部分介绍)
```

<span id='compare'></span>
##字符串比较

`==`比较的是对象的地址，值不能直接使用`==`来进行比较，应该使用对应的方法。

```objc
BOOL isEqual = [string10 isEqualToString:string11]; // 比较字符串的值是否相同
```

比较两个字符串大小，需要用到NSComparisonResult枚举类型。具体定义如下：

```objc
typedef NS_ENUM(NSInteger, NSComparisonResult) {
	NSOrderedAscending = -1L,		// 升序
	NSOrderedSame,					// 相同
	NSOrderedDescending			// 降序
};
```

```objc
// 判断两个字符串大小
NSComparisonResult compareResult1 = [string10 compare:string11]; // 区分大小写
NSComparisonResult compareResult2 = [string10 caseInsensitiveCompare:string11]; // 不区分大小写
```

<span id='transform'></span>
##转换类型

在实际操作过程中，可能需要遇到字符串转为其他类型的情况，如计算器中，获得输入框中的文字是字符串类型，但计算时，需要将它转为`double`类型。

```objc
double number1    = [@"2.4" doubleValue]; // number1 = 2.4
int number2       = [@"2" intValue];      // number2 = 2
NSInteger number3 = [@"2" integerValue];  // number3 = 2
float number4     = [@"4.6" floatValue];  // number4 = 4.6
BOOL number5      = [@"2" boolValue];     // number5 = YES
```

对于数字类型的字符串，直接转换就行。

- 对于`intValue`，转换到字符以前。如：`[@"123ab0c" intValue] == 123`；
- 对于`boolValue`，以`y`，`Y`，`t`，`T`开头的字符串与结果不为0的数字，转换结果为YES，其余情况为NO。如：`[@"t" boolValue] == YES`，`[@"0" boolValue] == NO`；

还可以将数组转为字符串（将数组的某一个元素，以某个分隔符，拼接成字符串）

```objc
// 定义数组
NSArray *array = @[@"abc", @"def"];
// 将数组以-拼接为字符串
NSString *string15 = [array componentsJoinedByString:@"-"]; // @"abc-def"
```

<span id='upper-lower'></span>
##转大小写

```objc
NSString *string13 = [@"abcSeW" uppercaseString]; // 转为大写
NSString *string14 = [@"abcSeW" lowercaseString]; // 转为小写
```