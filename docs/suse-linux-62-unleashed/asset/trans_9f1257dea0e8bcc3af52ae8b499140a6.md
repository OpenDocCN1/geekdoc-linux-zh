
# 文件系统管理

第 18 章

# 图 18.3
`yeast` 命令用于在 SuSE 系统上添加或删除硬盘分区。

![](img/cbac72550c7126a22162e94d91a0c360_582_0.png)

# 图 18.4
`yeast` 命令将检测系统中的存储设备，以便进行分区或格式化调整。

![](img/cbac72550c7126a22162e94d91a0c360_582_1.png)

文件系统管理

# SUSE 系统管理
第三部分

# 图 18.5
`vast` 命令用于在所选的存储设备上删除或更改分区类型。

![](img/cbac72550c7126a22162e94d91a0c360_583_0.png)

许多操作系统不区分设备表面准备数据（格式化）和构建新文件系统的过程。Linux 区分了这两者，主要是因为在任何情况下只有软磁盘需要格式化，而且因为 Linux 提供了多达六种可以在（任何块设备上）创建的文件系统。在这些程序程序都单独设计格式化软磁盘的功能是糟糕的设计，并且它要求你为每种类型的新文件系统学习一种不同的操作方法。软磁盘的格式化过程是单独处理的。（更多信息请参阅本章稍后介绍“软磁盘”部分。）

文件系统最初由一个程序构建，该程序打开块设备并向其写入一些数据，以便当内核尝试挂载文件系统时，该设备已经包含了一个原始文件系统的镜像。这意味着内核和用于创建文件系统的程序必须对正确的文件系统结构达成一致。

Linux 提供了一个通用命令 `mkfs`，它允许你在块设备上创建文件系统。事实上，UNIX 使用同一套操作管理几乎所有的资源，`mkfs` 可用于在普通文件中生成文件系统。由于这种操作不寻常，`mkfs` 在执行之前会请求确认。操作完成后，你可以使用回环设备（loop device）挂载生成的文件系统。（更多信息请参阅本章稍后的“挂载文件系统”部分。）

由于可用文件系统的种类众多，几乎所有构建新文件系统的工作都委托给了每个文件系统的独立程序；然而，通用的 `mkfs` 程序为调用所有程序提供了单一接口。向顶层 `mkfs` 传递选项（例如 `-V` 显示其执行的命令，或 `-c` 检查设备坏块）并不罕见。通用 `mkfs` 程序还允许向特定文件系统的传递选项。大多数依赖于文件系统的选项都有合理的默认值，通常不需要更改。你可能想要传递给 `mke2fs`（构建 ext2 文件系统）的选项只有 `-m` 和 `-i`。`-m` 指定文件系统中保留给 root 用户空间（例如当系统磁盘可能完全满时的工作空间）。`-i` 选项较少使用，用于设置 inode 和磁盘块之间的平衡；它与预期的平均文件大小有关。如前所述，大多数情况下默认值是合理的，这些选项仅在特殊情况下使用：

```
# mkfs -ext2 /dev/fd0
mke2fs 1.14, 9-Jan-99 for EXT2 FS 0.5b, 95/08/09
Linux ext2 filesystem format
Filesystem label=
360 inodes, 1440 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1 block group
8192 blocks per group, 8192 fragments per group
360 inodes per group
```

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

```
# mount /floppy
# ls -la /floppy
total 14
drwx-xr-x 3 root root 1024 Sep 12 22:36 .
drwx-xr-x 20 root root 1024 Sep 10 04:38 -
drwx-xr-x 2 root root 12288 Sep 12 22:36 last+found
# umount /floppy
```

在这里，你看到了在软磁盘上创建和挂载 ext2 文件系统。图中显示了程序默认指定的文件系统结构。没有卷标签，每个 inode 占用 4,096 字节（4KB）（360x4=1,440）。块大小为 1KB，磁盘的 5% 留给了 root。这些是默认值（在 mke2fs 的手册页中解释）。创建文件系统后，你可以使用 `dumpe2fs` 显示 ext2 文件系统的信息，但记住将结果通过通过分页器（pager），因为此输出可能非常长。

![](img/cbac72550c7126a22162e94d91a0c360_584_1.png)
