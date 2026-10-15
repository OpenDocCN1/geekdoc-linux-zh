
```c
int bind_connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen, const struct sockaddr *faddr, socklen_t faddrlen);
```

### 7.6 IPv4 套接字选项
这些套接字选项由 IPv4 处理，级别为 `IPPROTO_IP`。我们将多播套接字选项的讨论推到第 21.6 节。

### IP_HDRINCL 套接字选项
如果在原始套接字上设置此选项（第 28 章），我们必须为发送的所有数据报构建 IP 头。内核为原始套接字发送的数据构建 IP 头，但某些应用程序（特别是 `traceroute`）构建自己的头部以覆盖某些字段的值。

当设置此选项时，我们构建完整的 IP 头，但有以下例外：

- IP 始终计算并存储 IP头部校验和。
- 如果我们将 IP 标识设置为 0，内核将设置该字段。
- 如果源 IP 地址是 `INADDR_ANY`，IP 将其设置为输出接口的主 IP 地址。
- 设置 IP 取决于实现。某些实现获取使用 `IP_OPTIONS` 套接字选项设置的任何 IP 并将其添加到我们构建的头部中，另一些要求我们的头部包含任何所需的 IP 。
- 某些字段必须使用主机字节序，某些使用网络字节序。这些取决于实现，使得使用 `IP_HDRINCL` 编写原始数据包不够可移植。

### IP_OPTIONS 套接字选项
设置此选项允许我们在 IP 头中设置 IP 。这要求对 IP 头中 IP 选项的格式非常熟悉。我们将在第 27.3 节结合 IPv4 源路由时讨论此选项。

### IP_RCVADDR 套接字选项
此套接字选项将接收到的 UDP 数据报的目的 IP 地址作为辅助数据通过 `recvmsg` 返回。我们将在第 22.2 节显示此选项的示例。

### IP_RCVIF 套接字选项
此套接字选项将接收 UDP 数据报的接口索引作为辅助数据通过 `recvmsg` 返回。我们将在第 22.2 节显示此选项的示例。

## Socket Option

此选项允许在 TCP、UDP 或 SCTP 段的 IP 头部中设置服务类型（TOS）字段（包含 DSCP 和 ECN 字段，见图 A.1）。如果我们对此选项调用 `getsockopt`，将返回将置于 IP 头部中 DSCP 和 ECN 字段的当前值（默认值为 0）。无法从收到的 IP 数据报文中获取该字段值。

应用程序可以将 DSCP 设置为与网络服务提供商协商的值，以提供预设的服务，例如为电话提供低延迟，或为批量数据传输提供高吞吐量。`diffserv` 架构与 RFC 2474 [Nichols et al. 1998] 中历史 TOS 字段的兼容性仅提供了有限的向后兼容。例如，将 `IP_tos` 设置为 `<netinet/ip.h>` 中内容的应用程序（如 `IP_TOS_LOWELAY` 或 `IP_TOS_THROUGHPUT`）应改用用户指定的 DSCP 值和 7（“网络控制”）；这意味着这意味着设置了 `IP_TOS_PREC_NETCONTROL` 或 `IP_TOS_PREC_INTERNETCONTROL` 的应用程序将在 `diffserv` 网络中工作。

RFC 3168 [Ramakrishnan, Floyd, and Black 2001] 包含了 ECN 字段的定义。应用程序通常应将 ECN 字段的设置留给内核，并在 `IP_TOS` 设置值的低两位指定零值。

## IP_TTL

通过此选项，我们可以设置并获取系统在给定套接字发送单播包时使用的默认 TTL（见图 A.1）。（多播 TTL 使用 `IP_MULTICAST_TTL` 套接选项设置，见第 21.6 节）。例如，BSD 对 TCP 和 UDP 套接字默认使用 64（指定在 IANA 的“IP Option Numbers”注册表中 [IANA]），对原始套接字默认使用 255。与 TOS 字段一样，调用 `getsockopt` 返回系统将在传出数据报中使用的字段默认值——无法从收到的数据报获取该值。我们将在图 28.19 的 `traceroute` 程序中设置此套接选项。

- [ Team LiB ]

## 7.7 ICMPv6 Socket Option

此选项由 ICMPv6 处理，其级别为 `IPPROTO_ICMPV6`。

## ICMP6_FILTER Socket Option

此选项允许我们获取并设置 `icmp6_filter` 结构，该结构指定 256 种可能的 ICMPv6 消息类型中将传递给原始套接字的进程。我们将在第 28.4 节讨论此选项。

## 7.8 IPv6 Socket Options

这些套接字选项由 IPv6 处理，级别为 `IPPROTO_IPV6` 字段。我们将多播套接选项的讨论推到第 21.6 节。我们注意到，这些许多选项使用了配合 `recvmsg` 函数的辅助数据，我们将在第 14.6 节进行描述。IPv6 套接字选项定义在 RFC 3493 [Gilligan et al. 2003] 和 RFC 3542 [Stevens et al. 2003] 中。

### IPV6_CHECKSUM

## Socket Option

此套接选项指定用户数据中校验和所在的字节偏移量。如果此值为非负值，内核将：(i) 计算并存储所有传出包的校验和，以及 (ii) 在输入时验证收到的校验和，丢弃校验无效的包。此选项影响所有 IPv6 套接字，但 ICMPv6 套接字除外（内核始终计算并存储 ICMPv6 套接字的校验和）。如果指定值为 -1（默认值），内核将不对该套接字的传出包计算和存储校验和，也不会验证收到的包。

所有使用 IPv6 的协议在其外部协议头部都应有一个校验和。这些校验和包含一个伪头部（RFC 2460 [Deering and Hinden 1998]），其中源 IPv6 地址（这与通常使用 IPv4 原始套接字实现的所有协议都不同）。内核不会强制使用原始套接字的应用程序进行源地址选择，而是由内核完成操作，然后结合标准的 IPv6 伪头部计算并存储校验和。

### IPV6_DONTFRAG

## Socket Option

设置此选项将禁用包的分片。如果包超过 MTU，它将被丢弃。我们将在第 21.6 节描述此。

### IPV6_NEXTHOP

## Socket Option

此选项指定数据报的下一跳地址。我们将在第 22.8 节描述。

### IPV6_PATHMTU

## Socket Option

此选项指定路径的 MTU。我们将在第 22.9 节描述。

### IPV6_RECVTCLASS

## Socket Option

设置此选项指定返回收到的流量类别（traffic class）。我们将在第 27.5 节描述。

### IPV6_HOPLIMIT

## Socket Option

设置此选项指定返回跳数限制（hop limit）。我们将在第 22.8 节描述。

### IPV6_HOPOPTS

## Socket Option

设置此选项指定返回收到的跳选项（hop options）。我们将在第 27.5 节描述。

### IPV6_REVPKTINFO

## Socket Option

设置此选项指定返回目的 IPv6 地址和到达的接口索引。我们将在第 22.8 节描述。

### IPV6_RECVRHDR

## Socket Option

设置此选项指定返回收到的 IPv6 路由头部（routing header）。我们将在第 27.6 节描述。

### IPV6_RECVPATHMTU

## Socket Option

设置此选项指定返回路径 MTU。我们将在第 22.9 节描述。

### IPV6_USE_MTU
