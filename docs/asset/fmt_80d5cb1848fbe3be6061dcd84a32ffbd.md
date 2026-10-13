
| ID | Name |
| :--- | :--- |
| 0 | Empty |
| 1 | Hidden |
| 2 | XENIS root |
| 3 | Hidden |
| 4 | Extended |
| 5 | Extended |
| 6 | Extended |
| 7 | Extended |
| 8 | Hidden |
| 9 | Hidden |
| 10 | Hidden |
| 11 | Hidden |
| 12 | Hidden |
| 13 | Hidden |
| 14 | Hidden |
| 15 | Hidden |
| 16 | Hidden |
| 17 | Hidden |
| 18 | Hidden |

# 从硬盘启动 Linux

为了在你的系统上安装和使用 Linux，你必须执行一些磁盘操作。第 2 章解释了你在设置 Linux 时会执行的一些磁盘操作。接下来的几节提供了关于这些磁盘操作的额外信息。

当你买一台 PC 时，硬盘通常被设置为一个巨大的分区，并且已经安装了 DOS 和 Windows。（如果你是最近购买的 PC，它可能预装了 Windows 2000 或 Windows XP。）要安装 Red Hat Linux，你必须从为 Linux 创建至少三个分区开始：一个用于交换空间，一个用于 Linux 内核的 `/boot` 分区，以及一个用于 Linux 系统的 `/` 分区。

如果你想保留现有的 Windows 操作系统，就必须调整 Windows 分区的大小并为 Red Hat Linux 创建磁盘空间。安装 Red Hat Linux 时，你可以将未使用的磁盘空间用于所有的 Linux 分区。

## 创建交换空间

交换空间是 Linux 使用作为内存扩展的磁盘分区。当某些内存驻留数据不再需要时，Linux 将这些数据存储在交换空间中。要创建交换空间，你必须使用 `fdisk` 创建分区。确保你将磁盘分区类型设置为 Linux swap（十六进制分区 ID 为 82）。通常，你像 Red Hat Linux 从此书光盘那样设置交换分区并开启交换。

如果你在安装程序之外设置交换空间，则需要使用 `mkswap` 命令初始化分区。在使用 `mkswap` 命令之前，你需要知道分区的大小（以块数计算）。

## 附录 B：磁盘驱动器

例如，要将 `/dev/hda4` 初始化为交换分区，请输入以下命令：

```
/sbin/mkswap -c /dev/hda4 192772
```

在这种情况下，192772 是交换分区的块大小。你可以跳过大小参数，因为 `mkswap` 命令可以从分区表中确定大小。

交换分区的大小取决于你需要的虚拟内存数量。在 Linux 中，你 PC 上的总内存量是交换分区大小和物理 RAM 数量的总和。虽然没有公式可以告诉你需要多少虚拟内存，但按照常识，你应该拥有至少与物理内存一样大的空间。

你可以拥有一个大到 2GB 的交换分区，并且可以多达八个交换分区。你需要做的就是为你创建的每个交换分区运行 `mkswap` 命令。

在 `mkswap` 完成后，使用 `/sbin/swapon` 命令开启交换。Linux 开始使用交换空间。

`/proc/swaps` 包含了你的 Linux 系统正在使用的交换空间信息。例如，以下是我检查系统上的 `/proc/swaps` 时得到的结果：

```
cat /proc/swaps
Filename      Type      Size  Used Priority
/dev/hda3     partition  192772 59528  -1
```

输出显示了当前的交换空间。虽然通常使用磁盘分区作为交换空间，但你也可以使用文件作为交换空间。交换空间列表的第一列标记为 `Filename`，这是因为你想使用文件作为交换空间，可以使用如下下面的命令创建该文件：

```
dd if=/dev/zero of=swapfile bs=1024 count=131072
```

这会创建一个一个大小为 131,072 的命名交换文件。输入 `/sbin/mkswap -c swapfile` 来初始化它并将该文件用于交换。

为了确保 Linux 每次启动时使用交换空间，你需要在 `/etc/fstab` 中包含一行指定交换分区的名称。例如，如果交换分区是 `/dev/hda3`，请向 `/etc/fstab` 添加以下行：

```
/dev/hda3      swap      defaults      0 0
```

如果你在安装 Linux 时创建了交换空间，安装程序会在 `/etc/fstab` 文件中添加相应的行。如果你以后创建了额外的交换空间，可能需要手动添加此类行。

如果你在 `/etc/fstab` 中放入了分区名称，但忘记在该分区上运行 `mkswap`，Linux 将显示以下错误消息：

```
Unable to find swap-space signature
```

修复方法是运行 `mkswap` 来初始化交换分区。

### 创建文件系统

在 Linux 中使用磁盘分区时，你必须在分区上创建一个文件系统。你可以将其理解为为 Linux 对分区进行格式化。当你按照第 2 章中描述的步骤安装 Linux 时，其中一个步骤会创建文件系统；设置程序会询问你是否想要格式化分区。对于 Linux 分区，设置程序使用 `mk2fs` 命令来创建 Linux 文件系统。

Linux 支持多种类型的文件系统，包括以下类型：

- *MS-DOS 文件系统*——这种 DOS 文件系统基于分配表（FAT）。这种文件系统类型由关键字 `msdos` 指定。
- *支持长文件名的 Microsoft Windows 文件系统*——这是一个支持长文件名的 DOS 兼容文件系统。该文件类型由关键字 `vfat` 识别。你应该使用此文件系统从 Linux 访问所有 DOS/Windows 磁盘。
- *Minix 文件系统*——Minix 是启发了 Linux 创建的原始 UNIX 克隆系统。Linux 从使用 Minix 文件系统开始，它将文件名限制在 14 或 30 个字符。`minix` 识别这种文件系统类型。
- *扩展文件系统*——这种旧的 Linux 文件系统由关键字 `ext` 指定。你不应再使用这种文件系统。
- *第二个扩展文件系统*——这是最新且最好的 Linux 文件系统。关键字 `ext2` 指这种文件系统类型。你可以在此文件系统更长的文件名。
- *第三个扩展文件系统*——这是 `ext2` 文件系统的增强版，带有日志功能以便在发生错误时快速恢复。关键字 `ext3` 指这种文件系统类型。Red Hat 安装程序会自动在 Linux 分区上创建 ext3 文件系统。要手动创建 ext3 文件系统，需要如下使用 `mk2fs` 命令：

```
/sbin/mk2fs -j /dev/hda3
```

该命令在 `/dev/hda3` 分区上创建 ext3 文件系统。`mk2fs` 命令会自动识别分区大小并使用它。`-c` 选项强制 `mk2fs` 在创建文件系统之前检查坏块（使用只读测试）。当你在使用标准 IDE、MFM 或 RLL 控制器的硬盘上安装 Linux 时，务必安装 ext3 文件系统。

### SCSI 磁盘控制器和 Linux

SCSI（读作 "scuzzy"）是一种日益流行的接口，用于连接多达七个不同设备到 SCSI 总线。每个设备和 SCSI 控制器都有唯一的 SCSI 标识符 (ID)。控制器通常设置为 SCSI 7；如有，可以使用 `/sbin/modprobe modname` 命令手动加载你的 SCSI 控制器驱动，其中 `modname` 指驱动名称。表 B-1：支持的 SCSI 控制器

| SCSI 控制器 | Linux 驱动模块 |
| :--- | :--- |
| 3ware 存储控制器 | 3wxxx |
| ACARD ATP870U | atp870u |
| Adapptec AHA-1460 (AHA152 兼容) | aha152_cs |
| Adapptec AHA-1510/152 (ISA) | aha152 |
| Adapptec AHA-154x (ISA) (所有型号) | aha152 |
| Adapptec AHA-174x (EISA) (增强模式) | aha174 |
| Adapptec AHA-274/274 (EISA) | aha274 |
| Adapptec AHA-284 (VLB) | aha284 |
| Adapptec AHA-2910 (PCI) | aha2910 |
| Adapptec AHA-2930/U/CU (PCI) | aha2930 |
| Adapptec AHA-2940/U/AW/UCU (PCI) | aha2940 |
| Adapptec AHA-2944/WD/UD/IW | aha2944 |
| Adapptec AHA-2950/U2W/U2B | aha2950 |
| Adapptec AHA-3916M | aha3916M |
