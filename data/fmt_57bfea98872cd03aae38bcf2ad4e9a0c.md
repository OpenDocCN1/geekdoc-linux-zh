
```
ptc6:~ # dumpe2fs /dev/hdb2 | less
dumpe2fs 1.28 (31-Aug-2002)
Filesystem volume name:   /1
Last mounted on:          <not available>
Filesystem UUID:          aa00942b-4b36-4248-bb9f-962dc00b58ab
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal filetype needs_recovery sparse_super
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              7225344
Block count:              14430150
Reserved block count:     721507
Free blocks:              12709195
Free inodes:              7079490
First block:              0
Block size:               4096
Fragment size:            4096
Blocks per group:         32768
Fragments per group:      32768
Inodes per group:         16384
Inode blocks per group:   512
Last mount time:          Sat Jun 19 08:38:59 2004
Last write time:          Sat Jun 19 08:38:59 2004
Mount count:              27
Maximum mount count:      -1
Last checked:             Sun Nov 2 10:13:11 2003
Check interval:           0 (<none>)
Reserved blocks uid:      0 (user root)
Reserved blocks gid:      0 (group root)
First inode:              11
Inode size:               128
Journal UUID:             <none>
Journal inode:            8
Journal device:           0x0000
First orphan inode:       0
```

虽然了解文件系统的配置方式很有趣，但在文件系统创建之后，真正需要调优的内容并不多。最重要的文件系统调优是在创建时完成的。最重要的参数之一是块大小。由于典型的 Oracle 数据库使用 8K 的块大小，较小的 OS 块大小意味着 OS 必须为每个 Oracle 请求执行多次 I/O。这并不意味着 I/O 是以 OS 块大小的单位发生的，只是说它可以执行最多为该大小的 I/O 操作。你应该使 OS 块大小尽可能接近 Oracle 块大小，或者更大。不幸的是，ext2 和 ext3 文件系统的最大块大小为 4K。Oracle 集群文件系统（OCFS）可以创建 1M 的块大小。我通常更喜欢在 OCFS 中使用 128K 的块大小。在创建 ext 文件系统时，请使用 4K 作为块大小。

这并不意味着 OCFS 每次只写入 128K。实际写入的大小将是已提交给文件系统的 I/O 的大小。这只是系统空间分配方式以及 OCFS 处理小文件与处理大文件之效率差异的体现。对 OCFS 的 I/O 最小尺寸为 4K，但如有必要可以大得多。

除了文件系统参数外，还可以使用 `elvtune` 命令来调优 Linux 中的电梯排序算法。电梯排序用于对 I/O 进行排序，使得磁头按物理顺序拾取请求，而不是来回跳动。当电梯向上运行时，它会先停在 3 楼然后停在 4 楼，即使 4 楼的按钮是在 3 楼之前按下的。运行 `elvtune device` 将显示当前设置，如下所示：

```
ptc6:~ # elvtune /dev/hdb2

/dev/hdb2 elevator ID      2
     read_latency:          128
     write_latency:         512
     max_pend_segments:     8192
```

这些参数指定了一种人工延迟，旨在允许多个 I/O 排队，以便进行电梯排序。虽然这对于单个磁盘驱动器是好事，但对于 RAID 控制器或 SAN 则是坏事。这是因为它实际上延迟了 I/O，以便设备驱动程序可以进行排序。但在 RAID 控制器或 SAN 中，执行电梯排序的是硬件，而不是设备驱动程序。

### 调优 RAID 控制器

有时，为了获得更好的性能，可以调优你的 RAID 控制器或 SAN。可以调优的内容和方法取决于 RAID 控制器的类型和品牌。通常，你可以调优以下组件：

1.  **缓存页大小** 缓存页大小应至少与 Oracle 块大小一样大。这减少了因需要为一个 Oracle I/O 分配多个缓存页而可能产生的额外开销。

2.  **读取和写入缓存大小** 通常，读取缓存和写入缓存可以独立指定。根据你的应用程序所做的操作，你可能需要更多的读取缓存，或者需要更多的写入缓存。

3.  **读取和写入缓存使用** 大多数 RAID 和 SAN 系统允许你基于每个 LUN 来分配读取缓存和写入缓存。某些 LUN 可能受益于读取缓存，其他 LUN 受益于写入缓存，还有些 LUN 两者都受益。随机 I/O（OLTP）不会从读取缓存中受益。大量的写入（如重做、归档等）则受益于写入缓存。

4.  **预读或预取** 在某些情况下，当应用程序需要大量的表扫描时（例如在数据仓库环境中），预取可能会帮助提高 Oracle 的性能。在 OLTP 环境中，当 I/O 主要呈随机性质时，预取可能不起作用。

根据你的硬件品牌和类型，有许多方法可以调优 I/O 子系统的硬件。如何调优取决于应用程序类型、I/O 访问模式以及正在发生的 I/O 数量。

## OCFS 调优

Oracle 集群文件系统（OCFS）的引入旨在提供一种方便的、高性能的、可集群化的文件系统。通过可集群化，OCFS 允许 RAC 集群中的多个系统访问相同的数据文件，这是 RAC 的关键。对 OCFS 的访问是通过一种称为 `O_DIRECT` 的机制完成的。`O_DIRECT` 允许以直接模式访问文件系统，绕过 Linux I/O 缓存。

由于 OCFS 的特性，你应仅通过 `O_DIRECT` 访问 OCFS 文件。Oracle 提供了一组被称为 coreutils 的工具。Oracle 的 coreutils 用带有相同名称但增加了 `O_DIRECT` 选项的工具替换了标准的 Linux 工具，如 `cp`、`dd` 和 `mv`。通过结合使用 `O_DIRECT` 选项（`-o`）和块大小选项（`direct`），性能可以显著改善。在我最近进行的一项测试中，`dd` 的性能

> **RAC I/O 访问**
>
> Oracle Real Application Clusters（RAC）需要所有集群节点都可见的共享存储。此共享存储的各种选项包括原始分区、ASM（Automatic Storage Management，自动存储管理）和 OCFS（Oracle Cluster Filesystem，Oracle 集群文件系统）。每种选项都有其自身的特性，且都是可行的选择。你所选择的选项将取决于你的需求。

使用 256K 块大小时，速率从 1.5 MBps 提高到了近 50 MBps，如下表所示。

| O_DIRECT 大小 | 时间 | MB/秒 | GB/小时 |
| :------------ | :--- | :----- | :---- |
| 0 | 815.00 | 1.26 | 4.42 |
| 64K | 24.03 | 42.62 | 149.84 |
| 128K | 21.28 | 48.13 | 169.20 |
| 256K | 20.58 | 49.75 | 174.91 |
| 512K | 43.78 | 23.39 | 82.23 |
| 1M | 44.10 | 23.22 | 81.64 |

这些测试是通过将一个 1GB 的文件从磁盘复制到 `/dev/null` 来执行的，方法如下：

```
time dd if=filetest | dd of=/dev/null
time dd -o_direct=256K if=filetest | dd of=/dev/null
```
