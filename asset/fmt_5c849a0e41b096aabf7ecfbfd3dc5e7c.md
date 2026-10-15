
```c
struct super_operations {
    struct inode *(*alloc_inode)(struct super_block *sb);
    void (*destroy_inode)(struct inode *, int flags);
    int (*write_inode)(struct inode *, struct writeback_control *wbc);
    int (*drop_inode)(struct inode *);
    void (*evict_inode)(struct inode *);
    void (*super)(struct super_block *);
    int (*sync_fs)(struct super_block *, int wait);
    int (*free_super)(struct super_block *);
    int (*freeze_super)(struct super_block *);
    int (*thaw_super)(struct super_block *);
    int (*fill_super)(struct super_block *);
    int (*stats)(struct dentry *, struct kstatfs *);
    int (*remount_fs)(struct super_block *, int *, char *);
    void (*umount_begin)(struct super_block *);
    int (*set_inodeb)(struct seq_file *, struct dentry *);
    int (*show_devname)(struct seq_file *, struct dentry *);
    int (*show_path)(struct seq_file *, struct dentry *);
    int (*show_stats)(struct seq_file *, struct dentry *);
    // ...
};
```

# 树莓派上的 Linux 操作系统基础

当设备被挂载时，文件系统将根据指定的位置合并到 VFS 文件层次结构中。该位置是在超级块中指定的，而超级块是通过在命名文件的 `file_system_type` 中指定的适当函数指针读取的。`mount` 系统调用执行了此项任务，它指定了要挂载的设备、相应的具体文件类型以及应该挂载文件系统的目录路径。使用 `strace` 来跟踪系统调用的执行情况。当你向树莓派插入 USB 盘并手动挂载时，可能需要临时禁用自动挂载；同样使用 `dmesg` 来找到与你的 USB 盘对应的设备路径。

- 列表 9.9.2 挂载 USB 盘
  - `sudo strace mount /dev/sda1 /mnt 2>&1 | grep mount`

超级块处理整个文件系统的 VFS 交互。单个文件使用名为 `inodes` 和 `dentries` 的结构进行处理，这些结构将在后续章节中介绍。

## 9.10 Inodes

`inode`（索引节点，即 index node）是支撑 Linux 文件系统的核心数据结构。文件系统中的每个实体（例如文件或目录）都有一个 `inode`。你可以通过 `linux/fs.h` 中的 VFS 源码来研究 `struct inode` 的定义。图 9.9 显示了 `inode` 数据结构的简化类视图。

图 9.9：`inode` 数据结构的类图表示。

每个 `inode` 存储了与文件相关的所有元数据，包括文件数据的身份标识符位置信息。典型的元数据项（例如所有者、文件大小和权限）直接存储在结构体中。扩展元数据（例如用于增强安全性的访问控制列表）存储在外部，并在 `inode` 结构中使用指针引用。

# 第 9 章 | 持久化存储

如前所述，`inode` 是 VFS 级别的内存数据结构。其他 Unix 操作系统将这些结构称为 `vnodes`。具体文件系统拥有 `inode` 的特化版本。例如，比较 `include/linux/fs.h` 中的 VFS `struct inode` 定义与 `fs/ext4/ext4.h` 中的 ext4 变体 `struct ext4_inode` `struct ext4_inode_info`。

`inode` 除了是内存数据结构外，还会序列化到磁盘。文件系统上的 `inode` 有固定数量。条目数量有一个限制，因为每个条目都需要一个 `inode`。

### 9.10.1 多重链接

文件名仅仅是指向 `inode` 的指针（硬链接）。多个文件名映射到同一个 `inode`。引用计数随 `ln` 命令增加，随 `rm` 命令减少。当引用计数达到零时，该 `inode` 就会变成孤立节点并可能被删除。

### 9.10.2 目录

从抽象上讲，目录是一个键值存储或字典。它将文件系统实体名称（字符串）关联到 `inode` 编号（整数）。系统对实体名称的长度有限制，最多 255。使用 `getconf NAME_MAX /` 来确认，如果你尝试创建一个超过此限制的文件名，将因“文件过长”错误而失败。

VFS 不对单个目录的条目数量设置限制。目录条目的唯一限制是每个条目都需要一个 `inode`，而文件系统上的 `inode` 数量是固定的。(`df -i` 检查空闲 `inode` 的数量。)

每个目录有两个特殊的条目，即 `.`（读作 dot）和 `..`（读作 dot dot）。

- `.` 指向目录本身，即它是引用图中的自环。`cd` 命令实际上是一个空操作。
- `..` 指向父目录。`cd ..` 命令允许我们遍历目录层次结构到达根目录 `/`。注意根目录的父目录是根目录本身，即根的父节点也是引用图中的自环。

每个进程都有一个当前工作目录（`cwd`）。例如，你可以通过 `pwd` 命令发现 bash 进程的工作目录，或者通过执行命令 `readlink /proc/n/cwd` 来获取 PID 为 `n` 的任意进程的工作目录。相对路径名（即不以根目录 `/` 开头的路径）相对于进程当前的工作目录进行解释。

绝对路径名（即以根目录 `/` 开头的路径）是基于从 VFS 系统根目录开始的文件路径。请注意，路径可能会跨越具体的文件系统，这些文件系统相对于 VFS 根目录在不同的偏移处挂载。

目录提供的关键功能之一是将文件名字符串映射到 `inode` 节点。图 9.10 所示的算法是该转换过程的高级概述。你可以在命令行上通过 `namei` 工具并带有文件名参数来调用此行为。

文件名字符串到 `inode` 节点号的转换是一项耗费资源的操作。一种称为目录项（`dentry`）的数据结构存储了这种映射。`struct dentry` 的定义在 `include/linux/dcache.h` 中。VFS 拥有一个目录缓存（`dcache`），用于处理频繁使用的转换。该缓存在内核文档中有详细描述，请参阅 `Documentation/filesystems/vfs.txt`，以及其他 VFS 结构和机制。

## 9.11 ext4

扩展文件系统是 Linux 的原生文件系统格式。目前的实现是 `ext4`，尽管它与早期的 `ext2` 和 `ext3` 版本有许多共同点。

查看文件 `/etc/fstab`，它显示了作为操作系统启动序列一部分挂载（即从根目录可访问）的文件系统。在你的树莓派系统中，默认文件系统格式化为 `ext4`，并直接挂载在根目录。

### 9.11.1 磁盘上的布局

文件系统在磁盘（或磁盘分区）上的布局被称为其格式。对于任何格式，第一个块总是启动块（boot block）。它可能包含可执行代码，在这种情况下，磁盘被用作启动设备。通常，这种启动代码序列非常短，并跳转到另一个位置以执行更大、更复杂的启动行为。

启动块块之后，`ext4` 有若干块组（block groups）。每个块组的大小和结构都是相同的；图 9.11 描述了单个块组。

| 超块 | 块组描述符 | 数据块位图 | inode 位图 | inode 节点表 | 数据块 |
|---|---|---|---|---|---|

| | | 11010 | 110110 | was_inode_table was_inode_table | X Y Z |

图 9.11：显示磁盘上 `ext4` 块组结构的示意图。

块组的前两个元素位于距离块组起始位置的固定偏移处。超块记录了高层文件系统元数据，如文件系统的总大小、每个块的大小、每个块组的块数、指向设备的设备指针，以及最近挂载和写入操作的时间戳。`struct ext4_super_block` 定义在 `fs/ext4/ext4.h` 中。注意，超块在磁盘上仅占用一个块。此磁盘上的超块自第 9.9.1 节概述的 VFS 内存超块结构，尽管它们之间共享部分数据。

理想情况下，超块在每个块组的开头都会复制一份。这在磁盘损坏时提供了冗余。如果有许多块组，则超块会在每隔 $n$ 个块组的开头稀疏地复制。
