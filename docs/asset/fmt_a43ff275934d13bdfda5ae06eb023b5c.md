
```
pvscan: listing all physical volumes
	/dev/hda7  20.00 Gi VG vg0
	/dev/hdc1  20.00 Gi VG vg0
```

`pvscan: listing all physical volumes`

`/dev/hda7  20.00 Gi VG vg0`

`/dev/hdc1  20.00 Gi VG vg0`

## 第3章：文件系统调优

```
pvscan: listing all physical volumes
	/dev/hda7  20.00 Gi VG vg0
	/dev/hdc1  20.00 Gi VG vg0
```

`pvscan: listing all physical volumes`

`/dev/hda7  20.00 Gi VG vg0`

`/dev/hdc1  20.00 Gi VG vg0`

4. 使用 `/sbin/mkfs /dev/hdc2` 创建 reiserfs 文件系统，但如果您为逻辑卷使用的是 ext2 文件系统，请改用 `/sbin/mk2fs /dev/hdc2`。

5. 使用 `/sbin/pvcreate /dev/hdc2` 使用 `/dev/hdc2` 创建一个新的物理卷。

6. 使用 `/sbin/vextend big_disk /dev/hdc2` 将分区添加到卷组。要验证磁盘分区已添加到卷组，运行 `/sbin/vgdisplay /dev/big_disk`。您应该看到如下输出：

```
--- volume group ---
Name: big_disk
  VG Status: active
  Size: 40.000
  PE: 20000 / 20000
  LV: 10000 / 10000 "vol1"
```

7. 您必须卸载使用该卷组的逻辑卷。在我的示例中，我可以运行 `umount /dev/big_disk/vol` 来卸载使用 `big_disk` 卷组的逻辑卷。

> 当您尝试卸载文件系统时遇到设备忙的错误信息，说明您正处于文件系统挂载内部，或者至少有一个用户（或程序）正在使用该文件系统。解决此类情况的最佳方法是从控制台将系统切换到单用户模式，使用 `/etc/rc.d/rc 1` 命令并离开您正尝试卸载的挂载点。

8. 增大逻辑卷的大小。如果新磁盘分区（假设）为 8GB，且你想扩展该大小的逻辑卷，请执行 `/sbin/lveend -L +8G /dev/big_disk/vol1`。你将看到如下输出：

```
lvext -- extending logical volume "dev/big_disk/vol1" to 
18 GB
lvext -- doing automatic backup of volume group "big_disk"
lvext -- logical volume "dev/big_disk/vol1" successfully extended
```

9. 逻辑卷成功扩展后，相应地调整文件系统的大小：

- 如果你使用 reiserfs 文件系统，可以运行 `/sbin/reiserfs -f /dev/big_disk/vol1`
- 如果文件系统已经挂载，运行不带 `-f` 选项的相同命令。
- 如果你使用 ext2 文件系统，可以使用以下命令调整文件系统和卷本身的大小：`/sbin/ext2fsadm -L +8G /dev/big_disk/vol1`

10. 你可以像往常一样挂载逻辑卷。

例如（如果你为磁盘使用 reiserfs 文件系统），以下命令将逻辑卷作为 reiserfs 文件系统挂载：

```
mount /dev/big_disk/vol1 /vol -t reiserfs
```

如果你使用 ext2 文件系统，请改用 `-t ext2`。

### 从卷组中移除磁盘或分区

在从逻辑卷移除磁盘之前，请备份所有文件。现在你有一个名为 `/dev/big_disk/vol1` 的卷，它由 `/dev/hda7`、`/dev/hdc1` 和 `/dev/hdc2` 组成。现在你想移除 `/dev/hda7`，因为它太慢（或者出于某种原因）。以下是操作方法。

> 每当我把一个逻辑卷缩小到更小的尺寸时，我都必须重新创建文件系统。所有数据都会丢失。教训是？始终先备份逻辑卷。

![](img/177ab5b774eeb101e12de61f8616d71a_87_0.png)

# 第一部分：系统性能

- 将物理卷 `/dev/hda7` 上的数据移动到同一卷中的另一个磁盘或分区。如果 `/dev/hdc1` 有足够的空间存放数据，你可以简单地运行 `/sbin/pmove /dev/hda7 /dev/hdc1` 命令来移动数据。如果两个地方都没有足够空间，且你想保存数据，则添加一个磁盘来替换 `/dev/hda7`。
- 使用以下命令从卷组中移除物理卷 `/dev/hda7`：`/sbin/vggrreduce big_disk /dev/hda7`
- 缩小逻辑卷 `/dev/big_disk/vol` 的大小。要减小 2GB，请先缩小文件系统：
- 如果你使用 reiserfs 文件系统，运行以下命令：`/sbin/resize_reiserfs -s -2G /dev/big_disk/vol /sbin/lvext -L -1G /dev/big_disk/vol`
- 如果逻辑逻辑卷使用 ext2 文件系统，运行以下命令：`/sbin/e2fsadm -L -2G /dev/big_disk/vol`

当 LVM 成熟并作为 Linux 下的主流磁盘管理解决方案支持时，它增加了存储可靠性，并在 Linux 最佳能力下简化了管理，使其向企业计算迈进良好。由于企业 IT 经理已经在关注 Linux，他们所需的技术可能会因为商业利益而自动获得快速通道。为企业支持 LVM 在未来将是一项业务，因此像 LVM 这样的技术将迅速成熟。处于这种技术的前沿，可以确保你的技能有很大需求。如果 LVM 尚未成为主流 Linux，请不要推迟它；它很快就将到来。

### 使用 RAID、SAN 或存储设备

任何关于存储管理的讨论，如果不谈独立磁盘冗余阵列（RAID）、存储区域网络（SAN）或现有的存储设备解决方案都是不完整的。其中许多方案涉及特定厂商的硬件，而非 Linux 特有的，因此我不会深入讨论这些问题。

### 使用 Linux 软件 RAID

我从未抽出时间使用 Linux 的软件 RAID 功能，因为软件 RAID 的某些特性让我感到困扰。我无法说服自己去尝试软件 RAID。我广泛地使用了硬件 RAID 设备，并发现它们是非常合适的解决方案。在所有将 RAID 作为解决方案的情况下，总有人愿意为硬件买单。因此，我无法将软件 RAID 作为一种经过测试的方案来推荐，其信心程度远不如硬件 RAID。

### 使用硬件 RAID

RAID 已经存在足够久，已变得非常可靠，且 Linux 存在硬件 RAID 解决方案。我喜欢的解决方案之一是 IBM 的 ServerRAID 控制器，它可以与 IBM 的外部存储设备如 EXP 15 和 EXP 200 连接。其他厂商也提供类似的解决方案。

硬件 RAID 解决方案通常使用超宽 SCSI 磁盘和 Linux 控制器。大多数 RAID 厂商现在都支持原生 Linux 驱动。

- 无论使用哪种 RAID（硬件或软件），你必须选择适合你需求的 RAID 级别。常见的 RAID 级别是 1 和 5。RAID 1 是镜像。要使用 RAID 5，至少需要三个磁盘。RAID 5 使用校验。

### 使用存储区域网络 (SAN)

存储区域网络（SAN）是连接存储设备的高速网络。它们通常用于企业环境为多个服务器提供共享存储访问。

### 使用存储设备

存储设备是提供服务的专用硬件。它们可备份、存档和其他存储任务。

### 使用内存文件系统

如果你正在为小型系统创建存储，内存中的临时文件系统可以提供高速访问。默认情况下，ramfs 可以使用的内存是系统内存的一半。如果你有 2GB 内存，ramfs 只能使用 1GB。与当今磁盘文件系统相比，即使是 2GB 的 ramfs 也小。ramfs 非常适合需要快速访问的小文件。

要使用 ramfs，必须在内核中启用支持：

1. 从 kernel.org 获取 Linux 源码，然后解压到 `/usr/src/linux-version` 目录（version 为内核版本）。这里假设为 2.4.1。
2. 选择 Files 子菜单。使用空格键选择将内存文件系统支持作为内核模块包含，并退出子菜单。
3. 确保按常选择你使用的其他功能（详见“调优内核”）。
4. 退出主菜单并保存内核配置。
5. 按照 menuconfig 程序的建议运行 `make dep` 命令。
6. 运行 `makeImage` 创建新内核。然后运行 `modules` 和 `make modules_install` 将模块安装在相应的位置。
