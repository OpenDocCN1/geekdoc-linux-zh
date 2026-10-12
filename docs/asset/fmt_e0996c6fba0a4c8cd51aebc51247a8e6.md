
```
};
```

方法如下：

- `int d_revalidate(struct dentry *dentry, struct nameidata *)`：确定给定的 dentry 是否有效。当 VFS 准备使用 dache 中的 dentry 时，调用此函数。大多数文件系统将此方法设置为 `NULL`，因为它们在 dache 中的 dentries 总是有效的。

- `int d_hash(struct dentry *dentry, struct gstr *name)`：从给定的 dentry 创建哈希值。当 VFS 将 dentry 添加到哈希表时，调用此函数。

- `int d_compare(struct dentry *dentry, struct gstr *name1, struct gstr *name2)`：由 VFS 调用比较两个文件名 `name1` 和 `name2`。大多数文件系统将其交给 VFS 默认处理，即简单的字符串比较。对于某些文件系统（如 FAT），简单的字符串比较是不够的。FAT 文件系统是对大小敏感的，因此需要实现一个忽略大小的比较函数。此函数需要 `dache_lock`。

- `int d_delete(struct dentry *dentry)`：当指定的 dentry 对象的 `d_count` 达到零时，由 VFS 调用。此函数需要 `dache_lock` 和 dentry 的 `d_lock`。

- `void d_release(struct dentry *dentry)`：当指定的 dentry 将被释放时，由 VFS 调用。默认函数什么都不做。

## 文件对象 279

```c
void d_iput(struct dentry *dentry, struct inode *inode)
```

当 dentry 对象丢失其关联的 inode 时（例如，条目从磁盘上被删除），VFS 会调用此函数。默认情况下，VFS 仅调用 `iput()` 函数来释放 inode。如果文件系统覆盖了此函数，它必须在执行所需的任何系统特有工作之外，额外调用 `iput()`。

## 文件对象

我们将看到的最后一个 VFS 对象是文件对象（file object）。文件对象用于表示由进程打开的文件。当我们从用户的角度考虑 VFS 时，脑海中浮现的就是文件对象。进程直接处理文件，而不涉及超块（superblocks）、inode 或 dentry。文件对象中的信息是最熟悉的（如访问模式和当前偏移量），文件操作也是如 `read()` 和 `write()` 这样的系统调用，这并不意外。

文件对象是打开文件的内存表示。该对象（而非物理文件）通过 `open()` 系统调用在进程中创建，并通过 `close()` 系统调用在进程中销毁。所有与文件相关的调用实际上都是操作表（operations table）中定义的方法。由于多个进程可以同时打开并操作同一个文件，同一个文件可能存在多个文件对象。文件对象代表了进程对打开文件的视图。该对象指向实际代表该打开文件的 dentry（而 dentry 再次指向 inode）。当然，inode 和 dentry 对象是唯一的。

文件对象由 `struct file` 表示，定义在 `<linux/fs.h>` 中。让我们来看该结构体，并添加了注释来描述每个条目：

```c
struct file {
    union {
        struct list_head f_list;      /* 文件对象列表 */
        struct rcu_head f_ruhead;     /* 释放后的 RCU 列表 */
    } f;
    struct path path;
    struct file_operations f_op;   /* 文件操作表 */
    spinlock_t f_lock;               /* 每个文件的结构锁 */
    atomic_t f_count;               /* 文件对象的引用计数 */
    unsigned int f_flags;           /* open 时指定的标志 */
    mode_t f_mode;                   /* 文件访问模式 */
    loff_t f_pos;                      /* 文件偏移（文件指针） */
    struct fown_struct f_owner;     /* 用于信号的所有者数据 */
    const struct cred *f_cred;      /* 凭证 */
    struct file_ra_state *f_ra;      /* 预读状态 */
    u64 f_version;                   /* 版本号 */
    void *f_security;              /* 安全模块 */
    void *private_data;             /* tty 驱动钩子 */
};
```

## 第 13 章 虚拟文件系统

```c
struct list_head      f_ep_links;      /* epoll 链接列表 */
spinlock_t           f_ep_lock;       /* epoll 锁 */
struct address_space *f_mapping;     /* 页缓存映射 */
unsigned long         f_mnt_write_state; /* 调试状态 */
```

与目录类似，文件对象实际上并不对应于任何磁盘数据。因此，对象中没有哪个标志表示该对象是否为“脏”的并需要写回磁盘。文件对象通过 `f_dentry` 指针指向其关联的 dentry。dentry 指向关联的 inode，这反映了文件本身是否是脏的。

## 文件操作

与所有其他 VFS 对象一样，文件操作表非常重要。与 `struct file` 关联的操作是构成标准 Unix 系统的系统调用。

对象方法在 `file_operations` 中指定，并定义在 `<linux/fs.h>` 中：

```c
struct file_operations {
    struct module *owner;
    loff_t (*llseek) (struct file *, char __user, loff_t *pp);
    ssize_t (*read) (struct file *, char __user, size_t, loff_t);
    ssize_t (*write) (struct file *, const char __user, size_t, loff_t);
    ssize_t (*aio_read) (struct kiocb *, const struct iovec *, unsigned long, loff_t);
    ssize_t (*aio_write) (struct kiocb *, const struct iovec *, unsigned long, loff_t);
    int (*readdir) (struct file *, void *, struct filldir_t *);
    int (*poll) (struct file *, struct poll_table_struct *);
    int (*ioctl) (struct inode *, struct file *, int, unsigned long);
    long (*locked_ioctl) (struct file *, unsigned int, unsigned long);
    long (*compat_ioctl) (struct file *, unsigned int, unsigned long);
    int (*mmap) (struct file *, struct vm_area_struct *);
    int (*open) (struct inode *, struct file *);
    int (*flush) (struct file *, struct f_owner_id);
    int (*release) (struct inode *, struct file *);
    int (*fsync) (struct dentry *, int datasync);
    int (*aio_fsync) (struct kiocb *, int datasync);
    int (*fdatync) (struct dentry *, int datasync);
    int (*count) (struct file *);
```
