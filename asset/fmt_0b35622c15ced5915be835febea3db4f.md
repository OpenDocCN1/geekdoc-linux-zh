
> HFS 与 HP-UX HFS 是不同的文件系统。HP-UX HFS 是在 HP-UX 系统上可用的一种非日志文件系统格式。

## 非标准 Linux 文件系统

对这些文件系统的支持需要显式地编译到 Linux 内核中，因为内核默认没有配置对它们的支持。

### IBM JFS

`IBM JFS` 是由 IBM 创建的一种易于使用的日志文件系统。它专为高吞吐量服务器环境设计。这与 AIX 版本 5 中提供的文件系统相同。Linux 对 JFS 的支持是由 IBM 编写的。IBM 为 Linux 事业贡献了一些代码，并且是 Linux 的坚定支持者。他们还决定在未来将 Linux 作为他们主要的服务器文件系统。

### SGI XFS

SGI 的扩展文件系统 (`XFS`) 是 SGI 为 Silicon Graphics 系统开发的最新文件系统，从工作站到其超级计算机系列（在卖给 Terra Computers 之前）。它自 2001 年 5 月起在 Linux 中可用。

`XFS` 为高性能设计。它能从系统崩溃中快速恢复，并支持极大的磁盘阵列（它可以处理高达百万 TB 的文件）。它是少数几个在生产环境中经过多年验证并具有良好记录的日志文件系统之一。

它的功能包括访问控制列表、卷管理、保证性 I/O 以及用于更快速恢复的日志记录。`XFS` 可以在使用时进行备份，这非常方便，因为由于此缩短了系统管理时间。这是一个快速文件系统，你现在可以使用你的红帽 Linux 读取它。

### FREEVXFS

`VxFS` 是由 Veritas 公司开发的 Veritas 文件系统。它用于 SCO UnixWare、HP-UX、Solaris 等其他系统。它的某些功能包括访问控制列表、日志、在线备份以及对最大 2TB 文件的支持。目前有三个版本的 VxFS 正在使用。版本 1 是原始 VxFS，版本 2 包含了支持和动态 inode 分配。版本 4 是最新版本，支持配额和大大文件。

## 第四章：红帽 Linux 文件系统

适用于 Linux 的名为 `VxTools` 的 GNU 工具可以读取 `VxFS` 版本 2 和 4。

`VxTools` 包包含的工具有 `vxmount`、`vxsum`、`vxls`、`vxcat`、`vxdump`、`vxcd` 和 `vxpwd`。目前 Linux 对 `VxFS` 文件系统仅有读取支持。

### GFS

`GFS` 是 Sistina 的全局文件系统。它是一种用于 SAN（存储区域网络）的集群日志文件系统，允许多个服务器读写共享 SAN 设备上的单个文件系统。

`GFS` 是可扩展的，因为可以在不关闭系统或不离线磁盘的情况下添加存储设备和服务器。它还为 SAN 中的所有数据创建一个单一映像，因此如果某个服务器故障，可以将其移除并替换，同时在剩余服务器之间重新平衡负载。

在适当的集群设置中，集群中的所有节点通过光纤通道、SCSI 连接或网络块共享相同的存储设备。每个节点都认为文件系统是本地机器的，`GFS` 跨集群同步文件。`GFS` 是完全对称的，因此没有哪个服务器是瓶颈或单点故障。`GFS` 使用标准的 Unix 风格文件语义。

## 内存文件系统与虚拟文件系统

这些文件系统并不像传统文件系统那样存在，它们要么完全存在于内存中，要么是虚拟文件系统（例如，它们是系统设备的接口）。

### CRAMFS

`cramfs` 设计用于将文件系统“挤压”到较小的 ROM 上，因此它简单、简单，并且能够很好地压缩内容。最大文件大小为 16MB，最大文件系统大小为 256MB。

由于 `cramfs` 是压缩的，因此无法即时更新。需要运行 `mkramfs` 工具来创建或更新 `cramfs` 磁盘映像。镜像通过逐个压缩文件创建，因此实现了随机访问。元数据没有压缩，但经过了优化以占用比其他文件系统更少的空间。例如，仅存储 gad 的低 8 位。这节省了空间，但也带来了潜在的安全问题。

### TMPFS

`tmpfs` 的结构基于这样一种理念：`/tmp` 文件系统中的任何内容很快就会被再次访问。`tmpfs` 存在于内存中，因此你在临时（temp）中的操作不会在重启后持续。

将 `/tmp` 创建为内存文件系统可以提升性能。Solaris 一直将 `/tmp` 创建为内存文件系统，因为 Solaris 的开销非常大。在 Linux 中以前没有过将 `/tmp` 创建为内存文件系统，因为 `ext2` 文件系统的性能已经很不错了。但对于那些觉得性能不够的人来说，这很有用。

# 第一部分：红帽 Linux 系统与网络管理定义

### RAMFS

`ramfs` 是一个在内存中的文件系统。

### ROMFS

`romfs` 是一种只读文件系统，它的设计初衷是为了尽可能节省空间。

### PROC

`proc` 是一个虚拟文件系统，作为系统设备的接口（例如）。

### SOFTWARE

`proc` 目录包含了关于运行中软件的 l。

# 第一部分：红帽 Linux 系统与网络管理定义

- `exe` -- 包含一个指向进程可执行文件的链接
- `fd` -- 包含所有进程文件描述符的目录
- `maps` -- 包含指向进程可执行文件和库文件的内存映射
- `mem` -- 包含该进程持有的内存
- `root` -- 包含一个指向进程根目录的链接
- `stat` -- 包含进程状态
- `statm` -- 包含进程状态信息
- `status` -- 包含人类可读格式的进程状态

### PROC 硬件信息

如前所述，`/proc` 目录也包含一些的硬件信息。这些信息在您编译内核时非常有用。如果您忘记了有关硬件的具体细节，可以查看 `/proc` 目录下的文件，获取关于 Linux 机器上安装和运行的信息。

如果您怀疑由于 IRQ 冲突导致了硬件问题，也可以查看 `/proc/interrupts` 文件。

下面是我工作用的台式机的中断文件。每个数字对应一个 IRQ。IRQ 列表末尾的缩写含义是 NMI（非掩码中断）、LOC（每个 CPU 内部 APIC 的本地中断计数器）和 ERR。ERR 是一个计数器，在启动时为 0，每当 IO-APIC 总线发生错误时加增。IO-APIC 总线连接 SMP 系统中的 CPU。当发生错误时，信息会立即重传，因此您不需要过于担心该字段适数量的错误。

```
[vnavrat@buffy vnavrat]$ less /proc/interrupts
CPU                                              
0: 9270204 XT-PIC timer
1: 30515   XT-PIC keyboard
2: 0        XT-PIC cascade
5: 9869566 XT-PIC Crystal audio controller
8: 1        XT-PIC rtc
11: 1233943 XT-PIC usb-uhci,eth0
12: 682220 XT-PIC PS/2 Mouse
14: 77739 XT-PIC ide0
15: 2694731 XT-PIC idel
NM1: 0
LOC: 9720557
ERR:
MIS: 0
```

# 第 4 章：红帽 Linux 文件系统

在主 `/proc` 目录中，许多文件包含有关系统硬件的详细信息。列出的细节类型诸如硬件类型、型号和制造商。

下面是 `proc` 中 `cpuinfo` 文件的内容。它告诉您您使用的是什么种处理器，最重要的是它的运行速度。

```
[vnavrat@buffy vnavrat]$ less /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 7
model name : Pentium III (Katmai)
stepping : 3
cpu MHz : 498.479
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
f00f_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 2
wp : yes
flags : fpu vme de pse tsc msr pae mce cx8 apic spec mtrr
pge mca cmov
pat pse36 mmx fxsr sse
bogomips : 992.87
```

一些重要的 `/proc` 文件有：

- `/proc/cpuinfo` — 包含 CPU 的信息
- `/proc/interrupts` — 告诉您在使用哪些中断
- `/proc/scsi` — 告诉您安装了什么种 SCSI 适配器
- `/proc/parport` — 包含系统上并行端口的信息
- `/proc/tty` — 包含可用且正在使用的 tty 信息
- `/proc/apm` — 包含高级电源管理信息
- `/proc/bus` — 包含特定特定信息的目录
- `/proc/devices` — 列出字符设备和块设备
- `/proc/dma` — 列出使用的 DMA 通道
- `/proc/filesystems` — 列出支持的文件系统
- `/proc/fs` — 包含文件系统参数
- `/proc/ide` — 包含 IDE 子系统的信息
