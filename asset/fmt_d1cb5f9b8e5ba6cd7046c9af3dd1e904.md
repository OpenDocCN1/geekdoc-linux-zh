
当 `fsck` 报告结果为“clean”时，表示它不需要运行文件系统完整性检查，因为最近已足够频繁地运行过一次检查（默认情况下，磁盘只有在有原因时或每隔几个月才会强制运行 `fsck`）。下一次计划运行 `fsck` 的时间信息是超级块的一部分。

您是否注意到这是一个“parallelizing”版本的 `fsck`？这是好事。这意味着该程序可以通过运行并行检查进程同时检查多个文件系统。这意味着即使在糟糕的关机序列之后，您也可以更快地启动系统。

此外，由于许多 Unix 系统支持不同的文件系统，`fsck` 是针对特定文件系统格式设计的 `fsck` 版本的前端。在本例中，由于系统检测到 `/dev/hdb` 是一个 `ext2` 文件系统，它将检查磁盘的请求交给了 `e2fsck` 处理。

最后，请注意最后一行报告了文件和块的使用情况和可用情况。这里有 11 个文件，共 64,000 个可能的文件，以及 8,094 个块，共 255,528 个可能使用的块。

### 3. -f 标志强制 fsck 无论下一次检查计划何时都进行适当的磁盘检查，而 -c 标志会导致程序测试并检查坏块。如果您想更清楚地了解程序正在做什么，请使用 -v 获取详细输出（请参阅表 9.1 获取有用的 fsck 标志列表）。

![](img/5ced0c78d748bd190e9027e5549a3622_200_1.png)

![](img/5ced0c78d748bd190e9027e5549a3622_201_0.png)

> 坏块是磁盘上会更改数据的块。通常这是磁盘介质问题，并且是一种潜伏的隐藏危险，可能导致文件损坏。出于这个原因，定期使用 `fsck` 检查坏块是个好主意。

```
# fsck -CfV /dev/hdb
Parallelizing fsck version 1.23 (15-Aug-2001)
[/sbin/fsck.ext2 -- /dev/hdb] fsck.ext2 -c /dev/hdb
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
Checking for bad blocks (read-only test): done
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information

/dev/hdb: ***** FILE SYSTEM WAS MODIFIED *****
/dev/hdb: 11/64000 files (0.0% non-contiguous), 8094/255528 blocks
```

书中“检查坏块”这一行在一两秒内就闪过，但当您在硬盘上运行此命令时，即使是相对较小的硬盘，也可能需要很长时间。不要惊讶，如果您可以在午餐外出并在它完成这一步之前返回。

### 表 9.1 有用的 fsck 标志

| 标志 | 含义 |
|------|---------|
| `-s` | 序列化：不要并行运行多个检查，而是依次运行。（如果您正在积极调试损坏的磁盘，请使用此选项。） |
| `-b superblock` | 告诉 `fsck` 尝试使用备用超级块。请记住，它们每 8,192 个块存储在磁盘上一次，因此第二个超级块是 8192×1，第三个是 2×8192+1，以此类推。 |
| `-c` | 检查文件系统上的坏块（实际上，这在 Linux 上调用了 `badblocks(8)`，有趣的是）。 |
| `-f` | 强制 `fsck` 检查磁盘，即使它认为磁盘是干净的。 |
| `-y` | 自动对错误提示回答 yes。 |
| `-t type` | 指定要检查的文件系统类型。通常，`fsck` 可以自动检测文件系统，但如果必须指定类型，最可能的选择是 `ext2`，或者可能是 `ext3`。 |
| `-A` | 检查所有已知磁盘。引用 `/etc/fstab` 中的列表（如下一小时所述）。 |

现在您可以看到，在此调用中 `fsck` 实际上对磁盘进行了六次遍历：一次检查坏块；再次检查 inode、块和大小的一致性；然后检查目录结构、目录连通性、inode 引用计数，最后是组摘要信息。即使没有任何信息表明遇到问题或进行了更改，程序最后仍会说“文件系统已修改”。有时这似乎是一个通用消息，但最安全的做法始终是假定它是真的，这就是为什么您不想在磁盘挂载时运行 `fsck`！

在 Unix 世界中似乎有两类管理工具——那些直接的，以及那些棘手且输出经常令人困惑的。毫无疑问，对于大多数系统管理员来说，`fsck` 属于后者。好消息是您不需要经常使用它，并且当您运行该程序时，在了解更多关于文件系统本身的结构后，大多数输出都是合理的。

#### 使用 fsck 修复问题

在上一节中，事情相当容易，因为磁盘上没有任何问题。当问题出现时，可能会让人害怕，但现在还不是按下恐慌按钮的时候！

##### 任务 9.2：使用 fsck 修复磁盘问题

为了说明 `fsck` 如何修复损坏的磁盘，我做了一件危险的事：在一个窗口中更改 `/dev/hdb` 的内容，同时在另一个窗口中运行 `fsck`。保证会引起麻烦，而且不出所料，确实如此。

1. 首先，`fsck` 程序被调用，要求检查坏块并强制进行完整的结构检查：

```
# fsck -cFv /dev/hdb
Parallelizing fsck version 1.20 (15-Aug-2001)
[/sbin/fsck.ext2 - ... /dev/hdb] fsck.ext2 -c /dev/hdb
e2fsck 1.23, 15-Aug-2001 for EXT2 FS 0.5b, 95/08/09
/dev/hdb is mounted.

WARNING!!! Running e2fsck on a mounted filesystem may cause
SEVERE filesystem damage.

Do you really want to continue (y/n)? yes

Checking for bad blocks (read-only test): done
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
```

到目前为止，一切顺利。与此同时，在另一个窗口中，我快速地复制了大量文件到磁盘上，重命名它们，最终又删除了它们。

脚下的这些变化导致 `fsck` 在第 4 遍检查时有点不高兴：

```
Pass 4: Checking reference counts
WARNING: PROGRAMMING BUG IN E2FSCK!
OR SOME BONEHEAD (YOU) IS CHECKING A MOUNTED (LIVE) FILESYSTEM.
inode_link_info[2] is 9, inode_i_links_count is 11. They should be the same!
Inode 2 ref count is 11, should be 11. Fix<y>?
```

2. 虽然说我们是蠢人这种指责可能有点苛刻，但 inode 引用计数错误是典型的 `fsck` 错误信息。它准确地指出了问题所在（`inode_link_info[2]` 为 9，而 `inode_i_links_count` 为 11），然后询问你是否要修复它。

输入 `y` 它会立即扩展为 `yes` 并继续。我的这个危险的文件系统恶作剧引入了很多问题：
