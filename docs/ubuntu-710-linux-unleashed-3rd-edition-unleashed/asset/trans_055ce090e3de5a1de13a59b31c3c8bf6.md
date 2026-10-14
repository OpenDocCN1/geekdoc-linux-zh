

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

输出很容易理解。inet 条目显示了接口的 IP 地址。UP 表示接口可供使用，BROADCAST 表示接口连接到的网络支持广播消息（以太网），RUNNING 表示接口正在运行，而 LOOPBACK 显示哪个设备（lo）是回环地址。eth0 上的最大传输单元（MTU）为 1500 字节。这决定了可以通过此接口传输的最大数据包大小（有时会“调优”为其他值以提高性能）。Metric 是一个 0 到 3 之间的数字，与接口信息被写入路由表的多少有关。数字越小，信息量越少。

ifconfig 命令可用于显示有关特定接口的信息或控制该接口，使用如表 14.1 中所列的命令。例如，要停用主机上的第一个以太网设备，请使用 ifconfig 命令、接口名称以及 down 命令，如下所示：

```
$ sudo ifconfig eth0 down
```

你也可以通过指定主机名或 IP 地址以及网络信息来配置并激活设备。例如，要使用特定 IP 地址配置并激活（“启用”）eth0 接口，请这样使用 ifconfig 命令：

```
$ sudo ifconfig eth0 192.168.2.9 netmask 255.255.255.0 up
```

如果你的系统 /etc/hosts 文件中已定义了一个主机（请参阅本章后面“网络配置文件”部分），你可以根据定义的主机名来配置并激活接口，如下所示：

```
$ sudo ifconfig eth0 dogdog.hudson.com up
```

阅读下一节，了解如何配置系统以与你的局域网配合工作。

### /sbin/route

用于配置网络的第二个命令是 route 命令。route 用于构建路由表（在内存中），用于路由数据包以及显示路由信息。它在 ifconfig 初始化接口之后使用。route 通常用于通过网关或到其他主机设置到其他网络的静态路由。命令配置如下：

```
$ route [options] [commands] [parameters]
```

要显示路由表，请使用不带选项的 route 命令。显示内容将类似于这样：

```
$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.2.0     *               255.255.255.0   U     0      0       0 eth0
default         .               0.0.0.0         UG    0      0       0 eth0
```

在第一列中，Destination 是接收主机的 IP 地址（或，如果主机在 /etc/hosts 或 /etc/networks 中，则为主机名）。default 条目是此机器的默认网关。Gateway 列列出了数据包必须经过才能到达目的地的网关。星号（*）表示数据包直接发送到主机。Genmask 是网络掩码。Flags 列可能有多个条目。在我们的示例中，U 验证路由已启用，G 指定 Destination 需要使用网关。Metric 列显示到 Destination 的距离。某些守护进程使用它来确定到达 Destination 的最简单路由。Ref 列由某些 UNIX 变体用于传达对路由的引用。Linux 不使用它。Use 列指示此条目已被查找的次数。最后，Iface 列是对应条目的接口名称。

使用 route 命令的 -n 选项将提供相同的信息，用 IP 地址代替名称和星号（*），如下所示：

```
# /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.2.0     0.0.0.0         255.255.255.0   U     0      0       0 eth0
0.0.0.0         192.168.2.1     0.0.0.0         UG    0      0       0 eth0
```

route 命令可以使用 add 选项向表中添加内容。使用 add 选项时，可以将主机（-host）或网络（-net）指定为目标。如果未使用选项，route 命令假定你正在配置发出命令的主机。route 命令最常见的用途是为主机添加默认网关、对于丢失路由表的主机，或网关地址已更改的情况。例如，要添加具有特定 IP 地址的网关，可以使用以下命令：

```
$ sudo route add default gw 149.112.50.65
```
