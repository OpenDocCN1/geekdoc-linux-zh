
此条目告诉 Linux 内核加载 `8139too.o` 内核模块以支持 `eth0` 网络设备。

另一方面，如果你安装了 Intel Ethernet Pro 网卡，你将使用如下条目：

```
alias eth0 eepro100
```

如果需要，你可以使用一个或多个可选条目向内核模块传递其他参数，以正确配置你的网卡。查看 `modprobe.conf` 页面以获取有关条目的更多信息。关于网卡内核模块的更多细节，请检查模块的源代码。（目前没有可用页面——这为任何编写文档的人提供了一个很好的机会。）

此外，检查 `/etc/modprobe.conf` 目录下的与内核模块相关的其他文件。

# 使用 modprobe 手动加载内核模块

你不需要使用 `/etc/modprobe.conf` 条目来初始化新网络设备的内核支持。作为 root 用户（使用 `sudo`），你可以使用 `modprobe` 命令配合模块名称手动加载或卸载设备的内核模块。例如，使用以下命令启用之前示例中的 RealTek 网卡：

```
matthew@seymour:~$ sudo modprobe 8139too
```

按下回车键后，你将看到来自内核环形缓冲区（ring buffer）的设备报告，你可以通过 `dmesg` 命令显示它。这里是该命令输出的后续：

```
matthew@seymour:~$ dmesg
```

...
`eth0`: RealTek RTL8139 Fast Ethernet @ 0ce8ee000, 00:30:1b:07:07d, IRQ 11
`eth0`: Identified 8139 chip type 0RTL-8139C
`eth0`: Setting half-duplex based on auto-negotiated partner ability 0000.

注意此时尚未为设备分配 IP 地址和其他设置。Linux 可以使用多个太网接口，第一个以太网设备编号为 `eth0`，第二个为 `eth1`，依此类推。内核识别的每个不同的以太网设备可能根据其内核模块的报告，报告了额外的或不同的信息。这里是一个示例：

```
matty@seymour:~$ dmesg
epro100c:vl109-t 2/29/99 Donald Becker #cesdesis.gsfc.nasa.gov/linux/drive/res/epro100.html
epro100c:$Revision: 1.36 $2000/11/17 Modified by Andrey V. Savochkin
&#x194;casaw@saw.sw.com$ and others
PCI: Found IRQ 10 for device 00:00.0
eth0: Intel Corporation 721383-0 [Ethernet Pro 100], 00:90:27:91:B2:B5, IRQ 10.
Board assembly 721383-0, Physical connectors: RJ45
```

（注：原文中重复的部分已省略）

## Table 18: ifconfig Options

| Use | Option |
|---|---|
| Create alias | `[device]` |
| Change IP address | `address` |
| Change the netmask | `netmask` |

## Table 19: Using Network Configuration Tools

| Use | Option |
|---|---|
| Change the broadcast | `[address]` |
| Take interface down | `down` |
| Bring interface up | `up (add IP)` |
| Set NIC promiscuous | `promiscuous` |
| Set multicast mode | `allmulti` |
| Enable or disable | `point-to` |

# 第 18 章 网络

`wlan0` Link encap:Ethernet HWaddr 00:16:ea:d4:58:88

inet addr:192.168.1.106 Bcast:192.168.1.255 Mask:255.255.255.0

inet6 addr fe80::216:eff:fed4:588/64 Scope:Link

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:325832 errors:0 dropped:0 overruns:0 frame:0

TX packets:302754 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueelen:1000

RX bytes:20731800 (207.3 MB) TX bytes:404442735 (40.4 MB)

此输出非常易理解。该条目显示了接口的 IP 地址。UP 表示接口已准备绪可以使用；BROADCAST 表示接口已连接到网络（以太网）；RUNNING 表示接口正在运行；LOOPBACK 显示了哪个设备是环回地址。`eth0` 上的最大传输单元（MTU）为 1500 字节。这决定了通过此接口传输的最大数据包的大小（有时为了提高性能会将其“调整”为其他值）。Metric 是一个 0 到 3 之间的数字，表示该接口在路由表中的优先级。数字越小越好。

可以使用 `ifconfig` 命令结合表 18.1 中列出的命令来显示或控制特定接口的信息。例如，要停用主机上的以太网设备，可以使用 `ifconfig` 命令、接口名称和 `down` 命令，如下所示：

```
mathew@seymour~$ sudo ifconfig eth0
```

你可以通过指定主机名或 IP 地址以及网络信息来配置并激活设备。例如，要使用特定的 IP 地址配置并激活（启动）`eth0` 接口，可以使用如下 `ifconfig` 命令：

```
mathew@seymour~$ sudo ifconfig eth0 192.168.2.9 netmask 255.255.255.0
```

如果你在系统的 `/etc/hosts` 文件中有默认项（参见本章后的“网络配置文件”部分），在本章稍后的部分，你可以根据定义的主机名配置并激活接口：

```
mathew@seymour~$ sudo ifconfig eth0 catcat.fakeurl.com
```

### ip

在准备此版本时，`ifconfig` 在我们的测试系统中运行良好，但它现在已不再默认安装。随着 `ip` 命令能提供更多功能，它正逐渐失去宠。。该命令通过一系列子命令来执行其任务。许多常用的子命令也有短别名，这些别名也列在这里。请注意，接下来列出的 IP 地址仅为示例；你网络中的地址可能会不同。

以下命令允许你获取有关所有网络接口的信息：

```
mathew@seymour~$ sudo ip add show
```

## 使用网络配置工具

要为特定接口（在此例中 `eth1`）分配 IP 地址，请使用以下命令：

```
matthew@semour:-$ sudo ip add 192.168.2.9 dev eth1
```

要删除已分配的 IP 地址，请使用此命令：

```
matthew@semour:-$ sudo ip del 192.168.2.9 dev eth1
```

如所示启用网络接口：

```
matthew@semour:-$ sudo ip link set eth1 up
```

要禁用网络接口，请使用以下命令：

```
matthew@semour:-$ sudo ip link set eth1 down
```

如下方式检查路由表：

```
matthew@semour:-$ sudo ip route show
```

要添加静态路由，使用以下命令：

```
matthew@semour:-$ sudo ip route 10.10.30.0/24 via 192.168.50.100 dev eth0
```

使用以下命令删除静态路由：

```
matthew@semour:-$ sudo ip route del 10.10.30.0/24
```

要添加默认网关，使用以下命令：

```
matthew@semour:-$ sudo ip route default 192.168.36.100
```

下一节将解释如何配置你的系统以与局域网（LAN）配合。

### ip route

另一个用于配置网络的命令是 `ip route` 命令。`ip route` 用于构建实现数据包路由的内存路由表，并显示路由信息。它在 `ip`（或 `ifconfig`）初始化接口后使用。`ip route` 通常用于通过网关或其他主机设置到其他网络的静态路由。
