#Route ULR 说明

## 1、路径
|route|说明|
|---|---|
|push|跳转|
|present|覆盖|
|pop|回退|
|none|正常，只是执行方法|

## 2、路由键值

|route key|说明|
|---|---|
|className|类名|
|classFunc|类方法名|
|instanceFunc|实例方法名|
|action|默认：0。0:先执行类方法，在执行实例方法，若无类方法默认执行`alloc`，若无实例方法默认执行`init`。1:无方法不执行|
|urlCode|参数是否经过urlCode加密，默认值是：0|

## 3、参数键值

|param key|说明|
|---|---|
|iParam1|实例方法的第一个参数|
|iParam2|实例方法的第二个参数|
|...|...|
|iParam5|实例方法的第五个参数|
|cParam1|类方法的第一个参数|
|cParam2|类方法的第二个参数|
|...|...|
|cParam5|类方法的第五个参数|


每种参数最多5个，超过5个请传字典或者数组的归档hash值。

## 4、示例

* 示例1

```
/*
    用LYFuncObject的initWithParam:param2:实例化，参数有iParam1,iParam2
    
    类似代码:
    [[LYFuncObject alloc]initWithParam:iParam1 param2:iParam2]
*/

LYLawyerPlatformUser://none?className=LYFuncObject&instanceFunc=initWithParam:param2:&iParam1=333&iParam2=88
```

* 示例2

```
/*
    跳转到UIViewController    
    
    类似代码:
    [[UIViewController alloc]init]
*/

LYLawyerPlatformUser://push?className=UIViewController
```


* 示例3

```
/*
    跳转到UIViewController    
    
    类似代码:
    [UIViewController new]
*/

LYLawyerPlatformUser://push?className=UIViewController&action=1&classFunc=new
```


* 示例4

```
/*    
    调用 LYFuncObject的@selector(classFunc:cParam1 param2:cParam2)初始化，然后调用示例方法@selector(show)
    类似代码:
    LYFuncObject *obj = [LYFuncObject classFunc:cParam1 param2:cParam2];
    [obj show];
*/

LYLawyerPlatformUser://none?className=LYFuncObject&classFunc=classFunc:param2:&istanceFunc=show&cParam1=11&cParam2=22
```




