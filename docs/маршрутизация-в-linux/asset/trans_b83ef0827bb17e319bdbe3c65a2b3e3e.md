

## 总结

本章涵盖了两个非常重要的主题：网络分析和服务质量。首先介绍了几个网络分析工具（NET-SNMP、MRTG 和 IPTraf），这些工具在网络支持和分析中应发挥非常重要的作用。

网络分析可以透视网络内部，帮助确定网络当前的表现以及未来可能的表现。提供 QoS 目前是网络中最具挑战性的方面之一，需要同时进行分析并理解这里所介绍的 QoS 概念。

## III
附录

- **A** Linux 路由资源
- **B** Linux 硬件路由解决方案

## Linux 路由资源

本附录为 Linux 管理员提供了许多路由资源的指引。虽然我们特别小心地选择了大多稳定的链接，但请记住 URL 是临时性的。

### Linux 路由守护进程

我们在本书中讨论了许多路由守护进程，还有一些因篇幅原因未能涵盖。表 A.1 列出了我们能够为 Linux 用户整理的最完整的多协议路由守护进程列表，按主页排列。此表的图例如下：

- y. 该功能在此程序的至少一个版本中得到支持。
- n. 该功能在此程序的任何版本中都不受支持。
- p. 该功能可能尚未实现，也可能已经实现，但目前仍在开发中。

与往常一样，这里的重点专门针对互联网协议（IP）。

### 表 A.1 多协议 Linux 路由守护进程及其功能定位

| 名称 | 主页 | 单播 | 多播 | IPv4 | IPv6 |
|---|---|---|---|---|---|
| bird | http://bird.network.cz/ | y | n | y | y |
| gated | http://www.gated.org/ | y | y | y | y |
| mrdt | http://www.mrdt.net/ | y | y | y | y |
| zebra | http://www.zebra.org/ | y | p | y | y |

表 A.2 包含了我们能够整理的最完整的单协议 Linux 路由守护进程列表。

### 表 A.2 单协议 Linux 路由守护进程及其功能定位

| 名称 | 主页 | 协议 |
|---|---|---|
| mrouted | ftp://parcftp.xerox.com/pub/net-research/ipmulti/ | DVMRP |
| pim6d | ftp://catarina.usc.edu/pub/pim/pimd/ | PIM-SM |
| pim6d-dense | http://antc.uoregon.edu/PIMDM/pimd-dense.html | PIM-DM |
| routed | 随所有主流 Linux 发行版提供。 | RIP-2 |

### Linux 路由和流量管理工具

网络管理员似乎总是知道又多一个统计数据，用以帮助确定网络连接的成本和使用效率数据、数据安全性等。Linux 世界有大量的网络工具。具体来说，本节重点介绍与路由结合使用的工具。

表 A.3 包含我们认为在您尽可能高效地实现工作自动化过程中可能会有用的程序列表。

### 表 A.3 与路由结合使用的 Linux 工具

| 名称 | 主页 | 描述 |
|---|---|---|
| CIPE | http://sites.inka.de/sites/bigred/devel/cipe.html | 加密 IP 封装（CIPE）项目正在致力于开发能够加密 IP 数据包以传输到特定目的地的路由器。 |
| Edge Fireplug | http://edge.fireplug.net/ | 专用 Linux 发行版，可将机器基本上转变为网络路由和防火墙设备。 |
| heartbeat | http://www.linux-ha.org/download/ | 监控工具，用于根据可用性动态切换网络信息。 |
| IPTraf | http://cebu.mozcom.com/riker/iptraf/index.html | IP 流量监控和统计信息生成器。 |
| lcrzoex | http://www.laurentconstantin.com/us/lcrzo/lcrzoex/ | 网络测试工具包。 |
| Linux Router Project | http://www.linuxrouter.org/ | 一个适合放在单张软盘上的 Linux 微发行版，启动并配置后可将机器变成路由器。 |
| MRTG | http://people.ee.ethz.ch/~oetiker/webtools/mrtg/ | 多路由器流量图形器（MRTG）可实时累积和分析数据，以向您展示网络性能数据。 |
| VisualRoute | http://www.visualware.com/visualroute/index.html | 图形化增强的 traceroute 实用工具。 |

### 相关资源

路由只是 TCP/IP 网络难题中的一块。还有许多其他方面您可能并不完全熟悉。表 A.4 列出了其中许多网络问题和难点的资源指引。

### 表 A.4 TCP/IP 网络问题资源
| 名称 | 主页 | 描述 |
|---|---|---|
| IETF Home | http://www.ietf.org/ | 互联网工程任务组（IETF）的所有工作组及其正在最终确定的协议的存储库。 |
| RFC Repository | http://www.faqs.org/rfcs | 可搜索的“请求评论（RFC）”存储库。 |
| Stardust | http://www.stardust.com/ | Stardust.com 提供了一系列与路由相关技术的频道，例如多播、服务质量、无线和 IPv6。 |
| Types of DSL | http://www.efficient.com/tic/dslt ypes.html | Efficient Networks 对现存的各类数字用户线路（DSL）的详细分类。 |
| USAGI Project | http://www.linux-ipv6.org/ | Linux IPv6 开发新闻和工具。 |

