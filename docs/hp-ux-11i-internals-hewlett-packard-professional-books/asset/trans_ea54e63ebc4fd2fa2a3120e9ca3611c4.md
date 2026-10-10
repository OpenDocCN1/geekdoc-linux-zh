
影响从一个磁道传输数据到另一个磁道所需时间的主要因素是**寻道时间**。有时你要寻找的数据只在一个磁道之外，而有时它可能在一千个磁道之外。平均寻道时间是磁头跨越其总磁道数 1/2（在我们这个 500 个磁道的例子中为 250 个磁道）进行重新定位所需的时间。

影响磁盘访问时间的另一个因素是*旋转延迟*。考虑一个旋转的磁盘盘片，其每个磁道周围分布着若干扇区。你需要的扇区可能是即将到达磁头下方的下一个，也可能刚刚经过磁头，在这种情况下，你必须等待磁盘完成一整圈的旋转。因此，平均旋转延迟是磁盘介质旋转半圈所需的时间。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_249_0.png)

## 图 8-8 HFS 文件系统布局

从设计者的角度来看，降低旋转延迟的唯一方法是使用更快的磁盘（最近你可能已经注意到 PC 市场中从 5400 rpm 硬盘向 10,000 rpm 或更高转速发展的趋势）。提高驱动器速度的缺点是磁头的公差必须增加，且速度意味着热量——驱动器转速越快，硬件设计者要处理的热量散失就越多。这两个问题导致了成本的增加。至于寻道时间，趋势是增加磁道数量而不是减少，因为硬件设计者始终在努力提高其驱动器的容量。

这正是文件系统设计者选择实施一种“软”解决方案来应对这一挑战的地方。通过将磁盘划分为多个柱面组，并尽可能在柱面组内分配 inode 及其相关数据块，平均寻道时间可以得到大幅改善。每个柱面组包含一部分 inode 表、一个冗余的超级块副本（`fsck` 实用程序可以使用这些副本之一来恢复损坏的超级块），以及用于管理和监视本地柱面组空间利用率的本地化元数据。

重新考虑我们的例子；假设整个磁盘被划分为 100 个柱面组。每个柱面组（CG）将映射到 10 个相邻磁道。虽然旋转延迟保持不变，但包含文件数据的所有单个数据块都将位于一个 10 磁道的区域内。对于访问这个单个文件，平均寻道时间将从移动 500 个磁道所需的时间减少到移动 5 个磁道所需的时间！仅仅通过遵循这些文件数据放置的惯例，我们就能看到访问时间的巨大改善。我们意识到这是一个过度简化的解释，但它将我们的思路引向了正确的方向。

## 直接和间接块指针

你可能会想知道固定大小的 inode 如何指向大小各异的文件的所有数据块。如果块大小是固定的，inode 大小也是固定的，那么似乎隐含了一个最大文件大小。为了解决这个问题，HFS inode 采用四种类型的块指针：

-   直接指针（每个 inode 12 个）
-   单重间接指针（每个 inode 1 个）
-   双重间接指针（每个 inode 1 个）
-   三重间接指针（每个 inode 1 个）

最初的 AT&T 文件系统具有 512 字节的块，inode 为 128 字节，并有空间容纳 15 个块指针（每个指针为 32 位）。让我们检查这种模型的限制（图 8-9）。

有 12 个直接指针定位包含文件数据的前 12 个块，允许存储 12 * 512，即 6 KB 的空间。如果文件增长超过此大小，则使用第 13 个指针（单重间接指针）指向一个可以容纳额外直接指针的数据块（块大小为 512 意味着一个间接块将容纳额外的 128 个指针）。第 14 个指针（双重间接）可以指向一个包含额外单重间接指针的块，第 15 个指针（三重间接）可以指向一个包含额外双重间接指针的块。通过这种方式，固定大小的 inode 可以映射非常大数量的文件数据块。

![](img/08b7d2492fc1415a694a5fb16a8fdeb3_251_0.png)

对于具有 8K 字节块的文件系统，最大文件大小为：

| 指针类型 | 计算方式 | 结果 |
| :--- | :--- | :--- |
| 12 个直接指针 | 12 x 8K | 96 KBytes |
| + 单重间接 | 2K x 8K | 16 MBytes |
| + 双重间接 | 2K x 2K x 8K | 32 GBytes |
| + 三重间接 | 2K x 2K x 2K x 8K | 64 TBytes |

## 图 8-9 Inode

使用最初的 512 字节块大小，我们获得以下能力：
-   直接指针 → 12 × 512 = 6 KB
-   单重间接 → 128 × 512 = 64 KB
-   双重间接 → 128 × 128 × 512 = 8 MB
-   三重间接 → 128 × 128 × 128 × 512 = 2 GB

使用更现代的 8-KB 块大小，我们获得以下结果：
-   直接指针 → 12 × 8 KB = 96 KB
-   单重间接 → 2 KB × 8 KB = 16 MB
-   双重间接 → 2 KB × 2 KB × 8 KB = 32 GB
-   三重间接 → 2 KB × 2 KB × 2 KB × 8 KB = 64 TB

## HFS Inode

inode 是定义文件时至关重要的元数据结构。文件的所有属性——所有权限、类型、大小、凭据、时间戳、链接计数和数据块指针——都存储在这个结构中。文件的唯一未在 inode 中存储的属性是它的名称！实际上，名称是一个用于定位特定文件数据的抽象概念，它的存在是为了方便人类引用文件。

通过保持文件属性（其 inode 数据）和其名称（目录项）之间这种程度的分离，创建指向同一个 inode 的多个文件名就变得很简单。这是创建硬链接的基础（由 `ln` 命令引用）。

为了研究 HFS inode 的结构，让我们看看 HP-UX 内核中的 `icommon` 结构（列表 8.1）。

## 列表 8.1 `icommon` 结构字段

```c
inode type (upper 4 bits) and access mode (lower 12 bits)
   0 0 2 0 u_short ic_mode

   0x1000 IFIFO       FIFO or named pipe
   0x4000 IFDIR       Directory
   0x6000 IFBLK       Block special file
   0x7000 IFCONT      Continuation inode
   0x8000 IFREG       Regular file
   0x9000 IFNWK       Network special file (retired)
   0xA000 IFLNK       Symbolic Link
   0xC000 IFSOCK      Socket

   current number of directory links (hard links) to this inode,
   2 0 2 0 short ic_nlink
   low 16 bits of the owner's UID and GID
   4 0 2 0 u_short ic_uid_lsb
   6 0 2 0 u_short ic_gid_lsb
   file size in bytes
   8 0 8 0 long ic_size
   timestamps (access, inode modification, and creation)

   Note: the modification timestamp refers to the last time the
   contents of the inode were modified and does not necessarily
   mean that the file's contents were changed

   16 0 4 0 u_int ic_atime.tv_sec
   20 0 4 0 u_int ic_atime.tv_usec
   24 0 4 0 u_int ic_mtime.tv_sec
   28 0 4 0 u_int ic_mtime.tv_usec
   32 0 4 0 u_int ic_ctime.tv_sec
   36 0 4 0 u_int ic_ctime.tv_usec
   next are the 12 direct block pointers
   40 0 4 0 int ic_un2.ic_reg.ic_db[0]
   44 0 4 0 int ic_un2.ic_reg.ic_db[1]
   48 0 4 0 int ic_un2.ic_reg.ic_db[2]
   52 0 4 0 int ic_un2.ic_reg.ic_db[3]
   56 0 4 0 int ic_un2.ic_reg.ic_db[4]
   60 0 4 0 int ic_un2.ic_reg.ic_db[5]
   64 0 4 0 int ic_un2.ic_reg.ic_db[6]
   68 0 4 0 int ic_un2.ic_reg.ic_db[7]
   72 0 4 0 int ic_un2.ic_reg.ic_db[8]
   76 0 4 0 int ic_un2.ic_reg.ic_db[9]
   80 0 4 0 int ic_un2.ic_reg.ic_db[10]
   84 0 4 0 int ic_un2.ic_reg.ic_db[11]
   followed by the single indirect, double indirect, and triple 
   indirect block pointers  
   88 0 4 0 int ic_un2.ic_reg.ic_un.ic_ib[0]  
   92 0 4 0 int ic_un2.ic_reg.ic_un.ic_ib[1]  
   96 0 4 0 int ic_un2.ic_reg.ic_un.ic_ib[2]

   If this is a fast symbolic link, the block pointers are replaced with  
   40 0 60 0 char[60] ic_un2.ic_gsymlink  
   A fast symbolic link allows the symbolic or “soft link” pathname to be stored in the inode  
   instead of a data block. This is possible as long as the linkage path doesn't exceed 59  
   characters in length.

   the status flags  
   100 0 4 0 int ic_flags  
   0x01 IC_FASTLINK enable fast symbolic links  
   0x02 IC_LARGEUIDS enable use of large UIDs

   blocks held  
   104 0 4 0 int ic_blocks  
   108 0 4 0 int ic_gen  
   upper 16 bits of the owner's UID and GID if large UIDs have  
   been enabled  
   112 0 2 0 u_short ic_uid_msb  
   114 0 2 0 u_short ic_gid_msb  
   116 0 4 0 int ic_spare[0]  
   120 0 4 0 int ic_spare[1]  
   continuation inode number (if needed)  
   124 0 4 0 u_int ic_contin
```

正如我们从这个列表中看到的，HFS inode 的大小为 128 字节。如果使用访问控制列表（ACLs），inode 中的最后四个字节指向一个*延续* inode，该 inode 保存多达 13 个额外的访问控制设置。有关 ACL 的更多信息，请参考 `chacl` 和 `lsacl` 的手册页。

## 使用 fsdb 追踪元数据

研究文件系统内部结构的另一个有用工具是 *fsdb*。它类似于经典的 *adb* 调试实用程序，不同之处在于它是设计用来允许 root 用户检查驻留在磁盘上的元数据结构。为了加强关于 HFS inode 和文件系统元数据基本组织的知识，我们使用 *fsdb* 检查安装在 `/dev/vg00/lvol10` 上的 HFS 文件系统（列表 8.2）。该文件系统的挂载点是 `/chriss`，它下面存储着一个名为 `/chriss/stuff` 的数据文件，该文件包含以下三行文本：

