

由于修改启动菜单是一项艰复杂的任务，Kali 默认包含了两个可以启用持久化的菜单项：Live USB 持久化（Live USB Persistence）和 Live USB 加密持久化（Live USB Encrypted Persistence），如图 9.1 所示，名为“持久化菜单项”[第 241 页]。

![](img/4d5d0d3397277b3d6e29d1328d013586_266_0.png)

图 9.1 持久化菜单项

启用此功能时，live-boot 将扫描所有分区以寻找标记为 `persistence` 的文件系统（可以通过 `persistence-label=value` 启动参数覆盖），安装程序将为在该分区的 `persistence.conf` 文件中列出的目录（每行一个目录）设置持久化。特殊值 "union" 允许通过联合挂载（union mount）实现所有目录的完全持久化，这是一种只存储与底层文件系统相比的更改的叠加层。持久化目录的数据存储在包含相应 `persistence.conf` 文件的文件系统中。

## 9.4.2. 在 USB 盘上设置非加密持久化

在本节中，我们假设你已经按照第 2.1.4 节“在 DVD-ROM 或 USB 盘上拷贝镜像”[第 19 页]的说明准备好了 Kali Live USB 盘，并且使用了一个空间足够大容纳 ISO 镜像（约 3 GB）以及你想要持久化的目录数据的 USB 盘。我们假设 USB 盘被 Linux 识别为 `/dev/sdb`，并且仅包含默认 ISO 镜像中的两个分区（`/dev/sdb1` 和 `/dev/sdb2`）。执行此操作时务必小心。如果你对 USB 盘进行重新分区，可能会损坏数据。

要添加新分区，你必须知道复制到 live 的镜像大小。然后使用 `parted` 创建分区。以下命令分析 ISO 镜像名称 `kali-linux-2016.1-amd64.iso`，假设该文件也存在 USB 盘上：

```
# parted /dev/sdb print
Model: SanDisk Cruiser Edge (scsi)
Disk /dev/sdb: 32,GB
Sector size (logical/physical): 512B/512B
Partition Table: mdos
Disk Flags:

Number Start End Size Type File system Flags
1 32,8KB 2852MB 2852MB primary boot, hidden
2 2852MB 2945MB 93,4KB primary
# start=\$(du --block-size=1MB kali-linux-2016.1-amd64.iso | awk '{print $1}')
# echo "Size of image is $start MB"
Size of image is 2946 MB
# parted -a optimal /dev/sdb mkpart "${start}MB" 100%
Information: You may need to update /etc/fstab.
```

```
# parted /dev/sdb print
Model: SanDisk Cruiser Edge (scsi)
Disk /dev/sdb: 32,GB
Sector size (logical/physical): 512B/512B
Partition Table: mdos
Disk Flags:

Number Start End Size Type File system Flags
1 32,8KB 2852MB 2852MB primary boot, hidden
2 2852MB 2945MB 93,4KB primary
3 2946MB 32,0GB 29,1GB primary
```

有了新的 `/dev/sdb3` 分区后，使用 `mkfs.ext4` 命令（以及通过 `-L` 选项设置标签）将其格式化为标记为 "persistence" 的 `ext4` 文件系统。然后将该分区挂载到 `/mnt` 目录并创建所需的 `persistence.conf` 配置文件。一如既往，格式化任何磁盘时都要倍小心。如果你格式化了错误的磁盘或分区，可能会丢失宝贵信息。

```
# mkfs.ext4 -L persistence /dev/sdb3
mke2fs 1.43-WIP (15-Mar-2016)
Creating filesystem with 7096832 4k blocks and 1776764 inodes
Filesystem UUID: dedede20c4-5239-479a-b115-9561ac8576
Superblock backups stored on blocks:
32768, 98304, 163840, 229376, 294912, 819200, 884736, 105632, 265208, 409600
```

```
Allocating group table: done
Writing inode tables: done
Creating journal (32768 blocks): done
Writing superblocks and accounting information: done
# mount /dev/sdb3 /mnt
# echo "union" > /mnt/persistence.conf
# ls -l /mnt
total 20
drwx-xr-x-- 2 root root 16384 May 10 persistence.conf
-rw-r-- 1 root root 34
```

现在 USB 盘已准备就绪，可以使用“Live USB Persistence”菜单启动。

## 9.4.3. 在 USB 盘上设置加密持久化

live-boot 同样能够处理加密分区上的持久化文件系统。通过加密分区创建 LUKS 容器来保护持久化数据，其步骤与非加密持久化类似，不同在于需要使用 `cryptsetup` 来初始化加密分区。在加密分区上挂载持久化时，同样需要在 `persistence.conf` 中配置相应的挂载项。

