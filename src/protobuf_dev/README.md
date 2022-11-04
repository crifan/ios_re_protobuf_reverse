# Protobuf正向

TODO：

* 【整理】Chromium相关：Protobuf源码和文档
* 【整理】Protocol Buffers中.proto文件写法即protocobuf的语法
* 【已解决】protobuf中字段规则类型：required和optional

---

* `protobuf`
  * `protobuf`=`Protocol Buffers`
  * 概述
    * Protocol buffers are Google's language-neutral, platform-neutral, extensible mechanism for serializing structured data
  * 特点
    * 比JSON、XML等格式，占用体积更小，更快，更简单
  * 是什么：是一系列的组合 = 包含三部分
    * `定义语言`：definition language
      * 自己写的：.proto文件
    * `代码`=`code`
      * 需要专门的protocol compiler (对应命令行工具是：protoc)去编译生成对应语言的代码
        * 用于操作数据的代码
    * `运行时`：language-specific protobuf runtime libraries
    * `序列化`：serialization format for data
      * 写入文件
      * 或：用网络传输
      * 注：
        * 相关名词
          * `序列化`=`serialize`=`encode`=`编码`
          * `反序列化`=`deserialize`=`parse`=`解析`=`decode`=`解码`
  * 支持多种语言
    * proto2
      * Java
      * Python
      * Objective-C
      * C++
      * PHP
    * proto3
      * Kotlin
      * Dart
      * Go
      * Ruby
      * C#
  * 支持场景
    * 临时短期的网络传输
    * 长期的数据保存
  * 特点
    * 支持扩展extended=extensions
      * Protocol buffers can be extended with new information without invalidating existing data or requiring code to be updated
      * In proto2, messages can allow extensions to define fields outside of the message, itself. For example, the protobuf library's internal message schema allows extensions for custom, usage-specific options.
    * 兼容性好
      * 向后兼容性很好
      * 向前兼容性也很好
        * 无缝的支持：
          * 字段的变化
          * 新增字段
          * 删除字段
  * 使用Protocol Buffers的好处
    * 体积小=占用空间少=数据存储很紧凑
    * 解析速度快
    * 支持多种语言
    * 有各种经过优化的功能（通过编译器生成的类去实现的）
  * protobuf工作流 Protocol buffers workflow
    * ![protocol_buffers_workflow](../assets/img/protocol_buffers_workflow.png)
  * proto compiler = protoc
    * 输入：.proto
    * 输出：对应的特定语言的代码
      * 对每个字段和方法，都有一个accessor访问器
        * 用于 在 数据结构 和 二进制数据 之间解析和转换
    * 编译生成的文件
      * C++：.h和.cc
      * Java：.java
      * Kotlin：.kt
      * Python：生成内容是一个模块module，放在.proto文件中
      * Go：.pb.go
      * Ruby：.rb
      * Objective-C：pbobjc.h和pbobjc.m
      * C#：.cs
      * Dart：.pb.dart
  * 相关
    * google内部常用到的一些protobuf定义
      * timestamp
        * protobuf/timestamp.proto at main · protocolbuffers/protobuf (github.com)
      * status
        * googleapis/status.proto at master · googleapis/googleapis (github.com)
  * 文档和代码
    * 详见：
      * 【整理】Chromium相关：Protobuf源码和文档

## protobuf举例

`.proto`定义：

```c
message Person {
  required string name = 1;
  required int32 id = 2;
  optional string email = 3;
}
```

-》序列化：Java 写入文件：

```java
Person john = Person.newBuilder()
    .setId(1234)
    .setName("John Doe")
    .setEmail("jdoe@example.com")
    .build();
output = new FileOutputStream(args[0]);
john.writeTo(output);
```

-》反序列化：C++解析

```cpp
Person john;
fstream input(argv[1],
    ios::in | ios::binary);
john.ParseFromIstream(&input);
id = john.id();
name = john.name();
email = john.email();
```

更多例子：

* [examples - external/github.com/google/protobuf - Git at Google (googlesource.com)](https://chromium.googlesource.com/external/github.com/google/protobuf/+/HEAD/examples)
