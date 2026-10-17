
### 3.32.0.1–3.39.255.254

从上述范围来看，`3.34.0.6/13` 的计算机无法与 `3.31.0.99/13` 的计算机通信，因为它们位于不同的子网。若要通信，它们之间必须有一个路由器。

![](img/c27875544958897d817484d558c208c8_561_0.png)

在对 C 类网络进行子网划分时，请确保丢弃每个范围中的第一个和最后一个 IP 地址，以用于该子网的广播地址和网络地址。

## IPv6 协议

随着互联网在 20 世纪 90 年代的发展，互联网服务提供商（ISP）意识到使用 IPv4 可用的 IP 地址数量不足以应对未来的增长。因此，IPv6 协议于 1998 年设计出来，以容纳更多的 IP 地址。IPv6 使用 128 位来标识计算机，而 IPv4 仅使用 32 位（4 个八位组）。这使得 IPv6 能够寻址多达 340,282,366,920,938,463,463,374,607,431,768,211,456（即 340 万亿万亿万亿）台独特的计算机。

![](img/c27875544958897d817484d558c208c8_561_1.png)

由于地址空间巨大，使用 IPv6 时不需要进行子网划分。

IPv6 IP 地址使用 8 个由冒号分隔的 16 位十六进制数字书写——例如，`2001:0db8:3c4d:0015:0000:0000:adbb:ef12`。如果 IPv6 IP 地址包含 `0000` 段，在大多数表示法中通常会被省略，因此 `2001:0db8:3c4d:0015::adbb:ef12` 等同于 `2001:0db8:3c4d:0015:0000:0000:adbb:ef12`。IPv6 环回地址是 `0000:0000:0000:0000:0000:0000:0000:0001`，但为了简洁，通常简写为 `::1`。

![](img/c27875544958897d817484d558c208c8_561_2.png)

与传统的十进制计数方案不同，十六进制使用扩展的计数系统，除了 0–9 数字外，还包括字母 A 到 F。因此，数字 10 在十六进制中称为 A，数字 11 称为 B，数字 12 称为 C，数字 13 称为 D，数字 14 称为 E，数字 15 称为 F。

尽管 IPv6 地址可以用几种不同的方式表示，但 IPv6 地址的前半部分由您的 ISP 分配，通常用于标识您的网络。IPv6 地址的后半部分称为链路本地部分，用于唯一标识局域网（LAN）中的计算机。

尽管如今大多数操作系统都支持 IPv6，但互联网上采用它的网络和计算机非常少。2014 年，谷歌报告称，任何国家/地区中采用 IPv6 的计算机比例均低于 3%。IPv6 缓慢的采用速度主要归因于两项允许 IPv4 为比以前多得多的计算机编址的技术：代理服务器和网络地址转换（NAT）路由器。

代理服务器和 NAT 路由器是具有 IP 地址并可以访问互联网等网络的计算机或硬件设备。网络上的其他计算机可以使用代理服务器或 NAT 路由器来代替它们获取网络或互联网资源。此外，有三个保留的 IPv4 地址范围不会分配给互联网上的计算机，且仅用于代理服务器或 NAT 路由器之后：

- 整个 `10.0.0.0` A 类网络（`10.0.0.0/8`）
- `172.16` 到 `172.31` 的 B 类网络（`172.16–31.0.0/16`）
- `192.168` C 类网络（`192.168.0.0–255.0/24`）

因此，冰岛代理服务器后的一台计算机和西雅图 NAT 路由器后的一台计算机可以使用相同的 IPv4 地址——例如，`10.0.5.4`——而不会出现问题，因为这些计算机中的每一台都仅使用自己的代理服务器或 NAT 路由器请求互联网资源。例如，公司可能会使用思科 NAT 路由器，允许公司内的其他网络和计算机访问互联网。同样，高速家庭互联网调制解调器通常作为 NAT 路由器运行，以允许家庭中的多台计算机访问互联网。

当今世界上大多数计算机通过代理服务器或 NAT 路由器获得互联网接入。由于这些计算机在保留网络范围内使用共享的 IPv4 地址，而不是使用唯一的 IP 地址，可用的 IPv4 地址数量一直保持较高水平，并减缓了 IPv6 的采用。

## 配置网络接口

![](img/c27875544958897d817484d558c208c8_562_0.png)

企业环境中的 Linux 计算机通常通过有线或无线网卡（NIC）连接到公司网络。在家里，越来越多的人通过网卡（NIC）连接到互联网，使用的技术包括光纤、WiMAX、数字用户线（DSL）和宽带有线电视网络（BCN）。

如果在安装期间检测到了 NIC，Fedora Linux 会自动配置合适的驱动程序，使 Linux 内核能够与 NIC 驱动程序协同工作。然而，由于安装介质中未包含适用于该 NIC 的合适 Linux 驱动程序，某些 NIC 在安装时无法被检测。

NIC 驱动程序通常包含在可以插入 Linux 内核的模块中。模块以 `.ko`（内核对象）扩展名结尾，通常存储在 `/lib/modules` 目录中。可以使用 `insmod` 或 `modprobe` 命令将它们手动加载到 Linux 内核中。要查看当前加载到 Linux 内核的模块列表，可以使用 `lsmod` 命令。可以使用 `rmmod` 命令从 Linux 内核中移除模块。

较旧的 Linux 内核在启动时自动从 `/etc/modprobe.conf` 或 `/etc/modules.conf` 文件中的条目加载模块。现代 Linux 内核使用硬件检测过程，在启动时自动加载模块。但是，您可以将特定模块的名称添加到文件中，以确保现代 Linux 内核在启动时自动加载该模块。这对于在启动过程中未被自动检测到的设备或提供额外内核功能的模块非常有用。

要在 Ubuntu Server 14.04 上在启动时加载特定模块，只需将模块名称添加到 `/etc/modules` 文件即可。对于 Fedora 20 系统，启动时会从 `/etc/modprobe.d` 目录内的文件加载额外的模块。例如，要在启动时加载 DEC tulip 有线网卡的模块并将其别名设为 `eth0`，只需将行 `alias eth0 tulip` 添加到 `/etc/modprobe.d` 目录中的新文件即可。然后，tulip 模块将从 `/lib/modules` 的子目录中找到，并加载到 Linux 内核中，被称为 `eth0`。

在项目 6-3 中，您修改了 `/etc/modules` 文件，以确保在启动时加载 ZFS 模块。

![](img/c27875544958897d817484d558c208c8_563_0.png)

![](img/c27875544958897d817484d558c208c8_563_1.png)

![](img/c27875544958897d817484d558c208c8_563_2.png)

![](img/c27875544958897d817484d558c208c8_563_3.png)

系统中的第一个有线以太网 NIC 通常称为 `eth0`，第二个有线以太网 NIC 通常称为 `eth1`，依此类推。类似地，系统中的第一个无线 NIC 称为 `wlan0`，第二个无线 NIC 称为 `wlan1`，依此类推。

某些 Linux 发行版为有线 NIC 提供硬件特定的别名。例如，`em1` 可能指嵌入在主板上的第一个有线 NIC，而 `p2p1` 可能指位于主板上第二个 PCI 扩展插槽（p2）中的第一个有线 NIC（p1）。

您可以使用 `lshw` 命令查看特定的硬件设备。例如，`lshw -C network` 命令将显示有关系统中 NIC 硬件的详细信息，包括所使用的内核模块。

在将 NIC 的驱动程序模块加载到 Linux 内核后，您可以配置其使用 TCP/IP。`ifconfig`（接口配置）命令可用于向 NIC 分配 TCP/IP 配置，以及查看计算机中所有网络接口的配置。要为 `eth0` 分配 IP 地址 `3.4.5.6`，子网掩码为 `255.0.0.0`，广播地址为 `3.255.255.255`，可以在命令提示符下使用以下命令：

```
ifconfig eth0 3.4.5.6 netmask 255.0.0.0 broadcast 3.255.255.255
```

或者，您可以从网络上的动态主机配置协议（DHCP）或引导协议（BOOTP）服务器接收 TCP/IP 配置。要为第一个以太网适配器从网络上的服务器获取并配置 TCP/IP 信息，可以在命令提示符下使用命令 `dhclient eth0`。

为您的 NIC 获取 IP 地址的过程因计算机处于 IPv4 或 IPv6 网络而异。如果您尝试从 DHCP 或 BOOTP 服务器为您的 NIC 获取 IPv4 配置，而网络中不存在 DHCP 或 BOOTP 服务器，您的系统将分配一个 `169.254.x.x` 的 IPv4 地址，其中 `x.x` 是随机生成的主机 ID。这种自动分配功能称为 **自动私有 IP 编址（APIPA）**。如果您的网络包含配置了 IPv6 的路由器，则会向每个 NIC 自动分配 IPv6 地址。这是因为 NIC 使用 **互联网控制报文协议版本 6**（ICMPv6）进行自动配置。

(ICMPv6) 路由器通告消息以探测其网络中的 IPv6 配置信息。或者，你可以从网络中的 DHCP 服务器获取你的 IPv6 配置。如果你的网络中没有配置了 IPv6 的路由器或 DHCP 服务器来为你的 NIC 提供 IPv6 配置，你的系统将分配一个 IPv6 链路本地地址，该地址以你 IPv4 地址的十六进制等效值开头，并以你的 NIC 硬件地址的后半部分结尾。

![](img/c27875544958897d817484d558c208c8_564_0.png)

要查看所有接口的配置，你可以不使用任何参数运行 `ifconfig` 命令，如下面输出所示：

```
[root@server1 ~]# ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
        inet 3.4.5.6 netmask 255.0.0.0 broadcast 0.0.0.0
        inet6 fe80::280:c6ff:feF9:1B8c prefixlen 64 scopeid 0x20<link>
        ether 00:80:C6:F9:1B:8C txqueuelen 1000 (Ethernet)
        RX packets 1550  bytes 611332 (597.0 KiB)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 722  bytes 62170 (60.7 KiB)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0
lo:   flags=73<UP,LOOPBACK,RUNNING> mtu 65536
        inet 127.0.0.1 netmask 255.0.0.0
        inet6 ::1 prefixlen 128 scopeid 0x10<host>
        loop txqueuelen 0 (Local Loopback)
        RX packets 4  bytes 340 (340.0 B)
        RX errors 0 dropped 0 overruns 0 frame 0
        TX packets 4  bytes 340 (340.0 B)
        TX errors 0 dropped 0 overruns 0 carrier 0 collisions 0
[root@server1 ~]#_
```

`ifconfig` 命令的输出显示，eth0 NIC 有一个 IPv4 地址 `3.4.5.6` 和一个 IPv6 地址 `fe80::280:c6ff:feF9:1B8c`，该地址由系统自动配置，因为 IPv6 地址的后半部分与硬件地址（ether `00:80:C6:F9:1B:8C`）的后半部分相同。它还显示了接口统计信息以及具有 IP 地址 `127.0.0.1` 的特殊回环适配器（lo）；该 IP 地址代表本地计算机，并且是所有使用 TCP/IP 的计算机所必需的。

![](img/c27875544958897d817484d558c208c8_564_1.png)

如果你重启计算机，为 eth0 配置的 TCP/IP 信息将会丢失。为了允许系统在每次启动时激活并配置接口的 TCP/IP 信息，只需在启动时由你的 Linux 发行版激活网络时读取的配置文件条目中添加相应条目即可。对于 Fedora 20 系统，你可以将条目添加到 `/etc/sysconfig/network-scripts/ifcfg-interface` 文件中，其中 interface 是网络接口的名称。下面是一个第一个以太网接口（eth0）配置文件的示例：

```
[root@server1 ~]# cat /etc/sysconfig/network-scripts/ifcfg-eth0
DEVICE=eth0
BOOTPROTO=none
HWADDR=00:80:C6:F9:1B:8C
IPADDR=3.4.5.6
NETMASK=255.0.0.0
GATEWAY=3.0.0.1
ONBOOT=yes
TYPE=Ethernet
IPV6INIT=yes
USERCTL=no
DEFROUTE=yes
IPV4_FAILURE_FATAL=yes
NAME="System eth0"
UUID=5fb06bd0-0bb0-7ffb-45f1-d6edd65f3e03
PEERDNS=yes
PEERROUTES=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_PEERDNS=yes
IPV6_PEERROUTES=yes
IPV6_FAILURE_FATAL=no
[root@server1 ~]# _
```

上述输出中的条目表明，第一个以太网适配器（eth0）的 TCP/IP 配置将在启动时激活（ONBOOT=yes），并且如果有配置了 IPv6 的路由器，IPv6 将使用 ICMPv6 自动配置（IPV6_AUTOCONF=yes）。

NIC 不从 DHCP 服务器获取信息（BOOTPROTO=none），而是使用 IP 地址 `3.4.5.6`、子网掩码 `255.0.0.0` 和默认网关 `3.0.0.1` 来配置 IPv4。此外，你可以将 BOOTPROTO=none 行更改为 BOOTPROTO=dhcp，以从网络中的 DHCP 服务器获取所有 TCP/IP 配置信息。

编辑 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件后，你不需要重启系统才能使新的 TCP/IP 配置生效。相反，只需运行 `ifdown eth0` 命令来取消配置 eth0 网络接口，然后运行 `ifup eth0` 命令来使用 `/etc/sysconfig/network-scripts/ifcfg-eth0` 文件中的设置配置 eth0 网络接口即可。或者，你可以使用 `ifconfig eth0 down` 和 `ifconfig eth0 up` 命令来禁用和启用 eth0 网络接口。

Ubuntu Linux 系统不在 `/etc/sysconfig/network-scripts` 目录下的文件中存储网络配置。相反，所有网络接口都是根据 `/etc/network/interfaces` 文件中存储的信息进行配置的。下面是一个示例 `/etc/network/interfaces` 文件，其中为 eth0 分配了静态 IP（`3.4.5.6`）：

```
[root@server1 ~]# cat /etc/network/interfaces
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto eth0
iface eth0 inet static
address 3.4.5.6
netmask 255.0.0.0
network 3.0.0.0
gateway 3.0.0.254
[root@server1 ~]#_
```

要改为使用 DHCP 配置 eth0，你只需将 `iface eth0 inet static` 行更改为 `iface eth0 inet dhcp`，并删除上述示例中的 `address`、`netmask` 和 `gateway` 行，然后使用 `ifdown eth0` 命令后跟 `ifup eth0` 命令重新加载配置，就像在 Fedora Linux 中那样，以禁用和启用网络接口。

为了更方便地配置网络接口，你可能可以从 GUI 环境中访问你的配置。大多数 Linux 发行版都包含一个图形网络配置工具，如果安装了 GUI 环境，就可以运行该工具。在 Fedora 20 中，你可以使用 Network 实用程序来配置 NIC 上的 IP。只需导航到 Activities, Show Applications, Settings, Network，然后单击图 12-2 中显示的齿轮图标。

![](img/c27875544958897d817484d558c208c8_566_0.png)

### 图 12-2 Network 实用程序
