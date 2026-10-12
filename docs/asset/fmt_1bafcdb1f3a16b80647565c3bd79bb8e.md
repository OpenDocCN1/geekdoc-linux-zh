
在前面的输出中，你可以看到 inode 表中有 151904 个 inode，其中 796808 个在创建新文件和目录时是空闲的。

## 文件系统错误

文件系统本身会随着时间的积累错误。这些错误通常被称为文件系统损坏，在大多数文件系统中常见。频繁访问的文件系统比不频繁的更容易损坏。因此，应该定期检查此类文件系统的错误。常见的文件系统损坏是因为没有使用 `shutdown`、`halt` 或 `reboot` 命令正常关闭系统。数据在写入磁盘之前会在内存中存储一段时间。将数据保存到磁盘的过程称为同步（`sync`）。如果关闭计算机电源，内存中的数据可能无法正常同步到磁盘，从而导致损坏。如果频繁使用硬盘执行数据库访问等密集型任务，也会发生文件系统损坏。随着系统的使用，写入硬盘的操作错误也会增加，硬盘本身是机械性的，会随着时间磨损。如果磁盘的某些区域无法保持充电，就会变得不可用；这些区域被称为坏块（`bad blocks`）。当操作系统发现坏块时，会将该坏块的引用放在文件系统的坏块表中。坏块表中的条目不会用于未来的磁盘存储。

要检查文件系统的错误，你可以使用 `fsck`（文件系统检查）命令，它可以检查许多类型的文件系统。`fsck` 命令接受一个指定文件系统类型的选项和一个指定要检查设备的参数；如果没有指定文件系统类型，则假设为 `ext2` 文件系统。同样重要的是，被检查的文件系统必须在运行 `fsck` 命令之前卸载，如下所示：

```
[root@server1]# fsck -t ext2 /dev/fd0

Parallelizing fsck version 1.23 (15-Aug-2001)

fsck 1.35 (28-Feb-2004)

e2fsck 1.35 (28-Feb-2004)

/dev/fd0 is mounted.
```

> 警告！！！在挂载的文件系统上运行 efsck 可能导致严重的文件系统损坏。

确定要继续吗？(y/n) **n**

```
check aborted.

[root@server1]# umount /dev/fd0

[root@server1]# fsck -t ext2 /dev/fd0

fsck 1.35 (28-Feb-2004)

e2fsck 1.35 (28-Feb-2004)

/dev/fd0: clean, 14/184 files, 45/1440 blocks

[root@server1]#
```

> 因为文件系统无法卸载，你应该只在单用户模式下对文件系统运行 `fsck` 命令，这将在后文的第 8 章“使用 Bash Shell”中讨论。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_282_0.png)

注意

从前面的输出可以看出，`fsck` 命令在检查文件系统时不会在终端屏幕上详细输出；这是因为除非使用 `-f` 选项进行完整检查，否则 `fsck` 命令仅执行快速检查，示例所示：

```
[root@server1]# fsck -f -t ext2 /dev/fd0

fsck 1.35 (28-Feb-2004)

e2fsck 1.35 (28-Feb-2004)

Pass 1: Checking inodes, blocks, and sizes

Pass 2: Checking directory structure

Pass 3: Checking directory connectivity

Pass 4: Checking reference counts

Pass 5: Checking group summary information

/dev/fd0: 14/184 files (0.0% non-contiguous), 45/1440 blocks

[root@server1]# _
```

表 6-6 显示了用于 `fsck` 命令的常用选项列表。

# 第 6 章 Linux 文件系统管理

## 表 6-6 fsck 命令的常用选项

| 选项 | 说明 |
| --- | --- |
| -f | 执行全文件系统检查 |
| -a | 允许 fsck 自动修复任何错误 |
| -A | 检查 /etc/fstab 中第6 字段为 1 或 2 的所有文件 |
| -Cf | 执行全文件系统检查并显示进度条 |
| -AR | 检查 /etc/fstab 中第6 字段为 1 或 2 的所有系统，但跳过 /filesystem |
| -V | 显示详细输出 |

如果 `fsck` 命令发现损坏的文件，它会向用户显示一条消息，询问是否修复错误；为了避免这些问题，您可以使用表 6-6 中的 `-a` 选项来指定 `fsck` 命令自动修复任何损坏。如果存在 `fsck` 命令无法修复的文件，它会将它们放在文件系统上的 `lost+found` 目录中，并将它们重命名为 inode 编号。

要查看 `lost+found` 目录的内容，只需挂载设备并查看挂载点正下方的 `lost+found` 目录内容。由于很难通过 inode 编号识别文件，大多数用户会定期删除该目录的内容。记住，当使用 `mkfs` 创建 ext2 或 ext3 文件系统时，`lost+found` 目录会自动创建。

就像您使用 `mk2fs` 命令创建 ext2 文件系统一样，您可以使用 `e2fsck` 命令来检查 ext2 或 ext3 文件系统。同样，`reiserfsck` 命令也可以检查文件系统。这些命令接受更多选项，并且比 `fsck` 更彻底地检查文件系统。例如，通过使用 `e2fsck` 命令的 `-c` 选项，可以检查硬盘上的坏块并将它们添加到文件系统上的坏块表中，以便未来不再使用它们，如下所示：

```
[root@server1 root]# e2fsck -c /dev/fd0

e2fsck 1.35 (read-only test): done

Pass 1: Checking inodes, blocks, and sizes

Pass 2: Checking directory structure

Pass 3: Checking directory connectivity

Pass 4: Checking reference counts

Pass 5: Checking group summary information

/dev/fd0: FILE SYSTEM WAS MODIFIED *****

/dev/fd0: 14/184 files (0.0% non-contiguous), 45/1440 blocks [root@server1 root]# _
```

## 硬盘配额

`badblocks` 命令可以执行与 `e2fsck` 命令 `-c` 选项相同的功能。

回想之前，`fsck` 命令在启动时通过从 `/etc/fstab` 文件的条目挂载文件系统运行时运行。`etc/fstab` 中第6 字段为 1 的任何条目会被检查，然后是第6 字段为 2 的条目。然而，通常 ext2 或 ext3 文件系统每挂载 20–40 次（或每隔 180 天）就会执行一次全文件系统检查。这可能会导致启动延迟几分钟甚至几小时，取决于所检查的文件系统的大小。要更改此，使用 `-i` 选项来调整 `tune2fs`，如下所示：

```
[root@server1 root]# tune2fs -i 0 /dev/fd0

tune2fs 1.35 (28-Feb-2004)

Setting interval between check 0 seconds
```
```
[root@server1 root]# #
```

`tune2fs` 命令可用于文件系统创建后更改或“调整”文件系统参数。如前面的示例所示，将检查间隔更改为 0 秒将禁用文件系统检查。

## 硬盘配额

如果 Linux 系统上有多个用户，必须有足够的硬盘空间来支持每个用户预计存储的文件。硬盘配额限制了用户在文件系统上创建的文件数量。此外，如果硬盘空间有限，您应该对文件系统实施配额限制。有两种类型的配额限制：软限制（soft limits）和硬性限制（hard limits）。软限制允许用户在一定时间内（默认为七天）超出配额，而硬性限制是强制性的，会防止用户超过它们。配额通常在启动时启用（如果 `/etc/fstab` 中有配额），但也可以通过 `quota` 和 `quotaoff` 命令分别开启和关闭。

要为 `/filesystem` 设置配额并限制用户，可以执行以下步骤：

1. 修改 `/etc/fstab` 文件，为 `/` 文件系统添加 `usquota` 和 `grquota` 挂载选项。生成的 `/etc/fstab` 文件应该如下：

```
[root@server1 root]# cat /etc/fstab
LABEL=/ ext3 defaults,usquota,grquota 1 1
none /dev/pts devpts gid=5,mode=620 0 0
none /proc proc defaults 0 0
none /sys sysfs defaults 0 0
```
