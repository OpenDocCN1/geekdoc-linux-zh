
如果你有外部调制解调器，你需要担心的问题只是串口驱动可用。如果你有内部调制解调器（它为你的机器添加了自己的串口），你可能会遇到 IRQ 问题。此外，如果调制解调器具有非标准芯片，Linux 可能无法识别它。任何标记为“Winmodem”的调制解调器都无法在 Linux 上工作。这些调制解调器虽然便宜，但依赖 CPU 完成过多的处理工作，购买新机器时应尽量避免。

极有可能，你不需要做任何事情就能让 Linux 与你的调制解调器通信。所需的唯一项（串口支持）几乎存在于内核中，通常用于鼠标。

如果你连接了外部调制解调器，它将连接到板载串口之一，不应该有 IRQ 冲突问题。如果你是内部安装的并存在 IRQ 冲突，有几种解决方法。

1. 如果你没有同时使用两个内置串口，请 BIOS 中禁用其中一个。在某些情况下，调制解调器卡上的串口将简单地变成它能承载的最低串口，然后使用该端口的 IRQ。否则，你可能需要通过卡上的跳线帽设置串口。请咨询随调制解调器附带的文档。

2. 你可以使用 `serialport` 将卡上的串口分配到不同的 IRQ。如果两个内置串口都被占用并添加了内部调制解调器，它将作为第三个串口呈现给系统。要更改 IRQ，请使用：

```bash
$ serialport /dev/ttyS2 5
```

这与 System V init 软件包自带的 `powerd` 不同。不同之处在于它可以在主模式或从模式下运行，允许你管理同一 UPS 或局域网上其他机器的关机。

## 20.3 磁带

（注：由于提供的原文在此处出现大量重复，译文已按要求对核心逻辑部分进行完整翻译）

## 20.5 3D 卡

随着专用 3D 显卡的价格低于 200 美并提供出色的 3D 图形，你现在可以在 Linux 上玩到许多与 Windows 98 相同的游戏，甚至更多。物理安装请按照说明书进行。一旦 Linux 运行，你将需要下载、编译并安装 Mesa 3D 库。大多数 3D 程序都需要 Mesa，而 Mesa 附带了几个演示程序用于测试功能。某些显卡（如 3Dfx voodoo 系列）需要你从 3Dfx 下载一些驱动程序以完成安装。查看 Mesa 主页获取有关支持哪些 3D 显卡的更多信息。安装完成后，执行以下命令让 Mesa 使用全屏模式：

```
setenv MESA_GLX_FX=1
```

如果没有此命令，Mesa 将在窗口中启动应用程序，这会减慢图形性能（非常慢！），但如果你需要，你仍然可以在窗口中进行 3D 操作。完成一些演示程序后，找一份 Glquake 让你的朋友们大惊眼镜吧。

## 20.6 USB 支持

USB（通用串行总线）是通过主板上的单个连接连接低速设备的方法。USB 允许你将键盘、鼠标、扫描仪、摄像机、数字扬声器甚至以太网接口直接连接到机器上。USB 为低速（1.5MB）和高速（12MB）设备提供，每台机器最多可支持 127 个设备。USB 是即插即用的，这意味着你可以随意更换设备。

遗憾的是，很少有操作系统对 USB 有完全支持。在编写本文时，Linux 的支持还很小，但由于 iMac 只有 USB 连接，因此它可以处理 USB 键盘和鼠标。在未来几个月里，USB 支持将集成到主内核中，许多设备将获得支持。

## 20.7 添加新硬盘

在某个时刻，你可能想要为你的机器添加额外的磁盘空间。安装新硬盘是一个相当轻松的过程。在本节中，我们假设你正在使用 SCSI 主适配器。此外，你应该已经拥有了 SCSI、SCSI 磁盘以及对 SCSI 控制器的支持，这些可能是由销售机器的供应商设置好的。

在这种情况下，添加另一个硬盘非常简单：只需检查新硬盘以确保它具有唯一的 SCSI ID，将其安装在 CPU 机箱或外部机箱中，然后重启。通常，SCSI ID 是通过跳线设置的。它们在磁盘上的位置以及如何设置应该在随磁盘附带的说明书中解释。

一旦安装好硬盘，你需要在其上创建一些 Linux 分区。通过运行 `fdisk`：

```bash
# fdisk /dev/sdb
```

此磁盘的柱道数设置为 1030。这比 1024 大，可能会导致以下问题：

- 1. 在启动时运行的软件（例如 LILO）。

- 2. 来自其他操作系统的引导和分区软件（例如 DOS FDISK, OS/2 FDISK）。

```
Command (m for help): p
Disk /dev/sdb: 64 heads, 32 sectors, 1030 cylinders
Units = cylinders of 2048 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sda1 | | 1 | 1 | 100 | 102384 | 6 | DOS 16-bit |

当你第一次获得驱动器时，可能会有很多奇怪的、可能毫无意义的分区。只需用 `fdisk` 中的 `d` 命令删除它们，这样你就可以从零开始了。

要添加新分区，使用 `n` 命令：

```
Command (m for help): n
Command action
  extended
  p primary partition (1-4)
p
Partition number (1-4): 1
First cylinder (1-100): 1
Last cylinder or +size or +sizeM or +sizeK ([1-100]):+50M
```

```
Command (m for help): p
Disk /dev/sdb: 64 heads, 32 sectors, 100 cylinders
Units = cylinders of 2048 * 512 bytes
```

| Device | Boot | Begin | Start | End | Blocks | Id | System |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/sdb1 | | 1 | | 51 | 52208 | 83 | Linux native |

```
Command (m for help): n
Command action
e extended
p  primary partition (1-4)
p
Partition number (1-4): 2
First cylinder (1-100): 52
Last cylinder or +size or +sizeM or +sizeK [52-100]: 100
```

默认情况下，分区被创建为 Linux native（扩展 2）文件系统。如果你需要更改文件系统类型，例如添加交换分区，请使用 `t` 命令：

```
Command (m for help): t
Partition number (1-4): 1
Hex code (type L to list codes): 82
Changed system type of partition 1 to 82 (Linux-swap)
```

与常识相反，从性能角度来说，拥有几个大分区比许多小分区更好，尽管你的系统的需求可能在决定如何划分磁盘方面起着最大的作用。设置好分区后，在它们上运行 `mkfs` 来实际创建文件系统：

```bash
# mkfs /dev/sdb2
```

现在你可以挂载它了：

```bash
# mount /dev/sdb2 /tmp
```

你可能想向 `/etc/fstab` 添加一个条目，以便在启动时自动挂载你的分区：

```
device mountpoint filesystem options dump
sdb2 /tmp defaults 1 2
```

如果你在让系统识别新磁盘遇到困难、在插入驱动器时启动，或者如果你遇到 SCSI 问题，这里是一些需要检查的项目：

- 它通电了吗？

- 所有线缆都连接牢固了吗？

- SCSI 总线必须是线性的；如果你有外部设备，确保你只使用内部连接之一。

- 设备在总线上是否有唯一的 ID？记住，PCMIA 驱动在某些情况下是工作的……（注：此处原文似乎有语义不完整）

## 20.8 USB 设备

USB（通用串行总线）是一种通过主板上的单个连接连接低速设备的方法。USB 允许你将键盘、鼠标、扫描仪、摄像机、数字扬声器甚至以太网接口直接连接到机器上。USB 为低速（1.5MB）和高速（12MB）设备提供，每台机器最多可支持 127 个设备。USB 是即插即用的，这意味着你可以随意更换设备。

遗憾的是，很少有操作系统对 USB 有完全支持。在编写本文时，Linux 的支持还很小，但它可以处理 USB 键盘和鼠标，由于 iMac 只有 USB 连接。在未来几个月里，USB 支持将集成到主内核中，许多设备将获得支持。

## 20.7 添加新硬盘
