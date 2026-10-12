
（其网络地址为 192.168.0.0）访问 Telnet 服务（由 `in.telnetd` 程序提供），请在 `/etc/hosts.allow` 文件中添加以下行：

```
in.telnetd:192.168.0.
```

如果你想让所有本地主机都能访问所有互联网服务，可以使用 `ALL` 关键字，并将该行重写如下：

```
ALL:192.168.0.
```

最后，要将所有互联网服务对所有主机开放，可以用 `ALL` 替换 IP 地址，如下所示：

```
ALL:ALL
```

你也可以使用主机名代替 IP 地址。

![](img/9f89727199836b0f871f1745838aa8b2_348_0.png)

要了解 `/etc/hosts.allow` 文件中条目的详细语法，请在终端窗口中的 shell 提示符下输入 `man hosts.allow`。

# /etc/hosts.deny

这个文件与 `/etc/hosts.allow` 正好相反——`hosts.allow` 指定哪些主机可以访问你系统上的互联网服务（如 TELNET 和 TFTP），而 `hosts.deny` 文件则标识必须被拒绝服务的主机。如果 `/etc/hosts.allow` 文件中没有适用于请求主机的规则，则会查询 `/etc/hosts.deny` 文件。如果 `hosts.deny` 文件中存在适用于该主机的规则，则服务将被拒绝。

`/etc/hosts.deny` 文件中的条目与 `/etc/hosts.allow` 文件中的条目格式相同——它们采用 `server:IP address` 格式，其中 `server` 指代提供特定互联网服务的程序名称，而 `IP address` 标识不允许使用该项服务的主机。

如果你已经在 `/etc/hosts.allow` 文件中设置了允许特定主机访问的条目，你可以在 `/etc/hosts.deny` 中放置以下行，以拒绝其他所有主机访问你系统上的任何服务：

```
ALL:ALL
```

![](img/9f89727199836b0f871f1745838aa8b2_348_1.png)

要了解 `/etc/hosts.deny` 文件中条目的详细语法，请在终端窗口中的 shell 提示符下输入 `man hosts.deny`。

# 检查 TCP/IP 网络

在配置好以太网和 TCP/IP 之后（无论是在安装 Fedora Core 期间，还是稍后运行网络配置工具时），你都可以毫无问题地使用各种网络应用程序。如果你遇到困难，Fedora Core 包含了几个帮助监控和诊断问题的工具。

### 检查网络接口

使用 `/sbin/ifconfig` 命令查看当前配置的网络接口。`ifconfig` 命令用于配置网络接口（即将 IP 地址与网络设备关联）。如果运行 `ifconfig` 时没有命令行参数，该命令将显示当前网络接口的信息。以下是一次典型的 `ifconfig` 调用及其输出结果：

```
/sbin/ifconfig
eth0      Link encap:Ethernet  HWaddr 00:08:74:E5:C1:60
          inet addr:192.168.0.6  Bcast:192.168.0.255  Mask:255.255.255.0
          inet6 addr: fe80::208:74ff:fe05:c160/64  Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:93700 errors:0 dropped:0 overruns:0 frame:0
          TX packets:74097 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:33574333 (32.0 Mb)  TX bytes:8832457 (8.4 Mb)
```

Interrupt:10 Base address:0x3000

eth1

```
Link encap:Ethernet HWaddr 00:02:20:8C:F8:C5
inet addr:192.168.0.8 Bcast:192.168.0.255 Mask:255.255.255.0
inet6 addr: fe80::202:2dff:fe8c:f8c5/64 Scope:Link
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:3403 errors:0 dropped:0 overruns:0 frame:0
TX packets:22 errors:1 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:1000
RX bytes:254990 (249.0 Kb) TX bytes:3120 (3.0 Kb)
Interrupt:3 Base address:0x100
```

lo

```
Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
inet6 addr: ::1/128 Scope:Host
UP LOOPBACK RUNNING MTU:16436 Metric:1
RX packets:3255 errors:0 dropped:0 overruns:0 frame:0
TX packets:3255 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
RX bytes:2686647 (2.5 Mb) TX bytes:2686647 (2.5 Mb)
```

该输出显示该系统当前有三个网络接口处于活动状态——环回接口（lo）和两个以太网卡（eth0 和 eth1）。对于每个接口，你可以看到 IP 地址，以及已交付和已发送分组的数据统计。如果 Fedora Core 系统有一个拨号 PPP 连接处于活动状态，你还会在输出中看到 ppp0 接口的条目。

### /etc/nsswitch.conf

这个文件被称为*名称服务开关*（NSS）文件，它指定了诸如名称解析库（NIS、NIS+）和当地配置文件（如 `/etc/hosts` 和 `/etc/shadow`）等服务如何交互。

NIS 和 NIS+ 是*网络信息服务*——另一种名称查找服务。新版 Linux 内核使用 `/etc/nsswitch.conf` 文件来确定优先级：当地配置文件、如 DNS（域名服务）之类的服务，还是 NIS。

例如，`/etc/nsswitch.conf` 文件中的以下 `hosts` 条目表示名称解析库先尝试 `/etc/hosts` 文件，然后尝试 NIS+，最后尝试 DNS：

```
hosts:		files nisplus dns
```

你可以通过在终端窗口中键入 `info libc “Name Service Switch”`（包括引号）来了解有关 `/etc/nsswitch.conf` 文件的更多信息。

### 检查 IP 路由表

另一个网络配置命令 `/sbin/route` 在不带任何命令行参数运行时也提供状态信息。如果你在检查与另一台主机的连接（通过指定 IP 地址）时遇到问题，请检查 IP 路由表以查看是否指定了默认网关。然后检查该网关的路由表，以确保通往外部网络的路径出现在该路由表中。

`/sbin/route` 命令的典型输出如下所示：

```
/sbin/route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.0.0     *               255.255.255.0   U     0      0      0 eth0
192.168.0.0     *               255.255.255.0   U     0      0      0 eth1
169.254.0.0     *               255.255.0.0     U     0      0      0 eth1
127.0.0.0       *               255.0.0.0       U     0      0      0 lo
0.0.0.0         192.168.0.1     0.0.0.0         UG    0      0      0 eth0
default
```

如该路由表所示，本地网络使用 eth0 和 eth1 以太网接口，默认网关是 eth0 以太网接口。默认网关是一种路由设备，它处理发往除 Fedora Core 系统所在网络以外的任何网络的分组。在本例中，发往除以 192.168.0 开头的地址以外的任何网络地址的分组都会被发送到网关——192.168.0.1。网关将这些分组转发到其他网络（当然，假设该网关连接到另一个网络，最好是互联网）。

### 检查与主机的连接

要检查到特定主机的网络连接，请使用 **ping** 命令。*ping* 是一个广泛使用的 TCP/IP 工具，它使用一系列互联网控制消息协议（ICMP，发音为 *icmp*）消息。ICMP 提供一种回显消息，每个主机都会对此做出响应。通过使用 ICMP 消息和回复，*ping* 可以确定另一个系统是否存活，并计算与该系统通信的往返延迟。

以下示例展示了如何运行 *ping* 以查看我网络上的某个系统是否存活：

```
ping 192.168.0.1
```

以下是该命令在我的家庭网络上显示的内容：

```
PING 192.168.0.1 (192.168.0.1) from 192.168.0.7 : 56(84) bytes of data.
64 bytes from 192.168.0.1: icmp_seq=1 ttl=254 time=1.36 ms
64 bytes from 192.168.0.1: icmp_seq=2 ttl=254 time=1.33 ms
64 bytes from 192.168.0.1: icmp_seq=3 ttl=254 time=1.36 ms
64 bytes from 192.168.0.1: icmp_seq=4 ttl=254 time=1.34 ms
--- 192.168.0.1 ping statistics ---
4 packets transmitted, 4 received, 0% loss, time 3026ms
rtt min/avg/max/mdev = 1.338/1.352/1.366/0.038 ms
```

在 Fedora Core 中，*ping* 会持续运行，直到你按下 Ctrl+C 停止它；然后它会显示统计摘要，显示在两个系统之间发送分组的典型耗时。在某些系统上，*ping* 仅报告远程主机是否存活。但是，你仍可以通过使用适当的命令行参数来获取计时信息。

### 检查网络状态

要检查网络状态，请使用 **netstat** 命令。该命令显示各种类型的网络连接状态（如 TCP 和 UDP 连接）。你可以使用 *netstat -i* 快速查看接口的状态，如下所示：

```
netstat -i
Kernel Interface table
Iface  MTU Met   RX-OK  RX-ERR  RX-DRP  RX-OVR    TX-OK  TX-ERR  TX-DRP  TX-OVR Flg
eth0  1500  0  94237    0        0       1     74889   0      0       0 BMRU
eth1  1500  0   3942    0        0      24      1      0     0 BMRU
lo    16436  0    3255   0        0      3255   1      0     0 LRU
```

在这种情况下，输出显示了环回和以太网接口的当前状态。表 4-2 描述了各列的含义。

![](img/9f89727199836b0f871f1745838aa8b2_351_0.png)

