# ELEX中台支付模块

![Objective-C](https://img.shields.io/badge/Objective--C-blue.svg?style=flat)
![Swift-5](https://img.shields.io/badge/Swift-5-red.svg?style=flat)
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
  pod 'EPPay'
end
```
Then, run the following command:

```bash
$ pod install
```

# 接入
导入头文件
```objc
#import <EPPay/EPPay.h>
```
## 获取商品详情
### 接口:
```objc
/// 获取商品信息
/// - Parameters:
///   - productIds: 商品Id数组
///   - completion: 完成回调
- (void)getDetailOfProducts:(NSArray<NSString *> *)productIds completion:(void (^)(NSError * _Nullable error, NSArray<EPPayProduct *> * _Nullable productInfos))completion;
```
### 商品信息详情:
```objc
@interface EPPayProduct : NSObject

/// 商品id（app store）
@property (nonatomic, copy) NSString *productId;

/// 商品名称
@property (nonatomic, copy, nullable) NSString *productName;

/// 商品描述
@property (nonatomic, copy, nullable) NSString *productDescription;

/// 商品类型（使用storekit2接口可用）
@property (nonatomic, assign) EPProductType productType;

/// 商品价格字符串（格式为 ---> CNY¥12）
@property (nonatomic, copy) NSString *formattedPrice;

/// 商品价格数字（格式为 ---> 12.34）
@property (nonatomic, strong) NSNumber *amount;

/// 货币名称缩写
@property (nonatomic, copy) NSString *currency;

/// 微单位商品价格数字（以微单位返回价格，其中 1,000,000 微单位等于 1 个货币单位）
@property (nonatomic, strong) NSNumber *micros_price;

/// 订阅周期，iOS11.2以上系统能获取到
@property (nonatomic, strong, nullable) EPPayProductSubscriptionPeriod *subscriptionPeriod;

/// 推介促销优惠
@property (nonatomic, strong, nullable) EPPayProductDiscount *introductoryPrice;
/// 是否符合优惠条件
@property (nonatomic, assign) BOOL isEligibleForIntroOffer;

@end
```

### 商品类型:
```objc
/** 
 *商品类型
 *app store商品类型
*/
typedef NS_ENUM(NSInteger,EPProductType) {
    /**类型未知*/
    EPProductTypeUnknown = -1,
    /**消耗型**/
    EPProductTypeConsumable = 0,
    /**非消耗型**/
    EPProductTypeNonConsumable,
    /**自动订阅型**/
    EPProductTypeAutoRenewable,
    /**非自动订阅型**/
    EPProductTypeNonRenewable,
};
```
示例:
```objc
NSArray<NSString *> *arrProductId;
[[EPPay pay] getDetailOfProducts:arrProductId completion:^(NSError * _Nullable error, NSArray<EPPayProduct *> * _Nullable productInfos) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
}];
```
## 支付购买
### 接口
```objc
/// 开始支付
///
/// ``` Objective-C
/// EPPayRequest *request;
/// [[EPPay pay] pay:request completion:^(NSError * _Nonnull error) {
///     if(error){
///          //处理失败
///     }else {
///         //处理成功
///     }
/// }];
/// ```
/// - Parameters:
///   - payRequest: 支付请求，详情看EPPayRequest类
///   - completion: 完成回调；error：支付错误信息，成功时error为nil
- (void)pay:(EPPayRequest *)payRequest completion: (void (^)(NSError *_Nullable error))completion;
```
### 购买请求
```objc
@interface EPPayRequest : NSObject

/// 商品id（app store）
@property (nonatomic, copy, readonly) NSString *productId;

/// 购买数量,默认1
@property (nonatomic, assign, readonly) NSInteger quantity;

/// 透传参数
@property (nonatomic, copy, readonly, nullable) NSString *payload;

/// 通知游戏的URL,空值默认使用配置地址
@property (nonatomic, copy, readonly, nullable) NSString *notifyUrl;

@end

```
示例
```objc
EPPayRequest *request;
[[EPPay pay] pay:request completion:^(NSError * _Nonnull error) {
    if(error){
    //处理失败
    }else{
    //处理登录成功
    }
}];
```

# 错误码

|  错误码  |       说明       |
| :-----: | :--------------: |
| 52000 | 未知错误 |
| 52001 | SDK未登录(未进入游戏) |
| 52002 | 商品列表为空 |
| 52003 | 本地化商品失败（未使用，对其安卓） |
| 52004 | *app store没有此产品 |
| 52005 | 插入订单失败（未使用，对其安卓） |
| 52006 | 已经购买（未使用，对其安卓）|
| 52007 | 用户取消支付 |
| 52008 | 支付失败 |
| 52009 | 当前正在进行支付 |
| 52010 | 设备不允许支付 |
| 52011 | 无效的产品 |
| 52012 | 当前正在补单 |
| 52013 | SDK下单失败 |
| 52014 | 创建UUID订单错误 |
| 12011 | 支付限制 |
| 14001 | 订单状态错误（sdk内未使用） |
| 14003 | 订单不存在 |
| 14004 | 订单票据验证失败,票据在到商店验证未通过 |
| 14005 | Payment后台商店配置不存在，（订单验证key等 |
