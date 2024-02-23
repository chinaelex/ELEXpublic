# ELEX中台埋点模块
![Objective-C](https://img.shields.io/badge/Objective--C-blue.svg?style=flat)
![Platform](https://img.shields.io/badge/platform-iOS-A1A1A1?style=flat)
![Region](https://img.shields.io/badge/region-CN_|_Oversea-green.svg?style=flat)
![version](https://img.shields.io/badge/iOS-12.0-orange.svg?style=flat)

# Requirements

- iOS 12.0+
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
  pod 'EPTrackSDK'
# elex埋点（可选）
  pod 'EPTrackSDK_ElexData'
#af埋点（可选）
  pod 'EPTrackSDK_AppsFlyer'
#firebase埋点（可选）
  pod 'EPTrackSDK_Firebase'
#facebook埋点（可选,ios12.0）
  pod 'EPTrackSDK_Facebook'
end
```
Then, run the following command:

```bash
$ pod install
```

# 接入
## 配置
SDKConfig_iOS.json文件添加配置参数
```json
  "appsFlyer": {
    "devKey": "xxxx"
  },
  "bi": {
    "appId": "xxxxxxxx",
    "url": "xxxxxx",
    "publicKey":"xxxx",
    "publicKeyVersion": 1
  },
```
- appsFlyer: AppsFlyer配置
	- devKey: AppsFlyer dev key
- bi: Elex自研埋点配置
	- appId: Elex埋点分配的APP ID
	- url:接收端地址
	- publicKey:公钥
	- publicKeyVersion: 密钥版本号

Note：Firebase和Facebook配置同账号模块

##埋点平台枚举
```objc
/** 
 * 打点平台类型
 */
typedef NS_ENUM(NSInteger , EPTrackPlatformType) {
    /** 默认值,不上报任何平台*/
    EPTrackPlatformTypeDefault,
    /** Facebook  */
    EPTrackPlatformTypeFacebook = 1,
    /** FireBase */
    EPTrackPlatformTypeFirebase = 2,
    /** AppsFlyer */
    EPTrackPlatformTypeAppsflyer = 3,
    /** Adjust */
    EPTrackPlatformTypeAdjust = 4,
    /** ElexData */
    EPTrackPlatformTypeElexData = 5,
};

```
## 埋点上报
### 接口
```objc
/**
 上报埋点
 
 此方法上报到接入的所有平台，埋点平台接入使用cocoapods接入；
 
 @param eventName 事件名称
 @param pPayload 上报参数
*/
- (void)reportEvent:(NSString *)eventName payload:(nullable NSDictionary *)pPayload;

```

## 埋点上报到指定平台
**<font color = red>对应埋点平台插件需要接入</font>**
### 接口
```objc
/**
 上报埋点到指定平台

 @param pType 埋点平台
 @param pName 事件名称
 @param pPayload 上报参数
*/
- (void)reportEventWithPlatformType:(EPTrackPlatformType)pType eventName:(NSString *)pName payload:(nullable NSDictionary *)pPayload;
```

## 获取埋点平台参数
### 接口
```objc
/**
 获取上报参数
 @param pType 埋点平台
*/
- (nullable NSDictionary *)getReportAttributesForPlatformType:(EPTrackPlatformType)pType;

```
