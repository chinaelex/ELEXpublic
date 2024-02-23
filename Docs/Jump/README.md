# ELEX中台应用跳转模块
**跳转模块提供应用跳转能力，支持跳应用app store详情和评分页面，也可跳转到自定义的URL**

## Requirements

- iOS 10.0+
- Xcode 13.0+

## Installation

EPSDK支持[CocoaPods](https://cocoapods.org)接入，各个模块如无特殊说明，支持的最低系统版本为iOS10.0；
### CocoaPods
[CocoaPods](http://cocoapods.org) is a dependency manager for Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

```ruby
source 'git@git.elex-tech.com:opt-connect/open-ios/elex-sdk-repo.git'
source 'https://cdn.cocoapods.org'
platform :ios, '10.0'

target 'UnityFramework' do
  pod 'EPSDK'
end
```
Then, run the following command:

```bash
$ pod install
```
# 接入
引入头文件
```objc
#import <EPSDK/EPSDK+Jump.h>
```

#### 跳转到评分页面
```objc
/// 跳转到当前应用的app store 评分页面
///
/// 需要在配置中设置apple appid
/// - Parameter completion: 完成回调
- (void)jumpAppStoreReviewWithCompletion:(nullable void (^)(NSError * _Nullable))completion;
```

#### 跳转到应用详情
```objc
/// 跳转到app store详情页面
///
/// 需要在配置中设置apple appid
/// - Parameter completion: 完成回调
- (void)jumpAppStorePageWithcompletion:(nullable void (^)(NSError * _Nullable))completion;
```

#### 跳转到指定URL
```objc
/// 跳转到指定URL
///
/// 如跳转到商店页面
/// ``` Objective-C
/// [[EPSDK sharedSDK] jumpWithURL:@"itms-apps://itunes.apple.com/app/(appId)" completion:nil];
///
/// ```
/// - Parameters:
///   - url: 跳转链接
///   - completion: 跳转结果回调
- (void)jumpWithURL:(NSString *)url completion:(void(^)(NSError *_Nullable error))completion;
```

#### 错误码
|  错误码  |       说明       |
| :-----: | :--------------: |
| -10000 | 跳转取消 |
| -10001 | 跳转URL不可用 |
| -10002 | 跳转不支持 |
| -10003 | 跳转商店评价次数限制 |```
