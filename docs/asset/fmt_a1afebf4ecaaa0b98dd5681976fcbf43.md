
[root@]# `lvextend -L +300M /dev/vg0/swap`

Size of logical volume `vg0/swap` changed from 500.00 MIB (125 extents) to 800.00 MIB (200 extents).

Logical volume `vg0/swap` successfully resized.

使用 `mswap` 命令将 LV 格式化为交换空间。

```bash
[root@]# mswap /dev/vg0/swap

mswap: /dev/vg0/swap: warning: wiping old swap signature.

Setting up swapspace version 1, size = 800 MIB (838860800 bytes)

no label, UUID=256a4d62-6180-4b1c-974e-7f4063ad660
```

使用 `swapon` 命令激活 LV 上的交换空间。

```bash
[root@]# swapon /dev/vg0/swap
```

## 减少卷组存储

减少 VG 涉及从 VG 中移除 PV。`pvmove` 命令将数据从一个 PV 上的区移动到 VG 中具有足够空间的另一个 PV 上。你可以在减少 VG 的同时继续使用 LV。使用 `pvmove` 命令在更改后自动备份 VG 的元数据。此选项使用 `vgcfbackup` 命令自动备份元数据。

```bash
[root@]# pvmove /dev/vgdb3
```

> 警告
> 在执行 `pvmove` 命令之前，请备份存储在 VG 中所有 LV 上的数据。操作期间意外断电可能会 VG 处于不一致状态，可能导致 LV 数据丢失。

使用 `vgreduce` 命令从 VG 中移除 PV。

```bash
[root@]# vgreduce vg01 /dev/vgdb3

Removed "dev/vgdb3" from volume group "vg01"
```

> 注意事项
> GFS2 和 XFS 文件系统不支持缩容，因此你无法缩小 LV 的大小。

## 移除 LVM 存储

使用 `lvremove`、`vgremove` 和 `pvremove` 命令移除不再需要的 LVM 组件。

## 准备文件系统

将必须保留的数据移动到另一个文件系统。使用 `umount` 命令卸载文件系统，然后删除 `/etc/fstab` 中该文件系统的条目。

```
[root@host ~] umount /mnt/data
```

> 警告
> 移除逻辑卷会破坏存储在逻辑卷上的任何数据。在移除逻辑卷之前，请备份或移动你的数据。

## 移除逻辑卷

使用 `lvremove` 命令移除不再需要的逻辑卷。在移除（磁盘）之前，先挂载 LV 文件系统。命令会提示确认移除。

```
[root@host ~] lvremove /dev/vg01/lv01

Do you want to remove active logical volume vg01/lv01? [y/n]: y

Logical volume "lv01" successfully removed.
```

LV 的物理区将变为释放，并可分配给卷组中现有或新的 LV。

## 移除卷组

使用 `vgremove` 命令移除不再需要的卷组。

```
[root@host ~] vgremove vg01

Volume group "vg01" successfully removed
```

VG 的物理区将变为释放，并可分配给系统上的新 VG。

## 移除物理卷

使用 `pvremove` 命令移除不再需要的物理卷。使用空格分隔的 PV 设备列表可以一次移除多个。此命令从元数据（或磁盘）中删除 LV 分区。该分区将不再可重新分配或格式化。

```
[root@host ~] pvremove /dev/vdb1 /dev/vdb2

Labels on physical volume "/dev/vdb1" successfully wiped.

Labels on physical volume "/dev/vdb2" successfully wiped.
```

## 参考
- `fdisk(8)`, `gdisk(8)`, `parted(8)`

# 第 6 章 | 管理存储栈

```
[root@servera ~]# mount /data
```

- 7. 验证已挂载的文件系统是否可访问，并显示 LVM 的状态信息。

### 7.1. 验证是否可以将文件复制到 /data 目录。

```
[root@servera ~]# cp -a /etc/*.conf /data

[root@servera ~]# ls /data | wc -l

32
```

### 7.2. 查看 PV 状态。输出显示 PV 使用了 `servera_group`。PV 大小为 256 MIB，物理区（physical extent）大小为 4 MIB。

共有 63 个 PE，其中 27 个 PE 可供分配，当前有 36 个 PE 已分配给 Lvs。按 MIB 为单位计算大时：

- 总计 252 MIB (63 PEs x 4 MIB)
- 空闲 108 MIB (27 PEs x 4 MIB)
- 已分配 144 MIB (36 PEs x 4 MIB)

```
[root@servera ~]# pvdisplay /dev/vdb2

--- Physical volume ---
PV Name /dev/vdb2
VG Name servera_group
PV Size 256.00 MIB / not usable 4.00 MIB
Allocatable yes
PE Size 4.00 MIB
Total PE 63
Free PE 27
Allocated PE 36
PV UUID FKKFY-WJIR-1jt2-sfy3-jYPy-Tyln-L62jj2
```

### 7.3. 查看 `servera_group` 的 VG 状态。输出显示 VG 大小为 508 MIB，PE 大小为 4 MIB。VG 的可用空间为 108 MIB。

```
[root@servera ~]# vgdisplay servera_group

--- Volume group ---
VG Name servera_group
System ID lvm2
Format 2
Metadata Areas 2
Metadata Sequence 2 read/write
VG Access
VG Status resizable
MAX LV 0
Cur LV 1
Open LV 1
Max PV 0
Cur PV 2
Act PV 2
```

| VG Size | 508.00 MiB |
| PE Size | 400.00 MiB |
| Total PE | 127 |
| Alloc PE / Size | 100 / 400.00 MiB |
| Free PE / Size | 27 / 108.00 MiB |
| VG UUID | g0ahhyT-90J5-1Gic-nnb5-G6T9-tLdk-dx8C9M |

### 7.4. 查看 `server_volume` LV 的信息。输出显示了所创建的逻辑卷。它还显示大小为 400 MiB，LE 大为 100。

```
[root@servera]# lvdisplay dev/server_group/server_volume

-- Logical volume --
LV Path /dev/server_group/server_volume
LV Name server_volume
VG Name server_group
VG UUID 939Fuit-eg7-B5HM-r1p5-DVZH-n5cn-j5e2tw
LV Write Access read/write
LV Creation time server.lab.example.com, 2022-04-11 03:25:12 -0400
LV Status available
# open 1
LV Size 400.00 MiB
LE Segments 2
Allocation inherit
Read sectors auto 8192
- currently set to 253:0
```

### 7.5. 以人类可读单位查看空闲空间。输出显示总大小为 395 MiB，可用大小为 372 MiB。

```
[root@servera]# df -h /data

Filesystem Size Used Avail Mounted on
/dev/mapper/server_group-server_volume 395M 24M 372M 6% /data
```
