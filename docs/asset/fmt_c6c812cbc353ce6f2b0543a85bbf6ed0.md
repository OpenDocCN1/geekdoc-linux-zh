
``` 
channel dnssec {

    "/var/log/named/dnssec.log" versions 4 size 10m;

    print-time yes;

    print-category yes;

    print-severity yes;

    debug 3;

};
```

在 BIND 中，你必须将调试级别设置为 3 才能看到步骤。这种日志每个签名产生两页输出。如果你正在监控繁忙的服务器，多个查询的日志数据将交织。整理这些混乱可能是挑战性的。

对于 NSD 和 Unbound，在配置文件中将详细设置为高于默认值（分别为 0 和 1），或者对于 Unbound，可以使用 `unbound-control` 直接动态调整。像 BIND 一样，Unbound 必须处于日志 3 才能显示步骤。

一旦一切正常，将 Unbound 的 `val-log-level` 设置为 1，以便为每个失败的签名打印一行错误消息。这种详细程度有助于你跟踪出现问题的站点。

如果验证名称服务器无法验证签名，它将返回 `SERVFAIL` 指示。底层问题可能是某人的配置错误，位于一个

# 在 BIND 中记录日志

信任链中的某些区域、来自入侵者的伪造数据，或者验证递归服务器本身的设置出现问题。尝试使用 `drill` 追踪信任链上的签名，查看问题所在之处。如果所有签名都通过了验证，则用 `dig` 查询该问题的站点，然后用 `dig +cd` 查询。`cd` 标志会关闭验证。在信任链的每个区域上尝试此操作，看看你是否能找到问题。你可以沿着信任链向上或向下查找。可能的结果是信任锚点 `trust anchor` 过期或签名过期。

## 17.14 微软与 DNS

多年来，ISC 和 BIND 一直在与微软 DNS 工具和 Active Directory 互操作性上苦苦。微软被指控故意不兼容标准，并且没有对它们所使用的协议扩展进行记录。然而，现在看来微软并不是想故意不兼容；它们只是能力略显平庸，并且正在使用带有 Bug 的软件，它们的 ASN.1 编码器和解析器对数据包进行了微调，以至于 BIND 无法理解。现在，一切都正常了。Bug 已经修复，BIND 和微软遵循 IETF 协议并可以互操作了。这是一个好消息。

坏消息是 Active Directory 与 Kerberos 和 LDAP 紧密集成，并遵循它们自己可靠的小径。全都一样。将任何一个部分——例如 Kerberos 密钥分布中心——替换为类似的开源实现注定会失败。BIND 可以通过 GSS-TSIG 与 Active Directory 进行身份验证，但授权几乎是不可能的，因为 AD 将一切都存储在地狱般的 LDAP 数据库中。

参见第 30 章“与 Windows 协作”，获取有关与 Active Directory 共处的提示。它从第 1135 页开始。

## 17.15 测试与调试

BIND 和 NS/Unbound 都提供了三种基本的调试工具：日志记录、控制程序和命令行查询工具。BIND 的工具箱是最成熟，但也最复杂。

### 在 BIND 中记录日志

`named` 的日志功能灵活到足以让你汗毛直竖。BIND 原本使用 `syslog` 来报告错误消息和异常。最近的版本通过增加另一层方向以及对直接写入文件的支持，泛化了 `syslog` 配置。在深入之前，让我们先看看下一页表 17.3 中的 BIND 日志术语简明字典。

> 参见第 11 章获取有关 `syslog` 的更多信息。

你在 `named.conf` 中通过 `logging` 语句配置 BIND 日志。首先定义通道 `channels`，即消息可能的目的地。然后你告诉不同类的消息 `categories` 去特定的通道。

### 表 17.13 BIND 日志词汇

| 术语 | 含义 |
|---|---|
| channel | 消息可以去的地方：syslog、文件或 /dev/nullᵃ |
| category | `named` 可以生成的一类消息名称；例如，关于动态更新的消息或关于回答查询的消息 |
| module | 生成消息的源模块名称 |
| facility | 一个 syslog 设施。DNS 没有自己特定的设施，但你可以选择所有标准设施中的任何一个。 |
| severity | 错误消息的“糟糕程度”；`syslog` 所指的优先级 |

ᵃ. `/dev/null` 是一个丢弃所有输入的伪设备。

当生成一条消息时，它会在源头被分配一个类别、一个模块和一个严重程度。然后它会被分发到与其类别和模块相关的所有通道。每个通道都有一个严重程度过滤器，告知消息必须达到什么严重程度才能通过。通往 `syslog` 的通道也会根据 `/etc/syslog.conf` 中的规则进行过滤。

这里是 `logging` 语句的轮纲：

```
logging {

  channel_def;

  channel_def;

  category category_name {

    channel_name;

    channel_name;

    ...

  };

}
```

### 通道 Channels

`channel_def` 的看起来取决于通道是文件还是 syslog 通道。你必须为每个通道选择 `file` 或 `syslog`；一个通道不能同时是两者。

```
channel_name {

  file path [versions numvers | unlimited] [sizespec];

  syslog facility;

  severity severity;

  print-category yes | no;

  print-severity yes | no;

  print-time yes | no;

}
```

对于文件通道，`numvers` 告诉保留多少个备份文件，`sizespec` 指定允许文件增长到多大，例如：2048、100k、20m、unlimited、default 然后进行自动滚动。滚动后的版本是 `mylog.0`、`mylog.1` 等。如果你将文件通道命名为 `mylog`...

查看第 346 页获取 syslog 名称列表。

在 syslog 情况下，`facility` 指定了用于记录消息的 syslog 设施名称。可以是任何标准设施。在实践中，只有 `daemon` 和 `local0` 到 `local7` 是合理的选择。

*channel_def* 中的其余语句都是可选的。*severity* 可以取以下值，按降序排列：critical、error、warning、notice 或 debug 带有一个可选的数字级别，例如 `severity debug 3`。`dynamic` 值也可以被识别，并匹配服务器当前的调试级别。

各种 *print* 选项添加或抑制消息前缀。`syslog` 会在每条记录的消息的前面添加时间记录报告信息，但不会添加严重程度或类别。生成消息的故事文件名模块也可以作为 *print* 选项可用。17.14 中列出的四个通道是默认定义的。这些默认设置适用于大多数安装。

| 表 17.14 预定义通道 |
| 通道名称 | 它的功能 |
|---|---|
| default_syslog | 发送到 syslog，设施 daemon，级别 info |
| default_debug | 记录到文件 named，级别 dynamic |
| default_stderr | 发送到标准错误，级别 info |
| null | 丢弃所有消息 |

类别是由程序员在编写代码时指定的。它们根据主题或功能而不是严重程度来组织日志消息。下一页的 17.15 显示了当前的类别列表。

### 日志消息 Log Messages

默认的日志配置为：

```
logging {

  category default { default_syslog; default_debug; };

};
```
