
`-p` 选项使得更改在立即生效并在重启后依然有效。

### 14.16 推荐阅读

STEVENS, W. RICHARD. 《TCP/IP Illustrated, Volume One: The Protocols》。Reading, MA: Addison-Wesley, 1994.

WRIGHT, GARY R., AND W. RICHARD STEVENS. 《TCP/IP Illustrated, Volume Two: The Implementation》。Reading, MA: Addison-Wesley, 1995.

这两本书是 TCP/IP 协议栈极佳且详尽的指南。虽然有些过时，但依然非常扎实。

STEVENS, W. RICHARD. 《UNIX Network Programming》。Upper Saddle River, NJ: Prentice Hall, 1990.

STEVENS, W. RICHARD, BILL FINNER, AND ANDREW M. RUDOFF. 《UNIX Programming, Volume 1, The Sockets Networking API (第3版)》。Upper Saddle River, NJ: Addison-Wesley, 2003.

STEVENS, W. RICHARD, 《UNIX Network Programming, Volume 2: Interprocess Communications (第2版)》。Upper Saddle River, NJ: Addison-Wesley, 1999.

这些书籍是涉及编程的网络类课程中学生的“圣经”。如果你只需要 Berkeley sockets 接口，原始版仍然是一个很好的参考书。如果你还需要 STREAMS 接口，那么包含 IPv6 的第三版是一个很不错的选择。这三本书都以典型的 Richard Stevens 风格编写，表述清晰。

TANENBAUM, ANDREW. 《Computer Networks (第4版)》。Upper Saddle River, NJ: Prentice Hall PTR, 2003.

这是第一本网络教材，到目前它仍然是一部经典。它详细描述了协议栈物理层和链路层中发生的所有底层细节。最新版本涵盖了无线网络、千兆以太网、点对点网络、基于 IP 的网络等内容。

SALUS, PETER H. 《Casting the Net, From ARPANET to INTER and Beyond》。Reading, Ma: Addison-Wesley Professional, 1995.

这是一部关于 ARPANET 如何成长为 Internet 的精彩历史，由一位历史学家编写，他与 UNIX 人打交道的时间足够，听起来就像他们中的一员！

COMER, DOUGLAS. 《Interworking with TCP/IP Volume 1: Principles, Protocols, and Architectures (第5版)》。Upper Saddle River, NJ: Prentice Hall, 2006.

Doug Comer 的《Interworking with TCP/IP》系列长期以来一直是 TCP/IP 协议的标准参考。这些书是为本科生设计的，是背景材料良好的入门来源。

HUNT, CRAIG. 《TCP/IP Network Administration (第3版)》。Seabastopol, CA: O'Reilly Media, 2002.

与“一览（in the nutshell）”系列的其他书籍一样，这本书针对 UNIX 系统管理员。书中有一半关于 TCP/IP，另一部分处理更高级的 UNIX 功能，如电子邮件和远程登录。

FARREL, ADRIAN. 《The Internet and Its Protocols: A Comparative Approach》。San Francisco, CA: Morgan Kaufmann Publishers, 2004.

KOZIEAK, CHARLES M. 《The TCP/IP Guide: A Comprehensive, Illustrated Protocols Reference》。San Francisco, CA: No Starch Press, 2005.

在 `isoc.org/internet/history` 可以找到关于 Internet 历史及其各种技术的优秀文档集。

### 14.17 练习题

- E14.1 监听（即遵循）ICMP 重定向如何允许未经授权的用户破坏网络？
- E14.2 网络链路的 MTU 是什么？如果将给定链路的 MTU 设置得太高会发生什么？设置得太低又发生什么？

### E14.3

网络 `134.122.0/16` 已被划分为 `/19` 网络。

- a) 有多少个网络？列出它们。它们的子掩码是什么？
- b) 每个网络可以有多少个主机？
- c) 确定地址 `134.122.67.124` 属于哪个网络。
- d) 每个网络的广播地址是什么？

### E14.4

网络 `128.138.2/24` 上的主机 `128.138.2.4` 想要向网络 `128.138.2/24` 上的主机 `128.138.2.12` 发送数据包。假设：
- 主机 `128.138.2.4` 路由到 `128.138.2.12`。
- 主机 `128.138.2.4` 路由到 `128.138.2.12`。
- 主机 `128.138.2.4` 路由到 `128.138.2.12`。
- 路由器 `128.138.2.1` 路由到 `128.138.2.12`。
- a) 列出发送数据包需要哪些步骤。
- b) 如果 `128.138.2.0` 的掩码是 `/26`，结果会发生变化吗？
- c) 如果 `128.138.2.0` 的掩码是 `/25`，结果会发生变化吗？

### E14.5

DHCP 租约是可以配置的。

### E14.6

在安装新的系统后，对于网络需要哪些步骤？

### E14.7

对于网络，安装后需要哪些步骤？

### E14.8

为 DHCP 服务器创建一个新的配置文件。

## 15 路由

跟踪数据包的去向并非易事。在第 14 章中，我们简单介绍了数据包转发。本章将详细研究路由。IP 路由是“下一跳”路由。在任何一点，处理数据包的系统只需要确定数据包目的地的下一个主机或路由器。这与许多遗留协议不同，后者在数据包离开源主机之前就确定了确切路径，这种方案被称为源路由。动态路由协议减轻了维护路由表的日常负担，它们允许自动发现路由。对于大多数情况，设置静态路由，第 14 章涵盖的内容就足够了。如果你在网络基础设施中使用 UNIX 系统，那么本章关于路由协议的信息将很有帮助。

### 15.1 数据包转发：深入观察

在深入研究路由表管理之前，让我们更详细地查看它们是如何使用的。考虑图 A 所示的网络。

图 A 示例网络

![](img/9b33263d3e7e36cd43da775601c8735_560_0.png)

路由器 R1 连接两个网络，而路由器 R2 将其中一个网络连接到外部。现在，我们假设 R1 和 R2 是通用计算机而非专用路由器。让我们查看一些路由表和特定的转发场景。首先，主机 A 的路由表：

```
A$ netstat -rn

Kernel IP routing table

Destination Gateway Genmask Flags Window Interface If

199.165.145.0 0.0.0.0 255.255.255.0 U 0 0 eth0

127.0.0.0 0.0.0.0 255.0.0.0 U 0 0 lo

0.0.0.0 199.165.145.24 0.0.0.0 UG 0 0 eth0
```
