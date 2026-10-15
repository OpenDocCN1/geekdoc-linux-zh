
# lvdisplay

```
# lvdisplay
--- Logical volume ---
LV Path /dev/rhel/swap
LV Name swap
VG Name rhel
LV UUID RckIC8-T5Or-vZF9-Er1e-IqW7-Q7Uc-f9cpvj
LV Write Access read/write
LV Creation host, time demoserver, 2023-04-10 14:11:15 -0400
LV Status available
# open 2
LV Size 3.75 GiB
Current LE 960
Segments 1
Allocation inherit
Read ahead sectors auto
- currently set to 256
Block device 253:1

--- Logical volume ---
LV Path /dev/rhel/home
LV Name home
VG Name rhel
LV UUID MMpQ05-Gry0-9qGg-zvGQ-Dszn-kIkd-ZpaqK6
LV Write Access read/write
LV Creation host, time demoserver, 2023-04-10 14:11:15 -0400
LV Status          available
# open             1
LV Size            <223.34 GiB
Current LE         57174
Segments           1
Allocation         inherit
Read ahead sectors auto
- currently set to 256
Block device       253:2

--- Logical volume ---
LV Path            /dev/rhel/root
LV Name            root
VG Name            rhel
LV UUID            OFqABO-azjy-47DO-bzRo-ha2O-sHz5-jjMPcF
LV Write Access    read/write
LV Creation host, time demoserver, 2023-04-10 14:11:17 -0400
LV Status          available
# open             1
LV Size            70.00 GiB
Current LE         17920
Segments           1
Allocation         inherit
Read ahead sectors auto
- currently set to 256
Block device       253:0
```

如上例所示，卷组 `rhel` 中的 70 GiB 空间分配给逻辑卷 `root`（用于 `/` 文件系统），大约 223.34 GiB 分配给 `home` 逻辑卷（用于 `/home`），3.75 GiB 分配给 `swap`（用于交换空间）。

现在我们知道了空间的使用情况，了解提供空间的设备（换句话说，哪些设备用作物理卷）通常很有帮助。要获取此信息，我们需要运行 `pvdisplay` 命令：

```
# pvdisplay
--- Physical volume ---
PV Name            /dev/sda2
VG Name            rhel
PV Size            <297.09 GiB / not usable 4.00 MiB
Allocatable        yes (but full)
PE Size            4.00 MiB
Total PE           76054
Free PE            0
Allocated PE       76054
PV UUID            siKTC2-fq47-LXTG-VWtc-Ma33-XRCm-5uF63v
```

显然，逻辑卷 `rhel` 控制的空间是通过位于 `/dev/sda2` 上的物理卷提供的。

现在我们对 LVM 配置有了更多了解，可以向卷组及其包含的逻辑卷添加空间。

## 32.3 从命令行向卷组添加额外空间

就像之前收集 RHEL 9 系统当前逻辑卷管理配置信息的步骤一样，可以从命令行对该配置进行更改。

在本章的剩余部分，我们假设已向系统添加了新磁盘，并且操作系统将其视为 `/dev/sdb`。我们还假设这是一个没有现有分区的全新磁盘。如果存在现有分区，应先备份它们，然后使用 `fdisk` 实用程序从磁盘中删除分区。例如，假设由 `/dev/sdb` 表示的设备包含以下两个分区：

```
# fdisk -l /dev/sdb
```

Disk `/dev/sdb`: 14.46 GiB, 15525216256 bytes, 30322688 sectors

Disk model: USB 2.0 FD

Units: sectors of 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x4c33060b

| 设备 | 启动 | 开始 | 结束 | 扇区 | 大小 | ID | 类型 |
|---|---|---|---|---|---|---|---|
| `/dev/sdb1` |  | 2048 | 30322687 | 30320640 | 14.5G | 83 | Linux |

在对这些分区上的任何文件系统进行卸载后，可以按如下方式删除它们：

```
# fdisk /dev/sdb

Welcome to fdisk (util-linux 2.37.4).
Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): d
Selected partition 1
Partition 1 has been deleted.

Command (m for help): w

The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

在进入下一步之前，请从 `/etc/fstab` 文件中删除这些文件系统的任何条目，以便系统在下次重启时不会尝试挂载它们。

磁盘准备就绪后，下一步是使用 `pvcreate` 命令将此磁盘转换为物理卷（如果存在，则同时清除 dos 签名）：

```
# pvcreate /dev/sdb
WARNING: dos signature detected on /dev/sdb at offset 510. Wipe it? [y/n]: y
  Wiping dos signature on /dev/sdb.
  Physical volume "/dev/sdb" successfully created.
```

如果创建失败并显示“Device /dev/<device> excluded by a filter”消息，则在创建物理卷之前可能需要使用 `wipefs` 命令清除磁盘：

```
# wipefs -a /dev/sdb
/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa
/dev/sdb: calling ioctl to re-read partition table: Success
```

物理卷创建后，我们现在需要使用 `vgextend` 命令将其添加到卷组（在本例中为 `rhel`）：

```
# vgextend rhel /dev/sdb
  Volume group "rhel" successfully extended
```

新物理卷现已添加到卷组中，可以分配给逻辑卷。为此，我们运行 `lvextend` 工具并提供希望扩展的体积大小。在本例中，我们希望将 `home` 逻辑卷的大小扩展 14 GB。请注意，我们需要提供逻辑卷的路径，可以从 `lvdisplay` 命令获得（在本例中为 `/dev/rhel/home`）：
