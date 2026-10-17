
第 1 行显示了在命令行提示符处输入的 `ifconfig` 命令（你可能需要包含路径）。第 2 行显示了第一个网络接口——`lo` 的配置。这是一个被称为回环设备（loopback device）的特殊设备。Linux 自动配置它以为自身提供网络连接（因此称为 loopback，即回环）。IP 地址 `127.0.0.1` 是一个特殊的回环地址。你可以通过 Telnet 到 IP 地址 `127.0.0.1` 在你的系统上进行测试。如果你运行了 `inetd` 进程，可以使用此功能在进程之间通信并模拟网络功能，而无需让机器实际连接到网络。第 3 行显示了回环接口的 IP 地址信息。第 4 行显示了回环接口的状态。这表示回环接口处于 UP（运行）。

已安装以太网卡的配置参数从第 9 行开始。这显示了网卡的名称（`/dev/eth0`）以及硬件 MAC 地址。MAC 地址对于每个制造的以太网卡来说都是唯一的。第 10 行显示了该设备在你的以太网网络上的 IP 地址信息。你必须确保 IP 地址和子网掩码适用于你的网络，否则你的 Linux 服务器将无法与其他设备通信。第 11 行显示了接口状态。第 12–14 行显示了接口的网络统计数据。这是一个实用的排错工具，以防出现任何网络问题。如果你无法与其他设备通信，但看到 TX（发送）和 RX（接收）数据包计数增加，通常表明你漏掉了系统上的 IP 地址。如果你看到大量错误和冲突，则表明你的网络介质存在问题，例如电缆损坏或网络集线器故障。第 15 行显示了网卡的硬件配置。不同的网卡使用不同的方法与 Linux 通信，因此请注意工作的是哪块特定的网卡。许多 PCI 即插用卡在 Linux 启动时会自动配置。如果发生这种情况，你需要密切关注启动信息，以查看分配给网卡的取值。通常情况下这不是一个问题。

`ifconfig` 命令的第二种格式允许你手动设置网卡的配置参数。可用选项如表 4.2 所示。

### 表 4.2 ifconfig 命令选项

| 选项 | 说明 |
| --- | --- |
| Interface | 指定接口名称 |
| Up | 使接口尝试变为激活状态 |
| Down | 使接口尝试变为非激活状态 |
| -arp | 启用（或禁用）ARP 协议 |
| -promisc | 启用（或禁用）混杂模式 |
| -allmulticast | 启用（或禁用）多播功能 |
| metric N | 设置接口的路由目的的跃数（metric） |
| mtu N | 设置接口的最大传输单元（以太网为 1500） |
| dstaddaddr addr | 为点点链路（PPP）设置远程 IP 地址 |
| netmask addr | 设置 IP 子网掩码 |
| add addr/prefixlen | 向接口添加 IPv6 地址 |
| del addr/prefixlen | 从接口删除 IPv6 地址 |
| tunnel aa.bb.cc.dd | 创建一个新的 SIT (IPv6-IPv4) 设备，到给定的目标建立隧道 |
| irq addr | 设置设备使用的中断请求线 |
| io_addr addr | 设置设备在 I/O 空间中的起始地址 |
| mem_start addr | 设置设备共享内存的起始地址 |
| media type | 设置接口使用的物理端口或介质类型 |
| -broadcast addr | 如果给出了地址，则将接口的广播地址设置为 addr，否则清除接口的 IFF_BROADCAST 标志 |

`ifconfig` 命令的第二种格式允许你手动设置网卡的配置参数。可用选项如表 4.2 所示。

## [4] 配置你的 LINUX 系统

图 4.4 显示了红帽 Linux 用户可以使用哪些工具来简化网络生活。`netcefg` 程序是一个 X Windows 程序，它与 COAS 一样，允许你轻松地配置网络接口。每个网络接口都会列出来，并可以进行选择和编辑。请确保启用了 Aboot 选项，这样该接口将在下次启动时（以及之后的每次启动时）加载。

图 4.4
Red Hat netcefg 网络接口配置程序。

![](img/576b77705430d924d4e911445bf0a62d_88_0.png)

### 配置打印机

配置完美的 Linux 系统最复杂的部分之一就是让打印正常工作。同样，幸运的是有可用工具提供帮助，但在讨论它们之前，让我们先看看 Linux 打印到底是怎么。

大多数计算机用户熟悉通过 DOS 方法连接到 PC 的打印机。第一台打印机通常是 LPT1，第二台是 LPT2，第三台是 LPT3。Linux 没有采用这种命名约定。表 4.3 显示了 Linux 如何识别标准打印机。

表 4.3 Linux 并打印机
| Linux 设备 | DOS 打印机 |
|---|---|
| `/dev/lp0` | LPT1 |
| `/dev/lp1` | LPT2 |
| `/dev/lp2` | LPT3 |

一旦 Linux 识别到存在打印机，它必须能够与其通信。Linux 使用一个特殊的进程来持续监控打印作业并将其发送到打印机。`lpd` 进程在后台运行（假设你选择了启动它），并监控打印队列以寻找要发送到相应打印机的作业。它是如何知道要把哪些作业发送到打印机的呢？这正是棘手之处。`lpd` 进程读取一个特殊的配置文件 `/etc/printcap`，该文件对 Linux 系统可以打印的每个打印机都有特定的定义。创建一个完美的 `/etc/printcap` 文件就是 Linux 打印艺术的所在。列表 4.4 是一个示例 `/etc/printcap` 文件。

#### 列表 4.4 示例 /etc/printcap 文件

```
1 [jessica@shadrach /etc]$ cat printcap
2 #
3 lp:mylp:
4 :lp=/dev/lpd:\n5 :sd=/var/spool/lpd/lp:
6 :mx#:
7 :sh:
8 :if=/var/spool/lpd/lp/filter:
9 [jessica@shadrach /etc]$
```

第 3 行定义了打印机的名称。第一个列的是普通打印机名称。你应该有一个名为 `lpd` 的打印机，它被用作默认打印机。任何其他名称都是打印机的别名。第 4–7 行定义了 `lpd` 打印机的特性。每行都以一个能力代码开头。有很多选项可以配置到 `printcap` 文件中以定义打印机。`printcap` 的手册（man page）定义了所有可用选项。表 4.4 列出了你最可能遇到的一些重要选项。

#### 表 4.4 printcap 功能

| 名称 | 描述 |
|---|---|
| af | 如果进行计费，则使用的计费文件名 |
| br | 如果是串口打印机，则波特率 |
| if | 文本过滤文件的名称 |
| ff | 定义发送换页符的字符串 |
| fo | 当打印机首次打开时发送换页符 |
| lf | 错误日志文件的名称 |
| lo | 锁文件名 |
| lp | 如果打印机是本地打印机，则使用的设备名称 |
| mx | 最大打印文件大小（0 = 无限制） |
| of | 输出过滤文件的名称 |
| pl | 打印机页长（行） |
| pw | 打印机页宽（字符） |
| rm | 如果打印机是远程网络打印机，则机器名称 |
| rs | 将打印机用户限制为具有本地系统账户的用户 |
| sb | 在作业前打印短横幅（一行） |
| sc | 抑制向打印机的多次复制请求 |
| sd | 打印目录（spool directory）名称 |
| sh | 抑制打印并发页头 |

如果系统上有多个打印机，每台打印机在 `/etc/printcap` 文件中都有自己的部分。列表 4.4 中的示例表明该打印机连接到 LPT1 (`/dev/lpt0`)。它还使用 `/var/spool/lpd` 作为其打印目录，可以接受任何大小的打印过滤器，并使用文件 `/var/spool/lpd/filter` 作为输入过滤器。输入过滤器极难创建。它们控制打印数据呈现给打印机的方式。每种打印机使用不同类型的输入过滤器来为打印机格式化打印数据。激光打印机需要的数据与喷墨打印机不同。此外，`ghostscript` 是一个可以将 postscript 文件传递给打印机而无需用户进行复杂格式化的程序。大多数打印机输入过滤器都利用此程序帮助格式化打印输出。

### 轻松配置打印机

大多数 Linux 发行版通过提供图形实用程序来帮助安装和配置打印机。图 4.5 显示了 COAS 如何为 Caldera OpenLinux 系统配置打印机。

图 4.5
Caldera Open Administration 系统打印机配置辅助程序

![](img/576b77705430d924d4e911445bf0a62d_88_0.png)

## [第二部分] 运行 LINUX

### 发送到打印机

### 打印监控命令

#### 列表 4.5 示例 lpq 输出

```
1 [jessica@shadrach]$lpq
2 Printer: lp1@shadrach
3 Queue: 3 printable jobs
4 Server: pid 827 active
5 Unspooler: pid 826 active
6 Status: printed 21 bytes at 13:27:06
7 Rank Owner/ID Class Files
8 active rich@shadrach@826 A 826 test.txt      21 13:27:06
9 rich@shadrach@838 A 838 test.txt      21 13:27:19
10 rich@shadrach@843 A 843 test.txt      21 13:27:54
11 [rich@shadrach]$
```

#### 列表 4.6 示例 lprm 输出

```
1 [jessica@shadrach]$lprm 843
2 Printer lp1@shadrach:
3 checking 'rich@shadrach+843'
4 checking perms 'rich@shadrach+843'
5 dequeued 'rich@shadrach+843'
6 killing subserver '862'
7 [rich@shadrach]$
```
