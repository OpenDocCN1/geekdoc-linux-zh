
# 图 29.5 典型网络

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_709_0.png)

如果你不带参数使用 `route` 命令，它会报告路由规则。以下是对应示例网络的输出：

## 内核 IP 路由表

| Destination | Gateway Genmask | Flags Metric Ref Use Interface |
|---|---|---|---|---|---|------|
| 192.168.1.1 | * | 255.255.255.0 | UH | 0 | 0 | 0 eth0 |
| 192.168.100.1 | * | 255.255.255.0 | UH | 0 | 0 | 0 eth1 |
| 10.1.1.1 | * | 255.255.255.0 | UH | 0 | 0 | 0 eth2 |
| 192.168.1.0 | | 255.255.255.0 | | 0 | 0 | 0 eth0 |
| 192.168.100.0 | | 255.255.255.0 | | 0 | 0 | 0 eth1 |
| default | 0.0.0.0 | | UG | 0 | 0 | 0 eth2 |
| 127.0.0.1 | | 255.0.0.0 | U | 0 | 0 | 0 lo |

`Flags` 字段可以包含此类值：

- U，表示网络链路已启用（up）
- H，表示目标地址指向主机而非网络
- G，表示路由规则指定了网关

Metric、Ref 和 Use 字段在启用动态路由外，其他情况下都是无关紧的。

现在完成练习 29.1 以获得网络配置的实践经验。

# 练习 29.1

## 网络配置

如果你可以访问连接到网络的三个主机，请将其中一个配置为连接剩余主机的路由器。然后，通过使用 `linuxconf` 和 `route` 实验指定各种路由规则，直到你对操作路由表感到熟悉。

完成此练习时，请参考本章和其他资源。但请准备好在参加 RHCE 考试时无需帮助执行类似操作。

# 内核配置

Linux 内核提供了多种与网络相关的选项。你可以在图 29.6 中看到大部分选项，它显示了包含网络相关选项的 `makeconfig` 页面顶部。表 29.1 总结了最重要的选项。作为路由器的 Red Hat Linux 有两个特殊的选项：IP: advanced router 和 IP: optimize as router host，它们在图 29.6 中不可见。如果 Linux 系统主要或专门用路由器使用，你应该指定这些选项并重新编译内核。

## 图 29.6 内核网络选项

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_711_0.png)

## 表 29.1 内核网络选项

| Typical Value | Option | Description |
|---|---|---|
| Y/N | IP: advanced router | 如果主机主要用路由器使用，则指定 Y |
| Y | IP: aliasing support | 包括为单个接口分配多个 IP 地址的支持 |
| N | IP: ARP daemon | 包括用户空间 ARP 进程的支持 |
| M | IP: autof support | 包括对缺乏自身协议助手的协议的支持 |
| Y/N | IP: broadcast over IP | 包括使用通用路由封装 (GRE) 构建类似普通局域网广播的支持 |
| Y | IP: firewall packet netlink | 支持创建一个接收匹配特定数据包拷贝的字符设备；用于监控网络流量并检测可能的攻击 |
| Y | IP: firewalling | 包括防火墙规则的内核支持 |
| M | IP: GRE tunnels over IP | 包括在 IPv4 上封装 IPv4。这种支持比 IP: tuning 选项提供的更具兼容性 |
| Y | IP: ICMP masquerading | 支持防火墙翻译源自本地主机的 ICMP 包，例如，允许只有私有 IP 的主机访问互联网 |
| M | IP: ipmarkfw | 支持防火墙标记转发，一种类似于端口转发的功能 |
| N | IP: kernel level autfiguration | 在内核启动期间自动配置网络接口 IP 地址和路由表；用于支持通过网络启动 |
| Y | IP: masquerading | 支持防火墙翻译源自本地网络的 UDP 和 TCP 包，使其看起来像源自防火墙主机。例如，允许只有私有 IP 的主机访问互联网 |
| Y | IP: masquerading special modules support | 包括可以修改伪装规则的模块的支持；这些模块用于 ipautfw 和端口转发 |
| M | IP: masquerading virtual server | 支持构建由两个或多个真实服务器组成的虚拟服务器 |
| 12 | IP: masquerading VS table size | 指定用于管理连接的哈希表的大小；实际表大小为2，其中 n 是指定的值 |
| N | IP: multicast routing | 支持路由组播包——即具有多个目标地址的数据包 |

### 表 29.1 内核网络选项（续）

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

### 表 29.1 内核网络选项（续）

| 典型值 | 选项 | 描述 |
| --- | --- | --- |
| Y | Kernel/User netlink socket | 支持通过字符特殊文件进行内核与用户进程之间的通信。 |
| Y | Netlink device emulation | 一种很快将被移除的后兼容性。 |
| Y | Network firewalls | 支持基于数据包过滤的防火墙和伪装。 |
| Y | Packet socket | 支持数据包协议，程序（如 tcpdump）使用它直接与网络设备通信。 |
| Y | Routing messages | 支持特殊文件 `/dev/route`，该文件允许你读取网络相关信息。 |
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

### 总结

在本章中，你学习了如何配置 Linux 路由器。的最重要主题是：

**路由** - 路由将数据包从一个网络主机转发到另一个主机。最基本的路由操作是转发，它接收从网络接口进入的数据包并通过适当的网络接口重新发送。要启用路由，请使用 `linuxconf` 设置 IP 网络配置选项。

Copyright©2000 SYBEX, Inc., Alameda, CA www.sybex.com

路由表 - Linux 内核维护着路由表，指定每个本地接口的网络地址以及通过该接口可以访问的网络和主机。

静态和动态路由 - 在静态路由中，路由表是手动建立和维护的。在动态路由中，路由表会自动更新以适应变化的情况（例如设备故障）。

配置路由 - 可以通过 `linuxconf` 或 `ifconfig` 和 `route` 命令配置路由。

配置路由内核选项 - Linux 内核支持多种路由选项。要配置系统作为路由器而非服务器或工作站，请启用内核选项 `IP: advanced router` 和 `IP: optimize as router not host`。

### 关键术语

在进入下一章之前，请确保你熟悉以下术语：

- 距离矢量路由协议
- 动态路由
- 外部

# 使用 ipchains 配置防火墙

本章涵盖的 RHCE 准备知识点：

- 能够使用 `ipchains` 实现基本的防火墙策略。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_723_0.png)

第 25 章“管理安全”描述了旨在保护系统免受未经授权使用的管理措施。除了这些实施在系统层面的保护措施外，大多数系统管理员还会采用实施在网络层实施的额外措施。一种流行的措施是*防火墙*，它可以过滤入站和出数据包，只允许授权的数据包进入和离开网络。

许多站点购买作为防火墙或防火墙/路由器的专用硬件单元。然而，Red Hat Linux 允许你配置运行在 PC 或 Red Hat Linux 支持的其他平台上的路由器。本章解释了基本的防火墙概念以及如何实现简单的防火墙。

## 防火墙概念

防火墙阻止未经授权的数据包进入或离开网络。Linux 内核 2.2 版本包含了对**iptables 功能**的支持，可以用于构建 IP 防火墙——即过滤 TCP/IP 数据包的防火墙。某些早期版本的 Linux 内核支持**ipfwadm 功能**，这是一个灵活性较低且现在已过时的功能。图 30.1 显示了一个典型的防火墙配置。在示例配置中，所有进入和离开受保护本地网络的数据包必须经过 Linux 防火墙。根据一组*防火墙规则*，防火墙会拦截可疑和未经授权的数据包。

## 图 30.1 典型的防火墙

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_724_0.png)

为了支持防火墙，Linux 内核必须使用相应的选项进行编译：

- Network firewalls
- IP: firewalling
- /proc filesystem

标准的 Red Hat 内核支持这些选项。要确定内核是否支持必要的选项，请检查文件 `/proc/net/ip_fwchains`；如果该文件存在，则支持这些选项。

> T/P 防火墙文档指出内核选项 IP: always defragment 必须配置。现在可以通过在 `/etc/sysctl.conf` 文件中包含行 `net.ipv4.ip_always_defrag=1` 来动态启用此选项。

## 伪装 (Masquerading)

伪装与防火墙密切相关，通常 Red Hat 系统会被配置为同时提供这两个功能。在伪装中，离开受保护网络的数据包被重写，使其看起来源自防火墙主机。同样，从受保护网络外部到达的相关数据包由防火墙主机重写，以指定实际目的地。伪装通常用于隐藏受保护网络内主机的身份。例如，网络内的主机可以分配私有 IP 地址——例如 192.168.1.0 C 类网络上的地址——但仍然可以包括互联网在内的外部网络。图 30.2 显示了一个典型的伪装防火墙。

## 图 30.2 伪装防火墙

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_725_0.png)

伪装 Linux 宿机的内核除了支持防火墙所需的选项外，还应该使用以下选项进行编译：

- IP: transparent proxy support
- IP: masquerading
- IP: masquerading special modules support
- IP: iportfw masc support

标准的 Red Hat Linux 内核包含了这些选项。

## iptchains 功能

`iptchains` 功能允许你控制 IP 数据包通过 Linux 内核的进度。图 30.3 显示了内核数据包路径。

## 图 30.3 内核数据包路径

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_726_0.png)

`ipchains` 功能允许你指定可以拦截、重定向或重写 IP 数据包的规则。规则可以根据以下区分数据包：

- 源主机或网络 IP 地址
- 源端口
- 目的主机或网络 IP 地址
- 目的端口
- 协议
- 连接类型 (SYN)

默认实现了三类过滤器，称为*链 (chains)*：

- input 链（入站链），控制数据包的接收
- output 链（输出链），控制数据包的发送
- forward 链（转发链），控制转发到另一个网络接口的数据包

## 使用 ipchains 实现防火墙

防火墙由三组 `ipchains`*数据包过滤器*规则组成，每个数据包链一组：input、output 和 forward。要使用 `ipchains` 功能实现防火墙，通过发布 `ipchains` 命令来指定过滤器规则，其通用形式为

```
