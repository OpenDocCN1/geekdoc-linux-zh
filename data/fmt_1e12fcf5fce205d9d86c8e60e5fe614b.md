
使用给定的 `family`、`type` 和 `proto` 选项创建一对套接字对象，其含义与 `socket()` 函数相同。此函数仅适用于 UNIX 域套接字（`family=AF_UNIX`）。`type` 可以是 `SOCK_DGRAM` 或 `SOCK_STREAM`。该函数返回一个两个套接字对象的元组。`socketpair()` 创建的两个套接字具有相同的地址族、类型和协议选项。此函数仅适用于 UNIX 域套接字（`family=AF_UNIX`）。`type` 可以是 `SOCK_DGRAM` 或 `SOCK_STREAM`。`socketpair()` 返回两个套接字对象的元组。

要打开 TCP 连接，请使用 `socket(AF_INET, SOCK_STREAM)`。要打开 UDP 连接，请使用 `socket(AF_INET, SOCK_DGRAM)`。该函数返回一个 `SocketType` 实例（稍后描述）。

使用给定的地址族、类型和 `proto` 选项创建一个一对套接字对象，其含义与 `socket()` 函数相同。此函数仅适用于 UNIX 域套接字（`family=AF_UNIX`）。`type` 可以是 `SOCK_DGRAM` 或 `SOCK_STREAM`。`socketpair()` 返回两个套接字对象的元组。

# 第 21 章 网络编程与套接字

`IPPROTO_IP` 级别可用以下选项：

| 选项名称 | 值 | 描述 |
| :--- | :--- | :--- |
| `IP_ADD_MEMBERSHIP` | `ip_mreg` | 加入多播组（仅设置）。`ip_mreg` 是一个紧凑二进制字符串，包含两个 32 位的 IP 地址 (`multiaddr`, `localaddr`)，其中 `multiaddr` 是多播地址，`localaddr` 是正在使用的本地接口。 |
| `IP_DROP_MEMBERSHIP` | `ip_mreg` | 离开多播组（仅设置）。`ip_mreg` 描述如上。 |
| `IP_HDRINCL` | `int` | 数据中包含 IP 头部。 |
| `IP_MAX_MULTICASTS` | `int` | 多播组的最大数量。 |
| `IP_MULTICAST` | `in_addr` | 出去接口。`in_addr` 是一个包含 32 位 IP 地址的紧凑二进制字符串。 |
| `IP_MULTICAST_LOOP` | `0,1` | 生存时间。`uint8` 是一个包含 1 字节无符号字符的紧凑二进制字符串。IP 头部。`ipopts` 是一个不超过 44 字节的紧凑二进制字符串。该字符串的内容在 RFC 791 中描述。 |
| `IP_RECVSTDADDR` | `0,1` | 数据报接收 IP 目的地址。 |
| `IP_RECVOPTS` | `0,1` | 数据报接收所有 IP 选项。 |
| `IP_REVERTOPS` | `0,1` | 响应接收 IP 选项。 |
| `IP_RETOPS` | `0,1` | 与 `IP_RECVOPTS` 相同，选项留空且不填充时间戳或路由选项。 |
| `IP_TOS` | `int` | 服务类型。 |
| `IP_TTL` | `int` | 生存时间。 |

`IPPROTO_IPV6` 级别可用以下选项：

| 选项名称 | 值 | 描述 |
| :--- | :--- | :--- |
| `IPv6_CHECKSUM` | `0,1` | 由系统计算校验和。 |
| `IPv6_DONTFRAG` | `0,1` | 如果超过 MTU 大小则不分片。 |
| `IPv6_DSTOPS` | `ip6_dest` | 目的选项。`ip6_dest` 是格式为 (`next`, `len`, `options`) 的紧凑二进制字符串，其中 `next` 是一个 8 位整数，给出下一个头部的选项；`len` 是一个 8 位整数，以单位指定头部的长度，不包括前 8 字节；`options` 是编码后的选项。 |
| `IPv6_HOPPLIMIT` | `int` | 跳数限制。 |
| `IPv6_HOPOTS` | `ip6_hbb` | 逐跳选项。`ip6_hbb` 的编码与 `ip6_dest` 相同。 |

## socket 481

| 选项名称 | 值 | 描述 |
| :--- | :--- | :--- |
| `IPV6_JOIN_GROUP` | `ip6_mreq` | 加入多播组。`ip6_mreq` 是一个包含 (`multiaddr`, `index`) 的紧凑二进制字符串，其中 `multiaddr` 是 128 位的 IPv6 多播地址，`index` 是本地接口的 32 位无符号整数索引。 |
| `IPV6_LEAVE_GROUP` | `ip6_mreq` | 离开多播组。 |
| `IPV6_MULTICAST_HOPS` | `int` | 多播数据包的跳数限制。 |
| `IPV6_MULTICAST_IF` | `int` | 出去多播包的接口。 |
| `IPV6_MULTICAST_LOOP` | `0,1` | 将出去的多播数据包传回本地应用程序。 |
| `IPV6_NEXTOP` | `sockaddr_in6` | 设置出去包的下一个头部。`sockaddr_in6` 是一个包含 `<netinet/in.h>` 中定义的 C 结构的紧凑二进制字符串。 |
| `IPV6_PKTINFO` | `ip6_pktinfo` | 数据包信息结构。`ip6_pktinfo` 是一个包含 (`addr`, `index`) 的紧凑二进制字符串，其中 `addr` 是 128 位的 IPv6 地址，`index` 是带有接口索引的 32 位无符号整数。 |
| `IPV6_RECDTOPSOPS` | `0,1` | 接收目的选项。 |
| `IPV6_RECVHLOMIT` | `0,1` | 接收跳数限制。 |
| `IPV6_RECVHOPOPTS` | `0,1` | 接收逐跳选项。 |
| `IPV6_RECVPTINFO` | `0,1` | 接收数据包信息。 |
| `IPV6_RECVTRHDR` | `0,1` | 接收路由头部。 |
| `IPV6_RECVTCLASS` | `0,1` | 接收流量类别。 |
| `IPV6_RTHDR` | `ip6_rthdr` | 路由头部。`ip6_rthdr` 是一个包含 (`next`, `len`, `type`, `segleft`, `data`) 的紧凑二进制字符串，其中 `next`, `len`, `type` 和 `segleft` 均为 8 位无符号整数，`data` 是路由数据。参见 RFC 2460。 |
| `IPV6_RTHDRDTOPS` | `ip6_dest` | 路由选项头部之前的目的选项头部。 |
| `IPV6_RECPATHMTU` | `0,1` | 启用接收 `IPV6_PATHMTU` 辅助数据项。 |
| `IPV6_TCLASS` | `int` | 流量类别。 |
| `IPV6_UNICAST_HOPS` | `int` | 单播数据包的跳数限制。 |
| `IPV6_USE_MIN_MTU` | `-1,0,1` | 路径 MTU 发现。1 对所有目的启用，1 仅对多播目的禁用。 |

# 第 21 章 网络编程与 Socket

```python
```
