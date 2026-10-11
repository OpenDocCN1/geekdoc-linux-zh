
由于修改启动菜单是一项艰复杂的任务，Kali 默认包含了两个可以启用持久化的菜单项：Live USB 持久化（Live USB Persistence）和 Live USB 加密持久化（Live USB Encrypted Persistence），如图 9.1 所示，名为“持久化菜单项”[第 241 页]。

![](img/4d5d0d3397277b3d6e29d1328d013586_266_0.png)

图 9.1 持久化菜单项

启用此功能时，`live-boot` 将扫描所有分区以寻找标记为 `persistence` 的文件系统（可以通过 `persistence-label=value` 启动参数覆盖），安装程序将为在该分区的 `persistence.conf` 文件中列出的目录（每行一个目录）设置持久化。特殊值 `union` 允许通过联合挂载（union mount）实现所有目录的完全持久化，这是一种只存储与底层文件系统相比的更改的叠加层。持久化目录的数据存储在包含相应 `persistence.conf` 文件的文件系统中。

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

有了新的 `/dev/sdb3` 分区后，使用 `mkfs.ext4` 命令（以及通过 `-L` 选项设置标签）将其格式化为标记为 `persistence` 的 `ext4` 文件系统。然后将该分区挂载到 `/mnt` 目录并创建所需的 `persistence.conf` 配置文件。一如既往，格式化任何磁盘时都要倍小心。如果你格式化了错误的磁盘或分区，可能会丢失宝贵信息。

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

`live-boot` 同样能够处理加密分区上的持久化文件系统。通过加密分区创建 LUKS 容器来保护持久化数据，其步骤与非加密持久化类似，不同在于需要使用 `cryptsetup` 来初始化加密分区。在加密分区上挂载持久化时，同样需要在 `persistence.conf` 中配置相应的挂载项。

### 添加“核弹”密码以增强安全性

Kali 提供了一个名为 `cryptsetup-nuke-password` 的软件包，该包通过修改 `cryptsetup` 早期启动脚本来实现一项新功能：你可以设置一个“核弹”密码——当使用时，它将销毁所有用于管理加密分区的密钥。

当你经常旅行并需要一种快速的方法来确保数据无法被恢复时，这非常有用。在启动时，只需输入核弹密码而不是原始密码，任何人（包括你本人）都将无法访问你的数据。

在使用该功能之前，明智之举是为你的加密密钥制作备份副本，并将它们保存在某个安全的地方。

你可以使用此命令配置核弹密码（假设你已经安装了该软件包）：

```
# dpkg-reconfigure cryptsetup-nuke-password
```

关于此功能的更多信息可以在以下教程中找到：

- [https://www.kali.org/tutorials/nuke-kali-linux-luks/](https://www.kali.org/tutorials/nuke-kali-linux-luks/)

## 9.5. 总结

在本章中，我们学习了修改 Kali 源码包，这些是 Kali 中发行的所有应用程序的基础构建模块。我们还发现了如何自定义和安装 Kali 内核。然后，我们讨论了 `live-build` 环境，并探讨了如何构建自定义的 Kali Linux ISO。我们还演示了如何创建加密和未加密的 Kali USB 安装。

### 9.5.1. 修改 Kali 软件包的总结提示

修改 Kali 软件包通常是 Kali 贡献者和开发者的任务，你可能有官方软件包无法满足的特定需求，而了解如何构建修改后的包可能非常有价值，如果你想分享你的更改、在内部部署这些更改，或者干净地将软件回滚到之前的状态。

当你需要修改某个软件时，下载源码、进行更改并使用修改后的软件可能很很有诱惑力。然而，如果你的应用程序需要系统级设置（例如带有 `make install` 步骤），那么它将用 `dpkg` 未知的文件污染你的文件系统，并产生无法通过包依赖关系捕获的问题。此外，这种类型的软件修改在分享时会变得更加繁琐。

在创建一个修改后的软件包时，通用流程总是相同的：获取源码包、解压它、进行你的更改，然后构建软件包。对于每一步，通常都有多个工具可以处理每个任务。

要开始重建 Kali 软件包，首先下载源码包，它由一个 `.dsc`（Debian 源码控制）文件和从该控制文件中引用的额外文件组成。

源码包存储在可以通过 HTTP 的镜像中。获取它们最有效的方法是使用 `apt source-package-name`，这要求你在 `/etc/apt/sources.list` 中添加 `deb-src` 行，并使用 `apt update` 更新索引文件。
