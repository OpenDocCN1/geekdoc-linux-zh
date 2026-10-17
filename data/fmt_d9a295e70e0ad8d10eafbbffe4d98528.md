
如果你仍然无法启动，应该参考 `LILO` man 页并检查互联网上 `LILO-HOWTO` 文件的更新。

## RAID 配置

Linux RAID 最近进展很大。现在有许多硬件 RAID 产品支持 Linux，特别是那些大品牌 PC 制造商。专用的 RAID 硬件无疑是最佳解决方案。替代方案是使用基于软件的 RAID 服务。Linux 提供了一个 RAID 软件 RPM，你可以用它来配置多个磁盘分区显示为一个分区。

共有六种 RAID 级别，代表冗余的不同排列，但在 Linux 软件中仅实现了三种：级别 0、1 和 5，以及一种被称为 Linear（线性）的模式。

本文假设你已经对 RAID 级别之间的差异有所了解，表 5-1 提供了快速概述。

`RAID0` 和 `RAID1` 都需要两个或多个驱动器，而 `RAID5` 需要三个或更多驱动器。

你可以在 RAID 集中分配额外的磁盘作为备用磁盘（spare disks）。当一个磁盘故障时，它会被标记为损坏，数据会在第一个备用磁盘上重建，该磁盘将用作替换，从而导致极少或没有停机时间。下一个示例演示了 `RAID1` 和 5。假设你的服务器有四个驱动器，操作系统加载在第一个上，它看起来应该像这样：

| 分区 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| hda | / | swap | /home | /var |
| hdb | | | | |
| hdc | | | | |
| hdd | | | | |

### RAID 配置 249

| TABLE 5-1 RAID 级别 | 说明 |
|---|---|
| RAID Level 0: 分带 (Striping) | 主要用于提高磁盘访问速度，但没有容余能力。成本因素最佳；每个字节可用。 |
| RAID Level 1: 镜像 (Mirroring) | 在另一个磁盘上保留分区的完整副本。提供良好的单盘容余；具有最佳读取性能；需要两个更多磁盘。成本因素较差。 |
| RAID Level 5: 数据和校验分带 (Data and Parity Striping) | 所有数据和校验位分布在所有磁盘上。使用本地 CPU，可以使用校验信息从任何单个故障磁盘重建信息。这种方法允许良好的容余能力以及潜在的读取和性能改进。这种设置需要 3 到 32 个分区/驱动器。((n-1)/n)*100%。 |

这不包括三个相对分离的驱动器 (`hda`, `hdc`, `hdb`)。下一个示例演示了 `RAID1` 和 5。假设你的服务器有四个驱动器，操作系统加载在第一个上，它看起来应该像这样：

| 分区 | 1 | 2 | 3 | 4 |
|---|---|---|---|---|
| hda | / | swap | /home | /var |
| hdb | | | | |
| hdc | | | | |
| hdd | | | | |

（注：第 288-290 页的 OCR 文本包含大量循环和错误。我已根据要求处理了清晰的部分。）

### RAID 配置 251

我们现在必须初始化 `md0` 和 `md1` 设备。要做到这一点，运行 `mkraid /md0; mkraid /md1`。`/proc/mdstat` 文件将显示你的 RAID 配置状态。你现在可以挂载设备、对其进行格式化并继续你的项目。为了将 RAID5 配置在 `/var` 分区上（为了保留邮件等），`/etc/raidtab` 应该修改如下：

```
raiddev /dev/md0

raid-level 5

nr-raid-disks 3

nr-spare-disks 1

persistent-superblock 1

chunksize 32

parity-algorithm symmetric

device /dev/hda

raid-disk 0

device /dev/hdb

raid-disk 1

device /hdc

raid-disk 2

device /hdd

spare-disk 0
```

再次运行 `mkraid /dev/md0` 以初始化 RAID5。

## 格式化 RAID 分区

在运行 `mke2fs` 格式化设备之前，你应该理解如何使用特殊的 `mke2fs` 选项。例如，如果块大小为 32KB，你应该每块使用 64 个块来连续写入 32KB。如果你使用 4K 块，则每块使用 8 个块。如果你在格式化 RAID5 时相对于写入操作指定块大小，你会看到性能的显著提高。对于后一个示例，输入：

```
mke2fs -b 4096 -R stride=8 /dev/md0
```

为了让自动检测正常工作，你需要将分区设置为 0xFD，如之前所述。你还必须在内核中开启自动检测。

## 第 252 第 5 章：高级安装

你将需要使用 `persistent-superblock` 选项。如果一切正常，当内核启动时，它会自动检测 RAID 并修复启动过程中因崩溃导致的任何错误。

具有 RAID 级别的根设备要稍微复杂一些。你可能对此兴趣手动将根分区的内容复制到其他设备。这样做之后，你应该使用 `LILO` 将内核写入这些驱动器的根设备。这将允许你的根设备在故障时有一个静态副本，以防发生故障。实现真正的根 RAID 是可能的，但这超出了本文的范围。更多信息请参阅 `Root-RAID-HOWTO` 文档获取详细说明。

## 练习 5-2

### 使用软件 RAID 镜像 /home 分区

假设存在以下双硬盘分区方案：

| 驱动器 1 | | |
| :--- | :--- | :--- |
| hda1 | 256 | / |
| hda2 | 64 | swap |
| hda3 | 500 | /home |
| hda4 | 256 | /var |

| 驱动器 2 | | |
| :--- | :--- | :--- |
| hdb1 | 1200 | /usr |
| hdb2 | 64 | swap |
| hdb3 | 100 | /tmp |
| hdb4 | 500 | (未分配) |

现在你将为 `hda3` 创建到 `hdb4` 分区的镜像（它们的精确大小应该接近，但不需要完全相同）。

> 警告：如果这是一个正在运行的系统，你在此继续之前需要先备份 `/home` 分区。否则，当前 `/dev/hda3` 上的所有数据将会丢失。

1. 在 Linux 中使用 `fdisk` 工具将两个分区 ID 标记为 0FD。

```
[root]# fdisk /dev/hda

Command (m for help) : t

Partition (1-4)

3

Partition ID (L to list options): FD

Command (m for help) : w

Command (m for help) : q
# fdisk /dev/hdb
```

```
Command (m for help) : t
Partition number (1-4)
4
Partition ID (L to list options): FD
Command (m for help) : w
Command (m for help) : q
```

使用这些代码行更新配置文件 `/etc/raidtab`：

```
[root]# vi /etc/raidtab

raiddev /dev/md0

raid-level 1

n-raid-disks 2

n-spare-disks 0

persistent-superblock 1

chunk-size 4

device /dev/hda3

raid-disk 0

device /dev/hdb4

raid-disk 1
```

3. 现在创建 RAID 设备文件 `md0` 并按此方式格式化它：

```
[root]# mkraid /dev/md0

[root]# mke2fs -b 4096 -R stride=8 /dev/md0
```
