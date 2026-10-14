
First cylinder (1-14593, default 3649):

Last cylinder or +size (1-14593, default 14593): +1G

```
- 10. 这完成了创建该分区的所需的信息，但再次没有告诉你实际上是否成功。使用 `p` 命令列出当前定义的任何分区：
```

Command (m for help): p

Disk /dev/sda: 120.0 GB, 120034123776 bytes

255 heads, 63 sectors/track, 14593 cylinders

Units = cylinders of 16065 * 512 = 822580 bytes

Device Boot Start End Blocks

/dev/sda1 3648 23258 

/dev/sda2 3649 26912 

```
确实，你现在有了一个 30GB 的分区和一个 1GB 的分区。

- 11. 现在，将这些更改写入磁盘并退出 `fdisk` 命令：
```

Command (m for help): w

The partition table has been altered:

Calling ioctl() to re-read partition table.

Syncing disks.

```
恭喜，你刚刚对磁盘进行了分区。通常情况下我们不会在磁盘上留下未使用空间，但通过这样做，我可以创建额外的分区。

下一步是将每个定义的分区格式化为文件系统或额外的交换空间。图形化工具通常会在创建分区时完成此操作，但在命令行并不友好。说实话，你真的会在安装系统后创建额外的分区，但我想确保你如何操作。99.9% 的情况下，你会使用 `mkfs` 工具来创建文件系统，它只是不同文件系统命令的封装。在 Linux 系统上，你将创建任何格式的文件系统：ext2、ext3、JFS、ReiserFS、Virtual FAT 或 XFS。文件系统类型在第 4 章“本地文件系统：标准与日志”节中有所介绍。使用文件系统的默认选项创建任何这些类型的文件系统，以下示例显示了在分区 `/dev/sda` 上创建 ext3 文件系统的命令和输出：
```
$ sudo mkfs -t ext3 /dev/sda

mke2fs.ext3 1.41.3 (12-Oct-2008)

Filesystem label=

OS: Linux

Block size=4096 (log=2)

Fragment Size=4096 (log=2)

366288 inodes, 7325632 blocks

366281 inodes (5.00%) reserved for the super user

First data block=0

22 block groups

32768 blocks per group, 32768 fragments per group

16352 inodes per group

superblock backed on blocks:

32768, 163840, 229376, 294912, 819200, 884736, 1605632, 

2654208, 4096000
```

# 添加硬件和附加外设

写入 inode 表：224/224
创建日志 (32768 块)：完成
写入超级块和文件系统信息：完成

此文件系统将在每挂载 25 次或每 180 天后检查一次，以先者为准。使用 `tune2fs -c` 或 `-i` 可以覆盖此设置。

就这样！你可以通过执行 `mount` 命令临时挂载此分区，或将其永久地添加到每次启动系统时都要挂载的文件系统列表中。这两个概念都已经在第 4 章中进行了解释。

`mkswap` 命令允许对对的分区进行格式化，使其能够作为系统虚拟内存管理器的交换空间（swap space）。例如，用于在 `/dev/sda2` 上创建交换区的命令以及该命令的输出如下：
```
# mkswap /dev/sda2

Setting up swap version 1, size = 1011703 kB

no label, UUID=731c0cf53-bf25-4f91-94c5-73a2b5befeb6
```
你可以通过执行 `swap /dev/sda2` 命令立即使用此交换空间。要将此交换分区永久地添加到你的系统，请将其添加到系统的 `/etc/fstab` 文件中，如第 4 章描述所示。

# 使用 PCMCIA 卡

PCMCIA（个人电脑内存卡国际）卡是设计用于支持便携式系统中可拆卸和可插入接口的原始机制。PCMCIA 卡通常被称为 PC 卡，因为没有人能记得这个缩写代表什么（正如可选的 PCMCIA 扩展含义所暗示的：“People Can Memorize Industry acronym”）。随着 USB 的兴起，PCMCIA 卡不再像以前那样常见，但它们在许多笔记本电脑上仍然是一项功能。

对于拥有相应接口的计算机系统，有提供有线和无线接口、调制解调调器、SCSI、USB 和 FireWire 的 PCMCIA 卡。在 Ubuntu 系统的 2.6 内核上，传统的 Linux PCIA 支持已集成到热插系统中，以支持在插入 PCMCIA 卡时创建设备节点。

识别插入你系统中的 PCMCIA 卡的主要应用程序是 `pccardctl`（以前名为 `cardctl`）。然而，内核处理程序的更改可能会返回有关 PCMCIA 卡的详细信息。要查看你的系统中存在哪些卡并显示它们的摘要信息，请执行 `pccardctl` 命令。它将返回如下内容：
```
$ pccardctl indent

Socket 0:

 no product info available

Socket 1:

 product info: " LEXAR ATA FLASH CARD " STORM " TE01"

 manifid: 0x4e01, 0x0200

function: 4 (fixed disk)
```

### 第三部分：面向系统管理员的 Ubuntu 和 Kubuntu

这显示我插入了两张 PCMCIA 卡，但关于第一张卡没有可用信息。其他 `pccardctl` 命令之一提供了更多信息。例如，`pccardctl ls` 命令显示了如下：
```
$ sudo pccardctl ls

Socket 0: [yentacard] (bus ID: 0000:02:03.0)

Card bus -- 请查看 [lspci1] 获取更多信息

Socket 1: [yentacard] (bus ID: 0000:02:03.1)

Socket 1 Device: [ata_pcmia] (bus ID: 1.0)
```
这意味着我第一个 PCMCIA 插槽中的 PCMCIA 网卡被处理为 PCI 卡，而紧凑闪卡则由并行 IDE (`ata`) 子系统处理。

在大多数情况下，热插拔/udev 子系统将自动创建必要的设备节点，使用标准机制在连接新的 PCMCIA 存储设备时、出现新的 PCMCIA 接口时等情况下通知你。

# 添加 PCI 卡

PCI 卡与我在本章中讨论大多数设备完全不同，因为它们通常提供对其他设备的支持，例如扬声器（PCI 声卡）和存储设备（PCI USB、FireWire 或 SCSI 卡），或者对如调制解调器、额外的串口或端口等基础设备的支持。在添加 PCI 卡之前你的系统必须处于关机状态，并且在启动过程中发现它们并不是一个事件。内核日志中可能出现新 PCI 卡的信息是连接到它们上的设备发现，例如现代的串口、磁盘驱动器等。

尽管如此，列出系统中的 PCI 设备是有用的，以验证卡是否已被系统正确识别。执行此操作的命令是 `lspci` 命令，它的输出如下：
```
0000:00.0 RAM memory: NVIDIA Corporation C51 Host Bridge (rev a2)

0000:00.01 RAM memory: NVIDIA Corporation C51 Memory Controller 0 (rev a2)

0000:00.02 RAM memory: NVIDIA Corporation C51 Memory Controller 1 (rev a2)

0000:00.03 RAM memory: NVIDIA Corporation C51 Memory Controller 5 (rev a2)

0000:00.04 RAM memory: NVIDIA Corporation C51 Memory Controller 6 (rev a2)

0000:00.05 RAM memory: NVIDIA Corporation C51 Host Bridge (rev a2)

0000:00.06 RAM memory: NVIDIA Corporation C51 Memory Controller 3 (rev a2)
```
