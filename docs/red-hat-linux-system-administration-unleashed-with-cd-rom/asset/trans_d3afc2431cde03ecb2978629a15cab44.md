
探测并口是一项危险的操作，可能导致系统锁定。更安全的做法是通过在启动命令行、lilo.conf 中或加载 parport 模块时指定这些参数来设置端口，例如地址和 IRQ 设置。

parport 模块将并口的控制分为两个模块，其中一个管理与架构无关的端口共享，另一个是与架构相关的模块。这两者中的一个或两个都可以编译为模块。

同样，关于此功能的更多文档可在 Documentation 目录中的 parport.txt 和 paride.txt 文件中找到。

许多现代系统，尤其是笔记本电脑和其他便携设备，都包含对高级电源管理（Advanced Power Management，简称 APM）的支持。支持 APM 的系统能够通过在空闲期间关闭显示器、使硬盘旋转停止并停靠，或完全挂起系统来节省电量。不幸的是，每个厂商对 APM 的实现都不同，使得在内核中支持它变得困难。这些差异还意味着，如果你的内核出现问题，你应首先关闭 APM 支持，然后尝试重现该问题。

对于在系统崩溃时采取行动的看门狗系统，有两个不同的位置提供选项。基于硬件的看门狗系统稍后设置，但在通用选项部分，你可以设置对基于软件的看门狗系统的支持。启用此选项后，内核将监控并定期更新 /dev/watchdog，如果更新未能按时进行，系统将被强制重新启动。此支持非常有用，如果你有远程管理的系统并且在崩溃时必须重新启动。

有关软件和硬件看门狗的更多信息可在内核 Documentation 树中的 watchdog.txt 文件中找到。

## 即插即用支持

在最近的内核中，已添加了一些对即插即用设备的支持，在内核配置的本节中，你可以选择是否包含它。请阅读这些选项的帮助信息并根据需要进行设置。

## 块设备

内核配置的下一个主要细分包含支持各种块设备的选项。这些选项包括对 IDE/ATAPI 设备的支持、并口 IDE 设备支持、各种 PCI 芯片组以及 Linux 软件 RAID 支持，后者在第 9 章“Linux and RAID”中有详细讨论。让我们更详细地了解一下其中一些选项。

块设备中最可配置的驱动程序之一是软盘驱动程序。该驱动程序不仅能够控制软盘驱动器，还能控制备份设备，并且能够运行多个磁盘控制器。可以通过内核命令行或通过 /etc/lilo.conf 文件中的 append 命令将一些命令行参数传递给软盘驱动程序。表 35.3 描述了其中一些选项。

### 表 35.3 软盘驱动程序选项

| Option | Description |
|---|---|
| floppy=daring | 在大多数现代 Pentium 系统上可用，此选项允许进行可加快软盘访问的优化，但不兼容。 |
| floppy=one_fdc | 此选项告诉驱动程序只有一个控制器可用。 |
| floppy=two_fdc or floppy=<address>, two_fdc | 使用两个控制器，第二个位于指定地址。 |
| floppy=thinkpad | 某些 ThinkPad 笔记本电脑需要此选项，因为它们颠倒了磁盘更改线的约定。 |
| floppy=omnibook or floppy=nodma | 防止使用 DMA 进行数据传输。某些 HP Omnibook 系统需要此选项。 |
| floppy=yesdma | 用于强制 DMA 模式。此选项为默认设置。 |
| floppy=nofifo | 如果在使用软盘时从以太网卡或其他设备收到 "Bus master arbitration" 错误，请使用此设置。 |
| floppy=<threshold>, fifo_depth | 设置 DMA 模式的 FIFO 深度。编译为模块允许对该参数进行实验以找到最佳设置。 |
| floppy=<drive>, <type>,cmos | 将指定驱动器的 CMOS 类型设置为给定类型。如果软盘驱动器多于两个，则需要此选项。 |
| floppy=broken_dcl | 避免使用磁盘更改线，并假定在每次重新打开设备时磁盘已被更改。对某些笔记本电脑和旧式 PC 有用。 |
| floppy=L40SX | 防止在接收到意外中断时打印消息。IBM L40SX 笔记本电脑需要此选项以防止视频和软盘控制器冲突。 |
| floppy=<nr>,irq and floppy=<nr>,dma | 设置指定设备的 IRQ 或 DMA 通道。 |
| floppy=slow | 某些步进速率较慢的 PS/2 机器需要此选项。 |

软盘模块选项的完整列表可在 /usr/src/linux/drivers/block 目录中的 README.fd 和 fdutils 软件包中找到。一套软盘驱动程序实用程序，包括增强的 mtools 工具包，可从 ftp://metalab.unc.edu/pub/Linux/system/Misc/ 下载。

### 提示

软盘驱动程序选项的指定方式如前表所示，但与许多其他内核和模块选项不同，你只允许进行一次此类声明。因此，要设置多个选项，必须一次性全部指定。例如，要向软盘模块指定 daring 和 two_fdc，你将发出以下命令：

```
insmod 'floppy="daring two_fdc"'
```

你还可以使用 LILO 配置文件 /etc/lilo.conf 中的 append 行、在内核命令行上或通过旧的环境变量语法将选项传递给软盘驱动程序。

在块设备选项下还选择了 Linux 下的增强 IDE 支持，除了支持多达八个 IDE 驱动器外，还支持 IDE/ATAPI CD-ROM、磁带驱动器和软盘驱动器。2.2 内核中的新驱动程序还包括对 OPTi 芯片组上 PIO 模式的支持、SCSI 主机仿真以及对大量芯片组的支持。

IDE 驱动器的调优使用 hdparm 实用程序完成。有关选项和调优的更多详细信息可在 Documentation 目录中的 ide.txt 文件中找到。

### 注意

如果在将 IDE 驱动程序作为模块加载时需要传递选项，必须在命令行中用分号替换任何逗号。

```
insmod ide.o options="ide0=serialize ide2=0x1e8;0x3ee;11"
```

## 循环设备

循环设备允许你创建文件然后将其作为文件系统处理。例如，你可以创建软盘的映像或从文件系统创建 CD-ROM 映像，然后使用循环设备将其挂载为常规文件系统，并在将映像提交到磁盘或 CD-R 之前进行更改。循环设备还用于一些可用的文件系统加密方案中，如 Loopback Encrypted Filesystem HOWTO 中所述，可在 http://www.linux.com/Loopback-Encrypted-Filesystem-HOWTO.html 找到。为了利用循环设备，你必须拥有最新版本的 util-linux 软件包。要确定支持你的内核的正确版本，请参阅 /usr/src/linux/Documentation 目录中的 Changes 文件。

## 网络块设备支持

在块设备下可以选定的一个实验性选项是对网络块设备的支持。网络块设备允许客户端系统通过 TCP/IP 透明地访问远程系统上的块设备。这与 NFS 或 Coda 不同，因为以这种方式访问的块设备可用于任何类型的文件系统，包括交换设备。

## Linux 软件 RAID

在块设备下可以选定的主要功能之一是对软件 RAID 的支持。该软件 RAID 在第 9 章中与在 Linux 下操作 RAID 阵列所需的实用程序一起进行了完整描述。

## 并口 IDE 设备

这里也包括对并口 IDE 设备的支持。此选项允许你使用通过并口连接到计算机的外部硬盘和其他 IDE/ATAPI 设备。需要注意的是，如果将此选项编译为模块，还必须将 parport 选项编译为模块。

## 网络选项

就像 UNIX 一样，Linux 是一种网络操作系统，独立的 Linux 系统很少见。即使是家庭办公室的工作站，通常也通过 PPP 网络协议连接到 Internet。没有网络服务的 Linux 工作站就像架在支架上的汽车。它拥有强大的引擎和许多很酷的按钮和旋钮，但...
