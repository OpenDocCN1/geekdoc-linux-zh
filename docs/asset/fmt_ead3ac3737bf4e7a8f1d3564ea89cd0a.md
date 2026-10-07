
`channel_def` 的外观取决于取决于通道是文件通道还是 syslog 通道。你必须为每个通道选择 `file` 或 `syslog`；一个通道不能同时是两者。

对于文件通道，`numbers` 告诉保留多少个文件的备份版本，`sizespec` 指定了文件在自动轮转之前允许增长到多大（示例：`2048`, `100k`, `20m`, `unlimited`, `default`）。如果你将文件通道命名为 `mylog`，轮转后的版本为 `mylog.0`、`mylog.1` 等。

在 syslog 情况中，`facility` 指定了用于记录消息的 syslog 设施名称。它可以是任何标准设施。在实践中，只有 `daemon` 和 `local0` 到 `local7` 是合理的选择。

`channel_def` 中的其余语句都是可选的。`severity` 可以取以下值（按降序排列）：`critical`、`error`、`warning`、`notice`、`info` 或 `debug`（带有可选的数字级别，例如 `severity debug 3`）。值 `dynamic` 会被识别并匹配服务器当前的调试级别。

各种 `print` 选项用于添加或抑制消息前缀。Syslog 会在每条记录的消息的开头加上时间和报告主机，而不是严重性或类别。生成消息的源文件名（模块）也可以作为打印选项。对于文件通道，仅打印时间（`print-time`）是有意义的—— syslog 会添加自己的时间戳，因此没有必要重复它们。

表 17.14 中列出的四个通道是默认预定义的。这些默认设置对于大多数安装来说都是足够的。

# 表 17.14 BIND 中预定义的日志通道

| 通道名称 | 作用 |
| :--- | :--- |
| `default_syslog` | 发送到 syslog 设施 `daemon`，严重性为 `info` |
| `default_debug` | 记录到名为 `named.run` 的文件，严重性设置为 `dynamic` |
| `default_stderr` | 发送到命名进程的标准错误，严重性为 `info` |
| `null` | 丢弃所有消息 |

# 类别 (Categories)

类别由程序员在编写代码时确定。它们根据主题或功能组织日志消息，而不仅仅根据严重性。下一页的表 17.15 显示了消息类的当前列表。

# 日志消息

默认日志配置为：

```
logging {

  category default { default_syslog; default_debug };

};
```

当你对 BIND 进行重大更改并增加日志级别时，应该监控日志文件。一旦验证 `named` 运行稳定，随后重新配置以仅保留严重消息。

查询日志具有很高的教育意义。你可以验证 `allow` 子句是否正常工作，查看是谁在查询你，识别损坏的客户端等。在进行重大重配置后，这是一个很好的检查方法，特别是你对更改前的查询负载有清晰的了解时。

# 表 17.15 BIND 日志类别

| 类别 | 包含内容 |
| :--- | :--- |
| `client` | 客户端请求 |
| `config` | 配置文件的解析和处理 |
| `database` | 关于数据库操作的消息 |
| `default` | 无特定日志选项的类别的默认值 |
| `delegation-only` | 被 delegation-only 区域强制返回 `NXDOMAIN` 的查询 |
| `dispatch` | 将入站数据包分发到服务器模块 |
| `dnssec` | DNSSEC 消息 |
| `edns-disabled` | 关于损坏服务器的信息 |
| `general` | 未分类消息的兜底分类 |
| `lame-servers` | 应该提供某个区域服务但未提供服务的服务器 |
| `network` | 网络操作 |
| `notify` | 关于“区域更改”通知协议的消息 |
| `queries` | 服务器接收到的每条查询都有一条短日志消息 (!) |
| `resolver` | DNS 解析，例如为客户端进行递归查找 |
| `security` | 经批准/未经批准的请求 |
| `unmatched` | `named` 无法分类的查询（错误的类别、无视图） |
| `update` | 关于动态更新的消息 |
| `update-security` | 对更新请求的批准或拒绝 |
| `xfer-in` | 服务器正在接收的区域传输 |
| `xfer-out` | 服务器正在发送的区域传输 |

* a. 父区域或子区域都可能存在问题；如果不进行调查无法判断。

要启动查询，只需将 `queries` 类别指向一个通道即可。写入 syslog 的效率低于直接写入文件，因此当你在记录每条查询时，请使用本地磁盘上的通道。留有大量的磁盘空间，并准备在获得足够数据后关闭查询日志。(`rndc querylog` 可以动态开启或关闭查询日志。)

视图（Views）的调试可能很麻烦，但幸运的是，匹配特定查询的视图会与查询一起被记录。

下面列了一些常见的日志消息：

- `Lame server resolving xxx.` 如果你关于你的某个区域收到此消息，说明你的配置有误。如果该消息是关于互联网上的某个区域，那么它是有害的；那是别人的问题。通过将其重定向到 `null` 通道丢弃是一个很好的方法。
- `query (cache) xxx denied.` 这可能是远程站配置错误、滥用，或者是某人将一个区域委托给了你，但你尚未配置它。

# BIND 日志配置示例

- `Too many timeouts resolving xxx: disabling EDNS.` 此消息可能是由于防火墙不允许超过 512 字节的 UDP 包或分片导致的。验证问题是否来自防火墙，并考虑将这些消息重定向到 `null` 通道。
- `Unexpected RCODE (SERVFAIL) resolving xxx.` 这可能是攻击，或者更有可能是反复查询无效区域的迹。
- `Bad referral.` 此消息指示区域服务器之间的通信故障。
- `Not authoritative.` 从器服务器无法获取权威数据。可能是它指向了错误的主服务器，或者主服务器加载区域时出现问题。
- `Rejected zone.` `named` 因为区域文件包含错误而拒绝。
- `No NS RRs found.` 区域文件未包含 NS 记录。可能是记录缺失，也可能是它们没有以制表符或其他空格开头。在后一种情况下，记录没有附加到 SOA 记录上，因此被误读。
- `No default TTL set.` 设置记录默认 TTL 的优方法是在区域文件顶部使用 `$TTL` 指令。此错误消息表示缺少 `$TTL`，在 BIND 9 中是要求的。
- `No root name server for class.` 你的服务器无法找到根域名。检查你的 hints 文件和服务器的连接性。
- `Address already in use.` `named` 想要运行的端口已被另一个进程占用，可能是另一个 `named` 实例。如果你没有看到其他的 `named`，它可能崩溃并留下了一个开启的 `rndc` 控制套接字，你需要追踪并删除它。解决问题的方法之一是用 `rndc` 停止 `named` 进程，然后重启 `named`。

```
$ sudo rndc stop

$ sudo /usr/bin/named
```
- `updating zone xxx: update unsuccessful.` 尝试对区域进行动态更新被拒绝，最可能是因为该区域 `named.conf` 中的 `allow-update` 或 `update-policy` 子句。这是一个常见的错误消息，是由配置不当的 Windows 引起的。

以下来自繁忙 TLD 域名服务器的 ISC `named.conf` 代码段展示了一个全面的日志方案。

```conf
channel default_log { # 默认通道，写入文件

    file "named.log" versions 3 size 10m;

    print-time yes;

    print-category yes;

    print-severity yes;

    severity info;

}

channel xfer-log { # 区域传输通道，写入文件

    file "xfer.log" versions 3 size 10m;

    print-category yes;

    print-severity yes;

    print-time yes;

    severity info;

}

channel dnnssec-log { # DNSSEC 通道，写入文件

    file "dnssec.log" versions 3 size 1M;

    severity debug 1;

    print-severity yes;

    print-time yes;

}

category default { default_log; default_debug };

category dnnssec { dnnssec-log };

category xfer-in { xfer-log };

category xfer-out { xfer-log };

category notify { xfer-log };
```

## BIND 中的调试级别

`named` 的调试级别由 0 到 100 的整数表示。数字越大，输出越详细。级别 0 关闭调试。级别 1 和 2 适用于调试你的配置和数据库。级别 4 以上的级别适用于代码维护者。

你可以在 `named` 命令行上使用 `-d` 标志来启动调试。例如：
```
$ sudo named -d2
```
你将以调试级别 2 启动 `named`。默认情况下，调试信息会被写入启动 `named` 的当前工作目录下的名为 `named.run` 的文件中。`named.run` 文件增长速度非常快，所以调试时不要去喝啤酒，否则等你回来时会遇到更大的问题。

你还可以通过 `rndc trace` 在 `named` 运行时开启调试，这会将调试级别递加 1；或者使用 `rndc trace level` 将调试级别设置为指定的值。`rndc notrace` 则完全关闭调试。你也可以通过定义一个包含严重性规范的日志通道来启用调试：
```
severity debug 3;
```
这会将级别 3 及以下的调试消息发送到该特定通道的末尾。通道定义中的其他行指定了这些调试消息的目的。级别越高，记录的信息就越多。

观察日志或调试输出可以说明 DNS 在现实世界中配置错误的频率有多高。名称末尾那个讨厌的小圆点（或缺少该点）导致了惊人的 DNS 流量。每个完全限定域名（FQDN）的末尾都需要该点。

## NSD/Unbound 中的日志记录

默认情况下，日志消息发送到标准错误（`stderr`）和带有 `daemon` 设施的 syslog。然而，如果 `unbound.conf` 或 `nsd.conf` 中 `server` 语句的 `log` 属性被设置，则日志将复制到指定的文件。

记录的数据量（错误始终包含）由你在配置文件中设置的详细程度（verbosity level）控制。在 `unbound` 中，你还可以通过命令行选项设置详细程度。详细程度范围为 0–5；`nsd` 的默认级别为 0，`unbound` 为 1。

要理解 `nsd` 中各种详细程度层级的含义可能有点困难。它们到 syslog 的映射关系大致如下：

- 级别 3 – syslog 严重性 "`error`"（错误）
- 级别 4 – syslog 严重性 "`warning`"（警告）
- 级别 5 – syslog 严重性 "`notice`"（通知）
- 级别 6 – syslog 严重性 "`info`"（信息）

`unbound` 的级别含义在配置文件的 man 页中记录如下：

- 级别 0 – 不记录信息，仅记录错误
- 级别 1 – 运行信息
- 级别 2 – 详细运行信息
- 级别 3 – 基于查询的查询级信息
- 级别 4 – 算法级信息
- 级别 5 – 缓存未和客户端识别

你可以使用 `-d` 标志调用 `nsd` 以开启调试模式。在这种模式下，`nsd` 会保持在前台运行，而不是派生并退出。这种行为等同于在 `nsd.conf` 的 `server` 句中设置 `debug-mode: yes`。如果你在定义特定层级的 DEBUG 时重新编译 `nsd`，将获得更多的调试信息，但这些信息主要对开发者有价值。

## 第 17 章 DNS：域名系统

`unbound` 同样也有一个 `-d` 标志来开启调试模式。你可以使用 `-v` 标志增加调试信息的详细程度；需要更多信息时请尝试 `-v`。调试输出与配置文件中设置的日志信息详细程度是分开的。你可以配置额外的日志来帮助调试 DNSSEC 签名验证问题；请参见第 666 页。

## 名称服务器控制程序

我们的三个名称服务器都带有一个控制程序：`nsdc` 控制 `nsd`，`rndc` 控制 `named`，`unbound-control` 控制 `unbound`。`nsdc` 仅在本地机器上工作，但如果需要，`rndc` 和 `unbound-control` 可以跨互联网工作。

`rndc` 使用网络套接字与 `named` 通信并使用 TSIG 认证进行安全。`unbound-control` 使用 SSL/TLS，而 `nsdc` 使用信号。

使用 BIND 的

表17.16 显示了 `rndc` 接受的一些选项。不带参数输入 `rndc` 会列出可用命令及其功能描述。早期的 `rndc` 命令像 `nsdc` 一样使用信号，但由于有超过25个命令，BIND 很快就耗尽了信号。产生文件的命令会将它们放在指定的任何位置。

| 命令 | 功能 |
| :--- | :--- |
| `dump` | 将数据库转储到 `named_dump.db` |
| `flush [view]` | 刷新所有缓存或指定视图的缓存 |
| `flushname [view]` | 从服务器中刷新指定的名称 |
| `freeze [class]` | 挂起动态区域的更新 |
| `thaw [class]` | 恢复动态区域更新 |
| `halt` | 在不写入等待更新的情况下停止 `named` |
| `querylog` | 切换对传入查询的跟踪 |
| `notify [class]` | 重新发送区域的通知消息 |
| `notrace` | 关闭调试 |
| `reconfig` | 重新加载配置文件和任何新区域 |
| `recursing` | 转储查询，`named` |
| `refresh [class]` | 为区域调度维护 |
| `reload` | 重新加载 `named.conf` 和区域文件 |
| `reload [class]` | 重新加载指定的区域或视图 |
| `restart` | 重启服务器 |
| `transfer [class]` | 从主服务器复制区域数据 |
| `stats` | 将统计信息转储到 `named.stats` |
| `status` | 显示运行中 `named` 的状态 |
| `stop` | 保存更新并停止 `named` |
| `trace` | 将调试级别递加 1 |
| `trace level` | 将调试级别设置为指定的值 |
| `validation newstate` | 动态启用/禁用 DNSSEC 验证 |

*此处的参数与资源相同，通常为互联网中的 TTL。
*在 BIND 9 (9.7.0) 中尚未实现，但它一直被承诺过——一定很难做到。

# 表 17.17 nsd 命令

| 命令 | 功能 |
| :--- | :--- |
| `start` | 启动 `nsd` 服务 |
| `stop` | 停止 `nsd` 服务（发送 SIGTERM信号） |
| `reload` | 重新加载编译后的区域数据库 |
| `rebuild` | 使用 `zonec` 重新构建区域数据库 |
| `restart` | 重启 `nsd`；即先停止后启动 |
| `running` | 检查 `nsd` 是否正在运行；无输出表示一切正常 |
| `update` | 尝试更新所有从区域 |
| `notify` | 向所有服务器发送消息 |
| `patch` | 将区域传输的更改（数据库）合并回区域文件（文本） |

在上述 20 个命令中，包含了常见的 start、stop 和 reread 类型，还包含了若干项允许对对缓存和已配置的本地数据区域进行细粒度控制的选项。像转发（forwarding）之类的选项可以动态配置或修改。你还可以导出（dump）或重新加载缓存。

# 服务器统计信息

我们的每台服务器都以不同的粒度收集统计数据，并根据请求将其导出到文件中。有多个选项可以配置：收集什么数据、写到何处、更新频率等。BIND 新的统计通道是最灵活的机制。NSD 的态度是：它是一个简洁、快速的服务器，如果你需要统计数据，应该由另一个程序来收集，让 NSD 专注于它的主工作。`unbound` 则介于两者之间。

BIND 和 `unbound` 可以将其统计信息发送到另一个程序进行展示和绘图。BIND 使用新的 `statistics-channels` 语句（第 612 页）和 XML。`unbound` 使用 `contrib` 目录下的插件连接到 Munin 或 Cacti（见第 886 页）。

`named` 在接收到 `rndc` 的推送会将信息写入工作目录下的 `named.stats`。

```
$ rndc stats
```

这里是 `vix.com` 域名服务器的一段输出片段。省略了部分；显示了大约 20 组数据，但我们只包含了两个：

```
+++ Statistics Dump ++++1248150900)

++ Incoming Queries ++

2650862 A

9105 NS

40378 SOA

85744 PTR

246258 MX

328092 TXT
```
