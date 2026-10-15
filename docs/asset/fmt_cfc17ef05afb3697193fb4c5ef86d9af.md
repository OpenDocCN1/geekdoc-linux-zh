
## no: 管理 AIX 网络调优参数

AIX 将其系统级 TCP/IP 选项分到了一个独立的、并行的持久属性/值对世界，这些对通过 `no` 命令而非 `chdev` 进行访问。区别在于，`no` 用于系统级配置，而 `chdev` 用于配置特定设备的实例。

你可以运行 `no -a` 来查看所有可用变量列表——目前有超过 125 个。表 14.14 列出了其中一些具有安全影响的变量。

### 表 14.14 AIX 安全相关的 TCP/IP 调优变量

| 变量 | 含义 | 默认值 |
| :--- | :--- | :--- |
| bcastping | 响应广播 ping | 0 |
| directed_broadcast | 允许转发广播包 | 0 |
| ipforwarding | 允许 IP 转发 | 0 |
| ignoreridirects | 忽略 ICMP 重定向 | 0* |
| ipscrouteforward | 转发源路由 IP 数据包 | 1* |
| ipscroutecevr | 接受源路由 IP 数据包 | 0 |
| ipscroutesend | 阻止发送源路由数据包 | 1 |

* a. 可能建议更改

要设置变量，请使用 `no -p -o variable=value`
例如，为了防止 TCP/IP 协议栈转发源路由数据包，你会使用命令：
`aix$ sudo -p -o ipscrouteforward=0`
`-p` 选项使得更改在立即生效并在重启后依然有效。

## 14.16 推荐阅读

STEVENS, W. RICHARD. *TCP/IP Illustrated, Volume One: The Protocols*. Reading, MA: Addison-Wesley, 1994.

WRIGHT, GARY R., AND W. RICHARD STEVENS. *TCP/IP Illustrated, Volume Two: The Implementation*. Reading, MA: Addison-Wesley, 1995.

这两本书是 TCP/IP 协议栈极佳且详尽的指南。虽然有些过时，但依然非常扎实。

STEVENS, W. RICHARD. *UNIX Network Programming*. Upper Saddle River, NJ: Prentice Hall, 1990.

STEVENS, W. RICHARD, BILL FENNER, AND ANDREW M. RUDOFF. *UNIX Programming, Volume 1, The Sockets Networking API (3rd Edition)*. Upper Saddle River, NJ: Addison-Wesley, 2003.

STEVENS, W. RICHARD, *UNIX Network Programming, Volume 2: Interprocess Communications (2nd Edition)*. Upper Saddle River, NJ: Addison-Wesley, 1999.

这些书籍是涉及编程的网络类课程中学生的“圣经”。如果你只需要 Berkeley sockets 接口，原版仍然是一个很好的参考书。如果你需要 STREAMS 接口，那么包含 IPv6 的第三版是一个很不错的选择。这三本书的写作风格都是典型的 Richard Stevens 风格。

TANENBAUM, ANDREW. *Computer Networks (4th Edition)*. Upper Saddle River, NJ: Prentice Hall PTR, 2003.

这是第一本网络教材，至今仍是经典。它详尽地描述了协议栈物理层和链路层中发生的所有细节。最新版涵盖了无线网络、千兆网络、点对点网络以及语音。

SALUS, PETER. *Internet: The History*. New York, NY: MIT Press, 2000.

COMER, DOUGLAS. *TCP/IP: A Top-Down Approach (5th Edition)*. Upper Saddle River, NJ: Prentice Hall, 2003.

FARREL, ADRIAN. *The Internet: A Modern Approach*. San Francisco, CA: Morgan, 2004.

KOZIER, CHARLES. *TCP/IP Guide: A Comprehensive*. San Francisco, CA: Starch, 2005.

HUNT, CRAIG. *TCP/IP Administration (3rd Edition)*. Sebastopol, CA: O'Reilly, 2002.

STEVENS, W. RICHARD. *TCP/IP Illustrated, Volume One: The Protocols*. Reading, MA: Addison-Wesley, 1994.

WRIGHT, GARY R., AND W. RICHARD STEVENS. *TCP/IP Illustrated, Volume Two: The Implementation*. Reading, MA: Addison-Wesley, 1995.

STEVENS, W. RICHARD. *UNIX Network Programming*. Upper Saddle River, NJ: Prentice Hall, 1990.

STEVENS, W. RICHARD, BILL FENNER, AND ANDREW M. RUDOFF. *UNIX Programming, Volume 1, The Sockets Networking API (3rd Edition)*. Upper Saddle River, NJ: Addison-Wesley, 2003.

STEVENS, W. RICHARD, *UNIX Network Programming, Volume 2: Interprocess Communications (2nd Edition)*. Upper Saddle River, NJ: Addison-Wesley, 1999.

TANENBAUM, ANDREW. *Computer Networks (4th Edition)*. Upper Saddle River, NJ: Prentice Hall PTR, 2003.

## 练习

14.1 如何 ICMP 重定向允许未经授权的用户攻击网络？

14.2 链路的 MTU 是多少？如果链路的 MTU 过高或过低会发生什么？

14.3 网络 134.122.0/16 被划分为 /19 网络。
a) 有多少个网络？列出来。
b) 每个网络有多少个主机？
c) 确定地址 134.122.67.12 属于哪个网络。
d) 每个网络的广播地址是多少？

14.4 位于 128.138.2.0/24 网络上的主机 128.138.2.4 想要向 128.138.129.12 发包。假设
* 128.138.2.4 刚刚启动，没有发送或接收过数据包。
* 网络上的其他机器已运行了很久。
* 路由器 128.138.2.1 与 128.138.129.1 有直接链路。
a) 发送所需的所有步骤。显示所有包的以太网和 IP 地址。
b) 如果网络是 128.138.0.0/16，你的答案会变化吗？为什么？
c) 如果网络 128.138.2.0 是 /26 而不是 /24，你的答案会变化吗？为什么？

14.5 DHCP 租约在服务器上是可以配置的。如果可分配的 IP 地址多于潜在客户端，应该将租约时间设得尽可能长（例如几周）吗？为什么？其他 DHCP 参数又呢？

14.6 安装新的 Linux 系统后，你会如何解决本章提到的安全问题？检查实验室中的 Linux 系统是否已经处理了这些问题。（可能需要 root 权限）。

14.7 在你的实验环境中添加新机器需要哪些步骤？在回答时，请使用适用于你的网络和本地情况的参数。假设操作系统已经安装。

14.8 为 ISC DHCP 服务器创建一个配置文件，分配范围在 128.138.192.[1-55] 的地址。租约时间设置为两小时，并确保以太网地址为 00:10:5A:C7:4B:99 的主机接收 IP 地址 128.138.192.55。

## 15 路由

追踪网络流量的下一个流向绝非易事。第 14 节简要介绍了 IP 数据包转发。在本章中，我们将更详细地检查转发过程，并研究几种允许路由器自动发现高效路由的网络协议。路由协议不仅减轻了维护路由信息的日常行政管理负担，还可以在路由器、链路或网络发生故障时，允许网络流量被快速重定向。

区分实际转发 IP 数据包的过程与驱动该过程的路由表管理是非常重要的，由于这两者通常被统称为“路由”。数据包转发是简单的，而路由计算是复杂的；因此，在实践中后者的含义更为更为频繁。本章仅描述单播路由：多播路由（向订阅者群组发送数据包）涉及一系列非常不同的问题，超出了本书的范畴。

对于大多数情况，第 14 节《TCP/IP 网络》中涵盖的信息就是你了解路由所需的全部知识。如果适当的网络基础设施已经就绪，你可以设置单条静态路由（如第 465 页开始的“路由”节所述），然后，你就拥有了足够的信息到达互联网上的几乎任何地方。如果你必须在复杂的网络拓扑中生存，或者你在使用 UNIX 或 Linux 系统作为网络基础设施的一部分，那么本章关于动态路由协议和工具的信息将大有用场。

IP 路由是“下一跳”路由。在任何给定点，处理数据包的系统只需要确定数据包在到达最终目的地路径中的下一个主机或路由器。这与遗留协议的方法不同，旧协议在数据包离开源主机之前就确定其将经过的精确路径，这种方案被称为源路由¹¹。

### 15.1 数据包转发：深入观察

在跳入路由表管理之前，让我们更详细地查看这些表是如何使用的。考虑图 A 所示的网络。

图 A 示例网络

![](img/579efec8c67772f31ecf34844bbb71a2_560_0.png)

路由器 R1 连接了两个网络，路由器 R2 将其中一个网络连接到外部。目前，我们假设 R1 和 R2 是通用计算机，而不是专用路由器。（我们假设本示例涉及的所有系统都使用 Linux 和 IPv4，在 IPv6 和 UNIX 系统上的命令和原理是类似的）。让我们来看一些路由表和一些特定的转发场景。首先，是主机 A 的路由表：

```
