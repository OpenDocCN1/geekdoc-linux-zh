
## 监控文件系统

块数量：2303311  
保留块数量：115165  
空闲块：644098  
空闲 Inode：796808  
首块：0  
块大小：4096  
片段大小：4096  
每组块数：32768  
每组片段数：32768  
每组 Inode 数：16224  
每组 Inode 块数：507  
文件系统创建时间：2004年6月20日 星期日 04:07:03  
最后挂载时间：2004年7月12日 星期一 11:49:22  
最后写入时间：2004年7月12日 星期一 11:49:22  
挂载次数：5  
最大挂载次数：-1  
最后检查时间：2004年6月20日 星期日 04:07:03  
检查间隔：0（无）  
保留块 UID：0（用户 root）  
保留块 GID：0（组 root）  
首个 Inode：11  
Inode 大小：128  
日志 Inode：8  
首个孤儿 Inode：309037  
默认目录哈希：tea  
目录哈希种子：d972eedf-28f8-4cac-9417-039a32206be0  
日志备份：Inode 块

```
[root@server1 root]#
```

在上面的输出中，可以看到 Inode 表中包含 1151904 个 Inode，其中 796808 个在创建新文件和目录时可自由使用。

### 检查文件系统错误

文件系统本身可能会随着时间积累错误。这些错误通常被称为**文件系统损坏**，且在大多数文件系统中都很常见。经常被访问的文件系统比不常被访问的更容易出现损坏。因此，应定期检查此类文件系统是否存在错误。最常见的文件系统损坏是由于未使用 `shutdown`、`halt` 或 `reboot` 命令正常关闭系统而导致的。数据在写入硬盘上的文件之前，会在内存中短暂存储。这种将数据保存到硬盘的过程称为**同步**。如果计算机电源被切断，内存中的数据可能无法正确同步到硬盘，从而导致损坏。如果硬盘频繁用于耗时任务（如数据库访问），也可能发生文件系统损坏。随着任何系统使用量的增加，写入硬盘时发生操作系统错误的可能性也随之增加。同理，物理硬盘本身是机械性质的，会随着时间推移而磨损。如果磁盘的某些区域无法保持磁荷，它们可能会变得不可用；这些区域被称为**坏块**。当操作系统发现坏块时，它会将该坏块的引用放入文件系统的坏块表中。坏块表中的任何条目都不会再用于未来的磁盘存储。

要检查文件系统错误，可以使用 **fsck（文件系统检查）命令**，它可以检查许多不同类型的文件系统。`fsck` 命令接受一个指定文件系统类型的选项和一个指定要检查设备的参数；如果未指定文件系统类型，则默认假设为 ext2 文件系统。另外需要注意的是，为了让 `fsck` 命令正常工作，被检查的文件系统必须事先卸载，如下所示：

```
[root@server1 root]# fsck -t ext2 /dev/fd0
Parallelizing fsck version 1.23 (15-Aug-2001)
fsck 1.35 (28-Feb-2004)
e2fsck 1.35 (28-Feb-2004)
/dev/fd0 is mounted.

WARNING!!! Running e2fsck on a mounted filesystem may cause
SEVERE filesystem damage.

Do you really want to continue (y/n)? n

check aborted.
[root@server1 root]# umount /dev/fd0
[root@server1 root]# fsck -t ext2 /dev/fd0
fsck 1.35 (28-Feb-2004)
e2fsck 1.35 (28-Feb-2004)
/dev/fd0: clean, 14/184 files, 45/1440 blocks
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_250_0.png)

> 由于 / 文件系统无法卸载，因此只应在单用户模式下对 / 文件系统运行 `fsck` 命令，这将在第8章“使用 Bash Shell”中详细讨论。

请注意，在前面的输出中，`fsck` 命令在检查文件系统时不会在终端屏幕上产生冗长的输出；这是因为除非使用 `-f` 选项执行完整检查（如下例所示），否则 `fsck` 命令只执行快速错误检查：

```
[root@server1 root]# fsck -f -t ext2 /dev/fd0
fsck 1.35 (28-Feb-2004)
e2fsck 1.35 (28-Feb-2004)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/fd0: 14/184 files (0.0% non-contiguous), 45/1440 blocks
[root@server1 root]#
```

表 6-6 列出了与 `fsck` 命令一起使用的常用选项。

| 选项 | 描述 |
| :--- | :--- |
| -f | 执行完整的文件系统检查 |
| -a | 允许 fsck 自动修复任何错误 |
| -A | 检查 /etc/fstab 中第六字段为 1 或 2 的所有文件系统 |
| -Cf | 执行完整的文件系统检查并显示进度行 |
| -AR | 检查 /etc/fstab 中第六字段为 1 或 2 的所有文件系统，但跳过 / 文件系统 |
| -V | 显示详细输出 |

如果 `fsck` 命令发现损坏的文件，它会向用户显示一条消息，询问是否修复该错误；为了避免这些消息，可以使用表 6-6 中列出的 `-a` 选项，指定 `fsck` 命令应自动修复任何损坏。如果存在 `fsck` 命令无法修复的文件，它会将其放置在相应文件系统的 lost+found 目录中，并将文件重命名为其 Inode 编号。

要查看 lost+found 目录的内容，只需挂载该设备，然后查看该挂载点正下方的 lost+found 目录内容。由于很难通过 Inode 编号识别丢失的文件，因此大多数用户会定期删除此目录的内容。请记住，当使用 `mkfs` 命令创建 ext2 或 ext3 文件系统时，会自动创建 lost+found 目录。

## 第 6 章：Linux 文件系统管理

就像可以使用 `mk2efs` 命令创建 ext2 文件系统一样，也可以使用 `e2fsck` 命令检查 ext2 或 ext3 文件系统。类似地，`reiserfsck` 命令可以检查 reiserfs 文件系统。这些命令接受更多选项，并且可以比 `fsck` 更彻底地检查文件系统。例如，通过使用 `e2fsck` 命令的 `-c` 选项，可以检查硬盘上的坏块并将它们添加到文件系统的坏块表中，以便将来不再使用它们，如下例所示：

```
[root@server1 root]# e2fsck -c /dev/fd0
e2fsck 1.35 (28-Feb-2004)
Checking for bad blocks (read-only test): done
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
/dev/fd0: ***** FILE SYSTEM WAS MODIFIED *****
/dev/fd0: 14/184 files (0.0% non-contiguous), 45/1440 blocks
[root@server1 root]#
```

![](img/09bf13b782f71165e17bb3839040c96a_252_0.png)

> **注意**
> `badblocks` 命令可用于执行与 `e2fsck` 命令带有 `-c` 选项相同的功能。

回顾前面提到的，`fsck` 命令在启动时运行，当时文件系统根据 `/etc/fstab` 文件中的条目进行挂载。`/etc/fstab` 中第六字段为 1 的条目首先被检查，然后是第六字段为 2 的条目。然而，通常每 20–40 次挂载 ext2 或 ext3 文件系统（或者每隔 180 天），就会强制进行一次完整的文件系统检查。根据被检查文件系统的大小，这可能会使启动延迟几分钟甚至几个小时。要更改此间隔，可以使用 `tune2fs` 命令的 `-i` 选项，如下所示：

```
[root@server1 root]# tune2fs -i 0 /dev/fd0
tune2fs 1.35 (28-Feb-2004)
Setting interval between check 0 seconds
[root@server1 root]#
```

`e2fsck` 命令可用于在文件系统创建后更改或“调整”文件系统参数。将检查间隔更改为 0 秒（如前例所示）会禁用文件系统检查。

