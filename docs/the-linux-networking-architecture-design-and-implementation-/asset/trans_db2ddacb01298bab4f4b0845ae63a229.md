
# 第 14 章 互联网协议 V4

允许您额外识别连接计算机的网络。为此，值 0.0.0.0 被用作接收地址，这意味着局域网内的所有计算机都被地址化。这些计算机的 ICMP 模块通过发送信息回复（Information Reply）来响应信息请求（Information Request），其中它们说明的是 LAN 标识符而不是 0.0.0.0。

标识符（Identifier）和序列号（Sequence Number）字段用于分配信息请求和信息回复对，类似于回显和回显回复对。类型（Type）字段定义如下：

```
Type = 0x08: 消息为信息请求。
Type = 0x10: 消息为信息回复。
```

## 14.4. 配置 ICMP

指定的 RFC 允许本地系统管理员控制某些 ICMP 函数的行为。Linux 实现包含三种可以使用 `sysctl()` 函数控制运行时行为的情况：

- 回显回复（Echo Replies）：出于安全考虑，系统管理员可以决定是否发送回显回复。此选项默认激活。
- 针对广播包的回显回复：系统管理员可以决定是否对发送至局域网内所有计算机的回显请求包（即目标地址为 0.0.0.0）发送回复。此选项默认禁用。
- 监控非法 ICMP 广播回复：可以忽略作为 IP 广播响应发送的错误 ICMP 消息。（参见 RFC 1122 [Brad89]）。默认情况下并非如此。

此外，RFC 1812 [Bake95] 规定 ICMP 消息的传输速率应该限制，且该限制应该是可配置的。传输函数 `icmp_send()` 相应的相应的限制，但速率只能在源代码中设置（在 `xrlim_allow()` 函数中，`XLRIM_BURST_FACTOR` 常量），这意味着你必须重新编译 Linux 内核。

## 14.4.3 Linux 内核中的 ICMP

Linux 实现主要在文件 `net/ipv4/icmp.c` 和相关的头文件 `include/linux/icmp.h` 中完成。每个 ICMP 消息类型定义为一个常量，其类型字段由 RFC 792 指定：

```
ICMP_ECHOREPLY = 0
ICMP_DEST_UNREACH = 3
ICMP_SOURCE_QUENCH = 4
ICMP_REDIRECT = 5
ICMP_ECHO = 8
ICMP_TIME_EXCEEDED = 11
ICMP_PARAMETER_PROB = 12
ICMP_TIMESTAMP = 13
ICMP_TIMESTAMPREPLY = 14
```

## 14.4 互联网控制消息协议 (ICMP)

ICMP_INFO_REQUEST = 15
ICMP_INFO_REPLY = 16
ICMP_ADDRESS = 17
ICMP_ADDRESSREPLY = 18

所有 IP 模块都使用 ICMP 实现来发送 ICMP 消息。

```
include/linux/icmp.h
```

从本地角度来看，除少数统计外，ICMP 层是无状态的，但两个计算机之间交换的消息可以包含状态。ICMP socket 是实现中唯一的中心结构。该 socket 只能通过 root 权限访问。这就是为什么例如 `ping` 命令需要 root 权限的原因。初始化函数 `icmp_unit()` 创建了这个 socket。

上一节提到的统计信息维护在数据结构 `icmp_statistics` 中。它包括发送和接收的总包数、产生的错误数以及 ICMP 类型的累计数。此统计变量的当前内容可以从伪文件 `/proc/net/snmp` 输出。该文件以简写 ICMP 类型的形式说明单个条目的含义，每个数据包前带有“In”（入）或“Out”（出），以及额外的一行来自统计的数值。以下是 `/proc/net/snmp` 内容的一个示例：

```
> /proc/net/snmp
Ip: ForwardingTTL InReceives InHErrors InAddrErrors ForDatagrams
UnknownProtos InDiscards InDelivers OutDiscards OutNoRoutes
ReasmTimeout ReasmReqs ReasmOKs ReasmFails FragOKs FragGenerates
Ip: 2 64 9 0 0 0 0 0 64 93 0 0 0 0 0 0 0 0
Icmp: InMsgs InErrors InUnreachable InTimeExcds InParmProbs InSrcQuenches
InRedirects InEcho InEchoReps InTimestamps InTimestampReps InAddrMask
InAddrMaskReps OutMsgs OutErrors OutUnreachable OutTimeExcds
OutParms
OutSrcQuenches OutRedirects OutEchos OutEchoReps OutTimestamps
OutTimestampReps OutAddrMask OutMaskReps
Icmp: 35 0 0 15 0 0 0 11 9 0 0 0 26 15 0 0 0 11 0  0
Tcp: RtoAlgorithm RtoMin RtoMax ConnActive PassiveOpens
Attempt EstabResets CurrEstab InSegs OutSegs Retrans InErrs OutRsts
Tcp: 0 0 0 4 0 0 0 816 888 0 0 0
Udp: Datagrams NoPorts InErrors OutDatagrams
Udp: 25 0 0
```

从本地角度来看，ICMP 层是无状态的，除少数统计外，但两个计算机之间交换的消息可以包含状态。ICMP socket 是实现中唯一的中心结构。该 socket 只能通过 root 权限访问。这就是为什么例如 `ping` 命令需要 root 权限的原因。初始化函数 `icmp_unit()` 创建了这个 socket。

统计信息维护在数据结构 `icmp_statistics` 中。它包括发送和接收的总包数、产生的错误数以及 ICMP 类型的累计数。此统计变量的当前内容可以从伪文件 `/proc/net/snmp` 输出。该文件以简写 ICMP 类型的形式说明单个条目的含义，每个数据包前带有“In”或“Out”，以及额外的一行来自统计的数值。以下是 `/proc/net/snmp` 内容的一个示例：

```
> /proc/net/snmp
Ip: ForwardingTTL InReceives InHErrors InAddrErrors ForDatagrams
UnknownProtos InDiscards InDelivers OutDiscards OutNoRoutes
ReasmTimeout ReasmReqs ReasmOKs ReasmFails FragOKs FragGenerates
Ip: 2 64 9 0 0 0 0 0 64 93 0 0 0 0 0 0 0 0
Icmp: InMsgs InErrors InUnreachable InTimeExcds InParmProbs InSrcQuenches
InRedirects InEcho InEchoReps InTimestamps InTimestampReps InAddrMask
InAddrMaskReps OutMsgs OutErrors OutUnreachable OutTimeExcds
OutParms
OutSrcQuenches OutRedirects OutEchos OutEchoReps OutTimestamps
OutTimestampReps OutAddrMask OutMaskReps
Icmp: 35 0 0 15 0 0 0 11 9 0 0 0 26 15 0 0 0 11 0  0
Tcp: RtoAlgorithm RtoMin RtoMax ConnActive PassiveOpens
Attempt EstabResets CurrEstab InSegs OutSegs Retrans InErrs OutRsts
Tcp: 0 0 0 4 0 0 0 816 888 0 0 0
Udp: Datagrams NoPorts InErrors OutDatagrams
Udp: 25 0 0
```

从本地角度来看，ICMP 层是无状态的，除少数统计外，但两个计算机之间交换的消息可以包含状态。ICMP socket 是实现中唯一的中心结构。该 socket 只能通过 root 权限访问。这就是为什么例如 `ping` 命令需要 root 权限的原因。初始化函数 `icmp_unit()` 创建了这个 socket。

统计信息维护在数据结构 `icmp_statistics` 中。它包括发送和接收的总包数、产生的错误数以及 ICMP 类型的累计数。此统计变量的当前内容可以从伪文件 `/proc/net/snmp` 输出。该文件以简写 ICMP 类型的形式说明单个条目的含义，每个数据包前带有“In”或“Out”，以及额外的一行来自统计的数值。以下是 `/proc/net/snmp` 内容的一个示例：

```
> /proc/net/snmp
Ip: ForwardingTTL InReceives InHErrors InAddrErrors ForDatagrams
UnknownProtos InDiscards InDelivers OutDiscards OutNoRoutes
ReasmTimeout ReasmReqs ReasmOKs ReasmFails FragOKs FragGenerates
Ip: 2 64 9 0 0 0 0 0 64 93 0 0 0 0 0 0 0 0
Icmp: InMsgs InErrors InUnreachable InTimeExcds InParmProbs InSrcQuenches
InRedirects InEcho InEchoReps InTimestamps InTimestampReps InAddrMask
InAddrMaskReps OutMsgs OutErrors OutUnreachable OutTimeExcds
OutParms
OutSrcQuenches OutRedirects OutEchos OutEchoReps OutTimestamps
OutTimestampReps OutAddrMask OutMaskReps
Icmp: 35 0 0 15 0 0 0 11 9 0 0 0 26 15 0 0 0 11 0  0
Tcp: RtoAlgorithm RtoMin RtoMax ConnActive PassiveOpens
Attempt EstabResets CurrEstab InSegs OutSegs Retrans InErrs OutRsts
Tcp: 0 0 0 4 0 0 0 816 888 0 0 0
Udp: Datagrams NoPorts InErrors OutDatagrams
Udp: 25 0 0
```

发送 ICMP 包：传输函数 `icmp_send()` 相应的相应的限制，但速率只能在源代码中设置（在 `xrlim_allow()` 函数中，`XLRIM_BURST_FACTOR` 常量），这意味着你必须重新编译 Linux 内核。

### Linux 内核中的 ICMP

Linux 实现主要在文件 `net/ipv4/icmp.c` 和相关的头文件 `include/linux/icmp.h` 中完成。每个 ICMP 消息类型定义为一个常量，其类型字段由 RFC 792 指定：

```
ICMP_ECHOREPLY = 0
ICMP_DEST_UNREACH = 3
ICMP_SOURCE_QUENCH = 4
ICMP_REDIRECT = 5
ICMP_ECHO = 8
ICMP_TIME_EXCEEDED = 11
ICMP_PARAMETER_PROB = 12
ICMP_TIMESTAMP = 13
ICMP_TIMESTAMPREPLY = 14
```
