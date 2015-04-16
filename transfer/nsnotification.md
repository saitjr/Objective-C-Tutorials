# NSNotification

NSNotification翻译为通知。继承于NSObject，遵守NSCoding、NSCopying、NSObject协议。

##使用条件

在传值层数较多，或需要用到广播(一个发送，多人接收)的时候，可以选用通知。

###实际例子：

鬼子进村了，村门口就一个大钟，有人去敲响，全村人就知道了，然后躲起来。

###程序例子：

当用户登录成功以后，发个通知“登录成功了”，相应的用户个人中心、用户好友列表、只要和用户有关的数据，全都变了。

当用户注销登录以后，发出通知，相应的用户数据，相关页面就应该清除，或变成请登录。

##使用方式

为了使用通知，我们来创建几个类，进行模拟用户登录的情况：

`LoginViewController`, `UserCenterViewController`, `ModifyUserViewController`，这些类都继承于`NSObject`。

要完整的写一个通知，分为四个步骤：

1. 发送通知；
2. 接收通知；
3. 接收到后做出相应处理；
4. 移除通知

首先，在`LoginViewController`中，创建一个公开方法`login`，在方法中发出登录成功的通知：

```objc
#import "LoginViewController.h"

@implementation LoginViewController

- (void)login {
    
    // 发送名为LoginSuccess的通知
    // 通过[NSNotificationCenter defaultCenter]单例获得通知中心对象
    // 调用postNotificationName:方法发出名为LoginSuccess的通知
    // object : 发送者，如果接受者不需要知道发送者是谁，可以传nil
    [[NSNotificationCenter defaultCenter] postNotificationName:@"LoginSuccess" object:nil];
}

@end

```

第二步，登录成功后，需要在`UserCenterViewController`、`ModifyUserViewController`中接收通知，并处理登录成功后的逻辑：

```objc
#import "UserCenterViewController.h"

@implementation UserCenterViewController

// 重写init方法，让UserCenterViewController一初始化，就准备接收通知
- (instancetype)init {
    
    self = [super init];
    
    if (self) {
        
        // 注册接收者与接收到以后，需要调用的方法
        // 参数1 Observer : 接受者（接收到后，谁来处理）
        // 参数2 selector : 接收到后，调用哪个方法来处理（接收到后，需要做什么）
        // 参数3 name     : 要接收通知的名字
        // 参数4 object   : 
        [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(loginSuccessNotification:) name:@"LoginSuccess" object:nil];
    }
    
    return self;
}

- (void)loginSuccessNotification:(NSNotification *)notification {
    
    NSLog(@"UserCenterViewController收到通知了");
}

@end

```

同样，`ModifyUserViewController`中的接收方式与`UserCenterViewController`相同，具体代码如下：

```objc
#import "ModifyUserViewController.h"

@implementation ModifyUserViewController

- (instancetype)init {
    
    self = [super init];
    
    if (self) {
        
        [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(loginSuccessNotification:) name:@"LoginSuccess" object:nil];
    }
    
    return self;
}

- (void)loginSuccessNotification:(NSNotification *)notification {
    
    NSLog(@"ModifyUserViewController收到通知了");
}

@end
```

最后一步，通知的移除。对于通知的接受者来说，<font color=red>当接受者释放之前，必须移除通知</font>。对象声明周期的最后一步，就是`dealloc`方法，所以，通知的移除，一般写在`dealloc`中。

对于上面的例子来说，`UserCenterViewController`、`ModifyUserViewController`就需要移除通知。

```objc
- (void)dealloc {
    
    [[NSNotificationCenter defaultCenter] removeObserver:self name:@"LoginSuccess" object:nil];
    [[NSNotificationCenter defaultCenter] removeObserver:self];
}
```

##具体分析

