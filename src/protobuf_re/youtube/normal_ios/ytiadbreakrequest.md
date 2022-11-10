# YTIAdBreakRequest

TODO：

* 【已解决】研究YouTube逻辑：从data解析出YTIAdBreakRequest所有的字段属性的值
* 【未解决】研究YouTube逻辑：获取YTIAdBreakRequest所有的字段的定义即name和number映射关系
* 【已解决】研究YouTube逻辑：protobuf类YTIAdBreakRequest

---

## 从data解码反序列化出YTIAdBreakRequest的protobuf的json字符串数据

想要从protobuf的类YTIAdBreakRequest序列化后的NSData数据data，去解析出：

对应的所有属性的值，包括嵌套的子属性的值

思路是：

`YTIAdBreakRequest`的基类=父类是`GPBMessage`，其中有Class级别的函数：

```objc
+ (id)parseFromData:(id)arg1;
```

所以可以直接拿来解析。

具体写法：

```bash
po [objc_getClass("YTIAdBreakRequest") parseFromData: newHttpBodyData]
```

即可得到：

整个protobuf类YTIAdBreakRequest的所有属性的值，包括嵌套的属性。


举例：

* 输入：二进制的data

```bash
(lldb) po newHttpBodyData
<0ab3160a 9b120a05 7a682d43 4e120243 4e520243 4e620541 70706c65 6a096950 686f6e65 392c3180 01058a01 0731372e 30382e32 92010369 4f539a01 0c31332e 332e312e 31374435 30a802f7 02b0029b 05c80202 f00201b8 03f702c0 039b05e8 0303f203 830e0ab8 04434d61 5a714a6f 47454f72 4b726755 51714d2d 6f467844 55673634 46455065 49726755 5134726d 75425244 53334b30 46454f71 64725155 516d6361 75425244 466d7134 46454d61 46725155 516c3943 75425243 44304b34 4645496a 70725155 51754975 75425244 74697130 46454b58 76725155 51326275 74425243 476f6134 46454f62 4e726755 516c4d2d 75425244 726d6130 4645497a 79725155 51703532 75425244 586b6130 46454a6a 55725155 51786232 75425243 43746134 46454f54 4b726755 51676357 74425244 667a7134 46454d65 78725155 51324c79 75425244 58396130 46454e76 4b726755 51373869 75425244 716c3677 4645496d 78726755 51676269 75425244 377a7134 46454a61 61725155 516d7236 75425244 316c7134 46454947 47726755 51305f47 74425243 626f4b34 46454b48 39725155 516f4c6d 75425244 4e344b30 46454a50 51726755 516e7632 74425244 72354b30 46454961 31726755 51367271 74425243 47793634 46454f54 4e726755 51394d65 74425243 6c734b34 46476a4a 42533342 6c5a4768 35545456 30566b4e 31515739 32633031 54556d52 75616a64 69624638 30526d68 454e6d70 4d576e5a 55593245 35525852 534f4768 47566b52 52515349 79515574 775a5752 6f655530 3164465a 44645546 76646e4e 4e55314a 6b626d6f 33596d78 664e455a 6f52445a 71544670 3256474e 684f5556 30556a68 6f526c5a 45555545 7147454e 4254564e 45515442 454e6b30 74634546 6f565551 3464444e 59524545 39505125 33442533 441adc04 434a5077 73706f47 45684d79 4f544134 4d544977 4e44677a 4e546b78 4e546b33 4e545530 474d615a 714a6f47 4b4a6e47 7267556f 7a654374 42536947 74613446 4b4f544b 7267556f 6a504b74 42536a30 78363046 4b4b5777 7267556f 35733275 42536a5a 75363046 4b4a7567 7267556f 6f4c6d75 42536a72 6d613046 4b4a5450 7267556f 67394375 42536961 76713446 4b4c694c 7267556f 6c394375 42536949 36613046 4b4e6938 7267556f 36703274 42536a31 6c713446 4b4e5344 7267556f 36706573 42536942 754b3446 4b4f724b 7267556f 39346975 4253696f 7a366758 4b496d78 7267556f 78623275 42536a6b 7a613446 4b4e6552 7251556f 68737575 4253696e 6e613446 4b4a5051 7267556f 36727174 42536943 74613446 4b494846 7251556f 6f663274 42536947 6f613446 4b4e5078 7251556f 37597174 42536965 5f613046 4b4a6a55 7251556f 6c707174 42536a47 68613046 4b494747 7267556f 70652d74 42536a53 334b3046 4b4e6631 7251556f 78374774 42536a46 6d713446 4b50764f 7267556f 37386975 42536a62 79713446 4b4e5f4f 7267556f 34726d75 42536a72 354b3046 4d6a4a42 5333426c 5a476835 54545630 566b4e31 51573932 63303154 556d5275 616a6469 62463830 526d6845 4e6d704d 576e5a55 59324535 52585253 4f476847 566b5252 51546f79 51557477 5a57526f 65553031 64465a44 64554676 646e4e4e 55314a6b 626d6f33 596d7866 4e455a6f 52445a71 54467032 56474e68 4f555630 556a686f 526c5a45 55554643 47454e42 54564e45 51544245 4e6b3074 6345466f 56555134 64444e59 52454539 50512533 44253344 2ae60443 4a507773 706f4745 6851784e 4449774f 544d354e 7a41784e 6a417a4f 4467334e 5445784d 52695438 4c4b6142 69697969 5034534b 4c7a4b5f 52496f33 347a2d45 69694167 7634534b 4f32455f 68496f38 395f3945 696a4c72 6630534b 4c364a5f 68496f31 594c2d45 69695369 7634534b 4972675f 52496f33 6f332d45 696a4a68 5034534b 4b54455f 52496f6e 34662d45 69694138 5f30534b 4d482d5f 52496f70 64443945 69695535 5077534b 4f4b5f5f 52496f67 594c3945 6969506a 5034534b 4e50655f 52496f6c 50443945 696a4b68 5f34534b 4d574f5f 68496f35 59442d45 696a4a2d 6630534b 4e47665f 52496f35 344c2d45 696a3533 7630534b 4f69435f 68496f33 4f443945 696a6872 5030534b 4e4c4c5f 52496f6e 765f3845 696a626b 5f30534b 4e794b5f 68496f77 49502d45 69693933 7630534b 5032735f 52496f79 2d7a3945 696a6267 5034534b 4b66385f 52496f71 72543945 696a4773 7630534b 4b6d715f 52496f6d 63623945 69693876 7630534b 4a764d5f 52496f2d 49762d45 696a4f77 5030534b 4965435f 68496f6a 34582d45 69693539 6677534b 4e664d5f 52496f68 617a3945 696a4b32 5030534d 6a4a4253 33426c5a 47683554 54563056 6b4e3151 57393263 30315455 6d527561 6a646962 46383052 6d68454e 6d704d57 6e5a5559 32453552 5852534f 47684756 6b525251 546f7951 5574775a 57526f65 55303164 465a4464 55467664 6e4e4e55 314a6b62 6d6f3359 6d78664e 455a6f52 445a7154 46703256 474e684f 55563055 6a686f52 6c5a4555 55464348 454e4254 564e4655 54424362 33526d4e 6b5a6164 33424755 55526b65 6a684a54 57356a64 30552533 448d0400 00004098 04e003f0 04018205 0d417369 612f5368 616e6768 6169a205 800320e5 89ffcfd9 ab8cfb92 012083f8 d594f8d8 aed25620 d5c1ccf7 9387d7fb 5520be84 878c8afe f0c4e701 20d9dd90 cccc848f f3800120 dade94fc aaacb990 5920c6ba 9597b4f9 c9b36120 86f2abaa 94cfaeed 2020c5c5 9488cddf ff879a01 20e2a1c0 b0e6df97 f22f209d a1cda588 d4fcf07e 20fd8ec3 a2f8c5c3 d00320d9 a899e6ad 94dbf91f 2095a5f6 cd83f3ff 9a1420dc ed99fce2 cfde93da 0120b498 bdc8c3a4 afbf1620 bddb83b1 f5dec6dd a20120c2 e7f8d890 f0cbca01 209ef581 908fd7bd bef70120 c0c688a7 fed0b3c1 3920a1ce fedfe18e a0e2bc01 20d286fb 98a2dfbd 970120f5 9a87c58d 92ced72d 20849ea7 c3be8fe4 db1620ed b4d3d3cb fee8dd1d 20c1cf86 ddb6ed98 f14b20e4 fbcc81c1 8d9d955e 2085dde5 94bcb799 fdb40120 fee8cccf 8a8df480 2c20a182 e5f2e282 81b80d20 848ad3ec 8ddcdc9f 252094ac f5959abb b6c28501 20e7ae92 eee6f1ea b6c90120 b7dbd39a f0f385e5 81012080 cf84abe7 bd9cb666 20a0af89 f7f0d4b3 edc10120 868099e5 d8a7b3ec d801f805 b1908001 8a060608 0110bd90 589a0605 0a034348 4e1a002a a101d201 9d010a97 01415041 52386e75 42734548 57666268 4d635f37 71627344 5a697352 68544f33 65745849 526a4b42 327a7673 516c396f 5f41764c 58647245 73316939 31417663 574a6a4a 646d4254 43613245 5a47765a 78677052 67525547 50535961 6b4a6166 73367067 4e38796a 746e3658 7354466b 50567865 6c5f474b 70306b65 33676245 582d6738 437a3057 72776d5f 6a666735 46376a59 33523530 10d8044a e0020add 020a026d 7312d602 6e4b496e 4f44696b 50625735 6e5a4437 2d6f7256 7773434e 44566759 536b6148 36454758 776d5f50 6c414b4b 47535659 51564854 6377335f 58655049 72456278 42545272 6d563355 55485457 462d4d52 4c446d64 35493950 67377631 5561336f 324d6a2d 42376242 6e457a4b 5064666e 46344471 4f585a77 41695f30 5a512d76 79556348 526b586d 7444484f 38625166 74465452 56746c79 596f6a75 74554439 634d4b66 47723741 2d416675 7558304c 755f7a78 2d35724e 6a4c6372 306a4a6b 31705266 6c4c794e 7a7a4262 5f782d71 5f6b3442 4b367438 346f6f6c 5779624c 43567463 6a536774 6a7a4d34 50485139 33307448 7752795f 4a34466a 31525f7a 4b696b4a 59507a6c 544a5051 4e525049 6b43716e 766d7339 4b4e3875 4e704839 7a775130 6d756746 75564e50 4f476168 4f436255 62585077 4d43626d 5f667878 335f5935 54427631 68346e7a 6e613850 6e436c70 6367620a 0a084341 45534167 674312f7 02414d75 79323937 6d4f7158 3242787a 4f724b79 676b4973 59644448 6b4c6947 5f417972 53305975 6334486e 6c73596d 6a373557 42484c62 484e374a 5f496744 48647862 476a4452 4e326c71 46395476 35444456 57514a69 35437a38 5553525f 7a524a53 7345392d 4e50594b 51353671 5f305776 6e4f646f 724e326b 31414346 774c3545 6654584e 69767268 634e4e30 31687965 33766168 524a7833 774d364b 4a465534 5f4c6364 6b647863 3363764a 6b537478 33302d63 5a59716d 746a6451 7a7a4d6c 6b4f5771 664b5a79 5a734e36 56526e2d 612d5a67 64623370 7137726a 62414c55 486e7839 5f56686d 42304362 58344a6e 44616f68 4f644b4d 71306278 54594f72 46394b73 3274704a 7964454f 3030534f 496a7270 705f4563 53693578 62434e65 64525147 58393667 6f414635 63443777 766b4146 46544475 3166414a 506e484e 46705335 68375f48 72553730 596d446d 7a717647 724c564c 76347a45 30625f62 766c7043 76516853 43443731 44496c39 32356341 18a0d119 20012a48 0a462097 032889e5 18300038 03400048 00580062 2d766964 656f5f66 6f726d61 743d3232 2673646b 763d692e 31372e30 38266f75 74707574 3d786d6c 5f766173 7432e801 00e80203 32104b4b 61304879 4471544d 30533961 3641>
```

* 解析

```bash
po [objc_getClass("YTIAdBreakRequest") parseFromData: newHttpBodyData]
```

* 输出：json格式的Protobuf数据

```json
(lldb) po [objc_getClass("YTIAdBreakRequest") parseFromData: newHttpBodyData]
2022-10-17 11:43:58.552972+0800 YouTube[21038:2204921] hook_ youtubeReqResp.xm YTIInnerTubeContext$descriptor: curDesc=<GPBDescriptor: 0x2803e7a40>
2022-10-17 11:43:58.553697+0800 YouTube[21038:2204921] hook_ youtubeReqResp.xm YTIInnerTubeContext$descriptor: curDesc=<GPBDescriptor: 0x2803e7a40>
2022-10-17 11:43:58.713094+0800 YouTube[21038:2204921] hook_ youtubeReqResp.xm YTIInnerTubeContext$descriptor: curDesc=<GPBDescriptor: 0x2803e7a40>
<YTIAdBreakRequest 0x286120d20>: {
    context {
      client {
        hl: "zh-CN"
        gl: "CN"
        carrier_geo: "CN"
        device_make: "Apple"
        device_model: "iPhone9,1"
        client_name: IOS
        client_version: "17.08.2"
        os_name: "iOS"
        os_version: "13.3.1.17D50"
        screen_width_points: 375
        screen_height_points: 667
        screen_pixel_density: 2
        client_form_factor: SMALL_FORM_FACTOR
        window_width_points: 375
        window_height_points: 667
        connection_type: CONN_WIFI
        config_info {
          cold_config_data: "CMaZqJoGEOrKrgUQqM-oFxDUg64FEPeIrgUQ4rmuBRDS3K0FEOqdrQUQmcauBRDFmq4FEMaFrQUQl9CuBRCD0K4FEIjprQUQuIuuBRDtiq0FEKXvrQUQ2butBRCGoa4FEObNrgUQlM-uBRDrma0FEIzyrQUQp52uBRDXka0FEJjUrQUQxb2uBRCCta4FEOTKrgUQgcWtBRDfzq4FEMexrQUQ2LyuBRDX9a0FENvKrgUQ78iuBRDql6wFEImxrgUQgbiuBRD7zq4FEJaarQUQmr6uBRD1lq4FEIGGrgUQ0_GtBRCboK4FEKH9rQUQoLmuBRDN4K0FEJPQrgUQnv2tBRDr5K0FEIa1rgUQ6rqtBRCGy64FEOTNrgUQ9MetBRClsK4FGjJBS3BlZGh5TTV0VkN1QW92c01TUmRuajdibF80RmhENmpMWnZUY2E5RXRSOGhGVkRRQSIyQUtwZWRoeU01dFZDdUFvdnNNU1Jkbmo3YmxfNEZoRDZqTFp2VGNhOUV0UjhoRlZEUUEqGENBTVNEQTBENk0tcEFoVUQ4dDNYREE9PQ%3D%3D"
          cold_hash_data: "CJPwspoGEhMyOTA4MTIwNDgzNTkxNTk3NTU0GMaZqJoGKJnGrgUozeCtBSiGta4FKOTKrgUojPKtBSj0x60FKKWwrgUo5s2uBSjZu60FKJugrgUooLmuBSjrma0FKJTPrgUog9CuBSiavq4FKLiLrgUol9CuBSiI6a0FKNi8rgUo6p2tBSj1lq4FKNSDrgUo6pesBSiBuK4FKOrKrgUo94iuBSioz6gXKImxrgUoxb2uBSjkza4FKNeRrQUohsuuBSinna4FKJPQrgUo6rqtBSiCta4FKIHFrQUoof2tBSiGoa4FKNPxrQUo7YqtBSie_a0FKJjUrQUolpqtBSjGha0FKIGGrgUope-tBSjS3K0FKNf1rQUox7GtBSjFmq4FKPvOrgUo78iuBSjbyq4FKN_OrgUo4rmuBSjr5K0FMjJBS3BlZGh5TTV0VkN1QW92c01TUmRuajdibF80RmhENmpMWnZUY2E5RXRSOGhGVkRRQToyQUtwZWRoeU01dFZDdUFvdnNNU1Jkbmo3YmxfNEZoRDZqTFp2VGNhOUV0UjhoRlZEUUFCGENBTVNEQTBENk0tcEFoVUQ4dDNYREE9PQ%3D%3D"
          hot_hash_data: "CJPwspoGEhQxNDIwOTM5NzAxNjAzODg3NTExMRiT8LKaBiiyiP4SKLzK_RIo34z-EiiAgv4SKO2E_hIo89_9EijLrf0SKL6J_hIo1YL-EiiSiv4SKIrg_RIo3o3-EijJhP4SKKTE_RIon4f-EiiA8_0SKMH-_RIopdD9EiiU5PwSKOK__RIogYL9EiiPjP4SKNPe_RIolPD9EijKh_4SKMWO_hIo5YD-EijJ-f0SKNGf_RIo54L-Eij53v0SKOiC_hIo3OD9EijhrP0SKNLL_RIonv_8Eijbk_0SKNyK_hIowIP-Eii93v0SKP2s_RIoy-z9EijbgP4SKKf8_RIoqrT9EijGsv0SKKmq_RIomcb9Eii8vv0SKJvM_RIo-Iv-EijOwP0SKIeC_hIoj4X-Eii59fwSKNfM_RIohaz9EijK2P0SMjJBS3BlZGh5TTV0VkN1QW92c01TUmRuajdibF80RmhENmpMWnZUY2E5RXRSOGhGVkRRQToyQUtwZWRoeU01dFZDdUFvdnNNU1Jkbmo3YmxfNEZoRDZqTFp2VGNhOUV0UjhoRlZEUUFCHENBTVNFUTBCb3RmNkZad3BGUURkejhJTW5jd0U%3D"
        }
        screen_density_float: 2
        utc_offset_minutes: 480
        user_interface_theme: USER_INTERFACE_THEME_LIGHT
        time_zone: "Asia/Shanghai"
        eml_template_context: " \345\211\377\317\331\253\214\373\222\001 \203\370\325\224\370\330\256\322V \325\301\314\367\223\207\327\373U \276\204\207\214\212\376\360\304\347\001 \331\335\220\314\314\204\217\363\200\001 \332\336\224\374\252\254\271\220Y \306\272\225\227\264\371\311\263a \206\362\253\252\224\317\256\355  \305\305\224\210\315\337\377\207\232\001 \342\241\300\260\346\337\227\362/ \235\241\315\245\210\324\374\360~ \375\216\303\242\370\305\303\320\003 \331\250\231\346\255\224\333\371\037 \225\245\366\315\203\363\377\232\024 \334\355\231\374\342\317\336\223\332\001 \264\230\275\310\303\244\257\277\026 \275\333\203\261\365\336\306\335\242\001 \302\347\370\330\220\360\313\312\001 \236\365\201\220\217\327\275\276\367\001 \300\306\210\247\376\320\263\3019 \241\316\376\337\341\216\240\342\274\001 \322\206\373\230\242\337\275\227\001 \365\232\207\305\215\222\316\327- \204\236\247\303\276\217\344\333\026 \355\264\323\323\313\376\350\335\035 \301\317\206\335\266\355\230\361K \344\373\314\201\301\215\235\225^ \205\335\345\224\274\267\231\375\264\001 \376\350\314\317\212\215\364\200, \241\202\345\362\342\202\201\270\r \204\212\323\354\215\334\334\237% \224\254\365\225\232\273\266\302\205\001 \347\256\222\356\346\361\352\266\311\001 \267\333\323\232\360\363\205\345\201\001 \200\317\204\253\347\275\234\266f \240\257\211\367\360\324\263\355\301\001 \206\200\231\345\330\247\263\354\330\001"
        memory_total_kbytes: 2099249
        notification_permission_info {
          notifications_setting: NOTIFICATIONS_SETTING_ENABLED
          last_device_opt_in_change_time_ago_sec: 1443901
        }
        client_store_info {
          ios_store_country: "CHN"
        }
      }
      user {
      }
      request {
        consistency_token_jars {
          encrypted_token_jar_contents: "APAR8nuBsEHWfbhMc_7qbsDZisRhTO3etXIRjKB2zvsQl9o_AvLXdrEs1i91AvcWJjJdmBTCa2EZGvZxgpRgRUGPSYakJafs6pgN8yjtn6XsTFkPVxel_GKp0ke3gbEX-g8Cz0Wrwm_jfg5F7jY3R50"
          expiration_seconds: 600
        }
      }
      ad_signals_info {
        params {
          key: "ms"
          value: "nKInODikPbW5nZD7-orVwsCNDVgYSkaH6EGXwm_PlAKKGSVYQVHTcw3_XePIrEbxBTRrmV3UUHTWF-MRLDmd5I9Pg7v1Ua3o2Mj-B7bBnEzKPdfnF4DqOXZwAi_0ZQ-vyUcHRkXmtDHO8bQftFTRVtlyYojutUD9cMKfGr7A-AfuuX0Lu_zx-5rNjLcr0jJk1pRflLyNzzBb_x-q_k4BK6t84oolWybLCVtcjSgtjzM4PHQ930tHwRy_J4Fj1R_zKikJYPzlTJPQNRPIkCqnvms9KN8uNpH9zwQ0mugFuVNPOGahOCbUbXPwMCbm_fxx3_Y5TBv1h4nzna8PnClpcg"
        }
      }
      active_players {
        player_context_params: "CAESAggC"
      }
    }
    params: "AMuy297mOqX2BxzOrKygkIsYdDHkLiG_AyrS0Yuc4HnlsYmj75WBHLbHN7J_IgDHdxbGjDRN2lqF9Tv5DDVWQJi5Cz8USR_zRJSsE9-NPYKQ56q_0WvnOdorN2k1ACFwL5EfTXNivrhcNN01hye3vahRJx3wM6KJFU4_Lcdkdxc3cvJkStx30-cZYqmtjdQzzMlkOWqfKZyZsN6VRn-a-Zgdb3pq7rjbALUHnx9_VhmB0CbX4JnDaohOdKMq0bxTYOrF9Ks2tpJydEO00SOIjrpp_EcSi5xbCNedRQGX96goAF5cD7wvkAFFTDu1fAJPnHNFpS5h7_HrU70YmDmzqvGrLVLv4zE0b_bvlpCvQhSCD71DIl925cA"
    break_position_ms: 420000
    break_index: 1
    override_playback_context {
      content_playback_context {
        time_since_last_ad_seconds: 407
        lact_milliseconds: 406153
        autoplays_since_last_ad: 0
        conn: 3
        vis: 0
        fling: false
        autoplay: false
        adsense_client_params: "video_format=22&sdkv=i.17.08&output=xml_vast2"
        autonav: false
        autonav_state: STATE_OFF
      }
    }
    client_playback_nonce: "KKa0HyDqTM0S9a6A"
}
```

## `YTIAdBreakRequest`类的头文件定义

`header_ModuleFramework/YTIAdBreakRequest.h`

```c
//
//     Generated by class-dump 3.5 (64 bit) (Debug version compiled Sep 17 2017 16:24:48).
//
//     class-dump is Copyright (C) 1997-1998, 2000-2001, 2004-2015 by Steve Nygard.
//

#import <Module_Framework/GPBMessage.h>

@class NSString, YTIInnerTubeContext, YTIPlaybackContext;

@interface YTIAdBreakRequest : GPBMessage
{
}

+ (id)descriptor;

// Remaining properties
@property(nonatomic) int adBlock; // @dynamic adBlock;
@property(nonatomic) int autonavState; // @dynamic autonavState;
@property(nonatomic) int breakIndex; // @dynamic breakIndex;
@property(nonatomic) unsigned long long breakLengthMs; // @dynamic breakLengthMs;
@property(nonatomic) long long breakPositionMs; // @dynamic breakPositionMs;
@property(copy, nonatomic) NSString *clientPlaybackNonce; // @dynamic clientPlaybackNonce;
@property(copy, nonatomic) NSString *clientSideAdTag; // @dynamic clientSideAdTag;
@property(retain, nonatomic) YTIInnerTubeContext *context; // @dynamic context;
@property(nonatomic) long long currentMediaTimeMs; // @dynamic currentMediaTimeMs;
@property(nonatomic) long long driftFromHeadMs; // @dynamic driftFromHeadMs;
@property(copy, nonatomic) NSString *encodedAdSafetyReason; // @dynamic encodedAdSafetyReason;
@property(copy, nonatomic) NSString *encodedParentEventId; // @dynamic encodedParentEventId;
@property(nonatomic) _Bool hasAdBlock; // @dynamic hasAdBlock;
@property(nonatomic) _Bool hasAutonavState; // @dynamic hasAutonavState;
@property(nonatomic) _Bool hasBreakIndex; // @dynamic hasBreakIndex;
@property(nonatomic) _Bool hasBreakLengthMs; // @dynamic hasBreakLengthMs;
@property(nonatomic) _Bool hasBreakPositionMs; // @dynamic hasBreakPositionMs;
@property(nonatomic) _Bool hasClientPlaybackNonce; // @dynamic hasClientPlaybackNonce;
@property(nonatomic) _Bool hasClientSideAdTag; // @dynamic hasClientSideAdTag;
@property(nonatomic) _Bool hasContext; // @dynamic hasContext;
@property(nonatomic) _Bool hasCurrentMediaTimeMs; // @dynamic hasCurrentMediaTimeMs;
@property(nonatomic) _Bool hasDriftFromHeadMs; // @dynamic hasDriftFromHeadMs;
@property(nonatomic) _Bool hasEncodedAdSafetyReason; // @dynamic hasEncodedAdSafetyReason;
@property(nonatomic) _Bool hasEncodedParentEventId; // @dynamic hasEncodedParentEventId;
@property(nonatomic) _Bool hasIsProxyAdTagRequest; // @dynamic hasIsProxyAdTagRequest;
@property(nonatomic) _Bool hasLiveTargetingParams; // @dynamic hasLiveTargetingParams;
@property(nonatomic) _Bool hasOverridePlaybackContext; // @dynamic hasOverridePlaybackContext;
@property(nonatomic) _Bool hasParams; // @dynamic hasParams;
@property(nonatomic) _Bool hasPlayerHeight; // @dynamic hasPlayerHeight;
@property(nonatomic) _Bool hasPlayerWidth; // @dynamic hasPlayerWidth;
@property(nonatomic) _Bool hasProxyAdTag; // @dynamic hasProxyAdTag;
@property(nonatomic) _Bool hasProxyAdTagChecksum; // @dynamic hasProxyAdTagChecksum;
@property(nonatomic) _Bool hasTopLevelDomain; // @dynamic hasTopLevelDomain;
@property(nonatomic) _Bool hasVideoId; // @dynamic hasVideoId;
@property(nonatomic) _Bool isProxyAdTagRequest; // @dynamic isProxyAdTagRequest;
@property(copy, nonatomic) NSString *liveTargetingParams; // @dynamic liveTargetingParams;
@property(retain, nonatomic) YTIPlaybackContext *overridePlaybackContext; // @dynamic overridePlaybackContext;
@property(copy, nonatomic) NSString *params; // @dynamic params;
@property(nonatomic) int playerHeight; // @dynamic playerHeight;
@property(nonatomic) int playerWidth; // @dynamic playerWidth;
@property(copy, nonatomic) NSString *proxyAdTag; // @dynamic proxyAdTag;
@property(copy, nonatomic) NSString *proxyAdTagChecksum; // @dynamic proxyAdTagChecksum;
@property(copy, nonatomic) NSString *topLevelDomain; // @dynamic topLevelDomain;
@property(copy, nonatomic) NSString *videoId; // @dynamic videoId;

@end
```
