

## 表 29.1 内核网络选项（续）

| 典型值 | 选项 | 描述 |
|---|---|---|
| N | IP: Multicasting | 支持将数据包发送到多台计算机——例如，用于连接到 MBONE（一种高速音视频网络）的主机。 |
| Y/N | IP: optimize as router not host | 禁用对拷贝和校验和操作的支持，这些操作可以提高主机性能但会降低路由器性能。 |
| Y | IP: TCP syncookie support | 支持用于防止 SYN 洪水拒绝服务攻击的 cookie 技术。 |
| Y | IP: transparent proxying | 允许防火墙将源自本地网络并目标为远程主机的数据包重定向到本地服务器（透明代理服务器）。 |
| M | IP: tunneling | 支持将具有一种协议的数据包封装在另一个协议的数据包中。 |
| M | IPL ipportfw masquerade support | 支持端口转发，允许你将源自本地网络且目标为防火墙指定端口的数据包转发到本地网络上主机的指定端口。 |
| M | IPVS: round-robin scheduling | 指定虚拟服务器将使用轮询调度。 |
| M | IPVS: weighted least-connection scheduling | 指定虚拟服务器将使用加权最小连接调度。 |
| M | IPVS: weighted round-robin scheduling | 指定虚拟服务器将使用加权轮询调度。 |

## 表 29.1 内核网络选项（续）

| 典型值 | 选项 | 描述 |
| --- | --- | --- |
| Y | Kernel/User netlink socket | 支持通过字符特殊文件进行内核与用户进程之间的通信。 |
| Y | Netlink device emulation | 一种很快将被移除的后兼容性。 |
| Y | Network firewalls | 支持基于数据包过滤的防火墙和伪装。 |
| Y | Packet socket | 支持数据包协议，程序（如 tcpdump）使用它直接与网络设备通信。 |
| Y | Routing messages | 支持特殊文件 /dev/route，该文件允许你读取网络相关信息。 |
| Y | Socket filtering |允许用户过滤数据包（TCP 数据包除外）。 |
| Y | TCP/IP networking | 支持 TCP/IP 协议。 |
| Y | Unix domain sockets | 支持 Unix 域套接字，即使未连接到网络的主机也会使用。 |

## 动态路由

Red Hat Linux 提供了支持动态路由的守护进程。如果你需要动态路由，应该安装并配置其中之一。`routed` 守护进程通过路由信息协议（RIP）提供基础动态路由。更复杂的 `gated` 守护进程提供了多种路由协议，例如：

- RIP 和 RIP-2
- 间间系统 (IS-IS)
- 开放路径优先 (OSPF-2)
- 外部网关协议 (EGP)
- 边界网关协议 (BGP-4)

RIP、IS-IS 和 OSPF-2 是内部路由协议，适用于网络或自治系统内部。RIP 是一种距离矢量路由协议，仅向邻居告知其路由。IS-IS 和 OSPF-2 是链路状态路由协议，要求每个路由主机维护网络地图。当网络链路状态发生变化时，广播消息会通知路由器变化。RIP 适用于管理局域网（LAN）；OSPF-2 适用于管理大型网络。EGP 和 BGP-4 是外部路由协议，适用于自治系统之间。特别是 BGP-4——一种距离矢量协议——被用于互联网，因此被 ISP 广泛使用。EGP 是一种已不再流行的旧协议。表 29.2 总结了这些协议。

## Red Hat Linux 支持的路由协议

| 协议 | 内部/外部 | 类型 |
| --- | --- | --- |
| BGP-4 | 外部 | 距离矢量 |
| EGP | 外部 | 距离矢量 |
| IS-IS | 内部 | 链路状态 |
| OSPF-2 | 内部 | 链路状态 |
| RIP, RIP-2 | 内部 | 距离矢量 |

## 总结

在本章中，你学习了如何配置 Linux 路由器。的最重要主题是：

**路由** - 路由将数据包从一个网络主机转发到另一个主机。最基本的路由操作是转发，它接收从网络接口进入的数据包并通过适当的网络接口重新发送。要启用路由，请使用 `linuxconf` 设置 IP 网络配置选项。

Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com

路由表 - Linux 内核维护着路由表，指定每个本地接口的网络地址以及通过该接口可以访问的网络和主机。

静态和动态路由 - 在静态路由中，路由表是手动建立和维护的。在动态路由中，路由表会自动更新以适应变化的情况（例如设备故障）。

配置路由 - 可以通过 `linuxconf` 或 `ifconfig` 和 `route` 命令配置路由。

配置路由内核选项 - Linux 内核支持多种路由选项。要配置系统作为路由器而非服务器或工作站，请启用内核选项 `IP: advanced router` 和 `IP: optimize as router not host`。

## 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 距离矢量路由协议
- 动态路由
- 外部

