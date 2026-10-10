
# 邻居发现 (Neighbor Discovery)

IPv6 的重大变化之一是停止使用所有广播，包括 `ARP get`。设备使用一种新进程在子网内相互通信。它们发送到对方的链路本地地址（`link-local address`），而不是 `MAC` 地址。手动分配 `IPv6` 地址的设备将生成一个链路本地地址。这些地址在无状态自动配置中是直接使用 `MAC` 地址生成的；其前缀不是从路由器学习的。链路本地地址始终采用 `FE80::/64` 前缀。

这意味着，主机不再需要通过学习 `MAC` 地址来发送本地数据，而是需要学习其子网内所有其他主机的链路本地地址。这是通过一个被称为“邻居发现”的过程实现的。它使用邻居请求消息（`neighbor solicitation messages`）和邻居公告消息（`neighbor advertisement messages`）完成。这些消息都发送到为该过程标准化的 `IPv6` 组播地址。

当主机需要另一个节点的链路层地址时，会在本地链路上发送邻居请求消息（见图 10.17）。邻居请求消息中的源地址是发送该请求的节点的 `IPv6` 地址。邻居请求消息中的目的地址是与目标节点 `IPv6` 地址对应的请求组播地址（`solicited-multicast address`）。邻居请求消息还包括源节点的链路层地址。

## 图 10.17 IPv6 邻居发现：邻居请求消息

![](img/4bd64f839ec160c6df32218bb0d3893c_405_1.png)

目标节点通过在本地链路上发送邻居公告消息进行响应，该消息 `ICMP` 数据包头的 `Type` 字段值为 `136`。邻居公告消息的数据部分包含发送公告的节点的链路层地址。源节点收到邻居公告后，源节点和目标节点即可通信。

# 隧道技术 (Tunneling)

当隧道作为向 `IPv6` 过度的机制时，它涉及到将一种类型的协议封装在另一种类型的协议中，以便跨支持该数据包类型或协议的网络进行传输。在隧道端点，数据包会被解封装，并以原始形式对其内容进行处理。

`Overlay` 将 `IPv6` 数据包封装在 `IPv4` 数据包中，以便跨越 `IPv4` 网络交付。`Overlay` 隧道可以在边界路由器之间，或边界路由器与支持 `IPv6` 和 `IPv4` 的主机之间配置。`Cisco IOS` 支持以下隧道：

- 手动 (`Manual`)
- 路由封装 (`GRE`)
- `ISATAP`

接下来的章节将介绍一些重要方法。

## GRE 隧道

虽然没有被作为 `IPv6` 转换机制，但在讨论隧道技术时，通用路由封装 (`GRE`) 隧道也值得讨论。`GRE` 是一种通用封装，允许通过 `VPN` 将数据包从一个网络传输到另一个网络。它的优点之一是能够使用路由协议。它还能够携带非 `IP` 流量，并且当实现为 `GRE over IPsec` 隧道时，它支持加密。当构建这种隧道时，`GRE` 封装将发生在 `IPSec` 加密过程之前。需要记住的一点是，两端的隧道接口必须在同一个子网内。

## 6to4 隧道

`6to4` 隧道对于在仍为 `IPv4` 的网络上传载 `IPv6` 数据非常有用。在某些情况下，你会有 `IPv6` 子网或你的网络部分全都是 `IPv6`，而这些网络将相互通信。这可能发生在广域网 (`WAN`) 或你无法控制的其他网络上。我们如何解决这个问题呢？通过创建一个隧道，为你跨越 `IPv4` 网络承载 `IPv6` 流量。现在拥有一个隧道并不难，理解它很难。它实际上是获取通常在网络中传输的 `IPv6` 数据包，将其抓取，并在前面放置一个 `IPv4` 头部，该头部指定的 `IPv4` 协议类型为 `41`。

## 第 10 章 ■ 路由协议

当你配置手动或自动隧道（在后续章节中介绍）时，必须配置三个关键部分：

- 隧道模式 (`tunnel mode`)
- `IPv4` 隧道源 (`source`)
- 位于 `2002::/16` 之内的 `6to4` `IPv6` 地址

## 手动 IPv6 隧道

为了实现这一点，我们将使用几台双栈路由器，只需要添加一些配置来在路由器之间建立隧道。隧道非常简单。我们只需要告诉每个设备隧道从哪里开始，到哪里结束。让我们来看。以下配置创建了所谓的手动 `IPv6` 隧道。

```
Router(config)#int tunnel 0
Router(config-if)# ipv6 address 2001:db8:1::/64
Router(config-if)#tunnel source 192.168.30.1
Router(config-if)#tunnel destination 192.168.40.1
Router(config-if)# mode ipv6ip
Router(config)#int tunnel 0
Router(config-if)# ipv6 address 2001:db8:2::/64
Router(config-if)#tunnel source 192.168.40.1
Router(config-if)#tunnel destination 192.168.30.1
Router(config-if)# mode ipv6ip
```

这将允许我们的 `IPv6` 网络进行通信。

## 6to4（自动）

以下配置使用了所谓的自动 `6to4`。“自动”意味着一旦设置了 `ISATAP` 服务器/路由器，只需配置客户端连接即可。示例配置所示：

```
R1(config)#ipv6 unicast-routing
R1(config)#interface tunnel 1
R1(config-if)# tunnel source ethernet
R1(config-if)# tunnel mode ipv6ip isatap
R1(config-if)# ipv6 address 2001:0DB8::/64 ei-64
```

值得注意的是：如果你在这种情况下穿越的 `IPv6` 网络存在 `NAT` 转换点，这将破坏我们创建的隧道 `IPv6` 封装。在后续章节中将讨论解决方案。

## 高级 IPv6 概念

```
Router(config-if)# interface
Router(config-if)# no ip address
Router(config-if)# ipv6 unnumbered ethernet
Router(config-if)# tunnel source ethernet
Router(config-if)# tunnel mode ipv6 6to4
Router(config-if)# exit
```

在使用 `6to4` 隧道时，很多情况下需要在创建邻居语句（例如在 `BGP` 中）引用隧道端点。这样做时，可以通过三种方式引用前面示例中的自动配置地址：

```
:: c0a8:6301
:: 192.168.99.1
0:0:0:0:0:192.168.99.1
```

要配置指向跨越 `6to4` 隧道的静态路由，使用 `ipv6 route` 命令。这样做时，命令引用的地址的低 `32` 位将对应于分配给隧道源的 `IPv4` 地址。例如，在下面的命令最后的 `32` 位将是隧道 `0` 的 `IPv4` 地址。

内部自动隧道地址协议是另一种在 `IPv4` 网络上传输 `IPv6` 数据包的机制。“自动”意味着一旦设置了 `ISATAP` 服务器/路由器，只需配置客户端连接即可。示例配置所示：

```
IPv6 route 2002::16 tunnel 0
```

## Teredo

`Teredo` 为位于 `IPv4` 网络但没有直接原生 `IPv6` 连接的 `IPv6` 主机提供了完整的 `IPv6` 连性。其独特之处在于即使位于家庭路由器等网络地址转换 (`NAT`) 设备之后也能执行其功能。

# 第 10 章 ■ 路由协议

基于 `IPv4` 的 `Teredo` 协议执行若干功能：

- 诊断 `IPv4` 之上的 `UDP` (`UDP4`) 连性并识别存在的 `NAT` 类型（使用 `STUN` 协议的简化替代方案）
- 为每个主机分配一个全局唯一的 `IPv6` 地址
- 将 `IPv6` 包封装在 `IPv4` 数据报中，以便在 `IPv4` 网络上进行传输（包括 `NAT` 穿透）
- 通过 `Teredo` 主机和原生（即非 `Teredo`）`IPv6` 主机路由流量
- 有一些组件可以构成 `Teredo` 基础设施：

`Teredo` 客户端 (`Teredo Client`) 通过 `NAT` 设备具有互联网 `IPv4` 连性，并使用 `Teredo` 隧道协议访问 `IPv6` 互联网的主机。

`Teredo` 服务器 (`Teredo Server`) 用于 `Teredo` 初始配置的已知主机。

`Teredo` 中继器 (`Teredo Relay`) `Teredo` 隧道的远端。`Teredo` 中继器可能会代表服务的 `Teredo` 客户端转发所有数据，但 `Teredo` 客户端到 `Teredo` 客户端之间的直接交换除外。

`Teredo` 主机特定中继器 (`Teredo Host-Specific Relay`) 服务范围仅限于其运行所在主机的 `Teredo` 中继器。

# 双栈 (Dual Stack)
