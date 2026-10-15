
# Dentry 对象（目录目项）

如前所述，VFS 将目录视为文件的一种类型。在路径 `/bin/vi` 中，`bin` 和 `vi` 都是文件——`bin` 是一个特殊的目录文件，而 `vi` 是普通文件。一个 `inode` 对象代表这些组件中的每一个。尽管有这种统一性，VFS 经常需要执行特定于目录的操作，例如路径名查找。路径涉及翻译路径的每个分量，确保其有效性，并跳转到下一个分量。

为了方便这种操作，VFS 使用了目录目项（dentry）的概念。dentry 是路径中的一个特定组件。使用之前的例子，`/bin/vi` 都是 dentry 对象。前两个是目录，最后一个是普通文件。这是一个重要的点：Dentries 包含了路径中的所有组件，包括文件。解析路径并遍历其组件是一项非凡的活动，既耗时又涉及大量操作，这些操作的执行开销很高且处理起来繁琐。dentry 对象让整个过程变得更加简单。

Dentries 可能包含挂载点。在路径 `/mnt/cdrom/foo` 中，组件 `/mnt`、`cdrom` 和 `foo` 都是 dentry 对象。VFS 会根据需要动态构建 dentries，并执行目录操作。

Dentry 由 `struct dentry` 结构体表示并定义在 `<linux/dcache.h>` 中。以下是该结构体，并附有描述每个部分的注释：

```c
struct dentry {
    atomic_t            d_count;      /* 使用计数 */
    unsigned int        d_flags;      /* dentry 标志 */
    spinlock_t          d_lock;       /* 每个目录的锁 */
    int                 d_mounted;    /* 这是一个挂载点？ */
    struct inode        d_inode;      /* 关联的 inode */
    struct list_head     d_hash;       /* 哈希条目列表 */
    struct dentry        d_parent;     /* 父级 dentry 对象 */
    struct qtree        d_name;       /* dentry 名称 */
    struct list_head     d_lru;        /* 未使用列表 */
    union {
        struct list_head d_child;    /* 目录中的子项 */
        struct list_head d_rcu;       /* RCU 链 */
    } d_u;
    struct list_head     d_subdirs;   /* 子目录 */
    struct list_head     d_aliases;   /* 别名 */
    unsigned long       d_time;      /* 时间 */
    struct dentry_operations d_op;  /* dentry 操作 */
    struct superblock *d_sb;        /* 超文件系统 */
    void                *d_data;      /* 数据 */
    char                d_name[DNAME_LEN]; /* 名称 */
    unsigned int        d_cored;      /* 核心标志 */
};
```

当指定的 dentry（目录项）即将释放时，由 VFS 调用。默认函数不执行任何操作。

## 文件操作接口

`void truncate(struct inode *inode)`

由 VFS 调用以修改给定文件的大小。在调用之前，必须将 `inode` 的 `i_size` 字段设置为所需的大小。

`int permission(struct inode *inode, int mask)`

检查 `.` 所引的文件是否允许指定的访问模式。如果允许访问，此函数返回 `0`，否则返回一个负数错误代码。大多数文件系统将此项设置为 `NULL` 并使用通用的 VFS 方法，该方法通过将 `inode` 对象中的模式位与给定的掩码进行比较。更复杂的文件系统（如支持访问控制列表 ACL 的文件系统）拥有特定的 `permission()` 方法。

`int setattr(struct dentry *dentry, struct inode *attr)`

由 `notify_change()` 调用，在 `inode` 被修改后通知一个“更改事件”。

`int getattr(struct vfsmount *mnt, struct dentry *dentry, struct kstat *stat)`

当 VFS 发现某个 `inode` 需要从磁盘刷新时被调用。扩展属性允许将键/值对与文件进行关联。

`int setxattr(struct dentry *dentry, const char *name, const void *value, size_t size, int flags)`

由 VFS 用于将 `dentry` 所引用的文件的扩展属性名称设置为某个值。

`ssize_t getattr(struct dentry *dentry, const char *name, void *value, size_t size)`

由 VFS 用于将特定文件的扩展属性值拷贝到 `value`。

`ssize_t listxattr(struct dentry *dentry, const char *list, size_t size)`

将指定文件的所有属性列表拷贝到缓冲区 `list` 中。

`int removexattr(struct dentry *dentry, const char *name)`

从给定文件中删除指定的属性。

## 文件对象 279

- `void d_iput(struct dentry *dentry, struct inode *inode)`
