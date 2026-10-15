

## LocalTalk 和 PhoneNET

原始的 LocalTalk 网络硬件使用总线拓扑（p. 81），意味着 Macintosh 计算机以单线方式相互连接。计算机硬件本身类似于高速串行端口，而电缆价格相当昂贵。LocalTalk 的速度限制在 2Mbps 以下——在其推出时算快，但与 10Mbps 的同轴以太网相比较慢，与当今 100Mbps 的 100BaseT 速度相比则慢得令人难以忍受。另一个限制是电缆长度：其最大长度为 1,000 英尺，这使其介于 10Base2 和 10Base5 以太网电缆的限制之间（见表 1.1，p. 10）。

为了既延长 LocalTalk 的电缆长度限制又降低电缆成本，Farallon 公司推出了名为 PhoneNET 的产品，该产品通过普通电话线传输 LocalTalk 信号。PhoneNET 的最大运行长度为 3,000 英尺，但并未提高 LocalTalk 的速度。由于 PhoneNET 使用计算机外部的适配器而不是内部硬件，因此只要计算机支持 LocalTalk，就可以使用 PhoneNET。

尽管相当罕见，但用于 PC 的 LocalTalk 板确实存在。如果你希望你的 Linux 服务器处理旧 LocalTalk 网络上的流量，可以尝试找到 Apple/Farallon LocalTalk 板或 COPS LocalTalk 板。这两种产品都在 Linux 2.2 系列内核中得到支持。本书未描述其配置和使用方法，但除基本配置外，本章所述的相同原则也应适用于使用此类产品的网络。

## Ethernet

由于以太网的速度优势巨大，为 10Mbps——现在为 100Mbps——Apple 最终开始生产带有以太网端口的 Macintosh。事实上，像 iMac 这样的近期机型已不再支持 LocalTalk，仅支持以太网，并且这些最新计算机支持 100BaseT 以太网。

幸运的是，以太网对所承载的数据类型并不挑剔，因此 Apple 能够将 AppleTalk 适配到以太网。由此产生的以太网承载 AppleTalk 的用法有时被称为 EtherTalk。你可以拥有一个仅承载 AppleTalk 流量的以太网网络，也可以拥有一个混合 AppleTalk 与 TCP/IP 的网络。鉴于 Open Transport 的速度优势，最好使用 Open Transport 将 AppleTalk 封装在 TCP/IP 内部！

## AppleTalk 与 TCP/IP 之间的差异

与 NetBIOS/NetBEUI 一样，AppleTalk 旨在用于小型计算机网络。对于办公室局域网中几十台计算机，它非常有效，但在此之外扩展性不佳。这部分是由于与 NetBIOS 类似，AppleTalk 的命名方案本质上是两层的：每台计算机都有自己的名称，并且计算机可以被分组到称为区域的集合中，这类似于 Windows 网络中的工作组或域（p. 277）。不过，没有办法将 AppleTalk 区域分组到更大的集合中。

相比之下，TCP/IP 旨在用于具有更多组织层级的更大网络。事实上，这也是 TCP/IP 而非 AppleTalk 或 NetBIOS 成为互联网基础的原因之一。

AppleTalk 使用 ID 号来标识单个计算机，但 AppleTalk 包含使网络上的计算机相互协商以自动确定其 ID 号的程序。因此，在 AppleTalk 网络中，你无需直接处理 IP 地址或其等价物——至少在 Open Transport 及其 AppleTalk over TCP/IP 进入方程之前如此。

## 同一以太网上的 TCP/IP 和 AppleTalk

尽管 AppleTalk 和 TCP/IP 是完全独立的协议，但它们可以在同一根以太网电缆上共存而不会冲突。这是因为以太网本身具有数据封装协议，如第 2 章“理解 TCP/IP”所述。就网络硬件和驱动程序的最低层级而言，任何给定的以太网数据包都只是以太网数据包。然而，随着驱动程序检查以太网数据包，它们很快就会发现数据应发送到哪个网络栈——TCP/IP 或 DDP，因此这两个协议在计算机网络层次结构的非常低的层级上就被分开了。

如本章前面所述，AppleTalk 也可以通过 TCP/IP 传输，在这种情况下，大部分以太网流量由 TCP/IP 数据报组成。在这种情况下，协议也共存——只有 TCP/IP 栈在将数据传递给 AppleTalk 栈的适当部分之前处理大部分数据。

## 将 AppleTalk 支持编译到你的内核中

在 Linux 上准备 AppleTalk 网络时，你必须采取的第一个步骤之一是将对 AppleTalk 的 DDP 的支持编译到你的内核中。你可以通过从网络选项配置区域中选择 AppleTalk DDP 来完成此操作，然后重新编译你的内核并重新启动，如第 6 章“为网络编译内核”所述。

重新启动新内核后，你可以通过输入以下命令来检查 AppleTalk 支持是否实际存在：

```
dmesg | grep Apple -
```

如果 Linux 成功加载了 DDP 支持，你会看到类似以下的响应：

```
NET4: AppleTalk 0.18 for Linux NET4.0
```

如果你没有看到此类消息，请尝试重新检查你的内核编译和加载步骤。例如，我发现自己经常忘记在编译新内核后运行 lilo，这会导致旧内核仍然存在。

