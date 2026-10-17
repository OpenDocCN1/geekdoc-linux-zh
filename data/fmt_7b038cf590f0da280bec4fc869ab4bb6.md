
```
[root@rhel6c ~]# mdadm --detail /dev/md0
/dev/md0:
Version : 1.2
Creation Time : Sun Jul 17 13:48:41 2011
Raid Level : raid5
Array Size : 16769664 (15.99 GB 17.17 GB)
Used Dev Size : 8384832 (8.00 GB 5.89 GB)
Raid Devices : 3
Total Devices : 3
Persistence : Superblock is persistent

Update Time : Sun Jul 17 13:49:43 2011
State : clean
Active Devices : 3
Working Devices : 3
Failed Devices : 0
Sparse Devices : 0

Layout : left-symmetric
Chunk Size : 64K
Name : rhel6c:0 (local to host rhel6c)
UUID : c10fd9c3:08f9a25f:be913027:999c8e1f
Events : 18

Number Major Minor Raiddevice State
0 8 17 0 active sync /dev/sdb
1 8 33 1 active sync /dev/sddc
3 8 49 2 active sync /dev/sdd1
```

## 11.3.7. 移除软件 raid

`raid` 在激活状态时在 `/proc/mdstat` 中可见。要完全移除 `raid` 以将磁盘用于其他用途，请使用 `mdadm` 停止（取消激活）它。

```
[root@rhel6c ~]# mdadm --stop /dev/md0
mdadm: stopped /dev/md0
```

现在可以对磁盘进行重新分区了。

## 11.3.8. 扩展阅读

查看 `mdadm` 的 man 页以获取更多信息。下面是一个在移除故障分区的同时添加新分区的命令示例。

```
mdadm /dev/md0 --add /dev/sdd1 --fail /dev/sdd1 --remove /dev/sdd1
```

## 11.4. 练习：raid

1. 向虚拟机添加三个每个为 1GB 的虚拟磁盘。
2. 在这三个磁盘上创建一个软件 `raid` 5。（不需要在上面创建文件系统）
3. 使用 `fdisk` 和在 `/proc` 中验证 `raid` 5 是否存在。
4. 停止并移除 `raid` 5。
5. 创建一个 `raid` 1 来镜像两个磁盘。

## 11.5. 方案：raid

1. 向虚拟机添加三个 1GB 的虚拟磁盘。
2. 在这三个磁盘上创建一个软件 `raid` 5。（不需要在上面创建文件系统）
3. 使用 `fdisk` 和在 `/proc` 中验证 `raid` 5 是否存在。
4. 停止并移除 `raid` 5。
5. 创建一个 `raid` 1 来镜像两个磁盘。

```
[root@elhel6 ~]# mdadm --create /dev/md0 --level=1 --raid-devices=2 \
/dev/sdb1 /dev/sdc1
mdadm Defaulting to version 1.2 metadata
mdadm: array /dev/md0 started.
[root@elhel6 ~]# cat /proc/mdstat
Personalities : [raid6] [raid5] [raid4] [raid1]
md0 : active raid sdc1[1] sdb1[0]
8384862 blocks super 1,2 [2/2] [UU]
[====>.......... resync = 20.8% (1741512/8384862) \
finish=0.5min speed=218144K/sec
```

## 第 12 章 逻辑卷管理

大多数 `lvm` 实现都支持物理存储分组、逻辑卷调整大小以及数据存储分组（数据迁移）。

物理存储分组是将多个块设备（硬盘，但也包括 `iSCSI` 等）组合成一个逻辑质质存储设备的雅称。若要扩大这个物理组，可以稍后添加块设备（包括分区）。

此物理组上 `Lvm` 卷的大小独立于各个组件的大小。该组的总大小是限制。

`lvm` 的优良特性之一是逻辑卷调整大小。你可以增加 `lvm` 卷的大小，有时甚至不需要停机。此外，你可以将数据从故障的硬盘设备中迁移出来，创建镜像并创建快照。

## 12.1. svm 简介

### 12.1.1. 标准分区的问题

在处理硬盘和标准分区时会遇到一些问题。考虑一个具有小型和一个大型硬盘设备的系统，其分区情况如下：第一块磁盘（`/dev/sda`）被分为两个部分，第二块磁盘（`/dev/sdb`）拥有分区和一些空闲。

![](img/66ba2c5c822cbe260e00b2d9933c1a54_112_0.png)

在示例中，考虑当你想要扩大 `/srv/project42` 的可用空间时的选项。你可以做什么？解决方案将迫使你卸载文件系统、备份数据、删除并重建分区，然后恢复数据并挂载文件系统。

### 12.1.2. lvm 解决方案

`lvm` 会在挂载的文件系统和硬件设备之间创建一个虚拟层。当正确使用 `svm` 时，就不需要为了扩大它而卸载文件系统。

![](img/66ba2c5c822cbe260e00b2d9933c1a54_112.png)

## 12.2. lvm 术语

### 12.2.1. 物理卷 (pv)

物理卷是任何块设备（磁盘、分区、`RAID` 设备甚至是 `iSCSI` 设备）。所有这些设备都可以成为卷组的成员。管理物理卷的命令以 `pv` 开头。

```
[root@centos65]# pvchange pvcreate pvresize pv
```

### 12.2.2. 卷组 (vg)

卷组是块设备和逻辑卷之抽象层。管理卷组的命令以 `vg` 开头。

```
[root@centos65]# vgbackup vgconvert xtend vgcreate vgreduce vgdisplay vgmerge
```

### 12.2.3. 逻辑卷 (lv)

逻辑卷在卷组中创建。包含文件系统的逻辑卷可以挂载。逻辑卷的使用与分区类似，使用相同的命令完成（`mkfs`, `mount`, `fck`, ...），但以 `lv` 开头。

```
[root@centos65]# lvchange xtend lvresize llvmreduce lvs conf
```

## 12.3. 示例：使用 lvm

此示例展示了如何使用 `lvm` 使用设备（例如 `/dev/sdc`，也可以是 `/dev/sdb` 或任何其他磁盘或分区），创建卷组 (`vg`) 以及如何创建和使用逻辑卷 (`vg/lv0`)。首先要做的是创建可以加入卷组的物理卷。此命令使磁盘或分区对卷组可用。

```
[root@RHEL4]# pvcreate /dev/sdc
Physical volume "/dev/sdc" successfully created 注意：使用整个设备时 Lvm 将正常工作，但同一台计算机（或同一 SAN）上的另一个操作系统将识别 lvm 并块设备标记为空！通过创建一个跨整个设备的分区，然后在分区而不是磁盘上运行 pvcreate 可以避免这种情况。注意，卷组可以添加更多设备。
```

```
[root@RHEL4]# vgcreate /dev/sdc

Volume group "vg" successfully created
```

最后一步 `lvcreate` 创建逻辑卷。

```
[root@RHEL4]# lvcreate --size 500m vg

Logical volume "lv0" created
```

逻辑卷 `/dev/vg1vol0` 现在可以格式化为 `ext3` 并挂载使用。

```
[root@RHEL42]# mkfs -m0 -j /dev/vg1vol0

mkfs -35 (28-Feb-2004)

Filesystem label=OS type Linux

Block size=1024 (log=0)

Fragment size=1024 (log=0) blocks

128016 inodes (0.8%) 留给超级用户

First data block=1

Maximum filesystem blocks=6763152

63 block groups每组 8192 个块，每组 8192 个碎片

每组 2032 个 inode

Superblock 备份存储在：8193, 24577, 40961, 57345, 73729, 204801, 221185, 401409

写入 inode 表：完成

创建日志 (8192 块)：完成

写入超级块文件系统计数：完成

此文件系统将每 7 天自动检查一次或以先到的时间为准。使用 tune2fs -c 进行覆盖。
```
