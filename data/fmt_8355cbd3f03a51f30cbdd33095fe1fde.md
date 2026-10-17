
提供了特定主机的 ARP 信息。ARP 在 Linux 上支持的另一个命令参数是 `-n`。此选项在列表中显示主机名或 IP 地址。选择使用 IP 地址显示 ARP 条目的一个原因是它的速度会快一点。IP 地址与主机名之间的映射通常通过域名服务器（DNS）完成，结果可能需要一些时间才能完成。在实践中，在大多数情况下这种延迟是可以忽略不计的。然而，如果名称解析机制（例如 NIS 或 DNS）出现延迟或其他运行问题，使用 `-n` 选项列出 ARP 缓存会更快。如果名称解析完全失效，且 ARP 缓存相当大，`arp -n` 将更快速地返回输出。使用本节第一个示例的格式的 ARP 列表将显示以下内容：

| `arp -n` | Hwtype | Hwaddress | Flags Mask | Iface |
|---|---|---|---|---|
| -> 10.0.2.10 | ether | 00:60:97:0E:A3:06 | C | `eth0` |
| -> 10.0.2.60 | ether | 00:00:1D:0A:5D:01 | C | `eth0` |

这些数字 IP 地址与第一个示例中的命名地址对应。

# 模块 11：基础网络工具 321

| 10.0.2.50 | ether | 00:C0:D4:00:09:40 | C | `eth0` |
| 10.0.2.127 | ether | 08:00:20:82:be:05 | C | `eth0` |
| 10.0.2.220 | ether | (incomplete) | | `eth0` |
| 10.0.2.126 | ether | 08:00:20:04:cf:2c | C | `eth0` |
| Entries: 6 Skipped: 0 | Found: 6 | | | |

如你所见，每个主机的 IP 地址已经显示，而不是实际的主机名。

如之前所示，`arp` 命令显示获取该条目的接口名称。根据上面的输出，所有映射都来自 `eth0` 接口。正如之前建议的那样，系统可能包含多个接口。这被称为多宿主（multi-homing）。在这些系统上显示 ARP 缓存时，输出包含每个接口的条目，如下所示：

| Address | Hwtype | Hwaddress | Flags Mask | Iface |
|---|---|---|---|---|
| durer.home.com | ether | 00:60:97:0A:33:06 | C | `eth0` |
| moster.home.com | ether | 00:60:97:0A:83:09 | C | `eth1` |
| probe2.home.com | ether | 00:80:96:0B:C1:01 | C | `eth1` |
| switch.home.com | ether | 00:00:1D:0A:5D:01 | C | `eth0` |
| probe.home.com | ether | 00:C0:D4:00:09:40 | C | `eth0` |

> 这两个条目与另外三个位于不同的接口。我们可以看到该系统有两个接口的映射。在这种情况下，输出中列出了 `eth0` 和 `eth1`。由于 ARP 通过接口跟踪条目，我们可以使用 `-i` 选项仅显示来自特定接口的映射。命令

```
# arp -i eth1
```

将显示来自 `eth1` 的映射：

| Address | Hwtype | Hwaddress | Flags Mask | Iface |
|---|---|---|---|---|
| moster.home.com | ether | 00:60:97:0A:83:09 | C | `eth1` |
| probe2.home.com | ether | 00:80:96:0B:C1:01 | C | `eth1` |

`ifconfig` 程序提供了大量的选项和关键字，用于配置一个或多个网络接口。表 11-3 列出了这些选项和关键字中最重要的部分。关键字用与其他命令行选项作为修饰符。

### 列出可用接口

要显示所有系统接口，请使用 `ifconfig -a` 命令：

```
#ifconfig -a
```

| 选项 | 含义 |
| --- | --- |
| `-a` | 应用于系统中当前安装的所有接口。 |
| `arp -arp` | 在此接口上启用地址解析协议 (ARP)；通过 `-arp` 选项禁用 ARP 的使用。 |
| `auto-dhcp` | 使用 DHCP 为此接口获取 IP 地址（仅限 Solaris 和 HP-UX）。 |
| `promis -promis` | (仅限 Linux) 在此接口上启用混杂模式（即监听流量）。`-promiscu` 选项禁用该模式。 |
| `allmulti -allmulti` | (仅限 Linux) 允许接口接收所有多播流量。`-allmulti` 选项将禁用多播包的接收。 |
| `broadcast -broadcast` | 使用给定的参数，设置或清除此接口的广播地址。这是一个网络层广播地址。 |
| `pointpoint -pointpoint` | (仅限 Linux) 为此接口启用点对点模式。基本假设是两个设备之间的专用链路。如果提供了地址，它将设置链路另一侧的协议地址。使用 `pointpoint` 关键字禁用点对点模式。 |
| `up` | 使接口启动或激活。 |
| `down` | 使接口关闭或取消激活。 |
| `netmask` | 设置此接口的 IP 网络子掩码。指定的参数可以以 `255.0.0.0`（点十进制）或 `0xff0000`（十六进制）的形式存在。 |
| `address` | 设置此接口的 IP 地址。这必须是一个未分配给其他系统的唯一 IP 地址。 |

表 11-3 `ifconfig` 命令行选项

UNIX 系统管理：入门指南

当在 Linux 上运行此命令时，将显示以下示例：

```
eth0 Link encap:Ethernet Hwaddr 00:10:5A:28:5D:7C

inet addr:10.0.2.201 Bcast:10.0.2.255 Mask:255.255.255.250

UP BROADCAST RUNNING PROMISC MULTICAST MTU:1500 Metric:1

RX packets:822 errors:1 dropped:0 overruns:0 frame:1

TX packets:108 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuel:10

Interrupt:10 Base address:0xfc00

lo Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.255.0.0

UP RUNNING MTU:3924 Metric:1

RX packets:92 errors:0 dropped:0 overruns:0 frame:0

TX packets:92 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuel:10

ppp0 Link encap:Point-to-Point Protocol

POINTPOINT NOARP MULTICAST MTU:1500 Metric:1

RX packets:0 errors:0 dropped:0 overruns:0 frame:0

TX packets:0 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuel:10
```

![](img/2928fe42a92e6fb43bbbe3768008092f_346_0.png)

在 Solaris 上：

```
lo0: flags=100849=UP,LOOPBACK,RUNNING,MULTICAST,IPv4> mtu 8232 index 1

inet 127.0.0.1 netmask ff00000

elx1: flags=100843=UP,BROADCAST,RUNNING,MULTICAST,IPv4> mtu 1500 index 2

inet 216.155.202.100 netmask fffff00 broadcast 216.155.202.255

eth0: 0a:4b:1f:8d:ef

lo0: flags=100849=UP,LOOPBACK,RUNNING,MULTICAST,IPv6> mtu 8232 index 1

inet ::128
```
