
```text
IPADDR=192.168.1.13
NETMASK=255.255.255.0
NETWORK=192.168.1.0
BROADCAST=192.168.1.255
MTU=1500
ONBOOT=yes
```

以及

```text
DEVICE=lo
IPADDR=127.0.0.1
NETMASK=255.255.0.0
NETWORK=127.0.0.0
BROADCAST=127.255.255.255
ONBOOT=yes
NAME=loopback
```

是上述网络文件描述的 redhat.toadranch.com 机器的 `ifcfg-eth0` 和 `ifcfg-lo` 文件。

# Linux 网络

针对 `eth0` 的基于 DHCP 的设置更为简单：

```text
DEVICE=eth0
BOOTPROTO=dhcp
ONBOOT=yes
```

在 `/etc/sysconfig` 中更改配置信息后，对相应的接口运行 `ifdown <ifname>`，然后运行 `ifup <ifname>`。如果你同时重新配置了多个接口，可以使用 `sysctl restart network` 命令来重置网络。

`network-scripts/route-ifname` 中的行在配置相应接口时会作为参数传递给 `ip route`。例如，该行：

```text
default 192.168.0.1
```

设置了默认路由。这实际上不是针对特定接口的配置，但为了清晰起见，它应该放在你预期默认路由数据包传输的接口的对应的文件中。

## Linux 网络硬件选项

`ethtool` 命令查询并设置网络接口的特定介质参数，例如链路速率和双工。它取代了旧的 `mii-tool` 命令，但某些系统仍然包含两者。如果未安装 `ethtool`，它通常包含在自己的一个可选包中（也称为 `ethtool`）。

你可以通过命名接口来查询其状态。例如，这个 `eth0` 接口（PC 主板上的一个通用网卡）启用了自动协商，并且目前正以全速运行：

```bash
ethtool eth0
```

`eth0` 的设置：

```text
支持的端口：[ TP MII ]
支持的链路模式：10BaseT/Half 10BaseT/Full
100baseT/Half 100baseT/Full
100baseT/Half 100baseT/Full
支持自动协商：Yes
通告的链路模式：10BaseT/Half 10BaseT/Full
100baseT/Half 100baseT/Full
100baseT/Half 100baseT/Full
通告自动协商：Yes
速率：1000Mb/s
双工：Full
端口：MII
PHYAD: 0
收发器：internal
自动协商：on
支持唤醒：magic
唤醒：g
当前消息级别：0x00000033 (51)
链路检测：yes
```

# 第 13 章 TCP/IP 网络

要将此接口锁定在 100 Mb/s 全双工，请使用命令

```bash
# ethtool -s eth0 speed 100 duplex full
```

如果你正尝试确定自动协商在你的环境中是否可靠，你可能发现 `ethtool -r` 很有帮助。它强制链路参数重新协商。

另一个有用的选项是 `-k`，它显示与协议相关的任务是分配给网络接口而不是由内核执行的。大多数接口计算校验和，并可以协助分段。除非你认为网络接口没有可靠地执行这些任务，否则将它们卸载到硬件上总是更好的。当你使用 `ethtool -k` 并结合各种子集来强制或禁用特定类型的卸载时（`-k` 选项用于设置它们）。

通过 `ethtool` 进行的任何更改都是暂时的。如果你希望这些更改持续生效，请确保 `ethtool` 是系统网络配置的一部分运行的；如果你只是安排某些 `ethtool` 命令在启动时运行，那么你的配置将无法正确覆盖接口在不重启系统的情况下重启的情况。

![](img/d87305f54c4a442cf382141acae4b84f_469_0.png)

在 Red Hat 和 CentOS 系统上，你可以在 `/etc/sysconfig/network-scripts` 下的接口配置文件中包含一个 `ETHTOOL_OPTS=` 行。`ifup` 命令会将整行解析为 `ethtool` 参数。

在 Debian 和 Ubuntu 中，你可以从 `/etc/network/interfaces` 中的特定网络配置直接运行 `ethtool` 命令。

## Linux TCP/IP 选项

Linux 将每个可调内核变量的表示放入 `/proc` 虚拟文件系统中。请参第 339 页有关 `/proc` 机制的通用信息。

网络变量位于 `/proc/sys/net/ipv4` 和 `/proc/sys/net/ipv6`。我们以前在这里显示过完整列表，但由于太多无法列出。

`ipv4` 目录包含比 `ipv6` 目录多得多，这主要是因为与版本无关的协议（如 TCP 和 UDP）将其参数限制在 `ipv4` 目录中。如 `tcp_` 或 `udp_` 前缀告诉你该参数与哪个协议相关。

`ipv4` 和 `ipv6` 内的子目录包含按接口设置的参数。它们包括 `all`、`default` 以及每个接口的子目录（包括回环接口）。每个子目录都有相同的文件。

## Linux 网络

```bash
ubuntu$ ls -F /proc/sys/ipv4/conf/
accept_local          drop_gratuitous_arp      proxy_arp
accept_redirects      drop_unicast_in_multicast  proxy_arp_pvlan
accept_source_route  force_igmp_version      route_local
arp_accept           forwarding             rp_filter
arp_announce        igmpv2_unsolicited_report_interval secure_redirects
arp_filter           igmpv3_unsolicited_report_interval  send_redirects
arp_ignore        ignore_routes_with_linkdown  shared_media
arp_notify        log_martians             src_valid_mark
boot_reply         mc_forwarding          tag
disable_policy      medium_id
disable_xfrm       promote_secondaries
```

如果你更改了 `conf/eth0` 中的变量，你的更改仅适用于该接口。如果你更改了 `conf/all` 目录中的值，可能会预期设置所有接口的值，但并不是。某些值与当前值进行 OR 操作，某些进行 AND 操作，另一些则进行 MAX 或 MIN 操作。据我们所知，内核代码中没有关于此过程的文档，因此最好避免限制你的修改。

如果你更改了 `conf/default` 目录中的变量，新值将传播到所有接口。另一方面，保留默认值作为参考是好的，以便你想撤销其他更改。

`/proc/sys/net/ipv4` 和 `/proc/sys/net/ipv6` 目录也包含每个接口的子目录。以 `gc`（垃圾收集）开头的文件决定 ARP 条目的进入和丢弃。这是 `/proc/sys` 中的变量列表：

```bash
ubuntu$ ls -F /proc/sys/ipv4/conf/
accept_local          drop_gratuitous_arp      proxy_arp
accept_redirects      drop_unicast_in_multicast  proxy_arp_pvlan
accept_source_route  force_igmp_version      route_local
arp_accept           forwarding             rp_filter
arp_announce        igmpv2_unsolicited_report_interval secure_redirects
arp_filter           igmpv3_unsolicited_report_interval  send_redirects
arp_ignore        ignore_routes_with_linkdown  shared_media
arp_notify        log_martians             src_valid_mark
boot_reply         mc_forwarding          tag
disable_policy      medium_id
```
