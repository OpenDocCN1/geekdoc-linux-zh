
`gated` 最初作为免费分发的软件发布，但在 1992 年它被私有化并移交给 Merit GateD 联盟。该联盟最终解散，`gated` 的权利仅对联盟成员开放。`gated` 的权利被嵌入式网络软件开发商 NextHop 收购。这实际上结束了 `gated` 在开源世界的生命，留下了一段段未诉说的苦涩故事。

一个很有前景的项目 XORP（可扩展开放路由器平台）应运而生，以填补 `gated` 没留下的空白。尽管 XORP 现在处于 Beta 测试阶段，但它正为生产环境做好准备，我们希望它能填补 `gated` 的空白。可以在 www.xorp.org 查看最新进展。

同时，需要多协议路由的用户可以考虑 GNU Zebra (www.zebra.org)，这是一个运行在大多数 Linux 平台上的基础（硬核）路由包。遗憾的是，它缺乏在生产环境中管理动态路由所需的大部分功能、便利特性和详细文档。在这种情况下，购买专用路由器（如 Juniper 或 Cisco 制造的设备）可能是对资源的最优利用。

# 第13章 – 路由

## 13.6 路由策略选择标准

网络路由基本上可以分为四种复杂度进行管理：

- 无路由
- 仅静态路由
- 大多为静态路由，但客户端监听 RIP 更新
- 到处都是动态路由

整个网络的拓扑对每个网段的路由需求有巨大影响。不同的网络可能支持不同程度的路由。以下经验可以帮助你选择策略：

- 独立网络不需要路由。
- 如果网络只有一个出口，该网络上的客户端（非网关机器）应该有一个指向该唯一网关的静态默认路由。除了网关本身外，不需要其他配置。
- 一侧有少量网络、另一侧有通往“世界”网关的网关，可以使用指向前者的静态路由和指向后者的默认路由。然而，如果双方都有多个一个路由选择，建议使用动态路由。
- 如果你使用 RIP 并担心其带来的网络和负载，请在活动模式下 `routed`——它会以短间隔广播它所知道的一切（无论正确与否）。要让客户端被动监听路由更新而不发送自己的信息，请使用 `routed-q`。
- 许多人会告诉你 RIP 是一个糟糕、极其可怕的协议，而 `routed` 是撒旦的延伸。事实并非如此。如果它对你有效且你对性能感到满意，尽管使用它。在过度工程的路由策略上花费时间并不会加分。
- `routed` 监听所有人的信息并相信它看到的一切。即使你使用 RIP 也是如此。即使你使用 RIP，你可能也会在 Cisco 处使用 IOS 提示符。
- 在拥有多个路径的 Cisco 设备上使用动态路由。
- 在跨越边界的路由 处使用 OSPF。
- 拥有多个上游节点的路由器必须使用 BGP。
- 对于一个具有稳定结构并连接到外部的站点，良好的策略是使用静态路由和动态路由的组合。
- 配置过于复杂的网络应依赖静态路由运行 `routed`。
- 多个上游的路由器使用静态路由。

## 13.7 Cisco 路由器

由 Cisco Systems, Inc. 制造的路由器是事实上的标准，占据了 70% 的路由器市场，操作相对容易。

从命令行提示符修改配置，使用 `config term`：

- 大多数 Cisco 产品运行 IOS，它定义了两个访问级别（用户和特权）。输入正确的密码后，你会收到 IOS 提示符。

```
$ telnet acme
```

User Access

Password:

输入正确的密码后，你会收到来自 Cisco 的解释器提示符。在该提示符下，你可以输入如 `show interfaces` 等命令。要进入特权模式，输入 `enable` 并在请求时输入特权密码。一旦进入特权级，你的提示符将变为 `#`：

```
acme-gw.acme.com#
```

这是一个典型的配置：

```
acme-gw.acme.com# show running
Current configuration:
version 12.1
hostname acme-gw
enable secret xxxxxxxx
ip subnet-zero

interface Ethernet0
description internal network
ip address 192.108.21.254 255.255.255.0
ip directed-broadcast
interface Ethernet1
description backbone network
ip address 192.225.33.254 255.255.255.0
no ip directed-broadcast

ip classless
line con 0
transport input none

line aux 0
transport input telnet
line vty 0 4
password xxxxxxxxxx
login

end
```

路由器配置可以通过多种方式修改。Cisco 提供了运行在某些 UNIX/Linux 和 Windows 版本下的图形界面工具。真正的网络管理员从不使用这些；命令行提示符总是“稳妥的选择”。也可以将配置文件传输到路由器上，以便使用你喜欢的编辑器进行编辑。

从命令行提示符修改配置，输入 `config term`：

```
acme-gw.acme.com# config term
```

输入配置命令，每行一个。以 CNTL/Z 结束。

```
acme-gw(config)#
```

然后你可以输入你希望在 `show running` 输出中看到的新配置。例如，如果我们想更改示例中 Ethernet0 接口的 IP 地址，我们可以输入：

```
interface Ethernet0
ip address 192.225.40.253 255.255.255.0
```

- 可以配置多种访问方法。如果你的站点已经使用了 Cisco 路由器，请联系你的网络管理员以他们开启了哪些方法。

完成配置命令的输入后，按下 <Control-Z> 返回到常规命令提示符。如果你对新配置满意，输入 `write mem` 将配置保存到非易失性内存中。

以下是成功使用 Cisco 路由的一些技巧：

- 使用 `hostname` 命令为路由器命名。这一预防措施有助于防止在错误的路由器上进行配置更改导致的意外。主机名始终显示在命令提示符中。
- 始终手头保留一份路由器配置备份。你可以编写一个短的 `expect` 脚本，每晚上通过 `tfps` 将运行中的配置传输到 Linux 机器上保存。
- 通过在路由器的 VTY 上设置访问控制列表（VTY 类似于 Linux 机器上的 PTY）来控制对路由器命令行的访问。这一预防措施可以防止无关人员试图入侵你的路由器。
- 在每个接口上使用访问控制列表来控制各个网络之间（以及可能到另一侧）的流量。请参阅第701页的“数据包过滤防火墙”获取有关如何设置访问控制列表的更多信息。
- 保持路由器的物理安全。如果你有物理访问 Cisco Cisco 设备的权限，很容易重置特权密码。

### 13.8 推荐阅读

PERLMAN, RADIA. Interconnections: Bridges, Routers, Switches, and Internet Protocols (2nd Edition). Reading, MA: Addison-2000.

这是该领域的权威著作。如果你只想买一本关于网络基础知识的书，这本应该是你的之选。此外，永远不要错过和 Radia 待在一起的机会——她非常有趣，而且脑子里装的知识多到令人惊叹。

HUITEMA, CHRISTIAN. Routing in the Internet (2nd Edition). Upper Saddle, NJ: Prentice Hall PTR, 2000.

这本书从零开始对路由进行了清晰且良好的介绍。它涵盖了大多数常用的协议，还涵盖了一些诸如多播等进阶话题。

MOY, JOHN T. OSPF: Anatomy of an Internet Routing Protocol. Reading, MA: Addison-Wesley, 1998.

由 OSPF 标准作者对 OSPF 的详尽阐述。

STEWART, W. BGP4 Inter-domain Routing in the Internet. Reading, MA: Addison-Wesley, 1999.

有很多与路由相关的 RFC。许多显示在表 13.3 中。

现代版本的 IOS 支持 SSH 协议。如果你的环境中可用 SSH，你应该使用它来替代标准的 TELNET 接口。

### 13.9 练习

表 13.3 路由相关的 RFC

| RFC | 标题 | 作者 |
|---|---|---|
| 2328 | OSPF 版本 2 | John T. Moy |
| 1058 | 路由信息协议 | C. Hedrick |
| 2453 | RIP 版本 2 | Gary Scott Melton |
| 1256 | ICMP 路由器发现消息 | Stephen D. Deering |
