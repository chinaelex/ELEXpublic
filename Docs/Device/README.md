# ELEX中台设备相关模块
![Objective-C](https://img.shields.io/badge/Objective--C-blue.svg?style=flat)
![Platform](https://img.shields.io/badge/platform-iOS-A1A1A1?style=flat)
![Region](https://img.shields.io/badge/region-CN_|_Oversea-green.svg?style=flat)
![version](https://img.shields.io/badge/iOS-12.0-orange.svg?style=flat)

# Requirements

- iOS 10.0+
- Xcode 13.0+

# Installation

EPSDK支持[CocoaPods](https://cocoapods.org)接入，各个模块如无特殊说明，支持的最低系统版本为iOS10.0；
## CocoaPods
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

## 麦克风权限
导入头文件
```objc
#import <EPSDK/EPDeviceUtils+MediaAuthorization.h>
```
设置``info.plist``添加``NSMicrophoneUsageDescription``
1. 麦克风权限是否可用
```objc
/// 麦克风权限是否可用
+ (BOOL)microPhoneAuthorizationEnable;
```
2. 获取麦克风权限
```objc
/// 请求麦克风授权
/// - Parameter completion: 完成回调Block，granted是否同意
+ (void)requestMicroPhoneAuthorizationWithCompletion:(void (^)(BOOL granted))completion;
```
## 摄像头权限
设置``info.plist``添加``NSCameraUsageDescription``
1. 摄像头权限是否可用
```objc
/// 摄像头权限是否可用
+ (BOOL)cameraAuthorizationEnable;

```
2. 获取摄像头权限
```objc
/// 请求摄像头授权
/// - Parameter completion: 完成回调Block，granted是否同意
+ (void)requestCameraAuthorizationWithCompletion:(void (^)(BOOL granted))completion;
```

## 追踪权限（ATT）
导入头文件
```objc
#import <EPSDK/EPDeviceUtils+Tracking.h>
```
设置``info.plist``添加``NSUserTrackingUsageDescription``
1. 追踪权限是否可用
```objc
/// 追踪权限是否可用
/// - Parameter directRequest: 是否直接请求
+ (BOOL)trackingAuthorizationEnable:(BOOL)directRequest;
```
2. 请求追踪权限授权
```objc
/// 请求用户授权追踪权限
/// - Parameters:
///   - directRequest: 是否直接请求
///   - completion: 完成回调Block，granted是否同意
+ (void)requestTrackingAuthorization:(BOOL)directRequest completion:(void (^)(BOOL granted))completion;
```



