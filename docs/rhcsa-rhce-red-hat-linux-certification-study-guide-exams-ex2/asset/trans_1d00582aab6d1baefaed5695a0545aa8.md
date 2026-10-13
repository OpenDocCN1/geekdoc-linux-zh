
调整大小通常与逻辑卷相关联的过程。有关更多信息，请参阅本章后面关于 resize2fs 命令的说明。

## 使用 parted：简要说明

在 parted 命令行提示符下，首先使用打印分区表命令。这可以让你查看分区表中的当前条目，前提是分区表存在。假设有足够的可用空间，你就可以新建一个（mkpart）分区，甚至可以创建并格式化文件系统（mkpartfs）。有关 parted 命令选项的更多信息，请使用 help 命令；例如，以下命令（加粗）提供了有关 mkpart 的更多信息：

```
(parted) help mkpart
    mkpart PART-TYPE [FS-TYPE] START END      make a partition
    
    PART-TYPE is one of: primary, logical, extended
    FS-TYPE is one of: ext3, ext2, fat32, fat16, hfsx,
    hfs+, hfs, jfs, linux-swap, ntfs, reiserfs, hp-ufs,
    sun-ufs, xfs, apfs2, apfs1, asfs, amufs5, amufs4,
    amufs3, amufs2, amufs1, amufs0, amufs, affs7, affs6,
    affs5, affs4, affs3, affs2, affs1, affs0
    START and END are disk locations, such as 4GB or 10%.
    Negative values count from the end of the disk.
    For example, -1s specifies exactly the last sector.
    
    mkpart makes a partition without creating a new
    file system on the partition.
    FS-TYPE may be specified to set an appropriate
    partition ID.
```

如果信息太多，直接运行命令即可。你将被提示输入必要的信息。请记住，驱动器最多可包含四个主分区，对应编号 1 至 4。其中一个主分区可以重新设计为扩展分区。剩余的分区是逻辑分区，编号为 5 及以上。

## 使用 parted：全新 PC（或硬盘）且无分区

对于任何真正全新的硬盘，第一步是创建新的分区表。例如，在我向虚拟 RHEL 系统添加新硬盘后，在 parted 中运行的几乎任何命令都会导致以下消息：

```
Error: /dev/sdb - unrecognised disk label.
```

在对该驱动器进行任何其他操作之前，我需要创建标签。如可用命令列表所示，我可以使用 mklabel 命令来完成。听起来可能很奇怪，但 Linux 使用的默认标签是 msdos；以下是我的操作命令：

```
(parted) mklabel
New disk label type? msdos
```

## 使用 parted：创建新分区

现在你可以在 parted 中使用 mkpart 命令创建新分区。当然，如果已存在扩展分区，则唯一可用的类型将是逻辑分区。

```
(parted) mkpart
Partition type? primary/extended? primary
File system type? [ext2]? ext4
Start? 1MB
End? 500MB
```

对于 parted，我使用 1MB，因为必须为 MBR 预留一些空间。虽然 MBR 只需要 512 字节，但 1MB 的条目可以避免错误消息。现在使用 print 命令查看结果：

```
(parted) print

Disk /dev/sdb: 10.7GB Sector size (logical/physical): 512B/512B
Partition Table: msdos
```

| 编号 | 起始 | 结束 | 大小 | 类型 | 文件系统 | 标志 |
|---|---|---|---|---|---|---|
| 1 | 1049kB | 500MB | 499MB | primary | ext4 | |

如果这是你创建的第一个分区，文件系统类型将为空。不幸的是，parted 并不能完美工作，即使你已设置 ext4 标签，仍需使用本章后面讨论的 mkfs.ext4 命令对其进行格式化。但只要没有错误，分区表已经写入磁盘。但就本章目的而言，暂时不要退出 parted。

![](img/9139201cfcaf4292284a0eed074928e5_339_0.png)

> GUI 版的 parted 工具（GParted、QTParted）确实支持格式化为更广泛的文件系统格式，尽管它们只是 parted 的“前端”。它们可能可在第 7 章所述的第三方存储库中找到。

## 使用 parted：删除分区

在 parted 中删除分区很容易。从 (parted) 提示符处，你只需使用 rm 命令按编号删除目标分区。当然，在删除任何分区之前，你应该：
- 从该分区保存所需的数据。
- 卸载该分区。
- 确保它未在 /etc/fstab 中配置，这样 Linux 在下次启动时不会尝试挂载它。
- 启动 parted 后，运行 print 命令以识别要删除的分区及其 ID 号。

例如，要从 (parted) 提示符删除分区 /dev/sdb10，请运行以下命令：

```
(parted) rm 10
```

## 使用 parted：创建交换分区

现在让我们重复该过程来创建交换分区。如有必要，删除之前创建的分区以腾出空间。使新分区的起始位置在前一个分区结束位置之后 1MB。你仍可使用相同的命令，只需将文件系统类型替换为 linux-swap 即可：

```
(parted) mkpart
Partition type? primary/extended? primary
File system type? [ext2]? linux-swap
Start? 501MB
End? 1000MB
```

现在使用 print 命令查看结果：

```
(parted) print
Model: ATA QEMU HARDDISK (scsi)
Disk /dev/sdb: 1049MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
```

| 编号 | 起始 | 结束 | 大小 | 类型 | 文件系统 | 标志 |
|---|---|---|---|---|---|---|
| 1 | 1049KB | 500MB | 499MB | primary | ext4 | |
| 2 | 501MB | 1000MB | 500MB | primary | | |

现在退出 parted。实施这些更改需要额外的工作。以下命令 mkswap、swapon 和 mkfs.ext4 将在本章后面介绍。

```
(parted) quit

# mkswap /dev/sdb2
# swapon /dev/sdb2
```

现在你可以使用以下命令格式化新的常规 Linux 分区：

```
# mkfs.ext4 /dev/sdb1
```

## 使用 parted：设置不同分区类型

当在 parted 中创建分区时，你可以使用 set 命令重置其用途。如果这些分区仍在该第二硬盘（或任何其他具有未使用分区的现有硬盘）上可用，请使用 parted 命令打开它。例如，以下命令打开该第二硬盘：

```
# parted /dev/sdb
```

运行 print 命令。现有分区的标志列应为空。现在你将使用 set 命令设置该标志。从这里显示的命令来看，标志被设置为将第二驱动器的第一个分区用作 LVM 分区：

```
(parted) set
Partition number? 1
Flag to invert? lvm
New state? [on/off] on
```

现在使用 print 命令查看结果：

```
(parted) print
Model: ATA QEMU HARDDISK (scsi)
Disk /dev/sdb: 1049MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
```

| 编号 | 起始 | 结束 | 大小 | 类型 | 文件系统 | 标志 |
|---|---|---|---|---|---|---|
| 1 | 1049kB | 500MB | 499MB | primary | ext4 | lvm |

类似的步骤也可用于配置分区或 RAID 阵列的组件。它也是一个标志；只需在刚才显示的“Flag to Invert”提示中将 lvm 替换为 raid 即可。如果你正在 RHEL 6 系统上跟随操作，请先确认结果。退出 parted，并运行以下命令：

```
# parted /dev/sdb print
# fdisk -l /dev/sdb
```

你将看到如 parted 命令之前所示的 lvm 标志；在 fdisk 命令的输出中，你将看到以下确认信息：

| 设备 | 启动 | 起始 | 结束 | 块 | Id | 系统 |
|---|---|---|---|---|---|---|
| /dev/sda1 |  | 1 | 263 | 487424 | fd | Linux LVM |

如果你已设置第 2 章所述的基础虚拟系统，这是一个很好的机会将分区设置为 LVM 卷的组件。现在你已拥有工具，使用 fdisk 还是 parted 并不重要。你可以选择使用所有可用空间。只需确保为此目的在多个硬盘上创建分区，以帮助说明逻辑卷的强大功能。

## 图形化选项

如前所述，磁盘分区有出色的图形前端可用。GParted 和 QtParted 选项基于 parted，分别设计用于 GNOME 和 KDE 桌面环境。由于它们无法从 Red Hat Network 获取，因此不受 Red Hat 支持，因此不会出现在任何 Red Hat 考试中。

RHEL 6 可用的一个图形化选项仅称为磁盘实用程序，可从 gnome-disk-utility 软件包获取。安装适当的软件包后，你可以使用 palimpsest 命令从命令行界面打开磁盘实用程序。

图 6-3 所示的磁盘实用程序屏幕显示了一个远非完美的应用程序。该屏幕描绘了第 2 章创建的基础虚拟机；它将虚拟硬盘设备 /dev/vda 列为外围硬盘。幸运的是，这只是一个微不足道的错误；该工具的功能不受影响。它仍然是一个非常强大的工具，可以以多种方式组织你的驱动器或销毁所有数据。

功能包括以下可点击选项：
- Format Drive 支持对整个驱动器的更改。
- Benchmark 允许测量读写性能。
