
如果需要，可以使用一个或多个选项条目将其他参数传递给内核模块，以正确配置网卡。有关使用条目的更多信息，请参阅 `modprobe.conf` 手页。关于网卡内核模块的更多具体信息，请检查模块源码，因为没有相关的手页（这对任何愿意编写文档的人来说都是一个极好的机会）。

Linux 内核和网络工具可用于诊断问题或排除网卡的故障。然而，如果你访问 Don Becker 的 Linux 以太网状态、诊断和设置工具页面（http://www.scyld.com/ethcard/diag.html），你会发现十多个针对各种 PCI 和遗留 ISA 以太网卡的硬件特定工具。如果你在网卡识别或配置过程中遇到困难，这些工具将非常有帮助。

# 使用 modprobe 手动加载内核模块

你不必使用 `/etc/modprobe.conf`...（注：文本在 OCR 处被截断/变得混乱，但根据提供的流程）：

你不必使用 `/etc/modprobe.conf`... 来手动加载模块。

# 命令行网络接口配置

你可以使用基础 Linux 网络工具从命令行配置网络接口。你可以通过使用命令行更改当前设置或通过编辑若干系统文件来通过命令行配置网络客户端主机。`ifconfig` 和 `route` 两个命令用于网络配置。`netstat` 命令用于显示网络连接信息。

```
/sbin/ifconfig
```

`ifconfig` 用于配置你的网络接口。你可以使用它来：

+ 激活或禁用你的网卡（NIC）或更改网网卡的模式
+ 更改你机器的 IP 地址、子网掩码或广播地址
+ 创建 IP 别名以允许你的网卡上使用多个 IP 地址
+ 为点对连接创建目的地址

你可以通过一个命令更改你想要更改的任意数量的选项。

该命令的基本结构如下：

```
/sbin/ifconfig [network device] options
```

表 18.1 显示了 `ifconfig` 选项的一个子及其用法示例。

| 用途 | 选项 | 示例 |
| --- | --- | --- |
| 创建别名 | -[network device] | ifconfig eth0:_[number] 10.10.10.10 |
| 更改 IP 地址 | | ifconfig eth0 10.10.10.12 |
| 更改子网掩码 | netmask [netmask] | ifconfig eth0 netmask 255.255.255.0 |
| 更改广播 | broadcast [address] | ifconfig eth0 broadcast 10.10.10.255 |
| 禁用接口 | down | ifconfig eth0 down |
| 启用接口 | up (添加 IP 地址) | ifconfig eth0 up (ifconfig eth0 10.10.10.10) |
| 设置网卡混杂模式 [开启/关闭] | -promisc | ifconfig eth0 prom [ifconfig eth0 -promisc] |
| 设置多播模式 [开启/关闭] | -allmulti | ifconfig eth0 allmulti [ifconfig eth0 -allmulti] |
| 启用 [禁用] | -pointoint | ifconfig eth0_pointoint |
| 点对点地址 | [address] | 10.10.10.20 [ifconfig eth0 pointoint_10.10.10.20] |

`ifconfig` 的 man 页显示了其他选项，使你的机器与多种网络类型交互，如 AppleTalk、Novell、IPv6 等。再次，请阅读 man 页以获取这些网络类型的详情。

# 使用网络配置工具

> 注意
>
> 混杂模式（Promiscous mode）会导致网卡接收网络上的所有数据包。它通常用于嗅探网络。多播模式允许网卡接收网络上的所有的多播流量。

如果不提供参数，`ifconfig` 会显示活动接口的状态。例如，在不带参数且有一个活动并配置的网卡的情况下，`ifconfig` 的输出类似于：

```
# /sbin/ifconfig
```

```
eth0 Link encap:Ethernet HWaddr 00:30:18:08:07:00
    inet addr:192.168.2.7 Bcast:192.168.2.255 Mask:255.255.255.0
    UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
    RX packets:12794 errors:dropped:0 overruns:0 frame:0
    TX packets:172675 errors:dropped:0 overruns:0 carrier:0
    collisions:7874 txqueuel:100
    RX bytes:1909839 (18.2 Mb) TX bytes:73768657 (70.3 Mb)
    Interrupt:11 Base address:0x20000
```

```
lo Link encap:Local Loopback
    inet addr:127.0.0.1 Mask:255.0.0.0
    UP LOOPBACK RUNNING MTU:16346 Metric:1
    RX packets:215214 errors:dropped:0 overruns:0 frame:0
    TX packets:215214 errors:dropped:0 overruns:0 carrier:0
    collisions:0 txqueuel:0
    RX bytes:68739000 (65.5 Mb) TX bytes:68739000 (65.5 Mb)
```

输出非常易懂。该条目显示了接口的 IP 地址。UP 表示接口已就绪可用，BROAD 表示接口已连接到支持广播的网络（以太网），RUNNING 意味着接口正在运行，而 LOOPBACK 显示设备（lo）是回环地址。`eth0` 上的最大传输单元（MTU）为 1500 字节。这决定了可以通过此接口传输的最大数据包的大小（有时为了提高性能会将其“调优”到其他值）。Metric 是一个从 0 到 3 的数字，与从接口放入路由表中的信息量有关。数字越小，信息量越少。

`ifconfig` 命令可以像表 18.1 列出的命令来显示特定接口的信息或控制它。例如，要禁用主机上的第一个以太网设备，使用 `ifconfig` 命令、接口名称和命令：

```
# ifconfig eth0 down
```

你也可以通过指定主机名或 IP 地址来配置并激活设备。例如，使用 `ifconfig` 命令使用特定 IP 地址配置激活接口：

```
# ifconfig eth0 up
```

如果你在系统的 `/etc/hosts` 文件中定义了（参见本章稍后的“网络配置”部分），你可以按照定义的主机名这样配置接口：

```
# ifconfig eth0 dog.com
```

配置网络的第二个命令是 `route` 命令。`route` 用于构建路由表（在内存中）以及显示路由信息。在 `ifconfig` 初始化接口后，`route` 通常用于通过网关设置路由。显示路由表，使用不带选项的 `route` 命令。输出类似于：

```
# /sbin/route
Kernel routing table
```

| 目的 | 网关 | 子网掩码 | 标志 | 量 | 接口 |
| --- | --- | --- | --- | --- | --- |
| --- | --- | --- | --- | --- | --- |
| 149.112.50.64 | * | 255.255.255.192 | U | 0 | eth0 |
| 208.59.243.0 | * | 255.255.255.0 | U | 0 | eth0 |
| 127.0.0.0 | * | 255.0.0.0 | U | 0 | lc |
| default | 149.112.50.6 | 0.0.0.0 | UG | 0 | eth0 |

在第一列中，Destination 是接收主机的 IP 地址（如果主机在 `/etc/hosts` 中则是主机名）。`default` 是此机器的默认网关。Gateway 列出了数据包到达目的必须经过的网关。星号 (*) 表示直接到达主机。Genmask 是子网掩码。Flags 列可以有多个条目。例如 U 路由已启用，G 指定需要使用网关。Metric 列显示到目的的距离。某些守护进程使用它找到目的的最优路由。Ref 列某些 UNIX 版本用于引用路由，Linux 不使用它。Use 列指示该条目被查找的次数。最后，Iface 列是对应条目的接口名称。

对 `route` 使用 `-n` 选项将提供 IP 地址替换名称和星号 (*) 的相同信息，如下所示：
