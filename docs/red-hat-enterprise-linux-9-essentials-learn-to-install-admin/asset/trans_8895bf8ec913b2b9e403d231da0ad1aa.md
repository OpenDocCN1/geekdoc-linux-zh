
## 将新磁盘添加到 RHEL 9 卷组和逻辑卷

### 32.1.3 逻辑卷（LV）

逻辑卷相当于磁盘分区，并且与磁盘分区一样，可以包含文件系统。

### 32.1.4 物理扩展区（PE）

每个物理卷（PV）都被划分为大小相等的数据块，称为物理扩展区。

### 32.1.5 逻辑扩展区（LE）

每个逻辑卷（LV）都被划分为大小相等的数据块，称为逻辑扩展区。

假设我们正在创建一个名为 VolGroup001 的新卷组。此卷组需要物理磁盘空间才能运行，因此我们分配三个磁盘分区 /dev/sda1、/dev/sdb1 和 /dev/sdb2。这些成为 VolGroup001 中的物理卷。然后，我们将在由这三个物理卷组成的卷组内创建一个名为 LogVol001 的逻辑卷。

如果 LogVol001 中的空间用完，我们将添加更多磁盘分区作为物理卷，并将它们分配给卷组和逻辑卷。

### 32.2 有关逻辑卷的信息

作为在 RHEL 9 中使用 LVM 的示例，我们将通过一个示例来演示如何为标准 RHEL 9 安装的 / 文件系统添加空间。考虑到根分区大小需要灵活，RHEL 9 将 / 文件系统设置为名为 rhel 的卷组内的逻辑卷（称为 root）。在对 LVM 设置进行任何更改之前，首先收集信息至关重要。

运行 mount 命令将输出有关一系列挂载点的信息，其中包括根文件系统的以下条目：

```
/dev/mapper/rhel-root on / type xfs (rw,relatime,seclabel,attr2,inode64,logbufs=8,logbsize=32k,noquota)
```

可以使用 vgdisplay 命令获取有关卷组的信息：

```
# vgdisplay
--- Volume group ---
VG Name              rhel
System ID
Format               lvm2
Metadata Areas       1
Metadata Sequence No 4
VG Access            read/write
VG Status            resizable
MAX LV               0
Cur LV               3
Open LV              3
Max PV               0
Cur PV               1
Act PV               1
VG Size              <297.09 GiB
PE Size              4.00 MiB
Total PE             76054
Alloc PE / Size      76054 / <297.09 GiB
Free PE / Size       0 / 0
VG UUID              8vZKNE-v6nY-uII2-NKk1-StmF-EkNp-NNKa9b
```

如上例所示，rhel 卷组的物理扩展区大小为 4.00MiB，总共有 297.09GB 可用于分配给逻辑卷。目前，已分配 76054 个物理扩展区，等于总容量。因此，我们必须添加一个或多个物理卷以增加分配给 rhel 卷组中任何逻辑卷的空间。vgs 工具对于显示系统中卷组可用空间的快速概览也很有帮助：

# vgs
| 卷组 | #PV | #LV | #SN | 属性 | 大小 | 空闲 |
|---|---|---|---|---|---|---|
| rhel | 1 | 3 | 0 | wz--n- | <297.09g | 0 |

可以使用 lvdisplay 命令以类似方式获取卷组中逻辑卷的信息：

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

如上例所示，卷组 rhel 中的 70 GiB 空间分配给逻辑卷 root（用于 / 文件系统），大约 223.34 GiB 分配给 home 逻辑卷（用于 /home），3.75 GiB 分配给 swap（用于交换空间）。

现在我们知道了空间的使用情况，了解提供空间的设备（换句话说，哪些设备用作物理卷）通常很有帮助。要获取此信息，我们需要运行 pvdisplay 命令：

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

显然，逻辑卷 *rhel* 控制的空间是通过位于 */dev/sda2* 上的物理卷提供的。

现在我们对 LVM 配置有了更多了解，可以向卷组及其包含的逻辑卷添加空间。

### 32.3 从命令行向卷组添加额外空间

就像之前收集 RHEL 9 系统当前逻辑卷管理配置信息的步骤一样，可以从命令行对该配置进行更改。

在本章的剩余部分，我们假设已向系统添加了新磁盘，并且操作系统将其视为 */dev/sdb*。我们还假设这是一个没有现有分区的全新磁盘。如果存在现有分区，应先备份它们，然后使用 *fdisk* 实用程序从磁盘中删除分区。例如，假设由 */dev/sdb* 表示的设备包含以下两个分区：

# fdisk -l /dev/sdb
Disk /dev/sdb: 14.46 GiB, 15525216256 bytes, 30322688 sectors
Disk model: USB 2.0 FD
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x4c33060b

| 设备 | 启动 | 开始 | 结束 | 扇区 | 大小 | ID | 类型 |
|---|---|---|---|---|---|---|---|
| /dev/sdb1 |  | 2048 | 30322687 | 30320640 | 14.5G | 83 | Linux |

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

在进入下一步之前，请从 /etc/fstab 文件中删除这些文件系统的任何条目，以便系统在下次重启时不会尝试挂载它们。

磁盘准备就绪后，下一步是使用 pvcreate 命令将此磁盘转换为物理卷（如果存在，则同时清除 dos 签名）：

```
# pvcreate /dev/sdb
WARNING: dos signature detected on /dev/sdb at offset 510. Wipe it? [y/n]: y
  Wiping dos signature on /dev/sdb.
  Physical volume "/dev/sdb" successfully created.
```

如果创建失败并显示“Device /dev/<device> excluded by a filter”消息，则在创建物理卷之前可能需要使用 wipefs 命令清除磁盘：

```
# wipefs -a /dev/sdb
/dev/sdb: 8 bytes were erased at offset 0x00000200 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 8 bytes were erased at offset 0x1fffffe00 (gpt): 45 46 49 20 50 41 52 54
/dev/sdb: 2 bytes were erased at offset 0x000001fe (PMBR): 55 aa
/dev/sdb: calling ioctl to re-read partition table: Success
```

物理卷创建后，我们现在需要使用 vgextend 命令将其添加到卷组（在本例中为 rhel）：

```
# vgextend rhel /dev/sdb
  Volume group "rhel" successfully extended
```

新物理卷现已添加到卷组中，可以分配给逻辑卷。为此，我们运行 lvextend 工具并提供希望扩展的体积大小。在本例中，我们希望将 home 逻辑卷的大小扩展 14 GB。请注意，我们需要提供逻辑卷的路径，可以从 lvdisplay 命令获得（在本例中为 /dev/rhel/home）：

```
# lvextend -L+14G /dev/rhel/home
  Size of logical volume rhel/home changed from <223.34 GiB (57174 extents) to <237.34 GiB (60758 extents).
  Logical volume rhel/home successfully resized.
```

最后一步是调整逻辑卷上驻留的文件系统大小以使用额外空间。执行方式将取决于文件系统类型，可以使用以下 df 命令并检查 Type 列来识别：

# df -T /home
| 文件系统 | 类型 | 1K-块 | 已用 | 可用 | 使用% | 挂载点 |
|---|---|---|---|---|---|---|
| /dev/mapper/rhel-home | xfs | 234070356 | 1669596 | 232400760 | 1% | /home |

如果 /home 使用 XFS 文件系统格式化，可以使用 xfs_growfs 实用程序调整其大小：

```
# xfs_growfs /home
meta-data=/dev/mapper/rhel-home isize=512    agcount=4, agsize=14636544 blks
       =                       sectsz=512   attr=2, projid32bit=1
       =                       crc=1        finobt=1, sparse=1, rmapbt=0
```
