
在某些情况下，还可以重新加载服务。这会尝试向单个服务发送信号，强制服务重新加载其配置文件。在大多数情况下，这意味着发送一个 `SIGHUP` 信号。并不是每个服务都支持此功能。

`rc.d` 系统不仅用于网络服务，它还贡献于大多数系统初始化。例如，考虑 `bfsck` 文件系统。当执行此脚本时，它将打印出以下消息：

将在 60 秒后启动后台文件系统检查。

因此，它被用于后台文件系统检查，许多系统依赖其他服务才能正常运行。NIS 和其他基于 RPC 的服务可能在 `rcbind` (portmapper) 服务启动之前无法启动。为了解决这个问题，依赖关系和其他元数据被包含在每个启动脚本顶部的注释中。`reader(8)` 程序用于在系统初始化期间解析这些注释，以确定满足依赖关系的服务调用顺序。每个启动文件的顶部可能包含以下单词：

- PROVIDE：指定此文件提供的服务。
- REQUIRE：列出此服务所需的服务。此文件将在指定服务之后运行。
- BEFORE：列出依赖于此服务的服务。此文件将在指定服务之前运行。

通过使用这种方法，管理员可以轻松地控制系统服务，而无需像某些 Unix 操作系统那样处理“运行级别分级”（unlevels）的麻烦。

关于 `rc.d` 系统的更多信息可以在 `rc(8)` 和 `rc.sub(8)` 手页中找到。

## 11.8 设置网络接口卡

由 Marc Vonfeuille 贡献。

如今，我们考虑计算机时无法不考虑网络连接。添加和配置网卡是任何 FreeBSD 管理员的常见任务。

### 11.8.1 定位正确的驱动

在开始之前，你应该知道你拥有的卡的模式、它使用的芯片，以及它是 PCI 卡还是 ISA 卡。FreeBSD 支持多种 PCI 和 ISA 卡。检查你所在发行版本的硬件兼容列表（Hardware Compatibility List）查看你的卡是否受支持。

一旦你的卡受支持，你就需要确定适用于卡的正确驱动程序。
`usr/src/sys/config/NOTES` 和 `/usr/src/sys/arch/config/NOTES` 将为你提供网络接口列表以及一些关于支持的芯片/卡的信息。如果你对哪个驱动是正确的有疑问，请阅读手册页。驱动程序将提供更多关于支持的硬件的信息，甚至是可能发生的问题。

如果你拥有一张常见的卡，你最需要费力寻找驱动程序的情况会在启动期间出现，如下：

```
dc0: <82c169 PNIC 100BaseTX> port 0xa00-0xa0ff mem 0xd3800000-0xd38000ff irq 15 at device 11.0 on pci0
```

### 第11章 配置与优化

在示例中，我们使用两块卡来驱动系统。

```
dc0: Ethernet address: 00:a0:cc:da mibus0 on dc0

uk0:<Generic 802.3 interface on miub0

ukpho0:10baseTX,baseX,100baseTX, auto

dc1: PCI on 100BaseTX 0x980ff mem 0xd380000-0xd3800ff irq 11 at device 12 on pci0

01:cc:da:db mibus1 on dc1

ukph1:<Generic 802.3 interface on miub1

ukpho1:10baseTX,baseX,100baseTX, auto
```

如果你的 NIC 不是 GENERIC，你需要加载正确的驱动程序。可以通过以下方式实现：

- 最简单的方法是使用 `kldload(8)` 加载模块。并不是所有 ISA 卡都可用。
- 或者，你可以在内核中静态编译网卡的支持。检查 `/usr/src/sys/conf/NOTES`、`/usr/src/sys/arch/NOTES` 路径。

### 11.8.2 配置网卡

一旦加载了网卡的驱动，就需要对网卡进行配置。在许多情况下，网卡在安装时已经配置好了。要显示系统的网络接口配置，输入以下命令：

```
# ifconfig
dc0: flags=UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 192.168.1.3 mask 0xffffff0 broadcast 192.168.1.255

ether 00:a0:cc:da

media: Ethernet autoselect (100baseTX full-duplex)

status: active

dcl: flags=UP,BROADCAST,RUNNING,MULTICAST> mtu 1500

inet 10.0.0.1 mask 0xffffff0 broadcast 10.0.0.255

ether 00:a0:cc:db

media: Ethernet 10baseT/UTP

status: no carrier

lo0: flags=POINPOINT,UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384

inet 127.0.0.1 mask 0xffffff0

tun0: flags=... mtu 1500
```

旧版本的 FreeBSD 可能在 `ifconfig(8)` 后面需要 `-a` 选项。关于 `ifconfig(8)` 语法的更多细节请参考手册页。本章省略了涉及 IPv6 (`inet6`) 的条目。

在此示例中显示了以下设备：

- `dc0`：第一个以太网接口
- `dcl`：第二个以太网接口
- `lp0`：并行接口
- `lo0`：回环设备
- `tun0`：由 `ppp` 使用的隧道设备

FreeBSD 根据内核启动检测网卡的顺序来使用驱动名称。例如，`sis2` 将是系统中使用 `sis(4)` 驱动的第三块网卡。

在示例中，`dc0` 设备处于启用并运行状态。关键指标是：

1. UP 表示卡已配置并就绪。
2. 网卡有一个地址 (`inet`)（在本例中为 192.168.1.3）。
3. 它有一个有效的子网掩码 (`netmask`: 0xffffff 等于 255.255.255.0)。
4. 它有一个有效的广播地址 (`inet`, 192.168.1.255)。
5. 网卡的 MAC 地址 (`ether`) 是 00:aa:cc:da:da。
6. 物理媒体处于自动选择模式 (`media`: Ethernet autoselect (100baseTX full-duplex))。我们看到 `dcl` 配置为运行在 10baseT/UTP 媒体上。关于驱动可用媒体类型的更多信息，请参考其手册页。
7. 链路状态为活动，即检测到了载。对于 `dcl`，我们看到 `status: carrier`。当以太网线插入端口时这是正常的。

```
if ifconfig(8) 输出类似

dc0: flags=BROADCAST,SIMPLEX,MULTICAST> mtu 1500

ether 00:aa:cc:da:da
```

这表示卡尚未配置。

配置你的网卡需要 root 权限。网卡配置可以通过 `ifconfig(8)` 从命令行完成，但你必须在每次重启系统后执行。`/etc/rc.conf` 文件是添加网卡配置的地方。

在编辑器中打开 `/etc/rc.conf`。你可以为系统上的每个网卡添加一行，在我们的示例中，我们添加了：

```
ifconfig_dc0="inet 192.168.1.3 netmask 255.255.255.0"

ifconfig_dcl="inet 10.0.0.1 netmask 255.255.255.0 media 10baseT/UTP*"
```

你必须将 `dc0`、`dcl` 等替换为对应卡的正确设备，并将地址替换为正确的地址。你应该阅读网卡驱动和 `ifconfig(8)` 手册页以获取更多关于选项的细节，并查看 `rc.conf(5)` 手册页获取更多关于 `/etc/rc.conf` 的信息。

你可能还需要编辑 `/etc/hosts` 以添加局域网（LAN）中各种机器的名称和 IP 地址，如果它们尚未在其中。如需更多信息，请参考 `hosts(5)` 和 `/usr/share/examples/etc/hosts`。

## 11.8.3 测试与故障排除

一旦你在 `/etc/rc.conf` 中作了必要的更改，你应该重启系统。这将使得接口的更改生效，并验证系统启动时是否存在任何配置错误。系统重启后，你应该测试网络接口。

### 11.8.3.1 测试以太网

为了验证以太网是否配置正确，你必须尝试两件事。首先，`ping` 接口本身，然后 `ping` 局域网上的另一台机器。

首先测试本地接口：

```
% ping -c 5 192.168.1.3

PING 192.168.1.3 (192.168.1.3): 56 bytes

64 bytes from 192.168.1.3: icmp_seq=0 ttl=64 time=0.082 ms

64 bytes from 192.168.1.3: icmp_seq=1 ttl=64 time=0.074 ms
```
