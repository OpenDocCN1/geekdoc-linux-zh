
100k, 20m, unlimited, default) 在其自动轮转之前。如果将一个文件通道命名为 mylog，则轮转后的版本为 mylog.0、mylog.1，依此类推。

请参阅第 346 页以获取 syslog 设施名称列表。

在 syslog 情况下，facility 指定用于记录消息的 syslog 设施名称。它可以是任何标准设施。实际上，只有 daemon 和 local0 到 local7 是合理的选择。

channel_def 中的其余语句是可选的。severity 可以具有的值（按降序排列）为 critical、error、warning、notice、info 或 debug（可带可选的数字级别，例如 severity debug 3）。值 dynamic 也被识别，并匹配服务器当前的调试级别。

各种 print 选项可添加或抑制消息前缀。Syslog 会在每条记录的消息前加上时间和报告主机，但不包括严重性或类别。生成消息的源文件名（模块）也可作为打印选项使用。仅对文件通道启用 print-time 才有意义——syslog 会添加自己的时间戳，因此无需重复。

表 17.14 中列出的四个通道默认由系统预定义。这些默认值对于大多数安装来说应该足够。

## 表 17.14 BIND 中预定义的日志通道

| 通道名称 | 其作用 |
|---|---|
| default_syslog | 发送到 syslog，设施为 daemon，严重性为 info |
| default_debug | 记录到名为.run 的文件，严重性设置为 dynamic |
| default_stderr | 发送到 named 进程的标准错误，严重性为 info |
| null | 丢弃所有消息 |

## 类别

类别由程序员在编写代码时确定。它们按主题或功能组织日志消息，而不仅仅是按严重性。下一页的表 17.15 显示了当前的消息类别列表。

## 日志消息

默认日志配置为：

```
logging {
    category default { default_syslog; default_debug; };
};
```

当你对 BIND 进行重大更改时，应监视日志文件，并可能提高日志级别。之后，在确认 named 稳定后，重新配置以仅保留严重消息。

查询日志可能非常有教育意义。你可以验证你的 allow 子句是否正常工作，查看谁在查询你，识别有问题的客户端等。这是在进行重大重新配置后进行的一项良好检查，尤其是当你对更改前查询负载的状况有较好了解时。

## 表 17.15 BIND 日志类别

| 类别 | 其包含内容 |
|---|---|
| client | 客户端请求 |
| config | 配置文件解析和处理 |
| database | 关于数据库操作的<|message|> |
| default | 没有特定日志选项的类别的默认值 |
| delegation-only | 因 delegation-only 区域而被强制为 NXDOMAIN 的查询 |
| dispatch | 将传入数据包分发到服务器模块 |
| dnssec | DNSSEC 消息 |
| edns-disabled | 关于损坏服务器的信息 |
| general | 未分类消息的汇总 |
| lame-servers | 应该提供区域服务但未提供服务的服务器 a |
| network | 网络操作 |
| notify | 关于“区域已更改”通知协议的消息 |
| queries | 服务器收到的每个查询的简短日志消息（！） |
| resolver | DNS 解析，例如为客户端进行的递归查找 |
| security | 已批准/未批准的请求 |
| unmatched | named 无法分类的查询（错误类别、无视图） |
| update | 关于动态更新的消息 |
| update-security | 更新请求的批准或拒绝 |
| xfer-in | 服务器正在接收的区域传输 |
| xfer-out | 服务器正在发送的区域传输 |

a. 父区域或子区域都可能有问题；如果不进行调查，无法确定。

在进行重大重新配置后执行此操作，尤其是当你对更改前的查询负载有较好的了解时。

要开始查询日志，只需将 queries 类别定向到一个通道即可。写入 syslog 的效率不如直接写入文件，因此当你记录每个查询时，请使用本地磁盘上的文件通道。确保有足够的磁盘空间，并在获得足够数据后准备关闭查询日志。 （rndc querylog 可动态切换查询日志的开和关。）

视图调试起来可能很麻烦，但幸运的是，与查询一起记录了匹配特定查询的视图。

下面列出了一些常见的日志消息：

- Lame server resolving xxx。 如果你收到关于自己某个区域的此消息，则说明你配置有误。如果消息涉及互联网上的某个区域，则无害；这是别人的问题。可以将其丢弃到 null 通道。
- ... query (cache) xxx denied。 这可能是远程站点配置错误、滥用，或有人将区域委托给你，但你未对其进行配置的情况。

