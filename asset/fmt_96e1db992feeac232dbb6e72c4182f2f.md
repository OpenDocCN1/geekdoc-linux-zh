
A primary partition consists of a continuous range of cylinders (physical disk areas) assigned to a particular file system. If you use only primary partitions, you are limited to four partitions per hard disk (because the partition table can only hold four primary partitions).

An extended partition also consists of a continuous range of disk cylinders, but it can be subdivided into logical partitions. Logical partitions do not require entries in the main partition table. In other words, an extended partition is a container for logical partitions.

If you need more than four partitions, create an extended partition instead of a fourth primary partition. This extended partition should include the entire remaining free cylinder range. Then create multiple logical partitions within the extended partition. The maximum number of partitions is 15 on SCSI disks and 63 on (E)IDE disks.

It does not matter which type of partitions you use on Linux systems; primary and logical partitions both work well.

Table 1.1 shows the names of the Linux devices used for hard drives.

| Device | Linux Name |
|---|---|
| Primary master IDE hard disk | `/dev/hda` |
| Primary slave IDE hard disk | `/dev/hdb` |
| Secondary master IDE hard disk | `/dev/hdc` |
| Secondary slave IDE hard disk | `/dev/hdd` |
| First SCSI or SATA hard disk | `/dev/sda` |
| Second SCSI or SATA hard disk | `/dev/sdb` |

Table 1-1

Partitions follow the naming convention of the device name and partition number. For example, the first partition on the first IDE drive would be `/dev/hda1` (`/dev/hda` + 1 as the first partition). The first logical partition defined on an IDE hard disk will always be number 5. Table 1.2 shows the partition names corresponding to the device the partition is defined on.

| Partition | Linux Name |
|---|---|
| First partition on first IDE hard drive | `/dev/hda1` |
| Second partition on first IDE hard drive | `/dev/hda2` |
| First partition on third SCSI hard drive | `/dev/sdc1` |
| First logical partition on first IDE hard drive | `/dev/hda5` |
| Second logical partition on first IDE hard drive | `/dev/hda6` |

Table 1-2

For example, if you perform a new installation of SUSE Linux on a system with two IDE drives, you might want the first drive to include a partition for swap and `/`. You might want to put all logs, mail, and home directories on the second hard drive.

We need translate all.

Let's continue translation.

### 硬盘分区的基础

分区将硬盘的可用空间划分为较小的部分。这让你可以在一个硬盘上安装多个操作系统，或为程序和数据使用不同的区域。

每块硬盘（在 Intel 平台上）都有一个分区表，可容纳四个条目。分区表中的一个条目可以对应一个主分区或一个扩展分区。然而，只允许一个扩展分区条目。

一个 主分区 由分配给特定文件系统的连续柱面范围（物理磁盘区域）组成。如果你只使用主分区，则每个硬盘最多只能有四个分区（因为分区表只能容纳四个主分区）。

一个 扩展分区 也由连续的磁盘柱面范围组成，但可以细分为逻辑分区。逻辑分区 不需要在主分区表中占用条目。换句话说，扩展分区是逻辑分区的容器。

如果需要超过四个分区，请创建扩展分区而不是第四个主分区。此扩展分区应包含整个剩余的空闲柱面范围。然后在扩展分区内创建多个逻辑分区。SCSI 磁盘上的最大分区数为 15，(E)IDE 磁盘上为 63。

在 Linux 系统上使用哪种类型的分区并不重要；主分区和逻辑分区都工作良好。

表 1.1 显示了用于硬盘的 Linux 设备名称。

| 设备 | Linux 名称 |
|---|---|
| 主 IDE 硬盘主盘 | `/dev/hda` |
| 主 IDE 硬盘从盘 | `/dev/hdb` |
| 从 IDE 硬盘主盘 | `/dev/hdc` |
| 从 IDE 硬盘从盘 | `/dev/hdd` |
| 第一块 SCSI 或 SATA 硬盘 | `/dev/sda` |
| 第二块 SCSI 或 SATA 硬盘 | `/dev/sdb` |

表 1-1

分区遵循设备名称和分区号的命名约定。例如，第一块 IDE 驱动器上的第一个分区将是 `/dev/hda1`（`/dev/hda` + 1 作为第一个分区）。在 IDE 硬盘上定义的第一个逻辑分区始终为编号 5。表 1.2 显示了分区所定义设备的对应分区名称。

| 分区 | Linux 名称 |
|---|---|
| 第一块 IDE 硬盘上的第一个分区 | `/dev/hda1` |
| 第一块 IDE 硬盘上的第二个分区 | `/dev/hda2` |
| 第三块 SCSI 硬盘上的第一个分区 | `/dev/sdc1` |
| 第一块 IDE 硬盘上的第一个逻辑分区 | `/dev/hda5` |
| 第一块 IDE 硬盘上的第二个逻辑分区 | `/dev/hda6` |

表 1-2

例如，如果你在具有两块 IDE 驱动器的系统上执行 SUSE Linux 的全新安装，你可能希望第一块驱动器包含一个用于 swap 和 `/` 的分区。你可能希望将所有日志、邮件和主目录放在第二块硬盘上。

To partition the hard drive manually, you need to know the following:

- The Basics of Hard Drive Partitioning
- The Basic Linux Partitioning Scheme
- YaST’s Partitioning Proposal
- YaST Expert Partitioner
