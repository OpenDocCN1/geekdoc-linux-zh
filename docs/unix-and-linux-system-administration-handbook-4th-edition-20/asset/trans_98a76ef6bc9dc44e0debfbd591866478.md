

## no: 管理 AIX 网络调优参数

坦率地说，`mktcpip` 不仅仅处理设备参数——它还会运行 `rc.tcpip` 脚本以启动相关的网络守护进程。

SMIT 的网络配置功能相当完善，因此你可以、也应该依赖 SMIT 进行大部分基础配置。请查看“Communications Applications and Services”（通信应用程序与服务）主题下的 TCP/IP 配置选项。

大多数系统管理员永远不需要在 `chdev/lsattr` 这一层级对设备配置选项列表进行操作。例如，以下查询显示了网络接口 `en3`的可配置参数：

| aix lsattr -H -E -1 en3 | 描述 | 可设置 |
| :--- | :--- | :--- |
| alias4 | IPv4 包含子网掩码 | True |
| alias6 | IPv6 别名分区长度 | True |
| arp | 开启地址解析协议 (ARP) | True |
| authority | 授权用户 | True |
| broadcast | 192.168.10.255 | True |
| mtu | 1500 最大数据包大小 | True |
| netaddr | Internet | True |
| netaddr6 | IPv6 地址 | True |
| netmask | 255.255.255.0 子掩码 | True |
| prefixlen | IPv6 地址的前缀长度 | True |
| remmtu | 远程节点 576 最大数据包大小 | True |
| security | 安全级别 | True |
| up | 当前接口状态 | True |
| tcp_mss | 设置 TCP 分段大小 | True |
| tcp_nodelay | 启用/禁用 TCP_NODELAY 选项；设置接收缓冲区空间 | True |
| tcp_recvpace | 设置发送缓冲区空间 | True |

`-H` 选项要求输出列带有标签，`-E` 选项请求当前的“有效”（而非默认）值，而 `-i` 选项指定用于探测 `/dev` 中条目的的设备。你可以运行 `lsdev -C` 来查看可用设备的完整列表。

要设置值，请使用 `chdev`。例如，要将 `en3` 的 MTU 设置为 1450 以上，可以使用以下命令：

```bash
aix sudo chdev -en3 -mtu=1450
```

## no: 管理 AIX 网络调优参数

AIX 将其系统级 TCP/IP 选项分到了一个独立的、并行的持久属性/值对世界，这些对通过 `no` 命令而非 `chdev` 进行访问。区别在于，`no` 用于系统级配置，而 `chdev` 用于配置特定设备的实例。

你可以运行 **no -a** 来查看所有可用变量列表——目前有超过 125 个。表 14.14 列出了其中一些具有安全影响的变量。

### ### 表 14.14 AIX 安全相关的 TCP/IP 调优变量

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

要设置变量，请使用
**no -p -o variable=value**
例如，为了防止 TCP/IP 协议栈转发源路由数据包，你会使用命令：
`aix$ sudo -p -o ipscrouteforward=0`
**-p** 选项使得更改在立即生效并在重启后依然有效。

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

