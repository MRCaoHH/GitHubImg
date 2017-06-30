# podspec 文件说明

|版本|修改人|修改时间|
|---|---|---|
|v1.0.0|曹辉辉|2017/6/30|

官方地址:[https://guides.cocoapods.org/syntax/podspec.html#specification](https://guides.cocoapods.org/syntax/podspec.html#specification)

## 1. podspec文件示例

```
Pod::Spec.new do |spec|
  spec.name         = 'Reachability'//名字
  spec.version      = '3.1.0'//版本
  spec.license = { :type => 'MIT', :file => 'MIT-LICENSE.txt' }//license配置
  spec.homepage     = 'https://github.com/tonymillion/Reachability'//主页
  spec.authors      = { 'Tony Million' => 'tonymillion@gmail.com' }//作者
  spec.summary      = 'ARC and GCD Compatible Reachability Class for iOS and OS X.'//总结
  spec.source       = { :git => 'https://github.com/tonymillion/Reachability.git', :tag => 'v3.1.0' }//源码位置
  spec.module_name  = 'Rich'//模块名称

  spec.ios.deployment_target  = '9.0'//iOS平台最低版本
  spec.osx.deployment_target  = '10.10'//osx平台最低版本

  spec.source_files       = 'Reachability/common/*.swift'//源文件路径
  spec.ios.source_files   = 'Reachability/ios/*.swift', 'Reachability/extensions/*.swift'//iOS平台源文件位置
  spec.osx.source_files   = 'Reachability/osx/*.swift'//osx平台源文件位置

  spec.framework      = 'SystemConfiguration'//需要导入的系统framework
  spec.ios.framework  = 'UIKit'//iOS平台需要导入的系统framework
  spec.osx.framework  = 'AppKit'//osx平台需要导入的系统framework

  s.vendored_frameworks = 'Reachability/Vendors/xxx.framework','Reachability/Vendors/xxx2.framework'//导入第三方的frameworks
  
  spec.vendored_libraries = 'libProj4.a', 'libJavaScriptCore.a'//导入第三方的静态库
  
  spec.resource_bundles  = {
    'MapBox' => ['MapView/Map/Resources/*.png'],
    'OtherResources' => ['MapView/Map/OtherResources/*.png']
  }//导入bundles
  
  spec.resource = ['Images/*.png', 'Sounds/*']//导入资源
  
  spec.public_header_files = 'Headers/Public/*.h'//公开的头文件
  spec.private_header_files = 'Headers/Private/*.h'//私有头文件
  
  spec.exclude_files = 'Classes/**/unused.{h,m}//不导入的文件
  spec.dependency 'SomeOtherPod'//导入其他的pod
  spec.dependency 'SomeOtherPod2','~>1.0.0'//多个pod，多行
end
```

## 2.导入其他的pod

```
   //多个多行
  spec.dependency 'AFNetworking','~>3.0.0'
  spec.dependency 'MJRefresh','~>1.0.0'
```

## 3.导入第三方*.framework,*.a（framework供应商并没有上传pod trunk，需要在自身pod中导入）

```
  s.vendored_frameworks = 'Reachability/Vendors/xxx.framework','Reachability/Vendors/xxx2.framework'//导入第三方的frameworks

  spec.vendored_libraries = 'libProj4.a', 'libJavaScriptCore.a'//导入第三方的静态库
```

## 4.资源导入

### 4.1 直接导入

```

spec.resources = ['Images/*.png', 'Sounds/*']
/*
这种方式导入在主工程中可以直接用[UIImage imageNamed:@"xx"]访问
*/  

```
### 4.2 通过bundle导入

```
spec.resource_bundles = {
    'BundleName' => ['DirectoryName/Assets/BundleName/*'],
    'BundleName2' => ['DirectoryName/Assets/BundleName2/*'],
}

或

spec.resource = 'Resources/HockeySDK.bundle'

```

访问方式：访问bundle 在用bundle访问对应的资源

```
NSBundle *bundle = [NSBundle bundleForClass:[self class]];
NSURL *bundleUrl = [bundle URLForResource:@"xxx" withExtension:@"bundle"];
if (bundleUrl) {
    bundle = [NSBundle bundleWithURL:bundleUrl];
    NSString *imgPath = [bundle pathForResource:imageName ofType:@"png"];
    UIImage *img = [UIImage imageWithContentsOfFile:imgPath];
}

```


