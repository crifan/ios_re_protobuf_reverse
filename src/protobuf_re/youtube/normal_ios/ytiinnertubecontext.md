# YTIInnerTubeContext

TODO：

* 【未解决】研究YouTube逻辑：从OnesieRequestProto子属性类型YTIInnerTubeContext找到生成data的机制

## `YTIInnerTubeContext`类的头文件定义

`header_ModuleFramework/YTIInnerTubeContext.h`

```c
//
//     Generated by class-dump 3.5 (64 bit) (Debug version compiled Sep 17 2017 16:24:48).
//
//     class-dump is Copyright (C) 1997-1998, 2000-2001, 2004-2015 by Steve Nygard.
//

#import <Module_Framework/GPBMessage.h>

@class NSMutableArray, NSString, YTIAdSignalsInfo, YTICapabilityInfo, YTIClickTrackingInfo, YTIClientInfo, YTIExperimentalData, YTIRequestInfo, YTIThirdPartyInfo, YTIUserInfo;

@interface YTIInnerTubeContext : GPBMessage
{
}

+ (id)descriptor;

// Remaining properties
@property(retain, nonatomic) NSMutableArray *activePlayersArray; // @dynamic activePlayersArray;
@property(readonly, nonatomic) unsigned long long activePlayersArray_Count; // @dynamic activePlayersArray_Count;
@property(retain, nonatomic) YTIAdSignalsInfo *adSignalsInfo; // @dynamic adSignalsInfo;
@property(retain, nonatomic) YTICapabilityInfo *capabilities; // @dynamic capabilities;
@property(retain, nonatomic) YTIClickTrackingInfo *clickTracking; // @dynamic clickTracking;
@property(retain, nonatomic) YTIClientInfo *client; // @dynamic client;
@property(copy, nonatomic) NSString *clientScreenNonce; // @dynamic clientScreenNonce;
@property(retain, nonatomic) YTIExperimentalData *experimentalData; // @dynamic experimentalData;
@property(nonatomic) _Bool hasAdSignalsInfo; // @dynamic hasAdSignalsInfo;
@property(nonatomic) _Bool hasCapabilities; // @dynamic hasCapabilities;
@property(nonatomic) _Bool hasClickTracking; // @dynamic hasClickTracking;
@property(nonatomic) _Bool hasClient; // @dynamic hasClient;
@property(nonatomic) _Bool hasClientScreenNonce; // @dynamic hasClientScreenNonce;
@property(nonatomic) _Bool hasExperimentalData; // @dynamic hasExperimentalData;
@property(nonatomic) _Bool hasRemoteClient; // @dynamic hasRemoteClient;
@property(nonatomic) _Bool hasRequest; // @dynamic hasRequest;
@property(nonatomic) _Bool hasThirdParty; // @dynamic hasThirdParty;
@property(nonatomic) _Bool hasUser; // @dynamic hasUser;
@property(retain, nonatomic) YTIClientInfo *remoteClient; // @dynamic remoteClient;
@property(retain, nonatomic) YTIRequestInfo *request; // @dynamic request;
@property(retain, nonatomic) YTIThirdPartyInfo *thirdParty; // @dynamic thirdParty;
@property(retain, nonatomic) YTIUserInfo *user; // @dynamic user;

@end
```
