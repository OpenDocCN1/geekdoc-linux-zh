
```text
$ dmesg
...
eep100:cv:1.09j-t 9/29/99 Donald Becker http://cesdis.gsfc.nasa.gov/linux/drivers/eep100.html
eep100.c: $Revision: 1.36 $ 2000/11/17 Modified by Andrey V. Savochkin <saw@saw.sw.com.sg> and others
PCI: Found IRQ 10 for device 00:d0.0
eth0: Intel Corporation 82557 [Ethernet Pro 100], 00:90:27:91:92:B5, IRQ 10.
 Board assembly 721383-007. Physical connectors present: RJ45
 Primary interface chip i82555 PHY #1.
 General self-test: passed.
 Serial sub-system self-test: passed.
 Internal registers self-test: passed.
ROM checksum self-test: passed (0x04f451b0).

...
```

在此示例中，已识别出一个 Intel Ethernet Pro 100 网卡。要禁用对网卡的支持，可以卸载内核模块，但通常只有在设备不再使用后才能卸载。请阅读下一节，了解如何在 Linux 内核识别网卡后配置网卡以及如何控制其行为。

## 使用网络配置工具

如果在初始安装后添加或更换网络硬件，则必须配置新硬件。您可以使用命令行或图形配置工具进行配置。要使用命令行配置网络客户端主机，可以使用命令组合或编辑`/etc`目录下的特定文件。要通过图形界面配置硬件，可以使用 Ubuntu 的图形工具`network-admin`用于 X。本节介绍可用于在 Ubuntu 系统上配置网络接口和网络设置的命令行和图形软件工具。您将了解如何控制网卡并管理系统与网络的交互方式。

如果您是 Linux 新手，使用命令行配置工具可能会显得困难。对于任何网络新手来说，`network-admin`图形工具是最佳选择。手动和图形方法都需要 root 权限才能工作。如果您没有 root 权限，请在尝试任何操作之前获取它。您不应编辑系统上图形网络管理工具使用的任何脚本或设置文件。您的更改将在下一次运行该工具（如`network-admin`）时丢失！要么采用手动方法并编写自己的网络设置脚本，要么坚持使用图形配置实用程序。

## 命令行网络接口配置

您可以使用基本的 Linux 网络实用程序从命令行配置网络接口。您可以使用命令更改当前设置或通过编辑多个系统文件来使用命令行配置网络客户端主机。两个命令`ifconfig`和`route`用于网络配置。`netstat`命令显示有关网络连接的信息。

```text
/sbin/ifconfig
```

`ifconfig`用于配置网络接口。您可以使用它来

- 激活或停用网卡或更改网卡模式

- 更改机器的 IP 地址、网络掩码或广播地址

- 创建 IP 别名以允许网卡上使用多个 IP 地址

- 为点对点连接设置目标地址

您可以使用单个命令更改任意多或任意少的这些选项。命令的基本结构如下：

```text
ifconfig [network device] options
```

表 14.1 显示了`ifconfig`选项的子集及其使用示例。

### TABLE 14.1 `ifconfig` Options

| 用途 | 选项 | 示例 |
|---|---|---|
| 创建别名 | `[network device]` | `ifconfig eth0:0 [number] 10.10.10.10` |
| 更改 IP 地址 |  | `ifconfig eth0 10.10.10.12` |
| 更改网络掩码 | `netmask [netmask]` | `ifconfig eth0 netmask 255.255.255.0` |
| 更改广播 | `broadcast [address]` | `ifconfig eth0 broadcast 10.10.10.255` |
| 关闭接口 | `down` | `ifconfig eth0 down` |
| 启动接口 | `up` (add IP address) | `ifconfig eth0 up (ifconfig eth0 10.10.10.10)` |
| 设置网卡混杂模式 | `[-]promisc` | `ifconfig eth0 promisc mode on [off]` |
| 设置多播模式 | `[-]allmulti` | `ifconfig eth0 allmulti on [off]` |
| 启用 [禁用] 点对点地址 | `[-]pointopoint` | `ifconfig eth0 pointopoint 10.10.10.20` |

`ifconfig`手册页显示了其他可使您的机器与 AppleTalk、Novell、IPv6 等多种网络类型接口的选项。再次阅读手册页以了解这些网络类型的详细信息。

### NOTE

> 混杂模式会导致网卡接收网络上的所有数据包。它通常用于嗅探网络。多播模式使网卡能够接收网络上的所有多播流量。

如果你的系统中`/etc/hosts`文件中定义了主机（请参阅本章后面的“网络配置文件”部分），你可以按照定义的`hostname`来配置并激活接口，如下所示：

```text
$ sudo ifconfig eth0 dogdog.hudson.com up
```

阅读下一节，了解如何配置系统以便与你的局域网协同工作。

### `/sbin/route`

用于配置网络的第二个命令是`route`命令。`route`用于构建路由表（在内存中），用于路由数据包以及显示路由信息。它在`ifconfig`初始化接口之后使用。`route`通常用于通过网关或到其他主机设置到其他网络的静态路由。命令配置如下：

```text
$ route [options] [commands] [parameters]
```

要显示路由表，请使用不带选项的`route`命令。显示结果看起来类似这样：

```text
$ route
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.2.0     *               255.255.255.0   U     0      0          0 eth0
default         .               0.0.0.0         UG    0      0          0 eth0
```

在第一列中，`Destination`是接收主机的 IP 地址（或，如果主机在`/etc/hosts`或`/etc/networks`中，则为主机名）。`default`条目是此机器的默认网关。`Gateway`列列出了数据包必须经过的网关才能到达目的地。星号（`*`）表示数据包直接发送到主机。`Genmask`是网络掩码。`Flags`列可能有多个条目。在我们的示例中，`U`验证路由已启用，`G`指定`Destination`需要使用网关。`Metric`列显示到`Destination`的距离。某些守护进程使用它来确定到达`Destination`的最简单路由。`Ref`列由某些 UNIX 变体用于传达对路由的引用。Linux 不使用它。`Use`列指示此条目被查找的次数。最后，`Iface`列是对应条目的接口名称。

使用`route`命令的`-n`选项将给出相同的信息，用 IP 地址代替名称和星号（`*`），看起来像这样：

```text
#### /sbin/route -n
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
192.168.2.0     0.0.0.0         255.255.255.0   U     0      0          0 eth0
0.0.0.0         192.168.2.1     0.0.0.0         UG    0      0          0 eth0
```

`route`命令可以使用`add`选项向表中添加条目。使用`add`选项时，你可以指定主机（`-host`）或网络（`-net`）作为目标。如果未使用选项，`route`命令假定你正在配置发出命令的主机。`route`命令最常见的用途是为一台丢失路由表的主机添加默认网关，或网关地址已更改时。例如，要添加具有特定 IP 地址的网关，可以使用以下命令：

```text
$ sudo route add default gw 149.112.50.65
```
