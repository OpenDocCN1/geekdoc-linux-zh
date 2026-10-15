

## Summary

在本章中，我们快速浏览了影响 Linux 2.4.x 系列中路由/网络的一些变化。特殊情况太多，无法全面涵盖每个场景，但我们希望这能让你对“新”内核的预期有一个大致的了解。

在编译新内核时，请务必阅读第 13 章“Building a Routing Kernel”，该章详细概述了编译 Linux 内核的过程。

我们还查看了一些 Linux 的“高级”路由工具以及设置基本 VPN。虽然绝非对 VPN 的详尽介绍，但如果您决定在 Linux 路由器上实现 VPN，这应该能帮助您入门。

![](img/5f0cc5444dfa57f5c5cc6a7830396eaa_192_0.png)

# 9

## Inside the Commands

LINUX 提供了一系列 NETWORKING 命令来支持网络故障排除、IP 配置和路由任务。本章涵盖 ifconfig、route、ping、traceroute、arp、netstat 和 tcpdump。除了 tcpdump 之外，这些命令很可能会随大多数 Linux 发行版的标准安装一起提供。这些命令（再次除外 tcpdump）源自早期版本的 BSD 和 AT&T 的 System V 命令。

## ifconfig

ifconfig 是用于将接口投入服务并指定第 1 层到第 3 层属性的命令，例如媒体类型、速度和网络地址。（第 1 层涵盖网络的物理方面，例如双绞线或同轴电缆，第 2 层涵盖数据层，包括媒体相关网络，例如以太网帧和以太网网络中的媒体访问控制。）ifconfig 通常位于 /sbin/ 目录中，但非 root 用户也可以运行该程序。然而，只有 root 才能进行配置更改。在大多数 Linux 版本中，ifconfig 命令由 net-tools 分发提供，可在 http://www.tazenda.demon.co.uk/phil/net-tools/ 获取。

除了接口配置之外，ifconfig 还用于报告接口状态；因此，ifconfig 的功能可以分为两个部分：接口报告和接口配置。

### Interface Reporting

最常见的是 ifconfig 用于接口报告，以协助网络故障排除。

不带任何参数的基本命令非常有用：

```
[root@lefty /sbin]# /sbin/ifconfig
et0      Link encap:Ethernet  HWaddr 00:E9:29:4B:AC:0C
          inet addr:192.168.1.254  Bcast:192.168.1.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:9833  errors:0  dropped:0  overruns:0  frame:0
          TX packets:10195 errors:0  dropped:0  overruns:0  carrier:0
          collisions:306  txqueuelen:100 
          Interrupt:10  Base address:0xb800

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          UP LOOPBACK RUNNING  MTU:3924  Metric:1
          RX packets:18  errors:0  dropped:0  overruns:0  frame:0
          TX packets:18  errors:0  dropped:0  overruns:0  carrier:0
          collisions:0  txqueuelen:0
```

ifconfig 已报告内核识别并配置为使用的所有接口。（Linux ifconfig 与其他版本的 UNIX 不同，不需要额外参数即可查看所有接口。）在 eth0 上，我们可以很容易地确定接口基于接口名称（eth0）、Link encap:Ethernet 以及 6 字节（48 位）地址是以太网。下一行报告了 IP 地址以及使用的广播地址和网络掩码。

第三行报告接口当前正在运行（UP），这意味着它可以发送和响应网络流量。它以广播方式运行（以太网的标准），并且还配置为侦听多播流量。多播配置是必需的，以允许内核和 RIP-2 等用户应用程序检查多播流量，因为 RIP-2 使用 RIP 多播地址 224.0.0.9。

最大传输单元（MTU）为 1500 字节，这是以太网帧的标准长度，ifconfig 已报告这是内核配置的大小。正如名称最大传输单元所暗示的那样，这是将从该接口传输的最大数据包大小。如果管理员手动降低 MTU 的大小，它只会影响传出数据包，这意味着系统仍会识别在拓扑支持的最大 MTU 范围内的传入数据包。常见的 MTU 大小如表 9.1 所示。

