
```text
[root@server1 root]# dmesg | tail
Bluetooth: RFCOMM socket layer initialized
Bluetooth: RFCOMM TTY layer initialized
parport0: PC-style at 0x378 [PCSPP,TRISTATE,EPP]
parport0: Printer, Brother HL-1440 series
parport_pc: Via 686A parallel port: io:0x378
lp0: using parport0 (polling).
lp0: console ready
agpgart: Found an AGP 2.0 compliant device at 0000:00:00.0.
agpgart: Putting AGP V2 device at 0000:00:00.0 into 1x mode
agpgart: Putting AGP V2 device at 0000:01:00.0 into 1x mode
[root@server1 root]#
```

你还可以通过查看 `/var/log/boot.log` 或 `/var/log/messages` 日志文件的内容来查看在启动期间成功或未能启动的系统进程。`boot.log` 文件仅包含服务启动信息，而 `messages` 包含启动信息以及启动后来自系统的其他消息。以下输出显示了一个 `boot.log` 示例：

```text
[root@server1 root]# tail /var/log/boot.log
Jul 16 08:38:33 server1 privoxy: privoxy startup succeeded
Jul 16 08:38:34 server1 gpm: gpm startup succeeded
Jul 16 08:38:35 server1 11im: 11im startup succeeded
Jul 16 08:38:36 server1 canna: succeeded
Jul 16 08:38:36 server1 crond: crond startup succeeded
Jul 16 08:38:38 server1 xfs: xfs startup succeeded
Jul 16 08:38:38 server1 anacron: anacron startup succeeded
Jul 16 08:38:38 server1 atd: atd startup succeeded
Jul 16 08:38:38 server1 readahead: Starting background readahead:
Jul 16 08:38:39 server1 rc: Starting readahead: succeeded
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_294_0.png)

#### 注意

> `boot.log` 和 `messages` 文件的大小可能随时间变得非常大。因此，系统会在 `/var/log` 目录中归档这些日志文件的旧副本，并在文件后添加一个数字以指示归档的最新程度。例如，要查看 `/var/log/boot.log` 的最新归档，你可以查看 `/var/log/boot.log.1` 文件。类似地，你可以查看 `/var/log/boot.log.2` 来查看 `/var/log/boot.log` 的第二新归档。

## 章节摘要

- 自 1986 年以来，已经开发了多种不同的 SCSI 标准。SCSI 硬盘驱动器通过 `SCSI ID` 进行唯一识别，并通过终结电缆连接到控制器。
- 每个外围设备在使用前必须配置中断请求（IRQ）和输入/输出（I/O）地址，并可选地使用直接内存访问（DMA）通道。如果设备符合即插即用（Plug-and-Play）标准，此配置可以自动分配给设备。
- 便携式笔记本电脑通常使用 `APM` 或 `ACPI` 在外设不使用时关闭其电源，以节省电池电量。
- 需要容错功能的计算机通常采用使用 `RAID` 配置的 SCSI 硬盘驱动器。
- 虽然 Linux 通常从 CD-ROM 介质安装，但也可以使用位于 DVD、硬盘以及 `NFS`、`FTP` 和 `HTTP` 服务器上的文件进行安装。你需要创建一个安装启动 CD-ROM 或可启动 USB 闪存驱动器来执行这些类型的安装。
- 你可以使用磁盘镜像软件或 `kickstart` 文件来简化在多台计算机上安装 Linux。
- 不受支持的显卡、超频 CPU、即插即用支持以及不正确的内存设置都可能导致安装失败。
- `/proc` 目录包含有关系统中检测到的硬件的信息，在验证安装是否成功时很有用。

## 关键术语

- `/proc/cpuinfo` — 包含有关当前系统中 CPU 配置信息的文件。
- `/proc/dma` — 包含有关当前系统中直接内存访问分配信息的文件。
- `/proc/interrupts` — 包含系统当前中断请求（Interrupt Request）分配信息的目录。
- `/proc/ioports` — 包含系统当前输入/输出地址分配信息的目录。
- `/proc/meminfo` — 包含系统当前物理内存和虚拟内存使用情况信息的目录。
- `/proc/modules` — 包含当前已并入内核的模块信息的目录。
- 高级配置和电源接口 (`ACPI`) — 一种允许操作系统控制何时向外围组件供电的标准。
- 高级电源管理 (`APM`) — 一种允许计算机 BIOS 控制何时向外围组件供电的标准。
- 刻录 — 将信息写入 CD-R、CD-RW、DVD-R 或 DVD-RW 的过程。
- 互补型金属氧化物半导体 (`CMOS`) — 主板上的一个存储器，用于存储引导过程期间使用的配置信息；它不是真正的 ROM 芯片，需要来自主板电池的微弱电流来维持存储内容。
- 直接存储器访问 (`DMA`) — 允许硬件设备直接访问物理内存的通道。
- 磁盘映像软件 — 用于制作硬盘或硬盘分区完全相同副本的软件。
- 磁盘镜像 — 一种 RAID 配置，也称为 RAID 1，由两个相同的硬盘组成，这两个硬盘并行写入相同的信息以确保容错能力。
- 磁盘条带化 — 一种 RAID 配置，属于 RAID 0 类型，用于将不同的信息写入不同的硬盘以加快访问时间。
- 带奇偶校验的磁盘条带化 — 一种 RAID 配置，也称为 RAID 5，用于将不同的信息写入硬盘以加快访问时间，并且包含奇偶校验信息以确保容错能力。
- 容错 — 一种在发生故障时表现出最少停机时间的设备。
- 文件传输协议 (`FTP`) — 用于在因特网上传输文件的最常用协议。
- 通用引导加载程序 (`GRUB`) — 一个用于启动 Linux 操作系统的程序。
- 超文本传输协议 (`HTTP`) — 用于在因特网上传输信息的底层协议。
- 输入/输出 (`I/O`) 地址 — 由特定硬件设备使用的物理内存中的地址。
- 安装日志文件 — 在安装过程中创建的文件，用于记录安装期间发生或失败的操作。
- 中断请求 (`IRQ`) — 处理器用于优先处理外围设备同时发出的服务请求的一种共享处理器时间的方法。
- 国际标准化组织 (`ISO`) 映像 — 包含 CD-ROM 或 DVD 上确切信息的大型单文件副本。
- `Kickstart` 配置器 — 一个可用于创建 `kickstart` 文件的图形实用工具。
- `kickstart` 文件 — 一个可以在 Red Hat Fedora Linux 安装开始时指定的文件，用于自动化安装过程。
- Linux 加载器 (`LILO`) — 一个用于启动 Linux 操作系统的程序。
- 逻辑单元号 (`LUN`) — SCSI 链中连接在特定节点上的每个设备的唯一标识符。
- 网络文件系统 (`NFS`) — 由 Sun Microsystems 开发的一种分布式文件系统，允许不同类型的计算机访问网络上共享的文件。
- 超频 — 以高于其额定时钟速度运行的 CPU。
- 即插即用 (`PnP`) — 系统 BIOS 自动允许设备分配所需 `IRQ`、`I/O` 地址和 `DMA` 信息的过程。
- 轮询 — 查询设备以查看是否有需要运行的服务的行为。
- 冗余独立磁盘阵列 (`RAID`) — 将多个硬盘驱动器的存储空间组合成一个更大的逻辑存储单元的过程。
- `SCSI ID` — 一个唯一标识并优先处理连接到 SCSI 控制器的设备的编号。
- 跨接 — RAID 级别 0 的一种类型，允许两个或更多设备表示为单个大容量卷。
- 目标 `ID` — 另请参阅 `SCSI ID`。
- 终端器 — 一种用于终止电气传导介质的设备，以吸收传输信号并防止信号回弹。

## 复习题

1. 系统定时器的默认 `IRQ` 分配是什么？
   - a. 0
   - b. 3
   - c. 5
   - d. 15
