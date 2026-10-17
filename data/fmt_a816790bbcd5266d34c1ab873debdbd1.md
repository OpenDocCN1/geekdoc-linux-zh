
`family` 指定协议族，是图 4.2 所示常量之一。该参数通常被称为 `domain`（域）而不是 `family`（族）。套接字类型是图 4.3 所示常量之一。`socket` 函数的 `protocol` 参数应设置为在 `AF_INET` 中找到特定协议类型，或设置为 0 以根据给定的 `family` 和 `type` 组合选择系统默认值。

并不是所有套接字族和类型的组合都是有效的。图 4.5 显示了有效的组合，以及每个每对有效的实际协议。标记为“Yes”的框是有效的，但没有简便的缩写。空白的框表示不支持。

| family | 描述 |
| --- | --- |
| AF_INET | IPv4 协议 |
| AF_INET6 | IPv6 协议 |
| AF_LOCAL | Unix 域协议（第 15 章） |
| AF_ROUTE | 路由套接字（第 18 章） |
| AF_KEY | 密钥套接字（第 19 章） |

**图 4.2** 用于 `socket` 函数的族常量。

| type | 描述 |
| --- | --- |
| SOCK_STREAM | 流式套接字 |
| SOCK_DGRAM | 数据报套接字 |
| SOCK_SEQPACKET | 顺序数据包套接字 |
| SOCK_RAW | 原始套接字 |

**图 4.3** 用于 `socket` 函数的套接字类型。

| Protocol | 描述 |
| --- | --- |
| IPPROTO_TCP | TCP 传输协议 |
| IPPROTO_UDP | UDP 传输协议 |
| IPPROTO_SCTP | SCTP 传输协议 |

**图 4.4** 用于 `AF_INET` 或 `AF_INET6` 的套接字协议。

| AF_INET | AF_INET6 | AF_LOCAL | AF_ROUTE | AF_KEY |
| --- | --- | --- | --- | --- |
| SOCK_STREAM | TCP | SCTP | Yes | | |
| SOCK_DGRAM | UDP | UDP | Yes | | |
| SOCK_SEQPACKET | SCTP | SCTP | Yes | | |
| SOCK_RAW | IPv4 | IPv6 | | Yes | Yes |

**图 4.5** 用于 `socket` 函数的族和类型组合。

你可能还会遇到作为 `socket` 第一个参数的相应 `PF_xxx` 常量。我们将在本节末尾介绍更多信息。

我们注意到，你可能会遇到 `AF_UNIX`（历史 Unix 名称）而不是 `AF_LOCAL`（POSIX 名称），我们将在第 15 章中详细介绍。

`family` 和 `type` 参数还有其他值。例如，4.1BSD 同时支持 `AF_NS`（Xerox NS 协议，通常称为 XNS）和 `AF_ISO`（OSI 协议）。同样，`SOCK_SEQPACKET`（顺序数据包套接字）类型由 Xerox 协议和 OSI 协议共同实现，我们将在第 9.2 节描述其用法。但 TCP 是一种 TCP 流协议，只支持 `SOCK_STREAM` 套接字。

Linux 支持一种新的套接字类型 `SOCK_PACKET`，它提供了对链路层的访问，类似于图 2.1 中的 BPF 和 DLPI。我们将在第 29 章介绍更多信息。

套接字密钥 `AF_KEY` 比其他都要新。它提供了对加密安全的支持。类似于路由套接字（`AF_ROUTE`）是内核路由的接口，套接字密钥是内核密钥密钥的接口。详情请见第 19 章。

成功时，`socket` 函数返回一个非负整数值，类似于文件描述符。我们称之为套接字描述符（socket descriptor）或 `sockfd`。要获取此描述符，我们只需要调用 `socket` 函数。

### AF_xxx 与 PF_xxx

你可能还会遇到相应的 `PF_xxx` 常量作为 `socket` 的第一个参数。我们将在本节末尾介绍更多信息。

我们注意到，你可能会遇到 `AF_UNIX`（历史 Unix 名称）而不是 `AF_LOCAL`（POSIX 名称），我们将在第 15 章中详细介绍。

## 4.3 connect 函数

`connect` 函数用于 TCP 客户端与 TCP 服务器建立连接。

```c
#include <sys/socket.h>

int connect(int sockfd, const struct sockaddr *servaddr, socklen_t len);
```

如果成功返回 0，出错时返回 -1
