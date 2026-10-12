
`struct dentry *d_parent;` /* 父目录的 dentry 对象 */

`struct qstr *d_name;`

`struct hlist_node *d_hash;` /* 哈希表项列表 */

`struct hlist_head *d_bucket;` /* 哈希桶 */

`unsigned char d_name[DNAME_INLINE_LEN_MIN];` /* 短名称 */

```c
// 原文结尾处有一个多余的 ```，这里假设上述结构体代码块需要闭合
```

## Dentry 对象 223

与之前的两个对象不同，`dentry` 对象不对应于任何磁盘数据结构。VFS 根据路径名称的字符串表示动态创建它。由于 `dentry` 对象没有物理存储在磁盘上，因此 `struct dentry` 结构体中没有标志位可以指定该对象是否被修改过（即它是否为脏数据以及需要写入磁盘）。

## Dentry 状态

一个有效的 `dentry` 对象可能处于三种状态之一：已使用（used）、未使用（unused）或负（negative）。已使用的 `dentry` 对应于有效节点（`d_inode` 指向关联的节点），并表示该 `dentry` 有一个或多个用户（`d_count` 为正数）。已使用的 `dentry` 正被 VFS 使用并指向有效数据，因此不能被丢弃。未使用的 `dentry` 对应于有效节点（`d_inode` 指向一个 `inode`），但表示 VFS 当前没有使用该 `dentry` 对象（`d_count` 为 0）。该 `dentry` 仍然指向一个有效对象——以备后之用。由于 `dentry` 没有被过早销毁，如果将来需要且路径查找完成，则该 `dentry` 可能不需要重新创建。然而，如果需要回收内存，可以丢弃该 `dentry`，因为它未被使用。负 `dentry` 不关联到任何有效节点（`d_inode` 为 NULL），因为该节点已被删除，或者该路径名称根本从未被创建。保留该 `dentry` 是为了快速解析未来的名称查找。虽然 `dentry` 很有用，但如果需要，它可以被销毁，因为实际上没有程序在在使用它。`dentry` 对象也可以被释放，并存放在 slab 对象缓存（slab object cache）中，如前一章所述。在这种情况下，任何 VFS 或文件系统代码中都没有对该 `dentry` 对象的有效引用。

## Dentry 缓存

在 VFS 层费力将路径名称中的每个元素解析为 `dentry` 对象并到达路径末尾后，丢弃所有工作将是浪费。相反，内核将 `dentry` 对象缓存在 dentry 缓存（dentry cache）中，或者简单地称为 `d`。

这个名称具有误导性。负 `dentry` 并没有特殊的负面含义。更好的名称可能是无效 `dentry`（invalid dentry）。

## 第12 章 虚拟文件系统

`dentry` 缓存由三部分组成：

- “已使用”`dentry` 的列表，它们通过 `inode` 对象的 `i_dentry` 字段与其关联的 `inode` 链接。由于一个特定的 `inode` 可以有多个链接，可能存在多个 `dentry` 对象；因此使用了列表。
- 一个由未使用和负 `dentry` 对象组成的双向链“最近最少使用”（LRU）列表。该列表按时间进行插入排序，使得列表头部的项是最新的。当内核必须移除项以回收内存时，会从尾部移除；这些是最旧的，且假设在不久将来使用的概率最低。
- 一个哈希表和一个哈希函数，用于快速将路径解析为关联的 `dentry` 对象。

哈希表由 `dentry hashtable` 数组表示。每个元素都是指向具有相同哈希值的 `dentry` 列表的指针。该数组的大小取决于系统中物理内存量。

实际的哈希值由 `d_hash()` 确定。这允许文件系统提供唯一的哈希函数。

哈希表查找通过 `d_lookup()` 执行。如果在 `dcache` 中找到匹配的 `dentry` 对象，则返回它。

作为一个例子，假设你正在编辑主目录下的源文件 `/home/dracula/src/the_sucks.c`。每当访问此文件时（例如，第一次打开它、之后保存它、编译它等），VFS 必须遵循每个目录条目以解析完整路径：`/home`、`dracula`、`src` 以及最后的 `.`（此处）。为了避免每次访问路径名称时都进行这种耗时的操作，VFS 可以首先尝试在 dentry 缓存中查找路径名称。如果查找成功，则不费力即可获取所需的最终 `dentry` 对象。相反，如果 `dentry` 不在 `dcache` 中，VFS 必须通过遍历路径的每个分量来手动解析路径。任务完成后，内核会将 `dentry` 对象添加到 `dcache` 中，以加速未来的查找。

`dcache` 还提供了 `inode` 缓存（`icache`）的前端。与 `dentry` 对象关联的 `inode` 不会被释放，因为 `dentry` 对 `inode` 保持着正计数。这使得 `dentry` 能将 `inode` 钉在内存中。当 `dentry` 被缓存时，相应的 `inode` 也会被缓存。因此，当从缓存成功查找路径名称时（如前面的示例所示），关联的 `inode` 已经在内存中了。

## Dentry 操作

`dentry_operations` 结构指定了 VFS 为给定目录条目调用的方法……

## Dentry 对象 225

`dentry_operations` 结构定义在 `<linux/dcache.h>` 中：

```c
struct dentry_operations {
    int (*revalidate)(struct dentry *, int flags);
    int (*hash)(struct dentry *);
    int (*compare)(struct dentry *, struct dentry *);
    int (*delete)(struct dentry *);
    void (*release)(struct dentry *);
    void (*iput)(struct dentry *, struct inode);
};
```

这些方法是：

- `revalidate(struct dentry *, int flags)`：确定给定的 `dentry` 是否有效。VFS 在需要时调用此函数。
- `hash(struct dentry *)`：创建一个哈希值。VFS 在添加 `dentry` 时调用它。
- `compare(struct dentry *, struct dentry *)`：由 VFS 调用以比较两个文件名。
- `delete(struct dentry *)`：VFS 在计数归零时调用。
- `release(struct dentry *)`：当 `dentry` 被删除时由 VFS 调用。
- `iput(struct dentry *, struct inode)`：VFS 在失去其 `inode` 时调用。

## 文件对象

文件对象（file object）是打开文件的内存表示。它响应 `open()` 系统调用而创建，并响应 `close()` 系统调用而销毁。由于多个进程可以同时打开并操作一个文件，同一个文件可以有多个文件对象。文件对象指向表示文件的 `dentry`（`dentry` 再指向 `inode`）。

该对象由定义在 `<linux/fs.h>` 中的 `struct file` 表示。我们查看该结构，并添加了注释：

```c
struct file {
    struct list_head     list;               /* 文件对象列表 */
    struct dentry        dentry;            /* 关联的 dentry 对象 */
    struct vfs_mount      *fsmount;           /* 关联的挂载文件系统 */
    struct file_operations *op;             /* 文件操作 */
    atomic_t              f_count;           /* 文件对象的使用计数 */
    unsigned int          f_flags;            /* open 时指定的标志 */
    mode_t                f_mode;            /* 文件访问模式 */
    loff_t                f_pos;             /* 文件偏移量（文件指针） */
    struct fown_struct   f_owner;           /* 用于信号的所有者数据 */
    unsigned int          f_uid;              /* 用户 UID */
    unsigned int          f_gid;              /* 用户 GID */
    int                   f_error;           /* 错误码 */
};
```
