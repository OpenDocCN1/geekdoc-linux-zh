

# 摘要

你在 Linux 中最有可能在大型、子网化或多网络环境中使用的单播路由协议是 RIP-1、RIP-2 和 OSPF。RIP-1 是至今仍在互联网上使用的最古老的 TCP/IP 路由协议之一。因此，它也是最不灵活的，真正只适用于小型网络。RIP-2 稍新且更安全，虽然它对于大型网络并没有好多少，但在许多情况下是比 RIP-1 更明智的选择。最后是更稳健的 OSPF。如果你的网络倾向于发生变化或机器经常出现故障，你最好选择这个选项。别忘了静态路由！对于非常小的局域网（大约 10 台机器）或子网，这可能就足够了。表 1.6 列出了每种协议的相关数据，可能对你感兴趣。

表 1.6 在 Linux 中实现单播路由协议的程序，以及包含重要背景信息的 RFC 文档

| Protocol | Program | RFC |
|---|---|---|
| RIP-1 | routed, gated, or zebra | 1058 |
| RIP-2 | gated or zebra | 1721 |
| OSPF | gated or zebra | 2328 |

一个阅读请求评论（RFCs）的极佳场所是 http://www.faqs.org/。如果你是一名程序员，并且发现自己在没有仔细阅读代码之前很难理解某些东西的工作原理，那么请前往 http://www.packetfactory.net/ 并查看他们的 libnet 项目的代码。其中包含处理 RIP-1 和 OSPF 的功能。

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_56_0.png)

## 2

## 多播协议

多播路由协议利用多播网络将信息广播到一个 IP 地址（频道或组），任何具有多播访问权限的计算机都可以收听。当路由器支持多播协议时，它可能需要也可能不需要知道在任何给定时间谁在收听。这取决于你的多播频道覆盖范围以及你选择的协议。

本章讨论了多种常用多播路由协议的背景信息。利用这些信息，可以就你希望用于管理自己的网络需求的协议做出明智的决定。

### 路由信息协议版本 2（RIP-2）

不，你的眼睛没有欺骗你。RIP-2 同时出现在单播和多播部分。你可以配置路由器使用此路由协议偶尔向多播地址发送更新——默认情况下发送到 224.0.0.9。事实上，RIP-2 有四种设置可用于指导其在多播和其他领域的行为：

- None. Disables all RIP-1 messaging.
- RIP-1. Tells RIP-2 to behave as though it were its predecessor.
- **RIP-1 Compatibility.** Tells RIP-2 to broadcast its updates directly to the other routers, taking into account those that need RIP-1 formatted data.
- **RIP-2.** Ignores RIP-1 issues and uses multicast to send updates.

None of these options, however, actually deals with multicast data aside from the protocol's own updates.

### 多播开放最短路径优先（MOSPF）

多播开放最短路径优先（MOSPF）协议是 OSPF 的一个版本，允许在自治系统内高效路由多播数据包（以及单播数据包）。此实现合并了 OSPF 和互联网组管理协议（IGMP），后者处理多播组成员资格。更妙的是，它保留了所有最佳功能，包括使用 OSPF 身份验证方案。

MOSPF 使用与 HELLO 协议相同的来回查询方式跟踪当前是多播组成员的节点。每个 MOSPF 路由器计算自己的树。注意“树”这个复数。每个路由器为每个源/目的对计算一棵单独的树。这棵树从源开始，经过路由器，一直到包含成员的网络。

停下来想一想这可能意味着什么。如果 MOSPF 路由器预先为自治系统中所有现有的多播源和组计算树，你的 MOSPF 路由器将忙于计算，以至于无法用于引导流量。

相反，只有当多播数据实际上需要从尚不存在树的源/目的对传输时，才会计算树。由于多播旨在将数据传递给所有组成员，其数据包（数据报）在沿最短路径传输时会为每个组成员复制一份。然而，这棵树并不像 OSPF 中那样对每个路由器都是唯一的——而是树的树干位于数据来源的路由器，所有接收和转发数据的路由器都使用该相同的起点作为其树。因此，处理这些数据的所有路由器都使用相同的最短路径树，即使它们各自自行计算。

> **构建树时处理平局**
> 如果存在成本相等的路径之间的平局，则不使用负载均衡。各种 MOSPF 实现都有特定的方法来选择用于最快、最短路径树的分支。

有趣的是，你可以在 OSPF 区域内混合使用 OSPF 和 MOSPF 路由器，甚至在整个自治系统中传播它们。为此，只需要有一组连续的能够进行多播的路由器，以便数据能够到达需要去的地方即可。

用于实现 MOSPF 的程序是 mrouted。你还需要进行一些调整，以便路由器完全启用多播。请参阅第 6 章，“Inside the Multicast Kernel 2.2.x Daemons”，了解如何完成此操作。

