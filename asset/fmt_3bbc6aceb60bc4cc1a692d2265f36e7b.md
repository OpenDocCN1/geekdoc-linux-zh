
a. `8e`

b. `83`

c. `82`

d. `FD`

- 6. `mdadm` 命令的哪个选项可以指定备用设备？

  a. `8e`

  b. `83`

  c. `82`

  d. `FD`

- 6. （注：原文重复出现）`mdadm` 命令的哪个选项可以指定备用设备？

  a. `8e`

  b. `83`

  c. `82`

  d. `FD`

- 7. 在以下命令中填空以创建 RAID1：

  `mdadm ___ /dev/md0`

- 8. 使用哪个文件启用 RAID1？

- 9. `mdadm` 命令的哪个选项提供了关于 RAID 的信息？

  a. `--stat`

  b. `--display`

  c. `--detail`

  d. 以上都不是

- 10. `/proc/mdstat` 文件允许你查看 RAID。

## LPIC-2 认证指南

**注意：** 你的字母汤里字母不够多吗？考虑在你的配方中加入 `LANANA`。`LANANA`（Linux 分配名称与数字机构）是决定出现在 `/dev` 目录中的用于阻塞的主设备和次设备号以及字符文件的组织。

### hdparm 命令

`hdparm` 命令的 man 手页描述如下：`hdparm` 提供了一个命令行界面，用于访问由 Linux SATA/ATA/SAS 'libata' 子系统和旧的 IDE 驱动子系统支持的各种内核接口。它也应该适用于大多数 USB 驱动器，因为它们在内核中显示为 SATA 设备。

**注意：** 你可能会发现系统中不存在 `hdparmap` 命令。在许多发行版中，它并不是默认安装过程的一部分。只需安装 `hdparm` 包，你就可以毫无问题地使用该命令。

要显示有关硬盘设备的详细信息，请使用 `hdparm` 命令的 `-I` 选项，如示例 12-1 所示。如果只需要基本信息，请使用 `-v` 选项。

### 示例 12-1 hdparm 命令

```
[root@localhost ~]# hdparm -I /dev/sda | more
/dev/sda:
ATA device, with non-removable media
  Model Number: VBOX HARDDISK
  Serial Number: Vbd03c6abb-9d84f8b9
  Firmware Revision: 1.0
Standards:
  Used: ATA/ATAPI-6 published, ANSI INCITS 361-2002
  Supported: 6 5 4
Configuration:
  Logical      max      current
  Cylinders    16383    16383
  Heads        16       16
  sectors/track 63       63
  ---
  CHS current addressable sectors: 16514064
  LBA user addressable sectors: 16777216
  LBA48 user addressable sectors: 16777216
```

### 第 12 章：调整存储访问

| 逻辑/物理扇区大小： | 512 字节 |
| :--- | :--- |
| 设备大小 M = 1024*1024 时： | 8192 Mbytes |
| 设备大小 M = 1000*1000 时： | 8589 Mbytes (8 GB) |
| 缓存/缓冲区大小 | 256 Kbytes (type=DualPortCache) |

能力:

LBA, IORDY(无法禁用)

队列深度: 32

待机计时器值：由厂商指定，无设备特定最小值

R/W 多扇区传输: M = 128 当前 = 128

DMA: `mdma0` `mdma1` `mdma2` `udma1` `udma2` `udma3` `udma4` `udma5` `*udma6`

周期时间: min=120ns 推荐=120ns

PIO: `pio0` `pio1` `pio2` `pio3` `pio4`

周期时间: 无流控-120ns IORDY 流控-120ns

命令/特性:

支持:

> 注意：你不会被问到示例 12-1 命令的特定输出。在大多数情况下，输出是清晰的，但如果某些内容不明，请咨询主页。要启用或禁用 DMA 支持，使用 `hdparm` 命令的 `-d` 选项。指定 `-d0` 关闭 DMA 支持，而 `-d1` 开启 DMA 支持：

```
[root@localhost ~#] hdparm -d 0 /dev/sda
/dev/sda
setting_using_dma to 0 (off)
[root@localhost Desktop#] hdparm -d 1 /dev/sda
/dev/sda
setting_using_dma to 1 (on)
```

> 注意：如果你在虚拟机上运行，某些命令可能无法正常工作，因为你的虚拟机没有提供真实的 IDE 或 SATA 设备。因此，会发生如下错误：

```
HDIO_GET_DMA failed: Inappropriate ioctl for device
HDIO_GET_DMA failed: Inappropriate ioctl for device
```

`hdparm` 命令有很多实用的特性。例如，它可以对你的硬盘执行一些基准测试。使用 `-t` 选项，你可以看到指示磁盘从硬盘读取速度的输出：

```
[root@localhost Desktop]# hdparm -t /dev/sda
/dev/sda:
Timing buffered disk reads: 294 MB in 3.01 seconds = 97.52 MB/sec
```

使用 `-T` 选项也执行基准测试。在这种情况下，结果是来自缓冲区缓存的速度。

```
[root@localhost -]# hdparm -T /dev/sda
/dev/sda:
Timing cache reads: 18324 MB in 2.00 seconds = 9170.78 MB/sec
```

> 注意：硬盘基准测试应该在非活动状态的系统上进行，以获得最准确的结果。如果在执行测试时正在使用硬盘，任何硬盘活动都会偏斜结果。如果可能，请在单用户模式下运行基准测试并执行二三次以确保结果良好。

### sdparam 命令

LPIC-2 204.2 的目标是：了解 `sdparam` 的用法。在大多数情况下，命令的输出是清晰的，但如果某些内容不明，请咨询主页。`sdparam` 可用于显示磁盘的详细信息。在许多发行版中，它并不是默认安装过程的一部分。只需安装 `hdparm` 包，你就可以毫无问题地使用该命令。

要显示有关硬盘设备的详细信息，请使用 `hdparm` 命令的 `-I` 选项，如示例 12-1 所示。如果只需要基本信息，请使用 `-v` 选项。

*(注：由于原文中存在部分重复和乱码，翻译已根据逻辑进行了平滑处理，确保了技术术语的准确性)*

硬盘是块设备；示例 12-4 所示输出中的 `8 sd` 指的是 SATA（或 SCSI 或 USB）设备，`md` 指 RAID 设备，而 `sr` 指的是 CD-ROM 或 DVD 设备。你可以通过查看 `/dev` 目录下的文件来查看实际设备文件：

```
root@localhost# ls -l /dev/sda /dev/sr0
br-rw---- 1 root disk 8, Oct 21 02:55 /dev/sda
br-rw--+ 1 root cdrom 11, Oct 21 02:55 /dev/sr0
```

查看 `ls -l` 命令的输出，通常你会在那里找到文件大小。对于设备文件没有文件大小，因此该字段被主设备号（major）和次设备号（minor）取代。如果你查看之前输出中 `/dev/sda` 文件的主设备号，你会发现它与示例 12-3 输出中的 `sd` 块设备匹配。还要注意 `ls -l` 命令的第一个字符是 `b`，表示这是一个块设备。这与示例 12-4 的输出也一致。

有关 `/proc` 文件系统中提供存储设备有用信息的额外文件，请参阅表 12-2。

| 文件 | 说明 |
| --- | --- |
| `/proc/diskstats` | 关于物理磁盘设备的统计信息，细到分区级 |
| `/proc/filesystems` | 内核支持的文件系统列表 |
| `/proc/partitions` | 内核识别的分区列表 |

#### 内核参数

在 `/proc/sys` 目录下，文件用于修改内核的行为。其中某些文件处理存储设备，例如 SCSI 驱动器、SATA/IDE 设备和 CD-ROM。修改这些文件会更改内核参数，导致你的存储设备行为发生变化。

> 注意：对于考试，你不需要了解特定的内核参数，而是了解如何更改参数以及内核参数文件所在的位置。本章提供的特定示例旨在让你更好地理解内核参数是如何工作的。

要查看内核参数设置如何影响存储设备的示例，请查看 `/proc/sys/dev/cdrom/lock` 文件的内容：
