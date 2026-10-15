
在继续之前，请确保已完成练习 13-6 中概述的 VDO 软件安装和启动启动步骤。

- 1. 在 `sdf` 磁盘上创建一个逻辑大小为 16GB、`slab` 大小为 128MB 的 VDO 卷 `vdo1`：

```
[user1@server2 ~]$ sudo vdo create --device /dev/sdf --name vdo1 --vdoSlabSize 128 --vdoLogicalSize 16
Creating Vdo1
Starting Vdo1
Starting compression on vdo1
VDO instance 2 volume is ready at /dev/mapper/vdo1
```

- 2. 使用 `vdo` 和 `lsblk` 命令列出新的 VDO 卷：

```
[user1@server2 ~]$ sudo vdo list
vdo1
[user1@server2 ~]$ lsblk /dev/sdf
NAME MAJ MIN SIZE RO TYPE MOUNTPOINT
sdf 8:0 4G 0 disk
└vdo1 253:2 0 16G vdo
```

输出显示了底层磁盘的逻辑大小（16GB）、类型（vdo）和实际大小（4GB）。

- 3. 使用 `mkfs.xfs` 命令用 XFS 文件系统初始化 VDO 卷。如步骤1输出所示，VDO 卷设备文件为 `/dev/mapper/vdo1`。添加 `-f` 标志以强制移除磁盘上的任何旧分区或标记信息。

- 4. 打开 `/etc/fstab` 文件，到文件末尾，使用其设备添加以下文件系统条目以实现持久化：

```
[user1@server2 ~]$ sudo mkfs.xfs /dev/mapper/vdo1
meta-data=/dev/mapper/vdo1 isize=512 agcount=4, agsize=1048576 blks sects=4096 attr=2, proj32bit=1 crc=1 finit=1, sparse=1, rmap=0 reflink=1 bsize=4096 blocks=4194304, imaxcount=25 unit=0 switch=0 blks bsize=4096 ascii-ci-0, ftype=2 bsize=4096 blocks=2560, version=2 sects=4096 unit=1 blks, lazy-count=1 extxts=4096 blocks=0, rextents=0
```

```
/dev/mapper/vdo1 /xfsvdo1 xfs x-systemd.requires=vdo.service 0
```

确保在 `fstab` 文件的文件系统条目中包含 `x-systemd.requires=vdo.service` （或尝试 `try_netdev`），否则系统在下次重启时将进入紧急目标（emergency target）。此选项会阻止挂载命令在 `vdo.service` 运行之前挂载此文件。

- 5. 使用 `mkdir` 命令创建挂载点 `/xfsdo1`：

```
[user1@server2 ~]$ sudo mkdir /xfsdo1
```

- 6. 使用 `mount` 命令挂载新文件系统。如果文件中存在任何无效或缺失的信息，此命令将失败。

```
[user1@server2 ~]$ sudo mount -a
```

带有 `-a` 标志的 `mount` 命令用于测试 `fstab` 文件。它应在更新该文件后、重启服务器之前执行，以避免系统处于不可启动状态。

- 7. 使用 `lsblk` 和 `df` 查看 VDO 系统的挂载状态、可用性和类型：

```
[user1@server2 ~]$ lsblk
NAME MAJ MIN SIZE TYPE MOUNTPOINT
sdf 8:0 4G 0 disk
└vdo1 253:2 0 16G vdo
[user1@server2 ~]$ df -h /xfsdo1
Filesystem Type Mounted on
/dev/mapper/vdo1 xfs 147M 16G /xfsdo1
```

`lsblk` 命令说明了 VDO 卷名 (`vdo1`)、位于 (`sdf`) 的磁盘以及 (4GB) 和逻辑 (16GB) 大小。`df` 命令显示了系统的逻辑大小和使用情况。该系统已添加到 `fstab` 文件中以持久化，这意味着未来重启将自动重新挂载。此文件系统现在可以用于存储文件。详情请第13章“分区”。

## 练习 15-3：在 LVM 中创建并挂载 Ext4 和 XFS 文件系统

此练习应在 `server2` 上以 `user1` 身份执行。

在此练习中，你将在 `sd` 分区上创建一个名为 `vgfs` 的 16MB 物理卷。卷组 PE 大小应设置为 16MB。你将创建两个大小为 80MB 的逻辑卷 `ext4vol` 和 `xfs`，并用 Ext4 和 XFS 类型初始化它们。你将通过卷设备文件名持久化地定义两个文件系统。你将创建挂载点 `/ext4fs` `/xfs`，挂载文件系统并验证它们的可用性和使用情况。

- 1. 使用 `parted` 命令在 `sd` 磁盘上创建一个 150MB 的分区：

```
[user1@server2 ~]$ sudo parted /dev/sd mkpart primary 1 181MB
```

- 2. 使用 `pvcreate` 命令将 `sd1` 分区初始化用于 LVM：

```
[user1@server2 ~]$ sudo pvcreate /dev/sd1
Physical volume "/dev/sd1" successfully created.
```

- 3. 使用物理卷 `sd1` 创建 PE 大小为 16MB 的卷组 `vgfs`：

```
[user1@server2 ~]$ sudo vgcreate -s 16 vgfs /dev/sd1
Volume group "vgfs" successfully created.
```

PE 大小在卷组创建后难以更改，因此在创建时定义。

- 4. 使用 `lvcreate` 命令在 `vgfs` 中创建两个大小为 80MB 的逻辑卷 `ext4vol` 和 `xfsvol`：

```
[user1@server2 ~]$ sudo lvcreate -n ext4vol -L 80MB vgfs
Logical volume "ext4vol" created.
[user1@server2 ~]$ sudo lvcreate -n xfsvol -L 80MB vgfs
Logical volume "xfsvol" created.
```

- 5. 使用 `mkfs.ext4` 命令用 Ext4 文件系统格式化 `ext4vol` 逻辑卷：

```
[user1@server2 ~]$ sudo mkfs.ext4 /dev/vgfs/ext4vol
mke2fs 1.4.3 (10-July-2018)
Creating filesystem with 81920 1k blocks and 20480 inodes
Filesystem UUID: 6a30d72f-00b3-4797-a7ba-c5f6d36f7a58
Superblock stored on blocks:
8193, 24577, 40961, 57345, 73729
```

```
Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

你也可以使用 `sudo mkfs -t ext4 /dev/vgfs/ext4vol`。

- 6. 使用 `mkfs.xfs` 命令用 XFS 文件系统类型格式化 `xfsvol` 逻辑卷：

```
[user1@server2 ~]$ sudo mkfs.xfs /dev/vgfs/xfsvol
meta-data=/dev/vgfs/xfsvol isize=512 agcount=4, agsize=1048576 blks sects=4096 attr=2, proj32bit=1 crc=1 finit=1, sparse=1, rmap=0 reflink=1 bsize=4096 blocks=4194304, imaxcount=25 unit=0 switch=0 blks bsize=4096 ascii-ci-0, ftype=2 bsize=4096 blocks=2560, version=2 sects=4096 unit=1 blks, lazy-count=1 extxts=4096 blocks=0, rextents=0
```
