

检查 SYN、ACK、RST 和 FIN 标志，但仅接受同时设置了 SYN 和 ACK 标志的数据包（对新连接的响应）。规则片段如下所示：

```
-p tcp --tcp-flags SYN,ACK,RST,FIN SYN,ACK
```

- `[!] --syn`—仅在 `-p tcp` 选项之后有效。这等同于以下内容：

  ```
  --tcp-flags SYN,RST,ACK SYN
  ```

- `--icmp-type [!] ICMP [sub]type`—仅在 `-p icmp` 选项之后有效。

以下是有效的 ICMP 类型和子类型（缩进在主类型之下）：

- 回显应答（pong）
- 目标不可达
  - 网络不可达
  - 主机不可达
  - 协议不可达
  - 端口不可达
  - 需要分片
  - 源路由失败
  - 网络未知
  - 主机未知
  - 网络禁止
  - 主机禁止
  - TOS 网络不可达
  - TOS 主机不可达
  - 通信禁止
  - 主机优先级违规
  - 优先级切断
- 源端抑制
- 重定向
  - 网络重定向
  - 主机重定向
  - TOS 网络重定向
  - TOS 主机重定向
- 回显请求（ping）
- 路由器通告
- 路由器请求
- 超时（ttl-exceeded）
  - 传输期间 TTL 为零
  - 重组期间 TTL 为零
- 参数问题
  - IP 头部错误
  - 缺少必需选项
- 时间戳请求
- 时间戳应答
- 地址掩码请求
- 地址掩码应答

- `--mac-source [!] mac-address`—仅在 `-m mac` 选项之后有效。适用于 INPUT 或 PREROUTING 链。规则片段如下所示：
  `-m mac --mac-source 00:00:ab:c0:45:a8`

- `--limit rate`—最大匹配速率（平均值）。默认值为 3/小时；超过匹配速率的数据包将被丢弃。如果你的系统无法承受每秒超过一个新连接，你可以将 limit 与以下规则片段一起使用：
  `-p tcp --syn`
  以防止服务器过载，尽管通常与 LOG 目标一起使用，以防止日志增长过快。速率可以指定周期（默认为 /hour），可用的周期为 /minute、/second、/hour 或 /day。规则片段：
  `-m limit --limit 1/second`

- `--limit-burst number`—在开始使用前面的 `--limit rate` 之前，最大初始匹配次数。每次未满足前面的 `--limit rate` 时，burst 会补充一个。默认的 `--limit-burst` 为 5。

- `--port [port[,port]...]`—仅在使用了 `-p tcp` 或 `-p udp` 选项，并且位于 `-m multiport` 选项之后时有效（参见后面的规则片段）。如果源端口和目标端口相同，并且与任意可选列出的端口匹配（最多允许 15 个逗号分隔的端口号），则匹配。一个仅匹配端口 25 和 110 的多端口规则片段示例：
  `-m multiport -p tcp --dport 25,110`

- `--mark value[/mask]`—匹配具有给定 mark（一个无符号值）的数据包。该值必须通过下文讨论的 MARK 目标进行设置。

- `--uid-owner userid`—仅在 OUTPUT 链中用于识别由特定用户创建的数据包时有效，而且即便如此，也只对某些本地创建的数据包有效。

- `--gid-owner groupid`—与 `--uid-owner` 类似，但应用于组。

- `--pid-owner PID`—与 `--uid-owner` 类似，但应用于进程 ID（PID）。

- `--sid-owner sessionid`—与 `--uid-owner` 类似，但应用于会话。

- `--state state`—匹配 TCP 连接状态。state 参数是一个逗号分隔的值列表，包含以下一个或多个：NEW、ESTABLISHED、RELATED、INVALID。NEW 适用于新连接（类似于 `--syn`，但包括整个新连接握手过程）。ESTABLISHED 适用于当前有效存在的连接。RELATED 适用于由于 ESTABLISHED 连接而发起的连接的数据包（例如 FTP 数据通道连接或 ICMP 错误消息，这些消息没有端口或连接状态）。通常你会将 ESTABLISHED 和 RELATED 一起使用。INVALID 状态指先前未涵盖的任何数据包——例如使用 TCP ping 的扫描、设置了 SYN 和 ACK 位但没有相应 SYN 数据包的数据包，或所有位都置位的 XMAS 树扫描（SYN、ACK、FIN、URG、PSH、RST）。一个规则片段可能如下所示：
  `-m state --state ESTABLISHED,RELATED`

- **unclean**—一个实验性选项，用于匹配异常或畸形数据包：

  ```
  -m unclean
  ```

- **--tos tos**—用于匹配下列 TOS 掩码之一。TOS 值必须首先由 netfilter 使用本节讨论的 TOS 目标进行设置。规则片段可以如下所示：

  ```
  -m tos --tos 16
  ```

表 36.1 列出了如果要基于服务类型（TOS）实现路由优先级时使用的值。

**表 36.1. TOS 掩码**

| TOS 名称 | TOS 数值 | 十六进制值 | 示例用途 |
|---|---:|---|---|
| 最小延迟 | 16 | 0x10 | FTP、telnet、ssh |
| 最大吞吐量 | 8 | 0x08 | FTP-data |
| 最大可靠性 | 4 | 0x04 | snmp、DNS |
| 最小成本 | 2 | 0x02 | nntp、email |
| 正常服务 | 0 | 0x00 |  |

## IPTABLES 目标

*目标* 是当数据包匹配规则规格时要采取的动作。所有内建链都有一个默认策略，如果没有其他规则覆盖它，则决定数据包的命运。所有策略默认为 ACCEPT。

除了内建的 ACCEPT、DROP、QUEUE 和 RETURN 目标之外，如果你已加载模块，还存在许多其他目标。由于 netfilter 灵活的框架，数量很容易增加。以下列表概述了当前包含的目标。

- **LOG**—允许记录匹配的数据包。考虑使用上文讨论的 limit 模块。LOG 目标可以采用以下任意可选参数：
  - `--log-level level`—允许指定日志级别。有关日志级别的更多信息，请参见第 21 章“系统审计和系统日志”。
  - `--log-prefix prefix`—允许你在日志开头附加最多 14 个字符，以标识日志条目。
  - `--log-tcp-sequence`—将记录 TCP 序列号（这可能带来安全风险）。
  - `--log-tcp-options`—读取并记录 TCP 数据包头部的选项字段。
  - `--log-ip-options`—读取并记录 IP 数据包头部的选项字段。

- **MARK**—设置防火墙标记（fwmark），供后续规则使用。这需要 mangle 表（`-t mangle`），并具有以下必需参数：
  - `--set-mark mark`—标记将是一个数值。

- **REJECT**—等同于 DROP，但会返回一条错误消息。仅在 INPUT、FORWARD 和 OUTPUT 链中有效（与 DROP 或 ACCEPT 相同）。REJECT 具有以下可选参数：
  - `--reject-with type`—允许你将默认的 icmp-net-unreachable 消息更改为 icmp-host-unreachable、icmp-port-unreachable 或 icmp-proto-unreachable 之一。如果规则指定了 `-p icmp`，则 reject-with 参数还可以使用 echo-reply。

- **TOS**—允许设置服务类型字段。仅在 PREROUTING 或 OUTPUT 链中有效。带有一个必需参数：
  - `--set-tos tos`—其中 tos 可以是上述列出的有效数值之一。

- **MIRROR**—一个实验性目标，试图通过交换源 IP 和目标 IP 来镜像数据包。仅在 INPUT、OUTPUT 和 FORWARD 链中有效。

- **SNAT**—需要 nat 表（`-t nat`），且仅在 POSTROUTING 链中有效。带有一个必需参数：
  - `--to-source ipaddress[-ipaddress][:port-port]`—将出站数据包的源地址更改为参数中指定的一个或多个地址。如果有必要，也会更改 udp 和 tcp 协议端口。通常不会进行端口改写。

- **DNAT**—需要 nat 表（`-t nat`），且仅在 PREROUTING 链中有效。带有一个必需参数：
  - `--to-destination ipaddress[-ipaddress][:port-port]`—将入站数据包的目标地址更改为参数中指定的一个或多个地址。如果有必要，也会更改 udp 和 tcp 协议端口。通常不会进行端口改写。

- **MASQUERADE**—需要 nat 表（`-t nat`），且仅在 POSTROUTING 链中有效。用于拨号连接。带有一个可选参数：
  - `--to-ports port[-port]`—这会覆盖默认的端口选择启发式规则。仅在 `-p tcp` 或 `-p udp` 时有效。

- **REDIRECT**—需要 nat 表（`-t nat`），且仅在 PREROUTING 和 OUTPUT 链（或从这些链调用的用户自定义链）中有效。将数据包发送到 localhost。带有一个可选参数：
  - `--to-ports port[-port]`—这会覆盖默认的端口选择启发式规则。仅在 `-p tcp` 或 `-p udp` 时有效。

## 用户自定义链

用户自定义链提供了一种将规则逻辑分组的方法。这些链作为目标从内建链中调用。在链中的任意位置，你都可以从同一表中调用用户自定义链。当用户自定义链在没有匹配的情况下终止时，它将返回到调用链中的下一条规则。

创建用户自定义链时，名称应使用小写字母，因为大写字母预留给内建链和目标使用。名称不能是内建名称或特殊值之一。

