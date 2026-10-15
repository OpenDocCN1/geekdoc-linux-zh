
这段代码有什么问题？重要吗？

# 28 原始套接字 (Raw Sockets)

## 28.1 引言

原始套接字提供了普通 TCP 和 UDP 套接字未提供的特性：

* 原始套接字允许我们读写 ICMPv4、IGMPv4 和 ICMPv6 数据包。例如，`ping` 程序发送 ICMP 回显请求并接收 ICMP 回显应答。（我们将在 28.5 节中开发自己版本的 `ping` 程序。）组播路由守护进程 `routed` 发送并接收 IGMPv4 数据包。

这种能力还允许使用 ICMP 或 IGMP 构建的应用程序完全作为用户进程进行构建，而不是在内核中放入更多代码。路由器发现守护进程（Solaris 2.x 下的 `rdisc`；TCP1 附录 F 描述了如何获取可用版本的源代码，例如）是通过这种方式构建的。它处理两个内核一无所知的 ICMP 消息（路由器告发现和请求）。

* 通过原始套接字，进程可以读写 IPv4 数据报，其数据报中包含一个不被内核处理的 IPv4 协议字段。回想图 A.1 中的 8 位协议字段。大多数内核只处理包含字段值为 1 (ICMP)、2 (IGMP)、6 (TCP) 和 17 (UDP) 的数据报。但协议字段中还定义了许多其他值：IANA 的“协议数字”注册表列出了所有值。例如，OSPF 路由协议不使用 TCP 或 UDP，但它直接使用 IP，将 IP 数据报的协议字段设置为 89。实现 OSPF 的门控程序必须使用原始套接字来读写这些 IP 数据报，因为它们包含一个内核一无所知的协议字段。这种能力同样适用于 IPv6。

* 通过原始套接字，进程可以使用 `IP_HDRINCL` 套接字选项构建它自己的 IPv4 头部。这可以用于构建 UDP 数据包，我们将在 29.7 节中展示该示例。

本章描述了原始套接字的创建、输入和输出。我们还将开发不同版本的、适用于 IPv4 和 IPv6 的 `ping` 和 `traceroute` 程序。

## 28.2 原始套接字的创建

创建原始套接涉及涉及步骤如下：

1. 当 `socket` 函数的第二个参数为 `SOCK_RAW` 时，它会创建一个原始套接字。第三个参数（协议）通常非零。例如，要创建一个 IPv4 原始套接字，我们写道：

```c
int sockfd;

sockfd = socket(AF_INET, SOCK_RAW, protocol);
```

其中 `protocol` 是 `<netinet/in.h>` 头文件定义的常量 `IPPROTO_xx` 之一，例如 `IPPROTO_ICMP`。
只有超级用户才能创建原始套接字。这防止了普通用户向网络写入自己的 IP 数据报。

2. `IP_HDRINCL` 套接字选项可以如下设置：

```c
const int on = 1;

if (setsockopt(sockfd, IPPROTO_IP, IP_HDRINCL, &on, sizeof(on)) < 0)

    error;
```

我们将在下一节描述此套接字选项的作用。

3. 可以在原始套接字上调用 `bind`，但很罕见。此函数只设置本地地址：原始套接字没有端口号的概念。关于输出，调用 `bind` 设置了将用于原始套接字上发送的数据报的源 IP 地址（但仅在未设置 `IP_HDRINCL` 套接字选项时）。如果没有调用 `bind`，内核将设置出站接口的源 IP 地址。

4. 可以在原始套接字上调用 `connect`，但很罕见。此函数只设置远程地址：同样，原始套接字没有端口号的概念。关于输出，调用 `connect` 让我们可以使用 `write` 或 `send` 代替 `sendto`，因为目标地址已经指定。

## 28.3 原始套接字的输出

原始套接字上的输出遵循以下规则：

* 正常输出通过 `sendto` 执行。
* 如果没有设置 `IP_HDRINCL` 选项，内核会填充数据报的头部字段。
* 如果设置了 `IP_HDRINCL` 选项，应用程序必须自己构建 IPv4 头部。

## 28.4 原始套字输入

关于原始套字输入，我们必须回答第一个问题是：内核将哪些 IP 数据报文传递给原始套字？适用以下规则：

- 接收到的 UDP 包永远不会被传递给原始套字。如果一个进程想要读取包含 UDP 或 TCP 包的 IP 数据报文，则必须在数据链路层读取数据包，如第 29 节所述。
- 大多数 ICMP 包在内核处理完 ICMP 消息后会传递给原始套字。源自 Berkeley 的实现会将所有 ICMP 包传递给原始套字，回显请求（echo request）、时间戳请求（timestamp request）和地址请求（address request）除外（TCPv2 第 302–303 页）。这三种 ICMP 消息完全由内核处理。
- 所有的 IGMP 包在内核处理完 ICMP 消息后都会传递给原始套字。
- 所有内核无法理解的协议的 IP 数据报文都会传递给原始套字。内核对这些数据包的唯一处理是对某些 IP 报部的最小化验证：IP 版本、IPv4 校验和、头部长度和目标 IP（TCPv2 第 213–220 页）。
- 如果数据报以分片形式到达，在所有分片到达并重组之前，没有任何内容会被传递给原始套字。

当内核有一个 IP 数据报要传递给原始套字时，它会检查所有进程的原始套字，寻找所有匹配的套字。IP 数据报的副本会被传递给每个匹配的套字。对每个原始套字都会执行以下测试，只有当三个测试都为真时，数据报才会被传递给套字：

- 如果在创建原始套字时指定了非零协议（`socket` 的第三个参数），则接收的数据报的协议字段必须匹配此值，否则数据报将不会传递给该套字。
- 如果通过 `bind` 在原始套字上绑定了本地 IP 地址，则接收的数据报的地址地址必须匹配此绑定地址，否则数据将不会传递给该套字。
- 如果通过 `connect` 为原始套字指定了远程 IP 地址，则接收的数据报的源 IP 地址必须匹配此连接地址，否则数据报将不会传递给该套字。

注意，如果使用协议为 0 创建原始套字，且既没有调用 `bind` 也没有调用 `connect`，那么套字将接收内核传递给原始套字的每一个原始数据报的副本。

每当接收的数据报传递给原始 IPv4 套字时，整个数据报（包括 IP 头部）都会传递给进程。对于原始 IPv6 套字，只有有效负载（即没有 IPv6 头部或任何扩展头部）会被传递给套字（例如图 28.11 和 28.22）。

## 原始套字

在传递给应用程序的 IPv4 头部中，`ip_len`、`ip_off` 和 `ip_id` 是主机字节序，且 `ip_len` 仅包含 IP 负载（减去头部长度），但其余字段为网络字节序。在 Linux 下，所有字段都保持为网络字节序。

如前所述，原始套字接口定义为提供一个与协议驻留在内核时所拥有的相同接口，因此字段的内容取决于操作系统内核。

我们在上一节中提到，在原始 IPv6 套字上收到的所有数据报都保持为网络字节序。

## ICMPv6 类型过滤

原始 ICMPv6 套字接收内核收到的大多数 ICMPv6 消息。ICMPv6 是 ICMPv4 的超集，包含了 ARP 和 IGMP 的功能（第 2.2 节）。因此，与原始 ICMP4 套字相比，原始 ICMPv6 套字可能会接收更多的数据包。大多数使用原始套字的应用程序对所有 ICMP 消息的一个小子集感兴趣。

为了减少通过原始 ICMPv6 套字从内核传递到应用程序的数据包数量，提供了一个应用程序指定的过滤器。过滤器使用数据类型 `struct <inet/icmp.h>` 声明。原始 ICMPv6 套字的当前过滤器通过 `setsockopt` 和 `getsockopt` 设置和获取，级别为 `IPPROTO_ICMPv6`，选项名称为 `ICMP6_FILTER`。

`icmp6_filter` 结构体的六种选项。

```c
#include <net/icmp.h>

void ICMPV6_FILTER_SETPASSALL(struct icmp6_filter *filter);

void ICMPV6_FILTER_SETBLOCK(struct icmp6_filter *filter);

void ICMPV6_FILTER_SEPASS(struct icmp6_filter *filter);

void ICMPV6_FILTER_SETPASS(int msgtype, struct icmp6_filter *filter);

int ICMPV6_FILTER_SETBLOCK(int msgtype, struct icmp6_filter *filter);

int ICMPV6_FILTER_BLOCK(int msgtype, const struct icmp6_filter *filter);
```

两者返回：如果消息通过（阻塞），返回 1，否则返回 0
