# ELEX中台防沉迷模块

![Objective-C](https://img.shields.io/badge/Objective--C-blue.svg?style=flat)
![Platform](https://img.shields.io/badge/platform-iOS-A1A1A1?style=flat)
![Region](https://img.shields.io/badge/region-CN-green?style=flat)
![version](https://img.shields.io/badge/iOS-10.0-orange.svg?style=flat)

中台防沉迷插件,引入插件自动加载，开发同学不用处理；
> Note:防沉迷起作用依赖于两个因素;
>- 插件正常引入；
>- 国内渠道登录后返回实名信息；


## Requirements

- iOS 12.0+
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
  pod 'EPSDK_AntiAddict'
end
```
Then, run the following command:

```bash
$ pod install
```