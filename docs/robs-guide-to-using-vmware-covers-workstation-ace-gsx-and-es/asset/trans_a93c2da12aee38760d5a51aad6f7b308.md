
可以 在 VNC 安装的引导加载程序中输入的参数有：

```
vnc=1 vncpassword=<pw> hostip=<ip> netmask=<ip> gateway=<ip>
```

hostip 和 netmask 参数是可选的，但如果省略它们，系统会提示你选择 DHCP 或手动输入静态 IP 信息。gateway 参数始终是可选的。如果用于远程安装的计算机与你要安装的虚拟机位于同一子网，则它们可以在没有网关地址的情况下通信。

![](img/25fe75b93b97a021effaba85db112a52_171_0.png)

图 13.5：正在侦听 VNC 连接的 Suse Linux 安装示例。

安装过程将开始，并会显示有关 IP 配置以及如何访问 VNC 服务器以继续安装的消息。

![](img/25fe75b93b97a021effaba85db112a52_171_1.png)

在你的远程计算机上，启动 VNC 客户端并通过其 IP 地址和屏幕号访问 VNC 服务器。例如，192.168.2.150:1，如图 13.6 所示。

图 13.6：使用 IP 地址和屏幕号从客户端访问安装。

## 14 VMware NetWare 提示

本章中的提示适用于 NetWare 操作系统。它们适用于所有版本，从 NetWare 4.x 到 Open Enterprise Server，除非另有说明。

### 14.1 VMware Tools 的可用选项

从 VMware Workstation v3.2 开始，NetWare 的 VMware Tools 变得可用。你可以使用 help 命令查看可用命令：

```
VMWTOOL Help
```

表 14.1：NetWare 的 VMware Tools 的可用命令。

| Command | Description |
|---|---|
| help | 显示命令和选项。 |
| partitionlist | 显示虚拟磁盘中所有磁盘分区列表以及分区是否可以缩小。 |
| shrink <partition> | 缩小列出的分区。如果未指定分区，则虚拟磁盘中的所有分区都会被缩小。缩小过程的状态会显示在系统控制台底部。 |
| devicelist | 列出虚拟机中的每个可移动设备及其设备 ID，以及设备是否已启用或禁用。可移动设备包括虚拟网络适配器、CD-ROM 和软盘驱动器。 |
| disabledevice or enabledevice <device name> | 禁用或启用虚拟机中指定的设备或设备。如果未指定设备，则虚拟机中的所有可移动设备将被禁用或启用。 |
| synctime on or off | 打开或关闭与主机操作系统时间的时间同步。默认情况下，时间同步处于关闭状态。不带任何选项使用此命令可查看当前时间同步状态。提示：只有在来宾操作系统的时间设置早于主机设置的时间时，才能将来宾操作系统的时间与主机操作系统的时间同步，它不得在未来。 |
| idle on or off | 允许你打开或关闭 CPU 空闲程序。默认情况下，空闲程序处于打开状态。CPU 空闲程序包含在面向 NetWare 来宾的 VMware Tools 中。**提示：** 不要使用较旧的常用 NW-IDLE NLM。使用这些 NLM 可能会导致性能下降而不是改善。 |

### 14.2 NetWare 的网络适配器

对于 NetWare 服务器应使用哪个适配器并不明显。在 VMware 中安装 NetWare 时，会根据你的 NetWare 版本提供两个或三个选项：CNEAMD.LAN 驱动程序，或 CPCNTNW.LAN 和 PCNTNW.LAN 驱动程序。

![](img/25fe75b93b97a021effaba85db112a52_173_0.png)

图 14.2：为 NetWare 来宾安装选择 PCNTNW.LAN 驱动程序。

我更喜欢使用 PCNTNW.LAN

为什么？有几个原因支持我做出此选择：

- 虚拟机包含 AMD am79C970A 以太网适配器。PCNTNW 驱动程序由 AMD 创建，而 CNEAMD 驱动程序是 Novell 的兼容驱动程序。
- PCNTNW 驱动程序来自 2000 年，CNEAMD 驱动程序来自 1998 年
- 与 CPCNTNW 和 CNEAMD 驱动程序相比，PCNTNW 驱动程序是用汇编语言编写的，而另外两个是用 C 语言编写的。这使得用 C 语言编写的驱动程序略有优势。然而 CPCNTNW.LAN 驱动程序更新（2002 年），并且并非在所有版本的 NetWare 中都可用，也未在 Yes Tested and Approved 程序中使用。我仍然更喜欢 PCNTNW 而非另外两个。

顺便说一下，这三个驱动程序都可以使用，并且 PCNTNW 和 CNEAMD 都被 Novell 的 Yes Tested and Approved 程序使用。你可以通过以下 URL 搜索此数据库：http://developer.novell.com/nss。

### 14.3 缩小你的 NetWare 磁盘

如何缩小磁盘在第 9.2 节：“缩小你的虚拟磁盘”中进行了描述。对于每个操作系统，你都可以采取一些额外步骤来为缩小虚拟机做好准备。最重要的是删除不必要的文件。

首先，你必须准备你的卷。按照以下步骤将磁盘缩小到非常小：

### 删除未使用的文件

你的 NetWare 文件系统上会有许多你可能不会使用的文件。首先在安装时要有所选择。你真的需要 exteNd Application Server 吗？还是带有 200MB 驱动程序集的 iPrint？

可以 在不出现任何问题情况下从服务器删除的文件：

- ConsoleOne (sys:\public\mgmt)（可从工作站使用，甚至更好使用 iManager）
- DNS/DHCP 管理控制台 (sys:\public\dnshcp)
- sys:\public\winnt & win95
- SYS:\CDROM$$.ROM 中的 CD-ROM 索引文件
- SYS:\PVSW（Pervasive SQL）

即使在新的服务器安装后，文件系统也充满了可恢复的文件（安装程序将许多临时文件解压到 SYS）。因此，在缩小之前，请确保先清理你的卷。清理可从客户端进行，但从
NetWare 6.5 service pack 1 开始，服务器上有一个新命令可执行此任务。

```
PURGEVOLUME SYS (or any other volume name for your server)
```
(清理过程的输出会打印到 Logger 屏幕)

你可以从 GUI 中的 VMware tools 菜单缩小磁盘。工具可通过 VMTOOLJ.NCF 命令启动。或者，你可以使用 FILLZERO.NLM 将所有未使用的块填充为零。该文件可在作者网站的 tools 部分获得，网址如下：www.robbastiaansen.nl。

### 14.4 在安装期间使用 VMware 的快照功能

在安装期间，主要是在其 GUI 部分，安装屏幕有时会冻结并停止工作。反复重新开始安装会变得烦人且耗时。通过使用新的快照功能，你可以回滚到安装过程中的之前点。

根据我的经验，每当你在安装中成功到达以下步骤之一时，都应创建快照：

- GUI 安装开始时。
- 安装文件复制完成后。
- 完成所有产品选择后（NetStorage 屏幕是最后一个；在该屏幕中，在它开始创建 eDirectory 对象之前创建快照）。

### 14.5 从 STARTUP.NCF 中删除平台支持模块

这取决于你的硬件，但你可能需要删除安装期间添加的多处理器平台支持模块 (MPS14.PSM)。加载此模块时，我经常遇到“FOUND SPINLOCK TO BE BUSY WITH SINGLE PROCESSOR ACTIVE” Abends。

有关此问题的更多信息可在以下技术信息文档中找到：“Single processor server abending often.” TID10067515

### 14.6 我的 NetWare 服务器不断丢失时间同步

在 VMware 中运行多个服务器需要 NetWare 服务器之间进行时间同步。你可以使用常规的 Timesync 机制设置此项。NetWare 虚拟机配置经常会丢失时间同步。如果你的 NetWare 服务器不断丢失时间同步，请按如下方式更改同步参数：

- 将轮询间隔设置为 3600
- 将短间隔设置为 600

解释这些参数的 TID 位于本段末尾。

注意：不要对 NetWare 和 VMware 使用 NTP 进行时间同步。NetWare 使用的常规 Timesync 同步（也通过 TCP/IP）对于大多数配置已足够。

注意：在 NetWare 服务器之间设置时间同步后，不要启用 VMware 在主机和来宾之间提供的时间同步。在 GUI 中的 VMware tools 中或使用命令 VMWTOOL SYNCTIME 检查此状态。

这里描述的参数仅适用于 Timesync。在较旧版本的 NetWare 上，你可以使用 MONITOR.NLM（使用 !h 开关显示隐藏参数）。但在 NetWare 5.1 和 6.x 中，你可以使用 Remote Manager 显示隐藏参数并相应地设置它们。

![](img/25fe75b93b97a021effaba85db112a52_176_0.png)

图 14.3：NetWare 时间同步参数。
