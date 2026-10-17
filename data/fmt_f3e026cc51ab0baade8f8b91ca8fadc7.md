
`struct quotact_ops` `*s_qcop;` `/* quota control methods */`

`struct export_operations` `*s_export_op;` `/* export methods */`

`unsigned long` `s_flags;` `/* mount flags */`

`unsigned long` `s_magic;` `/* filesystem's magic number */`

`struct dentry` `*s_root;` `/* directory mount point */`

`struct rw_semaphore` `s_umount;` `/* unmount semaphore */`

`struct semaphore` `s_lock;` `/* superblock semaphore */`

`int` `s_count;` `/* superblock ref count */`

`int` `s_need_sync;` `/* not-yet-synced flag */`

`atomic_t` `s_active;` `/* active reference count */`

`void` `*s_security;` `/* security module */`

`struct xattr_handler` `**s_xattr;` `/* extended attribute handlers */`

```
};
```

## 超级块操作

超级块对象中最重要的项是 `s_op`，它是指向超级块操作表的指针。超级块操作表由 `struct super_operations` 表示，并定义在 `<linux/fs.h>` 中。其结构如下：

```c
struct super_operations {
    struct inode *(*alloc_inode)(struct super_block *sb);
    void (*destroy_inode)(struct inode *);
    void (*dirty_inode)(struct inode *);
    int (*write_inode)(struct inode *, int);
    void (*drop_inode)(struct inode *);
    void (*delete_inode)(struct inode *);
    void (*put_super)(struct super_block *);
    void (*write_super)(struct super_block *);
    int (*sync_fs)(struct super_block *sb, int wait);
    int (*freeze_fs)(struct super_block *);
    int (*unfreeze_fs)(struct super_block *);
    int (*statfs) (struct dentry *, struct kstatfs *);
    int (*remount_fs) (struct super_block *, int, char *);
    void (*clear_inode) (struct inode *);
    void (*umount_begin) (struct super_block *);
    int (*show_options)(struct seq_file *, struct vfsmount *);
    int (*show_stats)(struct seq_file *, struct vfsmount *);
    ssize_t (*quota_read)(struct super_block *, int, char *, size_t, loff_t);
    ssize_t (*quota_write)(struct super_block *, int, const char *, size_t, loff_t);
    int (*bdv_try_to_free_page)(struct super_block*, struct page*, gfp_t);
};
```

创建、管理和销毁超级块对象的代码位于 `fs/super.c` 中。超级块对象通过 `alloc_super()` 函数创建并初始化。在挂载时，文件系统会调用此函数，从磁盘读取其超级块，并填充其超级块对象。

该结构中的每一项都是指向操作超级块对象的函数的指针。超级块操作对文件系统及其 inode 执行底层操作。

当文件系统需要对其超级块执行操作时，它会沿着其超级块对象中的指针找到所需的方法。例如，如果文件系统希望写入其超级块，它会调用：

```c
sb->s_op->write_super(sb);
```

在此调用中，`sb` 是指向文件系统超级块的指针。沿着该指针进入 `s_op` 即可得到超级块操作表，并最终找到所需的 `write_super()` 函数，然后对其进行调用。请注意，尽管该方法与某个超级块相关联，但调用 `write_super()` 时必须传入超级块参数。这是因为 C 语言缺乏面向对象的支持。在 C++ 中，像下面这样的调用就足够了：

```c
sb.write_super();
```

在 C 语言中，方法无法轻松获取其父对象，因此必须显式传入。让我们来看看 `super_operations` 中规定的部分超级块操作：

- `struct inode * alloc_inode(struct super_block *sb)`
  - 在指定的超级块下创建并初始化一个新的 inode 对象。

- `void destroy_inode(struct inode *inode)`
  - 释放给定的 inode。

- `void dirty_inode(struct inode *inode)`
  - 当 inode 被弄脏（修改）时由 VFS 调用。ext3 和 ext4 等日志文件系统使用此函数执行日志更新。

- `void write_inode(struct inode *inode, int wait)`
  - 将给定的 inode 写入磁盘。`wait` 参数指定操作是否应该是同步的。

- `void drop_inode(struct inode *inode)`
  - 当 inode 的最后一个引用被丢弃时由 VFS 调用。普通的 Unix 文件系统不定义此函数，在这种情况下，VFS 直接删除该 inode。

- `void delete_inode(struct inode *inode)`
  - 从磁盘删除给定的 inode。

- `void put_super(struct super_block *sb)`
  - 在卸载时由 VFS 调用以释放给定的超级块对象。调用者必须持有 `s_lock` 锁。

- `void write_super(struct super_block *sb)`
  - 使用指定的超级块更新磁盘上的超级块。VFS 使用此函数将已修改的内存中的超级块与磁盘同步。调用者必须持有 `s_lock` 锁。

- `int sync_fs(struct super_block *sb, int wait)`
  - 将文件系统元数据与磁盘上的文件系统同步。`wait` 参数指定操作是否同步。

- `void write_super_lockfs(struct super_block *sb)`
  - 防止对文件系统进行更改，然后使用指定的超级块更新磁盘上的超级块。目前由 LVM（逻辑卷管理器）使用。

- `void unlockfs(struct super_block *sb)`
  - 解除由 `write_super_lockfs()` 施加的防止文件系统更改的限制。

- `int statfs(struct super_block *sb, struct statfs *statfs)`
  - 由 VFS 调用以获取文件系统统计信息。与给定文件系统相关的统计信息被放置在 `statfs` 中。

- `int remount_fs(struct super_block *sb, int *flags, char *data)`
  - 当文件系统使用新的挂载选项重新挂载时由 VFS 调用。调用者必须持有 `s_lock` 锁。

- `void clear_inode(struct inode *inode)`
  - 由 VFS 调用以释放 inode 并清除包含相关数据的所有页面。
