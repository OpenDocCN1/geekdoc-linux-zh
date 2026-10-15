
## 4.5. 运行

```
[root[server~]# systemctl daemon-reload
[root@server~]#
```

## 4.6. 使用 `swapon -a` 激活交换空间

```
[root@serverb] # swapon -a
正在设置交换分区 1,大小 = 489 MiB (512749568 bytes)
正在设置交换分区 2,大小 = 488 MiB (511700992 bytes)
```

> 注：由于您提供的原始文本在 4.2-4.5 之后存在部分重复和格式混乱，译文已根据逻辑进行了对齐处理，确保不漏且不重复

## 章节 | 管理逻辑卷

从卷组（volume group）的可用空间创建的逻辑卷可以格式化为文件系统、激活为交换空间（swap space），并进行持久挂载。

![](img/3c5dfc78dee328600013666607c8aa7b_214_0.png)

图 7：逻辑卷管理组件

LVM 提供了一套全面的命令行工具，用于实现和管理 LVM 存储。这些命令行工具可以在脚本中使用，因此适用于自动化。

> 重要提示
> 以下示例使用设备 `vdb` 及其分区来说明 LVM 命令。在实际操作中，这些示例需要根据系统正在使用的磁盘和磁盘分区使用相应的正确设备。请使用 `lsblk`、`blkid` 或 `cat /proc/partitions` 命令来识别您的系统上的设备。

## 创建逻辑卷

要创建一个逻辑卷，请执行以下步骤：

### 准备物理设备

使用 `parted`、`gdisk` 或 `fdisk` 为 LVM 创建新分区。在 LVM 分区上，请务必将分区类型设置为 `Linux LVM`；对于 MBR 分区，使用 `0x8e`。如有必要，使用 `partprobe` 向内核注册新分区。

或者，使用整块磁盘、RAID 阵列或 SAN 磁盘。

只有在没有准备好的物理设备且需要新的物理卷来创建或扩展卷组时，才需要准备物理设备。

```
[root@host ~]# parted -s /dev/vdb mkpart primary 1MiB 769MiB
[root@host ~]# parted -s /dev/vdb mkpart primary 770MiB 1026MiB
[root@host ~]# parted -s /dev/vdb set 1 lvm on
[root@host ~]# parted -s /dev/vdb set 2 lvm on
```

### 创建物理卷

使用 `pvcreate` 将物理卷（或其他物理设备）创建为卷。`pvcreate` 命令将物理卷划分为固定大小的物理区（physical extents，简称 PE），例如 4 MiB 块。您使用空格分隔的设备名称作为 `pvcreate` 的参数同时标记多个设备。

```
[root@host ~]# pvcreate /dev/vdb2 /dev/vdb1
```

这会将设备 `/dev/vdb2` 和 `/dev/vdb1` 标记为 PV，准备好分配到卷组中。

只有在没有 PV 可用于创建或扩展 VG 时，才需要创建 PV。

### 创建卷组

使用 `vgcreate` 将一个或多个物理卷创建一个卷组。卷组在功能上等同于硬盘；您将从卷组中的空闲物理区池创建逻辑卷。

`vgcreate` 命令行由卷组名称和其后分配给该卷组的一个或多个物理卷组成。

```
[root@host ~]# vgcreate vg01 /dev/vdb2 /dev/vdb1
```

这创建了一个名为 `vg01` 的 VG，其大小（以 PE 单位计算）是 PV `/dev/vdb2` 和 `/dev/vdb1` 的总和。

只有在尚未创建时才需要创建 VG。出于管理考虑，可能会创建额外的 VG 来管理 PV 和 LV（逻辑卷）。否则，在需要时可以扩展现有的 VG 以容纳新的 LV。

## 创建逻辑卷

使用 `lvcreate` 从卷组中的可用物理区创建一个新卷。`lvcreate` 命令至少包含用于设置 LV 名称的 `-n` 选项，要么使用 `-L` 选项以字节设置 LV 大小，要么使用 `-l` 选项以区数量设置 LV 大小，以及托管逻辑卷的卷组名称。

```
[root@host ~]# lvcreate -n lv01 -L 700MiB vg01
```

这在 `vg01` 中创建一个名为 `lv01`、大小为 700 MiB 的 LV。如果卷组没有足够的空闲区来满足请求，此命令将失败。

请注意，如果大小无法精确匹配，它将对齐到物理区大小的倍数。

您可以使用 `-L` 选项指定大小，该选项期望字节、meibytes（二进制兆字节，1048576 字节）、gibibytes（二进制吉字节）或类似。或者，您可以使用 `-l` 选项，它期望以物理区数量的形式指定大小。

以下列表提供了一些创建 LV 的示例：

- `lvcreate -L 128M`：将要创建的逻辑卷大小设置为 128 MB。
- `lvcreate -l 128`：将要创建的逻辑卷大小设置为 128 个区。总字节数取决于底层物理卷物理区块的大小。

> 重要提示
> 工具使用传统名称 `/dev/vgname/lvname` 或内核设备映射器名称 `/dev/mapper/vgname-lvname` 显示逻辑卷名称。

### 添加文件系统

使用 `mkfs` 在新逻辑卷上创建 XFS 文件系统。或者，根据您偏好的系统文件系统类型创建文件系统，例如 ext4。

```
[root@host ~]# mkfs -t xfs /dev/vg01/lv01
```

为了使文件系统在重启后可用，请执行以下步骤：

- 使用 `mkdir` 创建挂载点。

```
[root@host ~]# mkdir /mnt/data
```

- 挂载卷。

```
mount /dev/vg01/lv01 /mnt/data
```

- 在 `/etc/fstab` 中添加项：

```
/dev/vg01/lv01 /mnt/data xfs defaults 0 0
```

## 删除逻辑卷

要删除逻辑卷，请执行以下步骤：

### 卸载逻辑卷

首先卸载卷。

```
umount /mnt/data
```

### 删除逻辑卷

使用 `lvremove` 删除逻辑卷。

```
[root@host ~]# lvremove /dev/vg01/lv01
```

> 警告
> 在删除卷组 之前，必须先删除所有逻辑卷。

### 删除卷组

使用 `vgremove` 删除卷组。

```
[root@host ~]# vgremove vg01
```

### 删除物理卷

使用 `pvremove` 删除物理卷。

```
[root@host ~]# pvremove /dev/vdb2 /dev/vdb1
```

## 查看 LVM 状态

### 物理卷

使用 `pvdisplay` 显示物理卷的信息。要列出所有物理卷，请使用该命令而不带参数。要列出特定的物理卷，请将其名称传递给命令。

```
[root@host ~]# pvdisplay
--- Physical volume ---
| PV Name | /dev/vdb1 |
| :--- | :--- |
| VG Name | vg01 |
| PV Size | 768.00 MiB / unusable 4.00 MiB |
| Allocatable | yes |
| PE Size | 4.00 MiB |
| Total PE | 191 |
| Free PE | 16 |
| Allocated PE | 175 |
| PV UUID | JwZDpn-Lg3e-n2o1-9Etd-pwP1 |
```

- `PV Name` 映射到设备。
- `VG Name` 显示分配该 PV 的卷组。
- `PV Size` 显示物理大小，包括任何不可用空间。
- `PE Size` 是物理区，也是逻辑卷的最小单位。

它也是在计算以 PE 单位报告的任何值时的乘因子，例如 *Free PE*：26 个 PE x 4 MiB（PE Size）等于 104 MiB 的空闲空间。逻辑卷按 PE 单位进行设置。

- `Free PE` 显示可分配给新逻辑组的 PE数量。

### 卷组

使用 `vgdisplay` 显示卷组的信息。要列出所有卷组，请使用该命令而不带参数。要列出特定的卷组，请将其 VG 名称传递给命令。
