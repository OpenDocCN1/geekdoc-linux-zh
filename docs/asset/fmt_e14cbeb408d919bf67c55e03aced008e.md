
struct `super_block` `(*get_sb)` (`struct file_system_type *`, `int`, `char *void`);

```c
struct super_block (*get_sb) (struct file_system_type *, int, char *void);
```

/* 这是一个用于终止超级块的函数 */

```c
void (*kill_sb) (struct super_block *);
```

`struct module {`

    `struct module *owner;`                /* 关联的模块（如果有） */

    `struct file_system_type *next;`    /* 列表中的下一个 `file_system_type` */

    `struct list_head fs_superblock;`  /* 超级块对象列表 */

`};`

```c
struct module {
    struct module *owner;                /* 关联的模块（如果有） */
    struct file_system_type *next;        /* 列表中的下一个 file_system_type */
    struct list_head fs_superblock;       /* 超级块对象列表 */
};
```

`get_sb` 函数用于读取超级块并在加载时填充超级块。其余函数描述了文件系统的属性。

每个文件系统只有一个 `file_system_type`，无论在其上挂载了多少个实例，或者该文件系统是否是否被挂载。

当文件系统实际挂载时，情况变得更有趣，此时会创建 `vfsount` 结构。该结构用于表示文件系统的特定实例。

`vfsount` 结构定义在 `<linux/mount.h>` 中。在这里：

```c
struct vfsount {
    struct list_head      hash;           /* 哈希表列表 */
    struct vfsount       *mnt_parent;   /* 父文件系统 */
    struct dentry         *mnt_mountpoint; /* 此文件系统根目录的 dentry */
    struct dentry         *dentry;
    struct super_block    *sb;             /* 此文件系统的超级块 */
    struct list_head      mnt_child;      /* 子节点列表 */
    struct list_head      list_head;       /* 父级子节点 */
    atomic_t              mnt_count;      /* 使用计数 */
    int                   mnt_flags;      /* 挂载标志 */
    char                  *mnt_devname;   /* 设备文件名 */
    struct list_head      mnt_list;       /* 描述符列表 */
};
```

维护所有挂载点列表的复杂部分在于文件系统与其他挂载点之间的关系。`vfsount` 的各种链表跟踪了这种关系。

`vfsount` 结构还存储挂载在 `mnt_flags` 字段上的标志（如果有）。表 11.1 是这些标志的列表。

## 表 11.1 挂载标志列表

| 标志 | 描述 |
| --- | --- |
| `MNT_NOSUID` | 禁止二进制文件上的 `setuid` 和 `setgid` 标志 |
| `MNT_NODEV` | 禁止访问设备文件 |
| `MNT_NOEXEC` | 禁止执行二进制文件 |

与进程相关的结构是 `fs_struct`，它包含了与进程相关的文件系统信息，并由进程描述符中的 `fs` 字段指向。该结构定义在 `<linux/fs_struct.h>` 中。以下是其定义及注释：

```c
struct fs_struct {
    int count;                  /* 使用计数 */
    atomic_t lock;              /* 保护结构的锁 */
    rwlock_t umask;             /* 默认文件权限 */
    struct dentry *root;        /* 根目录入口 */
    struct dentry *pwd;         /* 当前工作目录入口 */
    struct dentry *rootroot;     /* 备根目录入口 */
    struct vfsm_mount *root;    /* 根目录的挂载对象 */
    struct vfsm_mount *pwdmnt;  /* 当前目录的挂载对象 */
    struct vfsm_mount *altroot; /* 备根目录的挂载对象 */
};
```

该结构保存了当前进程的当前目录和根目录。

第三也是最后一个结构是 `namespace_structure`，它定义在 `<linux/namespace.h>` 中，并由进程描述符中的 `namespace` 字段指向。进程命名空间是在 `Linux` `2.4` 内核中引入的。它们允许每个进程对挂载的文件系统拥有独特的视图——如果需要，不仅是一个目录，而是一个完全独特的文件系统层级。以下是该结构及其常用的注释：

```c
struct namespace {
    atomic_t count;             /* 使用计数 */
    struct vfsm_mount *root;    /* 根目录的挂载对象 */
    struct list_head list;      /* 挂载点列表 */
    struct rw_semaphore *sem;   /* 保护命名空间的信号量 */
};
