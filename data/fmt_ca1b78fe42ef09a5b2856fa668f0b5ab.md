
# Linux 如何工作（早期访问）© 2021 Brian Ward

首先，使用 `p` 命令打印当前分区表（`fdisk` 命令大致如下）。你的交互界面可能看起来如下：

```
Command (m for help): p

Disk /dev/sdd: 4 GiB, 824841536 sectors, 836812 sectors

Units of sector: 1 * 512 = 512 bytes

Sector size (logical/physical): 512 bytes / 512 bytes

I/O size (minimum/optimal): 512 bytes / 512 bytes

Disklabel type: dos

Disk identifier: 0x88f290cc
```

| 设备 | 启动 起始 结束 扇区 大小 标识 类型 |
| /dev/sdd1 | | 2048 8368127 8366080 4G c W95 FAT32 (LBA) |

大多数设备已经包含一个 FAT 样类型的分区，例如这个 `/dev/sdd1`。因为你想为 Linux 创建新分区（当然，你确定这里不需要任何东西），你可以删除现有的分区：

```
Command (m for help): d

Selected partition 1

Partition 1 has been deleted.
```

> 请记住，`fdisk` 在你显式写入分区表之前不会进行任何更改，所以你还没有修改磁盘。如果你犯了无法挽回的错误，可以使用 `q` 命令退出 `fdisk` 而不写入。现在，你将使用 `n` 命令创建第一个 200MB 的分区：

```
Command (m for help): n

Partition type

p primary (0 primary, extended, 4 free)

e extended (container for logical partitions)

Select (default p): p

Partition number (1-4, default 1): 1

First sector (2048-8368127, default 2048) 2048

Last sector, +sectors or +size(K,M,G,T,P) (2048-8368127, default 8368127): +200M
```

创建了一个名为 'linux' 大小为 200 MiB 的新分区。

> 在这里，`fdisk` 提示你 MBR 分区样式、分区的起始位置及其 ID（或大小）。默认值通常就是你需要的。唯一改变的是使用 `+` 语法指定大小和单位来更改分区的结束位置/大小。创建第二个分区的方法相同，只是你将使用所有默认值，所以我们就不跳过那部分了。当你完成分区布局后，使用 `p`（打印）命令进行检查：

```
Command (m for help): p

[--snip--]

Device Boot Start End Sectors Size Id Type

/dev/sdd1 2048 411647 409600 200M 8 Linux
```

磁盘与文件系统 77

`/dev/sdd2 411648 8368127 7956480 3.8G`

当你准备好写入分区表时，使用 `w` 命令：

```
Command (m for help): w

The partition table has been altered.

Calling ioctl() to re-read partition table.

Syncing disks.
```

注意，`fdisk` 出于安全考虑不会询问你是否确定；它执行你的操作并退出。
如果你对额外的诊断信息感兴趣，请使用 `journalctl -k` 查看之前提到的内核读取消息，但记住，只有在你在使用 `fdisk` 时才能获取这些信息。

到此时，你已经具备了开始分区磁盘的基础知识，但如果你想了解更多关于磁盘的细节，请继续阅读。否则，请跳到第 4.2 节学习如何在磁盘上放置文件系统。

## 4.1.4 导航磁盘和分区几何结构

任何带有移动部件设备都会为软件系统引入复杂性，因为存在抗磨损的物理元件。硬盘也不例外；尽管你可以将硬盘看作是可以对任何块进行随机访问的块设备，但如果系统在如何在磁盘上布局数据方面不小心，可能会导致严重的后果。考虑图 4-3 所示的单盘片磁盘的物理属性。

![](img/048936acb6c295aeb3ea45b9102.png)

图 4-3：硬盘的俯视图

磁盘由安装在主轴上的旋转盘片组成，磁头连接在机械臂上，机械臂可以扫描磁盘半径。当磁盘在磁头下方旋转时，磁头只从固定位置读取数据。这个圆被称为*柱面*（cylinder），因为较大的磁盘有多个盘片，每个盘片的顶部和底部可以有一个或两个磁头，而所有的磁头都连接到同一个臂上并协同移动。由于机械臂的移动，磁盘上有许多柱面，中心周围的较小，外围周围的较大。最后，你可以将一个柱面划分为扇区。这种思考磁盘几何结构的方法被称为 CHS；在旧系统中，你可以通过这三个参数进行寻址来找到磁盘的任何部分。

> 轨道（track）是柱面中单个磁头访问的部分。这种（磁盘几何结构...
