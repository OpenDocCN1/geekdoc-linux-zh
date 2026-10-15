
扩展逻辑卷 `web1` 到 110.00 GB
逻辑卷 `web1` 调整调整大小

`lvchange` 命令用于在之后停用并重新激活它。这部分之所以需要是因为在我们之前的示例中 `web1` 已经存在一个快照。在调整大小操作后，快照

## HP-UX 逻辑卷管理

将“看到”额外的 10GB 分配空间，但由于文件系统的大小只有 100GB，快照仍然可用。

我们现在可以使用 `resize2fs` 调整文件大小。(`2` 来自原始的 `ext2` 文件系统，该命令支持所有版本的 ext。) 由于 `resize2fs` 可以从卷中确定新文件系统的大小，因此不需要显式地指定新大小。在缩小文件系统时，我们才需要进行指定。

```
$ sudo resize2fs /dev/DEMO/web1
```

`resize2fs 1.41.9 (22-Aug-2009)`

`Please run e2fsck -f /dev/DEMO/web1 first.`

哎！`resize2fs` 强制你双检文件系统调整的一致性。

```
$ sudo efsck -f /dev/DEMO/web1
```

`e2fsck 1.41.9 (22-Aug-2009)`

`Pass 1: Checking inodes, blocks, and sizes`

`/dev/DEMO/web1: 6432/653600 blocks (0.1% non-contiguous), 473045/2621400 blocks`

```
$ sudo resize2fs /dev/DEMO/web1
```

`resize2fs 1.41.9 (22-Aug-2009)`

`Resizing the output of /dev/DEMO/web1 (4k) blocks.`

`The filesystem on /dev/DEMO/web1 is now 28835840 blocks long.`

搞定！再次检查 `df` 的输出可以看到变化：

```
$ sudo mount /dev/DEMO/web1 /mnt/web1
$ df -h /mnt/web1
```

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/mapper/DEMO-web | 1109G | 188M | 103G | 1% | /mnt/web1 |

## HP-UX 逻辑卷管理

![](img/9b33263d3e7e36cd43da7756018c8735_299_0.png)

从 HP-UX 10.20 开始，HP 提供了一个完整的逻辑卷管理器，特别是考虑到 HP-UX 以前并不支持分区的概念。卷管理器是 LVM，就像 Linux 上的一样，尽管 HP-UX 版本是原始的。（实际上，它是 Veritas 软件……）

作为一个 LVM 操作的简单示例，这里是配置一个 75GB 硬盘供逻辑卷管理器使用的方法。如果你读过 Linux 示例，接下面的步骤将看起来很熟悉。虽然有一些不同之处，但整体过程本质上是相同的。

`pvcreate` 命令识别物理卷。

```
$ sudo pvcreate /dev/rddisk/disk4
Creating "/dev/rddisk/disk4"
Physical volume "/dev/rddisk/disk4" has been successfully created.
```

如果你将该磁盘作为启动盘，请向 `pvcreate` 添加 `-B` 选项以为启动块预留空间，然后运行 `mkboot` 来安装它。

## 第8 章 存储

将磁盘定义为物理卷后，你使用 `vgcreate` 命令将其添加到新的卷组。卷组存在两种元数据格式：版本 1.0 和 2.0。在创建卷组时，通过 `-V` 选项指定你想要的版本；版本 1.0 仍是默认值。2.0 有更大的限制，但它不能用于启动设备或交换卷。即使是版本 1.0 元数据也有宽松的限制，对于大多数用途来说足够。你可以通过 `lvmadm` 查看确的限制。作为参考，这里是 1.0 的限制：

```
$ sudo lvmadm -t -V 1.0
--- LVM Limits ---
VG Version 1.0
Max VG Size (Tbytes) 510
Max LV Size (Tbytes) 16
Max PV Size (Tbytes) 2
Max VGs 256
Max LVs 255
Max PVs 255
Max Mirrors 2
Max Stripes 255
Max Stripe Size (Kbytes) 32768
Max LXs per PV 65535
Max Xs per PV 65535
Max Extent Size (Mbytes) 256
```

你可以使用 `vgxtend` 向卷组添加额外的磁盘，但此示例卷组仅包含单个磁盘。

```
$ sudo vgcreate vg01 /dev/disk/disk4
Increased the number of physical extents per volume to 17501.
Volume group "dev/vg01" has been successfully created.
Volume configuration for /dev/vg01 has been saved in
/etc/lvmconf/vg01.con
```

一旦将磁盘添加到方便的卷组，就可以将卷组的磁盘池拆回逻辑卷。`lvcreate` 命令创建新的逻辑卷。使用 `-L` 标志以兆字节为单位指定大小，或使用 `-l` 标志以逻辑区（通常为 4MiB）为单位指定。以 MiB 为单位的大小会向上取整到逻辑区的倍数。

通过运行 `vgdisplay vgname` 可以评估卷组中的空闲空间量。

```
$ sudo lvcreate -L 25000 -n web1 vg01
Logical volume "dev/vg01/web1" has been successfully created.
Logical volume "vg01" has been extended.
Volume Group configuration for vg01 has been saved in /etc/lvmconf/vg01.conf
```

## AIX 逻辑卷管理

上述命令创建一个名为 `web1` 的 25GB 逻辑卷。一旦你创建了逻辑卷，可以通过运行 `vgdisplay vgname` 来验证它们的大小并确保它们已设置好。在许多情况下，你会在 `/dev/vg01/web1` 上创建文件系统并安排其在启动时挂载。详情见第 25 页。

创建逻辑卷的另一种常用方法是使用 `lvcreate` 创建零长度卷，然后使用 `lvextend` 添加存储空间。你可以精确指定卷组中的哪些卷应该是逻辑的。如果使用 `lvcreate` 分配空间，它将使用任何可用物理卷的区。与 Linux 不同，条带（HP-UX LVM 称为“分布式分配”）和镜像是逻辑层面的功能。你可以在使用 `lvcreate` 创建逻辑卷时或稍后通过 `lvchange` 请求它们。与 Linux 不同，逻辑卷管理器不支持快照。然而，临时快照是 VxFS 的一项功能。如果你计划使用逻辑卷作为启动或交换设备，必须在 `lvcreate` 时指定连续分配和 `-C` 标志，如下所示。
