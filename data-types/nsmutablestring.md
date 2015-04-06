# NSMutableString

可变字符串，继承自`NSString`。

之前介绍的`NSString`为不可变字符串，任何操作都不能在原字符串上进行。而`NSMutableString`不同，作为可变字符串，可直接对原字符串进行编辑。

注：因为`NSMutableString`继承与`NSString`，所以`NSString`的方法，`NSMutableString`依然可用。他们的方法，最大的区别在于，`NSString`会返回新的字符串，而`NSMutableString`对原字符串处理，返回`void`。

同样，对于`NSMutableString`也有很多常用方法，本讲将介绍：

- [初始化](#init)
- [添加](#append) / [删除](#delete) / [修改](#update)

<span id='init'></span>
##初始化

使用`NSString`的几种初始化方法，依然可以对`NSMutableString`有效，写法如下：

```objc
NSMutableString *string1 = [NSMutableString string];
NSMutableString *string2 = [NSMutableString stringWithFormat:@"abc"];
```

下面介绍两种独有的：

```objc
// 给出初始长度，进行字符串的初始化(这个初始长度不用太准确，因为系统分配的内容会随着字符串长度而变动)
NSMutableString *string3 = [[NSMutableString alloc] initWithCapacity:4];
NSMutableString *string4 = [NSMutableString stringWithCapacity:4];
```

<span id='append'></span>
##添加

```objc
[string2 appendString:@"def"]; // 从尾部追加字符串@"def"
[string2 appendFormat:@"%d", 9]; // 从尾部格式化追加字符串@"9"
[string2 insertString:@"000" atIndex:0]; // 在第0位插入字符串@"000"
```

<span id='delete'></span>
##删除

```objc
// 从0开始，删除3个字符
[string2 deleteCharactersInRange:NSMakeRange(0, 3)]; 
```

<span id='update'></span>
##修改

```objc
// 按范围替换
[string2 replaceCharactersInRange:NSMakeRange(0, 3) withString:@"vvv"];
// 完全替换
[string2 setString:@"333"];
```