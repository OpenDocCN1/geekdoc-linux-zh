
```c
struct hlist_head i_list;        /* 链表 */

struct hlist_node i_dentry;      /* dentry 链表 */

unsigned long     i_ino;        /* inode 号 */

atomic_t          i_count;      /* 引用计数 */

umode_t           i_mode;       /* 访问权限 */

unsigned int      i_nlink;      /* 硬链接数 */

uid_t             i_uid;        /* 所有者用户 ID */

gid_t             i_gid;        /* 所有者组 ID */

dev_t             i_dev;        /* 设备 */

loff_t            i_size;       /* 文件大小 */

};
```

文件本身的一部分。某些现代文件系统还使用数据库存储文件数据。无论什么情况，inode 都以适用于文件系统的方式构建。

```c
struct inode {
    struct timespec    i_atime;       /* 最后访问时间 */
    struct timespec    i_mtime;       /* 文件创建时间 */
    unsigned int       i_blksize;     /* 块大小（字节） */
    unsigned int       i_blocks_size; /* 块大小 */
    unsigned long      i_version;     /* 版本号 */
    unsigned long      i_blocks;      /* 文件大小（块） */
    spinlock           i_lock;        /* 字段 */
    struct inode       i_sem;         /* 信号量 */
    struct inode_operations i_inode;   /* inode 操作表 */
    struct file_operations i_fop;     /* 文件操作 */
    struct file_lock   i_sb;          /* 关联的超块 */
    struct file_lock   i_mapping;     /* 文件锁列表 */
    struct address_space i_bd;        /* 备地址空间 */
    struct address_space i_data;      /* 设备地址空间 */
    struct dentry      i_dquot[MAXQUOT]; /* dentry 磁盘配额 */
    struct inode       i_head;        /* 设备列表 */
    struct pipe_inode_info i_pipe;    /* 块设备驱动 */
    unsigned int       i_version;     /* 管道信息 */
    struct stat        i_stat;        /* 目录事件 */
    unsigned int       i_mode;        /* 目录通知 */
    unsigned int       i_flags;       /* 文件系统标志 */
    unsigned char      i_sock;        /* 是否为 socket */
    atomic_t           i_count;       /* 写入计数器 */
    void               i_security;    /* 安全模块 */
    uid32              i_generation;  /* inode 版本号 */
    union {
        void               *generic_ip; /* 文件系统特有信息 */
    };
};
```

## Inode 操作

特定的文件系统可能不支持 inode 对象中表示的属性。例如，某些文件系统可能不会创建时间戳。在这种情况下，文件系统可以自由实现它认为合适的功能；或者将`i_ctime`存储为零，让`i_ctime`等于`i_mtime`，或者任何它认为方便的方式。

与超级块（`superblock`）一样，`node_operations`非常重要，因为它描述了`VFS`可以在`inode`上调用的文件系统实现函数。与超级块一样，`node`操作通过以下方式被调用：

```
i->truncate(i)
```

其中`i`是指向特定`inode`的引用。在这种情况下，`truncate`操作在`i`存在且被调用的文件系统上运行。`inode_operations`结构定义在`<linux/fs.h>`中。

```c
struct inode_operations {
    int truncate(struct inode *inode, struct dentry *dentry, int mode);
    struct dentry *lookup(struct inode *inode, struct dentry *dentry);
    int (*link)(struct inode *inode, struct dentry *dentry);
    int (*symlink)(struct inode *inode, struct dentry *dentry, const char *name);
    int (*rmdir)(struct inode *inode, struct dentry *dentry);
    int (*knewdir)(struct inode *inode, struct dentry *dentry, dev_t dev);
    int (*create)(struct inode *inode, struct dentry *dentry, int mode);
    int (*readlink)(struct dentry *dentry, char *buf, int count);
    int (*follow_link)(struct dentry *dentry, struct nameidata *nameidata);
    void (*unlink)(struct dentry *inode);
    int (*permission)(struct inode *inode, int mode);
    int (*setattr)(struct dentry *dentry, struct inode *inode, struct kstat *atp);
    int (*chown)(struct dentry *dentry, struct inode *inode, const void *attr, size_t size);
    int (*setxattr)(struct dentry *dentry, const char *name, const void *value, size_t size);
    ssize_t (*listxattr)(struct dentry *dentry, char *list, size_t size);
    int (*removexattr)(struct dentry *dentry, const char *name);
};
```
