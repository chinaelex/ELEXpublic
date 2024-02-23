# ELEX中台客服模块
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
  pod 'EPSDK_AIHelp'
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
 "aiHelp": {
    "appKey": "xxxx",
    "domain": "xxxx",
    "appId": "xxxx",
  }
```

- aiHelp:AIHelp配置
	- appKey:AIHelp分配的APP KEY
	- domain:AIHelp分配的APP DOMAIN
	- appId:AIHelp分配的APP ID

### 打开客服页面
```objc
/// EPSDK 客服拓展
@interface EPSDK(CustomService)

/**
 显示客服页面
@param params 客服平台参数
e.g.
 AIHelp: entranceId,welcomeMessage
*/
- (BOOL)showCustomServicePageWithParams:(nullable NSDictionary *)params;

@end

```

