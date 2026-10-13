
```
[user1@server2 ~]$ sudo lvdisplay /dev/rhel/root
--- Logical volume ---
LV Path             /dev/rhel/root
LV Name             rhel
VG Name             Me60Ub-wc5j-1JIC-rdX-Uitm-Njj0-Zpy0IR
LV Write Access      read/write
LV Creation time,   server1.example.com, 2019-08-22 15:03:12 -0400
LV Status           available
# open
LV Size             <8.00 GiB
Current LE           2047
Segments           inherit
Allocation         auto
Read ahead sectors set to 256
Block device        253:0
```

输出并未显示 LE 的大小；但是，你可以将 LV 大小转换为 MB（8,000），然后将结果除以当前 LE 的数量（2,047），从而可以得到 LE 的大小（该结果接近 4MB）。

## LVM 操作与命令

LVM 工具集提供了大量的管理命令，用于执行各种磁盘和卷管理操作。这些操作包括创建和删除物理卷、卷组和逻辑卷；扩展和缩小卷组和逻辑卷；重命名卷组和逻辑卷；以及列出和显示物理卷、卷组和逻辑卷的信息。

表 14-1 总结了常用的 LVM 任务以及完成这些任务的命令。

| 命令 | 描述 |
| :--- | :--- |

### 创建和删除操作

| `pvcreate`/`pvremove` | 为 LVM 使用初始化/取消初始化磁盘或分区 |
| `vgcreate`/`vgremove` | 创建/删除卷组 |
| `lvcreate`/`lvremove` | 创建/删除逻辑卷 |

### 扩展和缩小操作

| `vgextend`/`vgreduce` | 向卷组添加/删除物理卷 |
| `lvxtend`/`lvreduce` | 扩展/缩小逻辑卷的大小 |
| `lvresize` | 调整逻辑卷的大小。使用 `-r` 选项，此命令会调用 `resize2fs` 命令并同时调整底层文件系统的大小。仅适用于 Ext2/Ext3/Ext4 文件系统类型 |

### 重命名操作

| `vgrename` | 重命名卷组 |
| `lvrename` | 重命名逻辑卷 |

### 列出和显示操作

| `pvs`/`pvdisplay` | 列出/显示物理卷信息 |
| `vgs`/`vgdisplay` | 列出/显示卷组信息 |
| `lvs`/`lvdisplay` | 列出/显示逻辑卷信息 |

## 表 14-1 常用 LVM 操作与命令

所有工具都接受 `-v` 选项以支持详细输出。请参考命令的帮助页以获取用法和更多详细信息。

如前所述，`server2` 上有 7 块磁盘供练习。执行 `lsblk` 命令确认：

```
sdb      8:16 0 250M 0 disk
sdc      8:32 0 250M 0 disk
sdd      8:48 0 250M 0 disk
sde      8:64 0 250M 0 disk
sdf      8:80 0 4G 0 disk
sdg      8:96 0 1G 0 disk
sdh      8:112 0 1G 0 disk
```

你将在后续练习中使用 `sdd` 和 `sde` 磁盘进行 LVM 活动。

## 练习 14-1：创建物理卷和卷组

此练习应在 `server2` 上以 `user1` 身份执行，需要时使用 `sudo`。

在此练习中，你将初始化 `sdd` 分区（90MB）和 `sde` 磁盘（250MB）用于 LVM。你将创建一个名为 `vgbroup` 的卷组并将两个物理卷加入其中。你将使用 16MB 的 PE 大小，并列出和显示卷组及物理卷。

### 1. 使用 `parted` 命令在 `/dev/sdd` 上创建一个大小为 90MB 的分区。你需要先对磁盘进行标记，因为它是一个新磁盘。

```
[user1@server2 ~]$ sudo parted /dev/sdd mklabel mdos
[user1@server2 ~]$ sudo parted /dev/sdd mkpart primary 1 91MB
[user1@server2 ~]$ sudo parted /dev/sdd print
Model: ATA HARDDISK (scsi)
Disk /dev/sdd: (logical):512B
Partition Table: mdos
```

`print` 子命令确认了分区的创建。

### 2. 使用 `parted` 命令为分区 (1) 设置 "lvm" 标记：

```
[user1@server2 ~]$ sudo parted /dev/sdd set 1 lvm
```

### 3. 使用 `parted` 的 `print` 子命令验证标记：

| Number | Start | End | Size | Type | Flags |
|---|---|---|---|---|---|
| 1 | 1049kB | 91MB | primary | |vm |

标记应用于 Flags 列。

### 4. 使用 `pvcreate` 命令初始化 `sdd` 分区和 `sde` 磁盘。注意 `sde` 不需要使用 `parted` 标记。

```
[user1@server2 ~]$ sudo pvcreate /dev/sdd /sde -v
Wiping signatures on new PV /sdd.
Wiping signatures on new PV /sde.
Set up physical volume /sdd with 17628 sectors.
Zeroing start of sdd.
Writing physical volume data to disk "/sdd".
Physical volume "/sdd" created.
Set up physical volume /sde with 51200 sectors.
Zeroing start of sde.
Writing physical volume data to disk "/sde".
Physical volume "/sde" created.
```

该命令生成了详细输出。现在你有两个物理卷可用。

### 5. 使用 `vgcreate` 命令创建卷组 `vgbook` 并将两个物理卷加入其中。使用 `-s` 选项指定 PE 大小的 MB。

```
[user1@server2 ~]$ sudo vgcreate -s 16 vgbook /sdd1 /sde
Wiping signatures on new PV /sdd1.
Wiping signatures on new PV /sde.
Adding physical volume /sdd1 to volume group 'vgbook'.
Adding physical volume /sde to volume group 'vgbook'.
Creating volume group "vgbook" metadata (seqno 0).
Creating volume group "vgbook" (seqno 1).
Volume group "vgbook" created.
```

上述命令用单个连字符组合了选项。

### 6. 列出卷组信息：

```
[user1@server2 ~]$ sudo vgs vgbook
VG #PV #LV Attr VSize Free
vgbook 2 0 wz-- 320m 0m
```

`vgbook` 卷组的总容量为 320MB。

### 7. 显示关于卷组及其包含的物理卷的详细信息：
