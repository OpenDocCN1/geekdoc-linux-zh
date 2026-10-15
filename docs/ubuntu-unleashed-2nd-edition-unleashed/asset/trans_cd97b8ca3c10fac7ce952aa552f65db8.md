

你可以用一条命令更改任意多或任意少的这些选项。命令的基本结构如下：

```
ifconfig [network device] options
```

表 18.1 显示了 ifconfig 选项的子集及其使用示例。

### Table 18.1 ifconfig Options

| 用途 | 选项 | 示例 |
|---|---|---|
| 创建别名 | `[network device]` | `ifconfig eth0:0 10.10.10.10` |
| 更改 IP 地址 | `[IP address]` | `ifconfig eth0 10.10.10.12` |
| 更改子网掩码 | `netmask [netmask]` | `ifconfig eth0 netmask 255.255.255.0` |
| 更改广播地址 | `broadcast [address]` | `ifconfig eth0 broadcast 10.10.10.255` |
| 关闭接口 | `down` | `ifconfig eth0 down` |
| 启动接口 | `up` (添加 IP 地址) | `ifconfig eth0 up` (`ifconfig eth0 10.10.10.10`) |
| 设置网卡混杂模式 | `[-]promisc` | `ifconfig eth0 promisc` (模式开启) / `ifconfig eth0 -promisc` (关闭) |
| 设置多播模式 | `[-]allmulti` | `ifconfig eth0 allmulti` (开启) / `ifconfig eth0 -allmulti` (关闭) |
| 启用/禁用点对点 | `[-]pointopoint` | `ifconfig eth0 pointopoint 10.10.10.20` (启用) / `ifconfig eth0 -pointopoint` (禁用) |

ifconfig 手册页显示了其他可使你的机器与多种网络类型（如 AppleTalk、Novell、IPv6 等）接口的选项。同样，请阅读手册页以了解这些网络类型的详细信息。

### NOTE

混杂模式会使网卡接收网络上的所有数据包。它常用于嗅探网络。多播模式使网卡能够接收网络上的所有多播流量。

如果没有给出参数，ifconfig 会显示活动接口的状态。例如，ifconfig 不带参数且有一个活动且已配置的网卡的输出看起来类似如下：

```
$ ifconfig
eth0  Link encap:Ethernet  HWaddr 00:0F:EA:B2:53:85
inet addr:192.168.2.5  Bcast:192.168.2.255  Mask:255.255.255.0
inet6 addr: fe80::20f:eaff:feb2:5385/64 Scope:Link
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
RX packets:471 errors:0 dropped:0 overruns:0 frame:0
TX packets:695 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:160637 (156.8 KiB)  TX bytes:86193 (84.1 KiB)
Interrupt:185 Base address:0x6000

lo
Link encap:Local Loopback
inet addr:127.0.0.1  Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING  MTU:16436  Metric:1
RX packets:19 errors:0 dropped:0 overruns:0 frame:0
TX packets:19 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:1336 (1.3 KiB)  TX bytes:1336 (1.3 KiB)
```

输出很容易理解。inet 条目显示接口的 IP 地址。UP 表示接口已准备就绪，BROADCAST 表示接口已连接到支持广播消息的网络（以太网），RUNNING 表示接口正在运行，LOOPBACK 显示哪个设备（lo）是回环地址。eth0 上的最大传输单元（MTU）为 1500 字节。这决定了可通过此接口传输的最大数据包大小，有时会被“调优”为其他值以提高性能。Metric 是 0 到 3 之间的数字，表示接口信息被放入路由表中的多少。数字越小，信息量越少。

ifconfig 命令可用于根据表 18.1 中列出的命令显示有关特定接口的信息或控制该接口。例如，要停用主机上的第一个以太网设备，请使用 ifconfig 命令、接口名称和命令 down，如下所示：

```
$ sudo ifconfig eth0 down
```

你也可以通过指定主机名或 IP 地址以及网络信息来配置并激活设备。例如，要使用特定 IP 地址配置并激活（“启动”）eth0 接口，请使用以下方式使用 ifconfig 命令：

```
$ sudo ifconfig eth0 192.168.2.9 netmask 255.255.255.0 up
```

如果你的系统中 /etc/hosts 文件中定义了主机（请参阅本章后面的“Network Configuration Files”部分），你可以根据定义的主机名来配置并激活接口，如下所示：

```
$ sudo ifconfig eth0 dogdog.hudson.com up
```

阅读下一节，了解如何配置你的系统以与你的局域网配合工作。

