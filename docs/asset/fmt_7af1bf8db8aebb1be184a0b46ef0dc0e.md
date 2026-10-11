
如果 `fdisk` 命令指示由于修改了磁盘（如前面的示例），必须手动重新加载分区信息，你可以运行 `partprobe` 命令或重启系统。重启系统是确保 MBR 成功加载到内存中最可靠的方法。

`fdisk` 的替代方案是 `cfdisk` 命令。按照你之前检查的图 5-7 所示 `/dev/sda`，你可以使用它在屏幕底部快速创建、操作和删除分区，可以使用光标键导航。与 `fdisk` 一样，在 `cfdisk` 工具中进行更改后，你应该重启系统以确保 MBR 成功加载到内存。

## 5-7 cfdisk 工具

![](img/255973d661f18692a98dbc628624ab00_266_0.png)

分区类型: Linux (83)
属性: boot
文件系统 UUID: 8789961a-fbca-4411-a3d8-195556f3719
文件系统: ext4
挂载点: `/boot` (已挂载)

[启动] [删除] [退出] [类型] [帮助] [写入] [导出]

不保存更改退出程序

电脑重启后，你可以使用之前讨论过的 `mkfs`、`mount` 和 `umount` 命令，并将分区设备文件作为参数。
要在之前创建的 `/dev/sda` 分区上创建 ext4 文件系统，你可以使用以下命令：

```
#server1 ~ # mkfs -t ext4 /dev/sda

mke2fs 1.43.8 (1-Jan-2020)

Creating filesystem with 732416 4 blocks and 183264 nodes

Filesystem UUID: c550e7-8eae-4b1c-8a5f-60d66

Superblock stored on: 32768, 16384

Allocating group tables: done

Writing inode: done

Writing superblocks and filesystem information: done
```

使用 `mkswap` 命令准备交换分区，并使用 `swapon` 命令来激活它。要将之前创建的 `/dev/sda` 分区准备并激活为虚拟内存，可以使用以下命令：

```
[root@server1 ~]# mkswap /dev/sda

Setting up cityscape version 1, size = 2.2 GIB (2366631936 bytes)

no label, UUID=6a18eb0-caa5-42e9-b329-0f56d2a42db9

[root@server1 ~]# swapon /dev/sda

[root@server1 ~]#
```

> 注意
> 你也可以使用 `swapoff` 命令停用交换分区。

接下来，你可以编辑 `/etc/fstab` 文件以确保新的 `/dev/sda6` 分区被激活为虚拟内存，如下：

```
[root@server1 ~]# cat /etc/fstab

#

# /etc/fstab

# 通过引用可访问的文件系统在 /dev/sda6 下维护

# 参见 man pages fstab(5), findfs(8), mount(8) 和/or blkid(8)

UUID=9f22f5add-035b-4d26-a9d0a6fa63      ext4 defaults 1 1

UUID=8789961a-fbca-1441-95f123719      ext4 defaults 1 2

44837de7-b796-e4edc-56d17ca62        swap defaults 0 0

/dev/sda1                             USBdrive auto noauto 0 0

/dev/sda5                             data defaults 0 0

/dev/sda6                             swap defaults 0 0

[root@server1 ~]#
```

如果你的硬盘采用的是 GPT 而不是 MBR，你可以使用 `fdisk` 或 `cfdisk` 命令在格式化文件系统或将其准备用于作为 Linux 交换分区之前，创建或修改 GPT 分区。或者，你可以使用 `gdisk` (GPT fdisk) 命令，使用与 `fdisk` 几乎相同的界面来创建和操作 GPT 分区。如果你的硬盘具有 MBR，`gdisk` 将首先提示你将 MBR 转换为 GPT，这将破坏磁盘上所有现有的 MBR 分区。

# 第 5 章 Linux 文件系统管理

245

许多 Linux 发行版还包含了 `parted` (GNU Parted 命令，可用于在 MBR 和 GPT 硬盘上创建和修改分区)。以设备文件作为参数运行 `parted`。在 GNU parted 工具中，你可以输入 `help` 来查找命令列表，或者输入 `print` 来打印现有的分区，如下：

```
[root@server1 ~]# parted /dev/sdb

GNU parted 3.2

Using /dev/sdb

Welcome to GNU Parted! Type 'help' to view a list of commands.

(parted) print

Model: ATA INTEL SSDSA2CW08 (scsi)

Disk /dev/sdb: 80.0GB

Sector size (logical/physical): 512B/512B

Partition Table: gpt
```

| 编号 | 结束 | 大小 | 文件系统名称 | 标志 |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 1049KB | 2001MB | 2000MB | xfs |
| (parted) | | | | |

从上一个输出可以看出，Intel SSD 使用了 GPT 分区表，并包含一个 200MB 的分区 (`/dev/sd1`)，该分区包含 XFS 文件系统。在接下来的示例中，使用 GNU parted 工具利用硬盘上的剩余空间创建了两个额外的分区：一个标签为 "data" 的 3GB 分区 (`/dev/sd2`) 和一个标签为 "logs" 的 2GB 分区 (`/dev/sd3`)。在创建过程中，会提示你输入文件系统类型。如果你计划之后将分区格式化为 Linux 文件系统，选择默认的 ext2 分区类型即可。然而，如果你计划将该分区用于交换，应在提示文件系统类型时指定 `linux-swap`。

```
(parted) mkpart

Partition name? [] data

File system type? [ext2]? ext4

Start? 2GB

End? 5GB

(parted) mkpart

Partition name? [] logs

File system type? [ext2]? ext4

Start? 5GB

End? 7GB

(parted) print

Model: ATA INTEL SSDSA2CW08 (scsi)

Disk /dev/sdb: 80.0GB
```
