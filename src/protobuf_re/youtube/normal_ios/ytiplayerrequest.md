# YTIPlayerRequest

TODO：

* 【未解决】研究YouTube逻辑：YTIPlayerRequest的descriptor
* 【未解决】研究YouTube逻辑：YTIPlayerRequest的context的protobuf的number不一致
* 【已解决】研究YouTube逻辑：通过GPBFieldDescriptor调试出YTIPlayerRequest的protobuf的属性字段定义

---

推导出`YTIPlayerRequest`的`protobuf`的字段定义，大概类似于：

```c
message YTIPlayerRequest {
    YTIInnerTubeContext *context = 1;
    NSString *videoId = 2;
    _Bool contentCheckOk = 3;
    YTIPlaybackContext *playbackContext = 4;
    _Bool racyCheckOk = 5;
    NSString *id_p = 6;
    NSString *t = 7;
    _Bool forOffline = 8;
    NSString *playlistId = 9;
    int playlistIndex = 10;
    unsigned int startTimeSecs = 11;
    NSString *params = 12;
    ??? = 13;
    NSData *offlineSharingWrappedKey = 14;
    GPBInt32Array *installedSharingServiceIdsArray = 15;
    YTIPlayerAttestationRequestData *attestationRequest = 16;
    NSString *referringApp = 17;
    NSString *referrer = 18;
    NSString *serializedThirdPartyEmbedConfig = 19;
    _Bool proxiedByOnesie = 20;
    ??? = 21;
    NSString *hostAppToken = 22;
    NSString *cpn = 23;
    ??? = 24;
    _Bool overrideMutedAtStart = 25;
    YTIPlayerRequestCaptionParams *captionParams = 26;
    ??? = 27;
    YTIPlayerRequestVideoQualitySettingParams *videoQualitySettingParams = 28;
}
```
