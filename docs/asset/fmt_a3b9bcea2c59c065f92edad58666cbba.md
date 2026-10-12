
VFS 使用此函数将指定文件的扩展属性 `name` 的值复制到 `value` 中。

`ssize_t listxattr(struct dentry *dentry, char *list, size_t size)`

将指定文件的所有属性列表复制到缓冲区 `list` 中。

`int removexattr(struct dentry *dentry, const char *name)`

从给定文件中移除给定的属性。

## Dentry 对象

如前所述，VFS 将目录视为一种文件类型。在路径 `/bin/vi` 中，`bin` 和 `vi` 都是文件——`bin` 是特殊的目录文件，而 `vi` 是普通文件。每个组件都由一个 inode 对象表示。尽管这种统一性很有用，但 VFS 经常需要执行特定的目录操作，例如路径名查找。路径名查找涉及将路径的每个组件进行转换，确保其有效，并跟随它进入下一个组件。

为了便于此操作，VFS 采用了目录项（`dentry`）的概念。`dentry` 是路径中的一个特定组件。使用上面的例子，`/`、`bin` 和 `vi` 都是 `dentry` 对象。前两个是目录，最后一个是普通文件。这是一个重要的点：`Dentry` 对象是路径中的*所有*组件，包括文件。解析路径并遍历其组件是一项非平凡的练习，耗时长且涉及大量的字符串操作，这些操作执行成本高且编码繁琐。`dentry` 对象使整个过程变得更加容易。

`Dentry` 也可能包括挂载点。在路径 `/mnt/cdrom/foo` 中，组件 `/`、`mnt`、`cdrom` 和 `foo` 都是 `dentry` 对象。VFS 在执行目录操作时，会按需即时构建 `dentry` 对象。

`Dentry` 对象由 `struct` `dentry` 表示，并定义在 `<linux/dcache.h>` 中。以下是该结构，其中注释描述了每个成员：

```c
struct dentry {
    atomic_t                    d_count;	/* usage count */
    unsigned int                d_flags;	/* dentry flags */
    spinlock_t                  d_lock;	/* per-directory lock */
    int                         d_mounted;	/* is this a mount point? */

    struct inode                *d_inode;	/* associated inode */
    struct hlist_node           d_hash;	/* list of hash table entries */
    struct dentry               *d_parent;	/* dentry object of parent */
    struct qstr                 d_name;	/* entry name */
    struct list_head            d_lru;	/* unused list */
    union {
        struct list_head        d_child;	/* list of dentries within */
        struct rcu_head         d_rcu;	/* RCU locking */
    } d_u;
    struct list_head            d_subdirs;	/* subdirectories */
    struct list_head            d_alias;	/* list of alias inodes */
    unsigned long               d_time;	/* revalidate time */
    struct dentry_operations    *d_op;	/* dentry operations table */
    struct super_block          *d_sb;	/* superblock of file */
    void                        *d_fsdata;	/* filesys-specific data */
    unsigned char               d_name[DNASE_INLINE_LEN_MIN]; /* short name */
};
```

与前面的两个对象不同，`dentry` 对象不对应任何类型的磁盘数据结构。VFS 从路径名的字符串表示即时创建它。由于 `dentry` 对象不物理存储在磁盘上，`struct dentry` 中的任何标志位都不指定该对象是否已修改（即，它是否脏化且需要写回磁盘）。

## Dentry 状态

有效的 `dentry` 对象可以处于三种状态之一：已使用、未使用或负值。

已使用的 `dentry` 对应于一个有效的 inode（`d_inode` 指向关联的 inode），并表明该对象有一个或多个使用者（`d_count` 为正）。已使用的 `dentry` 正被 VFS 使用，指向有效数据，因此不能被丢弃。

未使用的 `dentry` 对应于一个有效的 inode（`d_inode` 指向一个 inode），但 VFS 当前未使用该 `dentry` 对象（`d_count` 为零）。由于 `dentry` 对象仍指向一个有效对象，`dentry` 会被保留——缓存——以备再次需要。由于 `dentry` 未被过早销毁，如果未来需要它，则无需重新创建，路径名查找可以比 `dentry` 未缓存时完成得更快。然而，如果需要回收内存，由于该 `dentry` 未处于活跃使用状态，因此可以丢弃它。

负值 `dentry` 未关联到一个有效的 inode（`d_inode` 为 `NULL`），因为要么 inode 已被删除，要么路径名一开始就无效。然而，该 `dentry` 会被保留，以便未来查找能快速解析。例如，考虑一个守护进程，它不断尝试打开并读取一个不存在的配置文件。`open()` 系统调用持续返回 `ENOENT`，但这发生在内核构建路径、遍历磁盘目录结构并验证文件不存在之后。即使这种失败的查找也很昂贵，缓存“负值”结果也是值得的。虽然负值 `dentry` 很有用，但如果内存不是主要关切因素，因为它实际上没有被任何东西使用，所以它可以被销毁。

`dentry` 对象也可以被释放，驻留在 slab 对象缓存中，如前一章所述。在这种情况下，任何 VFS 或文件系统代码中都没有指向 `dentry` 对象的有效引用。

## Dentry 缓存

当 VFS 层费力将路径名中的每个元素解析为 `dentry` 对象并到达路径的末尾后，丢弃所有这些工作将是相当浪费的。相反，内核在 `dentry` 缓存或简称为 `dcache` 中缓存 `dentry` 对象。

`dentry` 缓存由三部分组成：

-   通过 inode 对象的 `i_dentry` 字段与其关联 inode 链接的“已使用”`dentry` 列表。由于给定的 inode 可以有多个链接，因此可能存在多个 `dentry` 对象；因此，使用了一个列表。

-   未使用和负值 `dentry` 对象的双向“最近最少使用”列表。列表插入在头部，使得靠近列表头部的条目比靠近尾部的条目更新。当内核必须移除条目以回收内存时，条目从尾部移除；那些是最旧的，据信在近期被使用的可能性最小。

-   用于快速将给定路径解析为关联 `dentry` 对象的哈希表和哈希函数。

哈希表由 `dentry_hashtable` 数组表示。每个元素是指向哈希值相同的 `dentry` 列表的指针。此数组的大小取决于系统中的物理 RAM 数量。

实际的哈希值由 `d_hash()` 确定。这使得文件系统能够提供唯一的哈希函数。

哈希表查找通过 `d_lookup()` 执行。如果在 `dcache` 中找到匹配的 `dentry` 对象，则返回该对象。失败时，返回 `NULL`。

作为一个例子，假设你正在你的主目录 `/home/dracula/src` 中编辑一个源文件 `the_sun_sucks.c`。每次访问该文件时（例如，当你最初打开它，稍后保存它，编译它等），VFS 必须跟随每个目录项以解析完整路径：`/`、`home`、`dracula`、`src`，最后是 `the_sun_sucks.c`。为了避免每次访问该路径名时进行这种耗时操作，VFS 可以首先尝试在 `dentry` 缓存中查找路径名。如果查找成功，则无需太多努力即可获取所需的最终 `dentry` 对象。相反，如果 `dentry` 不在 `dentry` 缓存中，VFS 必须通过遍历文件系统中的路径的每个组件来手动解析路径。完成此任务后，内核将 `dentry` 对象添加到 `dcache` 中，以加速任何未来的查找。
