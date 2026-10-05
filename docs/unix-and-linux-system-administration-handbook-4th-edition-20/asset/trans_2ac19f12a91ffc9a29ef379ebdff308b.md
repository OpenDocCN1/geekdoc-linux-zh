

# 21.13 NetFlow: 基于连接的监控

SNMP 以其报告流经接口的网络流量多少的能力而广为人周知。但如果你想了解更多关于流量的确切类型及其目的地，SNMP 就帮不上什么忙。在 UNIX 机器上，你可以运行脚本来挖掘一些额外细节，但这种选项在专用路由器上是不可用的。

作为回应，路由器厂商针对这个问题提出了自己的解决方案。这些解决方案中最流行的是 Cisco 的 NetFlow 协议。

NetFlow 通过七个键跟踪每一个连接：源地址和目的 IP 地址、源端口和目的端口号、协议（TCP、UDP 等）、服务类型（ToS）以及逻辑接口。这些元数据结合涉及的数据包数量和字节数等额外信息，可以发送到任何收集器。

主流 NetFlow 协议版本是 v5 和 v7，它们通常被归为类，因为它们相同之处在于 v7 增加了一个额外的字段（源路由器）。v7 用于 Cisco Catalyst 交换机。第 9 版本正变得流行。这种基于模板的方法使其非常灵活。

你可以让 NetFlow 向合适的接收器（如 Cisco 的 cflow）发送其元数据的运行账户。在繁忙的网络链路上，此配置会产生海量数据，因此你可能需要大量的磁盘空间，并寻找能够胜任的分析工具。

对于后者，一种可能性是 Dave Plonka 的 FlowScan 软件包。它没有及时更新，但仍然运行良好。你可以在 net.doit.wis.edu/~plonka/FlowScan 找到它。

# 使用 ndump 和 Nfsen 监控 NetFlow 数据

另一对收集和分析 NetFlow数据的有用工具是 Peter Haag 的 ndump (ndump.sourceforge.net) 和 Nfsen (nfsen.sourceforge.net)。收集器 (ncapd) 将 NetFlow 数据存储在磁盘上，以便以后由 ndump 处理。

ncapd 和 ndump 处理 NetFlow 协议版本 v5/7 和 v9。对于 IPv6 支持，你必须使用 v9；版本 5 和 7 不支持。

ndump 的工作方式类似于 tcpdump（见第 875 页）。它具有适用于 NetFlow 数据的类似过滤语法。灵活的输出格式允许你自定义记录的显示。内置摘要可以让你看到网络中的前 N 个说话者（talkers）以及其他有用信息。

以下（稍加压缩的）ndump 输出显示了哪些 IP 地址和网络交换流量最多，哪些端口目前最活跃，以及更多。

+   7. "talker" 是 NetFlow 中对创建网络流量设备的术语。

# 使用 nfdump 和 NfSen 监控 NetFlow 数据

- -s ip/flows 选项请求任何源或目的 IP 地址的信息，并按流排序。-n 10 将显示限制为前 10 项。

```
linux nfdump -M /nfdump/profiles-data/live/upstream -r 2009/07/28/nfdump.20090728105 -n 10 -s ip/flows
```

10 IP 地址流排序：

| 观测日期 | 持续时间 | IP 地址 | 流 | 数据包 | 字节 | bps | bps | bpp |
|---|---|---|---|---|---|---|---|---|
| 2009-07-28 12:02 | 467.596 | 192.168.92 | 28783 | 67420 | 3.8 M | 144 | 67347 | 58 |
| 2009-07-28 12:02 | 467.600 | 192.168.96 | 18928 | 43878 | 4.7 M | 94 | 85522 | 112 |
| 2009-07-28 12:02 | 464.444 | 192.168.19 | 17321 | 35454 | 1.3 M | 96 | 63881 | 46 |
| 2009-07-28 12:02 | 454.299 | 192.168.12 | 11554 | 29093 | 1.1 M | 69 | 23996 | |
| 2009-07-28 12:02 | 362.586 | 192.168.97 | 2083 | 6839 | 1110.4 | 2 M | 38883 | 11 |
| 2009-07-28 12:02 | 393.600 | 192.120.139 | 4802 | 61834 | 12568 | 32 | 125868 | 107 |
| 2009-07-28 12:02 | 452.353 | 192.168.93 | 4477 | 5144 | 5547 | 11 | 554019 | 9 |
| 2009-07-28 12:02 | 456.306 | 192.168.88 | 3416 | 6642 | 69776 | 14 | 122333 | 105 |
| 2009-07-28 12:02 | 459.732 | 192.168.108 | 2544 | 2552 | 35.5 M | 55 | 58478 | 131 |
| 2009-07-28 12:02 | 466.782 | 192.168.97 | 1947 | 21403 | 24.0 | 5 | 94988 | 229 |

总结：总流：8290，总字节：311.6 M，总数据包：75290，bps：5.3 M，平均 pps：1623，平均 bpp：430.
时间窗口：2009-07-28 12:02 - 2009-07-28 12:09
处理的总流：8290，跳过：0；流：51164
Sys：0.31065s/seconds：30036.1
Wall：0

由于 NetFlow 数据存储在磁盘上，你可以使用不同的过滤器对其进行分析。另一个很好的功能是 nfdump 能够将入站和出站流匹配为双向流。NfSen 是 NetFlow 的 Web 前端，位于 nfdump 之上，并将图表功能与 nfdump 的所有功能相结合。它显示三个类别：流、数据包和字节。NfSen 不仅仅创建静态图表——它让你浏览单个流。你还可以查看图表中的峰值，深入单个流，并应用任意 nfdump 过滤器。GUI 与底层 nfdump 的结合允许保存保存和显示设置以创建一个配置，以便将来轻松返回特定类型的分析。例如，监控你的 DMZ、Web 读取或客户端网络流量的配置也使 NfSen 成为安全事件响应团队的重要工具，因为它可以轻松跟踪特定类型的事件或流量。例如，下一页的图 F 显示了针对 SYN 攻击定制的显示。

# 图 F 用于 NfSen 的“SYN 洪水”配置

![](img/579ec8c67772f31ec3484bbb71a2_940.png)

安全调查通常发生在攻击几小时或几天后，但如果你确实保存了 NetFlow 数据，你就可以轻松创建一个追溯到之前的 NfSen 配置。这种回顾视图让你识别参与攻击的 IP 地址并跟踪可能影响的其他主机。你还可以设置 NfSen 来寻找办公外的流并在满足特定条件时触发报警。

# 在 Cisco 路由器上设置 NetFlow

要开始使用 NetFlow，必须配置网络设备将 NetFlow 数据发送到 nfcapd。本节概述了 Cisco 路由器上的 NetFlow 配置。

按接口启用 NetFlow 导出：

```
ios interface fastethernet 0/0
ios ip route-cache flow
```

告诉路由器在哪里发送 NetFlow 数据，输入以下命令：

```
ios ip flow-export nfcapd-hostname listen-port
```

下面的选项将长连接流分为 5 分钟的段。你可以选择 1 到 60 分钟之间的任何段长度，但它应该小于 nfdump 文件旋转周期（默认为 5 分钟）。

```
ios ip flow-export version 5
ios ip flow-cache timeout active 5
```

在 Catalyst 6500/7600 上，除了普通的 NetFlow 导出外，你必须启用 NDE (NetFlow Data Export)。

# 推荐阅读

如下所示：

```
ios# mls flow ip interface-full
mls flow ip ipv6 interface-full
mls nde sender version 5
```

在繁忙的路由器上，考虑激进地让小流超时：

```
ios# mls aging fast time 4 threshold 2
mls aging normal 32
ios mls aging long 900
```

你仍然需要传统的 NetFlow 配置，在每个接口上使用 `ip flow ingress` 或 `ip route-cache flow`，以便你看到发往路由器本身的“软件交换”流。

对于 NetFlow v9，配置可能会更长。取决于你的 IOS 版本，你也可以定义自己的模板。随着灵活 NetFlow (FNF) 的引入，NetFlow 环境变得更加复杂。

# 21.14 推荐阅读

Wikipedia 包含一个不错的（尽管是压缩的）SNMP 概述并指向 RFC。这是一个很好的起点。

MAURO, DOUGLAS R., AND KEV J. SCHMIDT. Essential SNMP (2nd Edition). Sebastopol, CA: O'Reilly Media, 2005.

SIMPLEWEB. SNMP 和互联网管理网站。simpleweb.org。

你可能发现以下 RFC 也很有用。我们用 RFC 内容描述替换了 RFC 的实际标题，因为某些实际标题是毫无帮助的流行语和术语堆砌。

