
Supported `FEC` modes: Not reported

Advertised link modes: `10baseT/Half` `10baseT/Full` `100baseT/Half` `100baseT/Full` `1000baseT/Full`

Advertised pause frame use: No

Advertised auto-negotiation: Yes

Advertised `FEC` modes: Not reported

Speed: `1000Mb/s`

Duplex: Full

Port: Twisted Pair

`PHYAD`: 0

Transceiver: internal

Auto-negotiation: on

`MDI-X`: off (auto)

```

```

# 表 15.1 `ip` 工具的命令选项

| 参数 | 描述 |
|--- | --- |
| `address` | 显示或设置设备上的 `IPv4` 或 `IPv6` 地址。 |
| `addrlabel` | 定义配置标签。 |
| `l2tp` | 基于 `IP` 的以太网隧道 (Tunnel Ethernet over `IP`)。 |
| `link` | 定义网络设备。 |
| `maddress` | 定义系统监听的组播地址。 |
| `monitor` | 监听 `netlink` 消息。 |
| `mroute` | 在组播路由缓存中定义项。 |
| `mrule` | 在组播路由策略数据库中定义规则。 |
| `neighbor` | 管理地址解析协议 (`ARP`) 或邻居发现 (`NDISC`) 缓存。 |
| `netns` | 管理网络命名空间。 |
| `ntable` | 管理邻居缓存操作。 |
| `route` | 管理路由表。 |
| `rule` | 管理路由策略数据库中的条目。 |
| `tcpmetrics` | 管理接口上的 `TCP` 指标。 |
| `token` | 管理标记的接口标识符。 |
| `tunnel` | 基于 `IP` 的隧道 (Tunnel over `IP`)。 |
| `tuntap` | 管理网络隧道 (`TUN`) 或网络桥接 (`TAP`) 设备。 |
| `xfrm` | 管理安全连接的 `IPSec` 策略。 |

每个命令选项都使用参数来定义执行的操作，例如显示网络设置或修改现有网络设置。列表 15.3 展示了如何使用 `show` 参数显示当前网络设置。

## 列表 15.3：`ip address show` 输出

```
$ ip address

1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group

default qlen 1000

link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00

inet 127.0.0.1/8 scope host

    valid_lft forever preferred_lft forever

inet6::128 scope host

    valid_lft forever preferred_lft forever

2: enp03:<BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc pfifo_fast

state group default qlen 1000

link/eth8:00:08:27:73:1c:6d brd ff:ff:ff:ff:ff:ff

inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic

    valid_lft 8411sec preferred_lft 8411sec

inet6 fe80::5432:eddb:5ea1:fb44/64 scope link noprefixroute

    valid_lft forever preferred_lft forever

```

列表 15.3 显示了 Linux 系统上的两个网络接口：

- `lo`—本地回环接口
- `enp03`—一个有线网络接口

本地回环接口是一个虚拟网络接口。任何本地程序都可以使用它与其他程序进行通信，就像它们跨越了网络一样。这可以简化数据传输程序的编写。
`enp03` 是 Linux 系统的有线网络连接。
`ip` 命令显示分配给接口的 IP 地址（同时分配了 IP 和 IPv6 本地地址）、子网掩码值以及关于接口数据包的一些基本统计信息。

如果输出没有显示分配给接口的网络地址，可以使用 `ip` 命令为接口指定主机地址和子网掩码值：

```bash
# ip address add 10.0.2.15/24 dev enp03
```

然后，你可以使用 `ip` 命令为网络接口设置默认路由器：

```bash
# route add default via 192.168.1.254 dev enp03
```

最后，使用 `link` 选项使网络接口激活：

```bash
# ip link set enp03 up
```

![](img/85a8584ad3f3bd69446d00a129bba855_366_0.png)

# 第 15 章 • 管理网络连接

## 认证目标

虽然 `ip` 命令是更改网络设置的一站式方法，但为你的网络指定设置的另一种方法是使用 `route` 命令：

```bash
# route add default gw 192.168.1.254 dev enp03
```

你也可以单独使用 `route` 命令来查看系统配置的当前默认路由器：

```bash
$ route
```

| Destination | Gateway | Genmask | Flags | Metric | Ref | Iface |
| --- | --- | --- | --- | --- | --- | --- |
| 192.168.1.0 | 192.168.1.254 | 0.0.0.0 | U | 0 | 0 | enp03 |
| | | 255.255.255 | U | 1 | | |

Linux 系统的默认路由器是 192.168.1.0，且通过 `enp03` 网络接口可用。输出还显示了连接的本地网络。如果你的网络通过多个路由器连接到多个网络，你可以使用 `route` 命令的 `add` 或 `del` 命令行选项在系统中手动创建路由表。格式如下：

```bash
route [add|del] gw gateway
```

其中 `target` 是目标主机，`gateway` 是路由器地址。

如果你的网络使用 DHCP，请确保 Linux 系统上运行着另一个 DHCP 客户端。该程序在后台与 DHCP 服务器通信并分配网络交互所需的 IP 地址。Linux 可用的 DHCP 客户端有：
- `dhcpcd`
- `dhclient`
- `pump`

`dhcpcd` 程序是最流行的，但在某些 Linux 发行版中也会看到另外两个。

在使用 `ip` 命令为无线接口分配地址之前，必须使用 `iwconfig` 命令分配 SSID 和密钥值：

```bash
# iwconfig wlan0 ssid "MyNetwork" key password
```

`ssid` 参数接入点名称，`key` 参数允许你指定连接所需的 ASCII 字符加密密钥。如果你不知道本地无线连接的名称，可以使用 `iwlist` 命令显示所有无线信号。只需指定无线设备并使用 `scan` 选项：

```bash
$ iwlist scan
```

## 真实场景

### 获取 Wi-Fi 驱动

遗憾的是，Linux 对 Wi-Fi 硬件的支持有限。如果你在尝试配置时没有看到 Wi-Fi 硬件，可能需要跟踪驱动。你可以使用第 6 章中描述的 `lspci` 工具开始这项任务，带有某些选项来查看可用硬件列表——例如，笔记本电脑的 `lspci` 输出包含了：

```
03:00.0 Network controller: Realtek Co., Ltd. RTL8191SE Wireless LAN (rev 10)
```
