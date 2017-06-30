#iOS代码规范

|版本|时间|修订人|
|---|---|----|
|v1.0|2017/06/06|曹辉辉|

## 1.语言

统一使用英文，全程或者缩写

```
//正确
UIColor *bgColor = [UIColor whiteColor];                                                                                                                           
 
//错误
UIColor *beiJingYanSe = [UIColor whiteColor];
 
//错误
UIColor *bgYanSe = [UIColor whiteColor];
```

## 2.代码组织

```    

#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Event

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}
```


## 3.大括号

```
//判断
if (user.isHappy) {
  //Do something
} else {
  //Do something else
}

//方法，注意-后面留一个空格
- (void)sayHello {
    //coding
}

//左对齐
[UIView animateWithDuration:1.0 animations:^{
  // something
} completion:^(BOOL finished) {
  // something
}];


//错误，冒号对齐
[UIView animateWithDuration:1.0
                 animations:^{
                     // something
                 }
                 completion:^(BOOL finished) {
                     // something
                 }];

//错误
- (void)sayHello
{
    //coding
}

//错误
if (user.isHappy)
{
    //Do something
}
else {
    //Do something else
}
```

## 4.属性申明

```
//@property后面一个空格，逗号后面加个空格，类型的前后都有一个控制，指针*要紧贴变量
@property (strong, nonatomic) UIWindow *window;

//错误，@property后面没有加空格
@property(strong, nonatomic) UIWindow *window;

//错误，逗号后面没有加空格
@property (strong,nonatomic) UIWindow *window;

//错误，指针*要紧贴变量
@property (strong, nonatomic) UIWindow* window;
```

## 5.静态变量命名详细

```
//详细
static NSTimeInterval const RWTTutorialViewControllerNavigationFadeAnimationDuration = 0.3;

//错误，太简洁
static NSTimeInterval const fadetime = 1.7;
```

## 6.常量使用静态变量

```
static NSString * const LYAboutViewControllerCompanyName = @"RayWenderlich.com";

static CGFloat const LYImageThumbnailHeight = 50.0;

//错误
#define CompanyName @"RayWenderlich.com"

#define thumbnailHeight 2
```

## 7.前缀
枚举、静态变量、宏、类、Category、协议要使用前缀

```
//正确
@interface LYStudent : NSObject

@end

//错误
@interface Student : NSObject

@end

//正确
@interface UIButton (LYCategory)
- (void)ly_setBackgroundColor:(UIColor *)color;
- (void)ly_setTitleColor:(UIColor *)color;
@end

//错误
@interface UIButton (Category)
- (void)setBackgroundColor:(UIColor *)color;
- (void)setTitleColor:(UIColor *)color;
@end

//正确
static CGFloat const LYImageThumbnailHeight = 50.0;
//错误
static CGFloat const ImageThumbnailHeight = 50.0;

//正确
#define LYWeakSelf __weak typeof(self) weakSelf = self
//错误
#define WeakSelf __weak typeof(self) weakSelf = self

//正确
typedef NS_ENUM(NSInteger, LYLeftMenuTopItemType) {
    LYLeftMenuTopItemMain = 0,
    LYLeftMenuTopItemShows = 1,
    LYLeftMenuTopItemSchedule = 2
};

//错误
typedef NS_ENUM(NSInteger, LeftMenuTopItemType) {
    LeftMenuTopItemMain = 0,
    LeftMenuTopItemShows = 1,
    LeftMenuTopItemSchedule = 2
};

```
## 8.Switch Case 使用枚举

正确

```
typedef NS_ENUM(NSInteger, LYRequestCode){
    LYRequestCodeFail = 0,//失败
    LYRequestCodeSuccess = 1,//成功
    LYRequestCodeUnlogin = 10,//未登陆
    LYRequestCodeUnAuth = 100,//未认证
};

switch (code) {
  case LYRequestCodeFail:
    // ...
    break;
  case LYRequestCodeSuccess:
    // ...
    break;
  case LYRequestCodeUnlogin:
    // ...
    break;
  case LYRequestCodeUnAuth:
    // ...
    break;
  default:
    // ...
    break;
}

```

错误

```
switch (code) {
  case 0:
    // ...
    break;
  case 1:
    // ...
    break;
  case 10:
    // ...
    break;
  case 100:
    // ...
    break;
  default:
    // ...
    break;
}
```

## 9.成员变量
成员变量名要用下划线区分。

```
@interface LYViewController : UIViewController{
    //正确
    BOOL _flag; 
    
    //错误
    BOOL flag;
}
@end
```

## 10.初始化函数


```
//正确
- (instancetype)init {
  self = [super init];
  if (self) {
    // ...
  }
  return self;
}

//错误
- (instancetype)init {
  if (self = [super init]) {
    // ...
  }
  return self;
}
```

## 11.错误处理

```
//正确
NSError *error;
if (![self trySomethingWithError:&error]) {
  // Handle Error
}

//错误
NSError *error;
[self trySomethingWithError:&error];
if (error) {
  // Handle Error
}
```
## 12.单例

```
+ (instancetype)sharedInstance {
  static id sharedInstance = nil;

  static dispatch_once_t onceToken;
  dispatch_once(&onceToken, ^{
    sharedInstance = [[self alloc] init];
  });

  return sharedInstance;
}
```

## 13.文件导入

在`.h`文件中引入类尽量使用`@class ClassName;`，而不是`#import 'ClassName.h'`


```
//正确
#import <UIKit/UIKit.h>
@class LYModel;

@interface LYViewController : UIViewController
@property (nonatomic, strong) LYModel *param;
@end
```

```
//错误
#import <UIKit/UIKit.h>
#import "LYModel.h"

@interface LYViewController : UIViewController
@property (nonatomic, strong) LYModel *param;
@end
```

## 14.NSString、 NSDictionary、 NSArray、NSNumber的初始化

```
//正确
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone" : @"Kate", @"iPad" : @"Kamal", @"Mobile Web" : @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingZIPCode = @10018;

//错误
```
## 15.协议属性

```
//正确、弱引用
@property (weak, nonatomic) id<SGOAnalyticsDelegate> analyticsDelegate;

//错误、不符合规范
@property (nonatomic) id<SGOAnalyticsDelegate> analyticsDelegate;

//错误、使用强引用容易导致循环引用
@property (strong, nonatomic) id<SGOAnalyticsDelegate> analyticsDelegate;
```

## 16.Block使用

Block引用到self都需要申明`__weak`

```
__weak typeof(self) weakSelf = self;

void (^blockName1)(void) = ^{
    // do some things
    NSLog("%@",weakSelf);
};

//Block临时变量声明
typedef void (^LYCompletion) (id object, NSError *error);
LYCompletionBlock block = ^ (id object, NSError *error) { 
    /* ... */ 
};

//错误
void(^block)(id, NSError*) = ^void(id obj, NSError *error) { 
    /* ... */ 
};
```

## 17.命名规则

```
//驼峰命名规则
//属性、变量、方法的首字母小写
//类名、类型名的首字母大写

//特例
//Category的方法名和属性名的命名规则是
//前缀_驼峰命名
//例如:

@interface UIButton (LYCategory)
- (void)ly_setBackgroundColor:(UIColor *)color;
- (void)ly_setTitleColor:(UIColor *)color;
@end

```

## 18.多参数函数名

```
//正确
- (void)sendAction:(SEL)aSelector to:(id)anObject forAllCells:(BOOL)flag;

//错误
- (void)sendAction:(SEL)aSelector :(id)anObject :(BOOL)flag;
```

## 19.点(.)语法

```
//正确
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;

//错误
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.sharedApplication.delegate;
```

## 20.逻辑控制

```
//正确
- (void)someMethod {
    if (![someOther boolValue]){
         return;
    }
    //Do something important
}

//错误
- (void)someMethod {
    if ([someOther boolValue]){
           //Do something important
    }
}
```

## 21.三目运算符
三目运算符不嵌套使用

```
//正确
result = c > d ? c : d
result = a > b ? result : y;

//错误
result = a > b ? x = c > d ? c : d : y;
```

## 22.全部使用懒加载

```
@property(strong, nonatomic) UIWindow *window;

- (UIWindow *)window {
    if (_window){
        _window = [[UIWindow alloc]initWithFrame:[UIScreen mainScreen].bounds];
    }
    return _window;
}
```

## 23. @synthesize 使用

```
//正确
@synthesize userName = _userName;

//错误
@synthesize userName;
```

## 24.类注释

例子:

```

#import <Foundation/Foundation.h>


/**
 归档工具
 */
@interface LYArchiverTool : NSObject

@end
```

## 25.ViewController 命名

所有ViewController一定要全

```
@interface LYHomeViewController : UIViewController

@end
```

## 26.布局时不直接使用数组,使用变量

```
```

## 27.无用代码一定要删除

## 28.颜色、图片、字体统一使用主题管理




