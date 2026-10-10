

# 第 5 章
## 服务器宕机了吗？追查网络问题的根源

大多数服务器都连接到某种网络，并通常使用网络来提供某种服务。网络中可能会出现各种各样的问题，因此网络故障排除技能对于负责这些服务器或其上服务的任何人来说都至关重要。Linux 提供了一整套网络故障排除工具，本章将讨论几种常见的网络问题，以及如何利用 Linux 中可用的一些工具来追查根本原因。

网络故障排除技能对 DevOps 团队的每个成员都价值连城。软件几乎必然以某种方式通过网络进行通信，在许多应用程序中，网络连接对软件的功能而言至关重要。当网络出现问题时，从系统管理员到 QA 团队，再到整个开发团队，可能所有人都会注意到。无论你的网络部门是否是独立的群体，当你的整个 DevOps 团队共同诊断网络问题时，你将获得对该问题更好的整体视图。你的开发团队会提供关于你的软件如何在网络上运行的深入知识；你的 QA 团队会解释应用程序在异常环境下的行为，并为你提供一份网络缺陷历史积压列表；你的系统管理员会提供关于网络应用程序在 Linux 下如何工作的整体视角。在一起，你们将能够比任何单独的团队更快地诊断出网络问题。

### 服务器 A 无法与服务器 B 通信

最典型的网络故障排查场景之一是，一台服务器无法与网络中的另一台服务器通信。本节将以一个示例来说明，其中名为 dev1 的服务器无法访问名为 web1 的第二台服务器上的 Web 服务（端口 80）。可能有无数种不同的问题会导致这种情况，因此我们将逐步执行一系列测试，以隔离问题原因。

通常，在排查此类问题时，你可能会跳过其中一些初始步骤（例如检查链路），因为后续更深入的测试也会排除这些可能性。例如，如果你测试并确认 DNS 工作正常，那就证明你的主机可以在本地网络通信。不过，对于这个示例，我们将遍历每个中间步骤，以说明你可能如何测试每个层级。

### 是客户端还是服务器的问题？

缩小问题原因范围的一个快速测试是，去同一网络上的另一台主机尝试访问该服务器。在这个示例中，你会在同一网络（如 dev1）上找到另一台服务器，例如 dev2，并尝试访问 web1。如果 dev2 也无法访问 web1，那么你知道问题更可能出在 web1 上，或者出在 dev1、dev2 和 web1 之间的网络上。如果 dev2 可以访问 web1，那么你知道问题更可能出在 dev1 上。首先，假设 dev2 可以访问 web1，因此我们将故障排查重点放在 dev1 上。

### 是否已插入网线？

执行的首要故障排查步骤是在客户端进行。你首先要验证客户端到网络的连接是否健康。为此，你可以使用 ethtool 程序（通过 ethtool 包安装）来验证你的链路是否处于激活状态（即以太网设备在物理上已连接到网络）。如果你不确定使用哪个接口，请运行 /sbin/ifconfig 命令以列出所有可用的网络接口及其设置。因此，如果你的以太网设备位于 eth0

```bash
$ sudo ethtool eth0
Settings for eth0:
  Supported ports: [ TP ]
  Supported link modes:  10baseT/Half 10baseT/Full
                          100baseT/Half 100baseT/Full
                          1000baseT/Half 1000baseT/Full
  Supports auto-negotiation: Yes
  Advertised link modes:     10baseT/Half 10baseT/Full
                              100baseT/Half 100baseT/Full
                              1000baseT/Half 1000baseT/Full

  Advertised auto-negotiation: Yes
  Speed: 1000Mb/s
  Duplex: Full
  Port: Twisted Pair
  PHYAD: 0
  Transceiver: internal
Auto-negotiation: on
Supports Wake-on: pg
Wake-on: d
Current message level: 0x00000f (255)
Link detected: yes
```

这里，在最后一行，你可以看到 link detected 被设置为 yes，这表明 dev1 在物理上已连接到网络。如果这里设置为 no，你需要物理检查 dev1 的网络连接，确保它已连接。既然它已物理连接，你可以继续下一步。

> 注意
>
> ethtool 的用途不仅限于检查链路。它还可以用于诊断和修复双工问题。当 Linux 服务器连接到网络时，通常它会与网络进行自动协商，以查看它可以使用哪些速度以及网络是否支持全双工。示例 ethtool 输出中的 Speed 和 Duplex 行说明了 100Mb/s 全双工网络应报告的内容。如果你注意到主机上的网络速度缓慢，其速度和双工设置是一个很好的检查点。如前一个示例中那样运行 ethtool，如果你注意到 Duplex 设置为 half，请运行：
>
> ```bash
> $ sudo ethtool -s eth0 autoneg off duplex full
> ```
>
> 将 eth0 替换为你的以太网设备。

### 接口是否已启用？

一旦你确认已物理连接到网络，下一步是确认你的主机上的网络接口配置是否正确。检查此问题的最佳方法是运行 ifconfig 命令，并将你的接口作为参数。因此，要测试 eth0 的设置，你会运行：

```bash
$ sudo ifconfig eth0
eth0 Link encap:Ethernet HWaddr 00:17:42:1f:18:be
inet addr:10.1.1.7 Bcast:10.1.1.255 Mask:255.255.255.0
inet6 addr: fe80::217:42ff:fe1f:18be/64 Scope:link
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:11 errors:0 dropped:0 overruns:0 frame:0
collisions:0 txqueuelen:1000
TX packets:11 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:229 (229.0 B) TX bytes:212 (21.1 kB)
Interrupts:10
```

这里可能最重要的一行是输出的第二行，它告诉我们主机配置了 IP 地址 (10.1.1.7) 和子网掩码 (255.255.255.0)。现在，这些设置对于此主机是否正确，需要你进行确认。如果接口未配置，请尝试运行 `sudo ifup eth0`，然后再次运行 `ifconfig` 查看接口是否启动。如果设置错误或接口无法启动，请在基于 Debian 的系统上检查 /etc/network/interfaces，或在基于 Red Hat 的系统上检查 /etc/sysconfig/network-scripts/ifcfg-<interface>。你可以通过这些文件纠正网络设置中的任何错误。如果主机通过 DHCP 获取 IP，你需要将故障排查转移到 DHCP 主机，以查明为什么你无法获取租约。

#### 是否在本地网络上？

看到接口已启用后，下一步是查看是否设置了默认网关以及你是否可以访问它。`route` 命令将显示当前的路由表，包括你的默认网关：

```bash
$ sudo route -n

Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
10.1.1.0        *               255.255.255.0   U     0      0      0 eth0
default         10.1.1.1        0.0.0.0         UG    100    0      0 eth0
```

你感兴趣的行是最后一行，以 default 开头。这里你可以看到主机的网关为 10.1.1.1。请注意，在 `route` 命令中使用了 `-n` 选项，因此它不会试图将这些 IP 地址解析为主机名。一方面，这样命令运行得更快，但更重要的是，你不想让任何潜在的 DNS 错误干扰你的故障排查。如果你在这里没有看到配置的默认网关，而你想到达的主机位于不同的子网（例如，web1，位于 10.1.2.5），那很可能是你问题的原因。要修复此问题，请确保在基于 Debian 的系统上在 /etc/network/interfaces 中设置网关，或在基于 Red Hat 的系统上在 /etc/sysconfig/network-scripts/ifcfg-<interface> 中设置；或者如果你通过 DHCP 获取 IP，请确保 DHCP 服务器上设置正确，然后在基于 Debian 的系统上使用以下命令重置接口：

```bash
$ sudo service networking restart
```

