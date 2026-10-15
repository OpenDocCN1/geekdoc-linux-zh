
![](img/c0f2cd6655e598a6e6ffb6a15368bc67_241_0.png)

# 242

# 第11章 连接互联网服务提供商 207

## 设置电缆或 DSL

如果你幸运住在可以高速访问的地区，并计划进行真正的上网，那么电缆和 DSL 调制器无疑是值得考虑的选项。

正如名称，电缆调制器是一种允许你连接系统并使用电缆提供商网络进行数据传输的设备。和普通调制调器一样，电缆调制器通过调制和解调数字信号工作；然而，该设备要复杂一些。它既是调制器，又是电视调谐器，还是桥器。该设备连接到标准以太卡，通常提供 1 到 1.5 Mbps 的速度。

数字用户用户线路 `DSL` 也通过标准以太卡连接到你的系统，因此你需要采取的配置步骤基本上与电缆调制器相同。这项技术允许你在普通电话线上建立高速连接而不会占用你的电话线。性能与电缆相似（较新的 `DSL` 服务提供 6 或 8 Mbps），但取决于你的购买量，`DSL` 可能会贵一些。

## 哪种技术更好？

目前，这可能是最常见的问题，因为很少有用户可以选择使用哪种方法。不过这种情况很快就会改变，随着运营商升级网络和市场开放。

使用电缆调制器时，你与地理区域内的其他人共享网络带宽。通常情况下这不是大问题，但随着这种设备变得流行，情况可能会发生。许多电缆公司不允许你从家里系统提供服务，因为这样做会影响同一社区其他用户的服务水平。另外，在电缆公司成为公共运营商（如 `MCI`）之前，你通常没有选择可以使用哪种 `ISP`。

# 设置以太网卡

你要做的第一工作是为以太网卡配置内核驱动程序。通常，当你申请高速访问时，可以与你的互联网服务提供商 `ISP` 安排技术人员为你进行硬件配置。不过在大多数情况下，你的 `ISP` 都有能力为 `Windows` 配置连接。你主要需要知道你的网卡使用的是哪种芯片，因为你需要这些信息来选择要使用的驱动程序。`Linux` 支持许多以太网卡，最近我们注意到厂商正在为其新的以太网模型使用 `Linux` 驱动。稳妥的方法是获取一个使用以下驱动之一的网卡；在使用之前，请询问你的硬件供应商网卡需要什么驱动：

- `SMC`
- `3c509`
- `Lance`
- `NE2000`

许多 `Linux` 发行版已经在内核中编译了对常用网卡的支持。如果你的发行版情况如此，你只需要安装网卡并配置网络接口即可。

尝试执行 `cat /proc/net/dev`。如果你的网卡被系统识别，你应该看到一行包含以太网设备信息的行。

> 根据惯，以太网设备名称为 `ethx`，其中 `x` 是代表特定网卡的数字：`eth0` 是第一块卡，`eth1` 是第二块，以此此类推。

或者，你可以使用 `ifconfig` 命令获取这些信息；参见列表 11-1 中的示例输出。

## 列表 11-1：ifconfig 的示例输出

```
$ /sbin/ifconfig -a

dummy Link enc:Ethernet Haddr 00:00:00:00:00:00

BROADCAST NOARP MTU:1500 Metric:1

TX packets:0 errors:0 dropped:0 overflows:0 carrier:0

collisions:0 txqueuelen:
```

```
eth0 Link enc:Ethernet Haddr 00:EE:3F:01:90:0F

BROADCAST MULTICAST MTU:1500 Metric:1

RX packets:0 errors:0 dropped:0 overflows:0 frame:0

TX packets:0 errors:0 dropped:0 overflows:0 carrier:0

collisions:0 txqueuelen:100
```

```
Interrupt:9 Base address:0xdc00

10 Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.255.0.0

UP LOOPBACK RUNNING MTU:3924 Metric:1

RX packets:18 errors:0 dropped:0 overflows:0 frame:0

TX packets:18 errors:0 dropped:0 overflows:0 carrier:0

collisions:0 txqueuelen:
```

如果你没有在以太网卡上看到任何信息，要么你的内核没有驱动程序，要么该驱动程序被编译为模块且尚未加载。

## 加载驱动模块

支持以太网卡的 `Linux` 驱动模块存储在 `/lib/modules/uname-r*/net` 目录中。在重新编译内核之前，在此处查看是否存在适用于你网卡的驱动程序。

`uname -r` 命令返回你系统的内核发布版本。如果你查看 `/lib/modules` 目录，你会看到类似 `/lib/modules/2.2.13`（或你安装的任何内核版本）的内容。

你希望在系统启动期间加载的内核模块在 `/etc/modules.conf` 文件中配置。因此，假设你有一块 3Com 兼容以太网卡，你应该在该文件中添加一个条目：

```
# load the driver for my Ethernet card

alias eth0 3c59x
```

这会导致你的系统为第一块以太网卡加载 `3c59x` 驱动程序。如果你有一块工业标准架构 `ISA` 卡（而不是 `PCI` 总线卡），你还应该包含一条指示网卡基 `I/O` 地址的行，因为自动探测可能无法工作。例如，如果你的网卡基地址为 `0x280`，`IRQ`（中断请求查询）为 `12`，那么你应该添加类似这样的第二个条目：

```
# specify the base I/O address and interrupt request

# line for my card

options 3c59x io=0x280 irq=12
```

查看你的以太网适配器文档以查找特定网卡的配置信息。

## 配置内核以支持以太网

以下是启用以太网适配器所需的选项：

```
Network device support -->

Ethernet (10 or 100Mbit) -->

<*> your_driver_from_the_list
```

> 提示：有关在 `Linux` 下配置网络适配器的详细信息，请参见 `Linux` 文档中的 `Ethernet-HOWTO`。

## 配置你的接口

在连接互联网之前，你必须设置好供使用的接口。

### 使用静态地址

如果你的 `ISP` 为你提供了专用 `IP` 地址，你必须使用 `ifconfig` 程序来配置网卡。与其手动设置，不如将必要的命令放入脚本文件中，我们可以从命令行或启动时的启动脚本中执行它，如列表 11-2 所示。

#### 列表 11-2：静态 IP 的网络接口配置脚本

```
#!/bin/sh

# inet-up - setup our Internet connection

/sbin/ifconfig eth0 192.168.1.10 netmask 255.255.255.0

# we're not on LAN, so this will be default.

/sbin/route add default eth0
```

### 使用 DHCP 获取地址

许多 `ISP` 使用动态主机协议 `DHCP` 分配 `IP` 地址。在这种情况下，我们将使用 `dhclient` 程序配置我们的接口，如列表 11-3 所示。

#### 列表 11-3：用于 DHCP 的接口脚本

```
#!/bin/sh

# inet-up - setup our Internet connection

/sbin/dhclient eth0
```

## 连接互联网服务商

要验证接口已启用，使用 `ifconfig` 命令：

```
$ /sbin/ifconfig eth0

eth0 Link encap:Ethernet Haddr 00:EE:3F:01:90:0F

inet addr:128.0.0.1 Mask:255.255.255.0

BROADCAST MULTICAST MTU:1500 Metric:1

RX packets:18 errors:0 dropped:0 overflows:0 frame:0

TX packets:0 errors:0 dropped:0 overflows:0 carrier:0

collisions:0 txqueuelen:100
```

## 测试

现在接口已启用，你可以通过 `ping` 命令对其进行测试。尝试 `ping` 服务器的 `IP` 地址：

```
$ ping 192.168.0.15

PING 192.168.0.15 (192.168.0.15): 56 data bytes

64 bytes from 192.168.0.15: icmp_seq=0 ttl=128 time=160.8 ms

64 bytes from 192.168.0.15: icmp_seq=1 ttl=128 time=155.8 ms
```
