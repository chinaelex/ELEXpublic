# elex sdk repo

![Objective-C](https://img.shields.io/badge/Objective--C-orange.svg?style=flat)
![Platform](https://img.shields.io/badge/platform-iOS-red.svg?style=flat)
![Region](https://img.shields.io/badge/region-CN_|_Oversea-green.svg?style=flat)
![version](https://img.shields.io/badge/iOS-10.0-orange.svg?style=flat)

ELEX中台 iOS SDK Cocoapods specifications.

## Features
- Account(账号)
- Pay(支付)
- Report(埋点上报)
- Jump(跳转)


### Account

- 手机号一键登录 ![CN](https://img.shields.io/badge/CN-green.svg?style=flat)
- 手机号验证码登录 ![CN](https://img.shields.io/badge/CN-green.svg?style=flat)
- 审核账号密码登录 ![CN](https://img.shields.io/badge/CN-green.svg?style=flat)
- 自动登录 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat)
- Apple登录 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat)
- 游客登录 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat)
- 邮箱登录 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat)
- Facebook登录 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat)
- Google登录 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat)

### Pay
- IAP内购 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat)
- SK2版本内购 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat) ![version](https://img.shields.io/badge/iOS-15.0-orange.svg?style=flat)

### Report
- ElexData自研埋点 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat)
- AppsFlyer埋点 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat)
- Facebook埋点 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat)
- Firebase埋点  ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat)

## Installing

EPSDK支持[CocoaPods](https://cocoapods.org)或手动接入，各个模块如无特殊说明，支持的最低系统版本为iOS10.0；
### CocoaPods
```ruby
platform :ios, '10.0'

target 'UnityFramework' do
  pod 'EPSDK'
end
```

<!-- -->### Install manually


## Account 接入

### 自动登录
```ruby
platform :ios, '10.0'

target 'UnityFramework' do
  pod 'EPSDK_Account'
end
```
#### Obj-C usage
```objc
[[EPSDK sharedSDK] loginWithType:EPLoginTypeAuto complition:^(NSError * _Nonnull error, EPAccount * _Nonnull account) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
 }];
```
#### C++ usage
``` C++
epsdkLogin(0)
```


### 游客登录
target 'UnityFramework' do
  pod 'EPSDK_Account'
end
```
#### Obj-C usage
```objc
[[EPSDK sharedSDK] loginWithType:EPLoginTypeGuest complition:^(NSError * _Nonnull error, EPAccount * _Nonnull account) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
 }];
```
#### C++ usage
``` C++
epsdkLogin(1)
```


### 手机号验证码登录 | 审核渠道账号密码登录 | 邮箱登录
```ruby
platform :ios, '10.0'

target 'UnityFramework' do
  pod 'EPSDK_Account_ElexPassport'
#(友盟登录可选)
  pod 'ElexPassport_UMeng'
end
```
#### Obj-C usage
```objc
[[EPSDK sharedSDK] loginWithType:EPLoginTypeChannel complition:^(NSError * _Nonnull error, EPAccount * _Nonnull account) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
 }];
```
#### C++ usage
``` C++
epsdkLogin(3)
```

==**手机号验证码登录和Umeng手机号一键登录都属于渠道登录，SDK会根据是否有Umeng登录插件和Umeng一键登录可用来判断使用Umeng一键登录还是手机号验证码登录**==

### Facebook登录 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat) ![version](https://img.shields.io/badge/iOS-12.0-orange.svg?style=flat)

```ruby
platform :ios, '12.0’

target 'UnityFramework' do
  pod 'EPSDK_Account_Facebook'
end
```

#### 配置info.plist
- FacebookAppID:xxxxxx
- FacebookAutoLogAppEventsEnabled:（YES ｜ NO）
- FacebookClientToken:xxxxxxx
- FacebookDisplayName:xxxx
添加URL Schemes
```xml
<key>LSApplicationQueriesSchemes</key>
<array>
     <string>fbauth2</string>
     <string>fbapi</string>
     <string>fb-messenger-share-api</string>
     <string>fb-messenger-api</string>
     <string>fbshareextension</string>
</array>
```
#### Obj-C usage
```objc
[[EPSDK sharedSDK] loginWithType:EPLoginTypeFacebook complition:^(NSError * _Nonnull error, EPAccount * _Nonnull account) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
 }];
```
#### C++ usage
``` C++
epsdkLogin(20)
```

### Google登录 ![Oversea](https://img.shields.io/badge/Oversea-green.svg?style=flat) 

```ruby
platform :ios, '10.0’

target 'UnityFramework' do
  pod 'EPSDK_Account_Google'
end
```
#### Obj-C usage
```objc
[[EPSDK sharedSDK] loginWithType:EPLoginTypeGoogle complition:^(NSError * _Nonnull error, EPAccount * _Nonnull account) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
 }];
```
#### C++ usage
``` C++
epsdkLogin(21)
```

### Apple登录 ![CN | Oversea](https://img.shields.io/badge/CN_|_Oversea-green.svg?style=flat) 

```ruby
platform :ios, '10.0’

target 'UnityFramework' do
  pod 'EPSDK_Account'
end
```
#### Obj-C usage
```objc
[[EPSDK sharedSDK] loginWithType:EPLoginTypeApple complition:^(NSError * _Nonnull error, EPAccount * _Nonnull account) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
 }];
```
#### C++ usage
``` C++
epsdkLogin(23)
```

## 放沉迷 ![CN](https://img.shields.io/badge/CN-green.svg?style=flat) 
```ruby
platform :ios, '10.0’

target 'UnityFramework' do
  pod 'EPSDK_AntiAddict'
end
```
==**防沉迷起作用依赖于两个因素，1.插件正常引入；2.国内渠道登录后返回实名信息；**==

## Pay
```ruby
platform :ios, '10.0’

target 'UnityFramework' do
  pod 'EPPay’
end
```
### 支付接口
#### Obj-C usage
```objc
/// 开始支付
/// - Parameters:
///   - payRequest: 支付请求，详情看EPPayRequest类
///   - completion: 完成回调；error：支付错误信息，成功时error为nil
- (void)pay:(EPPayRequest *)payRequest completion: (void (^)(NSError *_Nullable error))completion;
```

#### C++ usage
``` C++
/** 购买商品*/
void epsdkiapBuyProductInfo(const char *jsonString);

/**  支付接口*/
void epsdkPay(const char *product);
```


### 获取商品详情
```objc
/// 获取商品信息
/// - Parameters:
///   - productIds: 商品Id数组
///   - completion: 完成回调
- (void)getDetailOfProducts:(NSArray<NSString *> *)productIds completion:(void (^)(NSError * _Nullable error, NSArray<EPPayProduct *> * _Nullable productInfos))completion;
```
#### C++ usage
``` C++
/** 请求IAP内购产品信息*/
void epsdkiapRequestProductsFromAppleServer(const char *jsonString);
```

## 埋点
```ruby
platform :ios, '10.0’

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
#### Obj-C usage
```objc
/// 上报埋点
/// - Parameters:
///   - pType: 埋点平台
///   - pName: 事件名称
///   - pPayload: 上报参数
- (void)reportEventWithPlatformType:(EPTrackPlatformType)pType eventName:(NSString *)pName payload:(nullable NSDictionary *)pPayload;

/// 上报埋点，上报到接入的所有平台
/// - Parameters:
///   - eventName: 事件名称
///   - pPayload: 上报参数
- (void)reportEvent:(NSString *)eventName payload:(nullable NSDictionary *)pPayload;


/// 获取上报参数
/// - Parameter pType: 埋点平台
- (nullable NSDictionary *)getReportAttributesForPlatformType:(EPTrackPlatformType)pType;
```

#### C++ usage
``` C++
/// 埋点接口
/// - Parameters:
///   - eventName: 事件名称
///   - payload: 埋点参数json字符串
void epsdkTrack(const char *eventName, const char *payload);

/// 打点接口
/// - Parameters:
///   - platformType: 埋点平台
///   - eventName: 事件名称
///   - payload: 埋点参数json字符串
void epsdkTrackEvent(int platformType, const char *eventName, const char *payload);

/** 获取 AppsFlyer属性*/
    const char *epsdkAppsFlyerAttrs(void);
```

## 跳转

#### Obj-C usage
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
```objc
/// EPSDK跳转错误码
typedef NS_ENUM(NSInteger,EPSDKJumpErrorCode) {
    EPSDKJumpErrorCodeCancel = -10000,
    EPSDKJumpErrorCodeURLInvalid = -10001,
    EPSDKJumpErrorCodeNotSupport = -10002,
    EPSDKJumpErrorCodeReviewCountLimit = -10003,
};
```

## MARK
==**EPSDK使用cocoapods方式接入，在unity2019之后的版本，unity统一导出UnityFramework.framework,SDK需要接入到framework中，需要在Podfile中修改SDK的target的依赖。**==

```ruby
post_install do |installer|
    handle_mainTarget('Pods-Unity-iPhone', installer)
end

def find_line_with_start(str, start)
    str.each_line do |line|
        if line.start_with?(start)
            return line
        end
    end
    return nil
end

def handle_mainTarget(name, installer)
    installer.pods_project.targets.each do |target|
        if target.name != name
            next
        end
        target.build_configurations.each do |config|
            xcconfig_path = config.base_configuration_reference.real_path
            xcconfig = File.read(xcconfig_path)
            old_line = find_line_with_start(xcconfig, "OTHER_LDFLAGS")
        
            if old_line == nil
                next
            end
            new_line = "OTHER_LDFLAGS = $(inherited) -ObjC\n"
      
            new_xcconfig = xcconfig.sub(old_line, new_line)
            File.open(xcconfig_path, "w") { |file| file << new_xcconfig }
        end
    end
end
```