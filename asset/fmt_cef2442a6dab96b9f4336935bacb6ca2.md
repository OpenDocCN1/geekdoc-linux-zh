
当 `vnode` 的引用计数降为 0 时，`VN_RELE()` 会调用该系统的 `VOP_INACTIVE()` 方法。每个引用 `vnode` 的子系统都必须在引用开始时调用 `VN_HOLD()`，并在每次引用结束时调用 `VN_RELE()`。文件系统在 `vnode` 引用计数降为零时决定处理它；如果需要，其他系统会保留 `vnode` 一段时间，使其处于构建好的可用状态。`UFS` 文件系统在最后一次释放后保留 `vnode` 一段时间，以便虚拟内存系统能够保留文件的 `inode` 和缓存，而 `PCFS` 文件系统则在调用 `VOP_INACTIVE()` 时释放 `vnode` 以及所有与 `vnode` 关联的缓存。

## 13.2.4 分页节点缓存的接口

Solaris 通过使用 `vnode` 表示虚拟内存的后备存储，从而统一了文件管理和内存管理。内存页代表一个特定的 `vnode` 和偏移量。文件系统利用内存关系来实现文件系统内 `inode` 的缓存。为了缓存 `vnode`，文件系统让内存系统创建一个物理内存页，该页代表该 `vnode` 及其偏移量。

虚拟内存系统提供了一组用于缓存管理和 I/O 的函数。

### 表 13-3 来自 `pvn.h` 的 Solaris 7 分页函数

| 函数 | 描述 |
| --- | --- |
| `pvn_getpage()` | 查询页是否为脏。如果是脏页则返回 1，否则返回 0。 |
| `pvn_plist_init()` | 释放页上的锁。 |
| `pvn_read_done()` | 写入后解锁页。对于异步写入，该函数通常由 `pageio_done()` 调用。对于同步写入，它由 `pageio_done()` 调用。 |
| `pvn_cluster()` | 查找连续的脏页范围。 |
| `pvn_write()` | 查找 `vfs` 层中所有的脏页。 |

## 13.2.5 vnode 上的块 I/O

块 I/O 子系统提供支持向 `vnode` 发起 I/O。表 13-4 所示的三个函数启动了页之间的 I/O。

### 表 13-4 来自 `bio.h` 的 Solaris 7 块 I/O 函数

| 函数 | 描述 |
| --- | --- |
| `bdev_strategy()` | 使用块设备启动页上的 I/O。 |
| `pageio_done()` | 等待 I/O 完成。 |
| `pageio_setup()` | 通过设置 `B_PAGEIO` 标志并将页列表放入 `b_pages` 字段，设置页上的 I/O。 |

## 13.3 vfs 对象

`vfs` 层为文件系统提供了管理接口，以支持挂载和卸载等命令。

### vfs 对象

接口通过虚拟文件系统（`vfs`）对象实现独立。`vfs` 对象表示文件系统状态的封装以及每个文件系统管理接口的方法集。每种文件系统类型都提供该对象的实现。图 13.3 展示了 `vfs` 对象。

![](img/6356e5c1a4c2ea1083732d1b35e8cf75_592_0.png)

表 13-5 列出了所有的 `vfs` 接口方法。

### 表 13-5 来自 `sys/vfs.h` 的 Solaris 7 vfs 接口方法

| 方法 | 描述 |
| --- | --- |
| `vfs_mount()` | 在提供的 `vnode` 上挂载文件系统。 |
| `vfs_unmount()` | 卸载系统。 |
| `vfs_root()` | 查找文件系统的根 `vnode`。 |
| `vfs_statfs()` | 查询文件系统缓存的统计信息。 |
| `vfs_sync()` | 刷新文件系统缓存。 |
| `vfs_get()` | 查找匹配唯一文件 ID 的 `vnode`。 |
| `vfs_mountroot()` | 在根目录上挂载文件系统。 |
| `vfs_swapvp()` | 未使用。 |

下面显示了 `vfs` 接口以及来自 `sys/vfs.h` 的相关结构。

- 每个挂载的文件系统结构包含一个操作数组和一个实例记录。
- 文件系统存储在一个单向链表中，以 "`rootvfs`" 为头，以 `NULL` 结尾。文件系统的实现程序不应访问此列表；该列表仅在内核的 `vfs` 层使用。

```c
typedef struct vfs {
    struct vfs             *vfs_next;
    struct vfs_op          *vfs_op;
    struct vnode          *vfs_nodecovered;
    uint_t               vfs_flags;
    uint_t               vfs_fstype;
    int                  vfs_file_type_index;
    int                  vfs_system_id;
    cadd_t               vfs_data;
    dev_t                vfs_dev;
    ulong_t              vfs_count;
    short_t              vfs_mounts;
    struct vfs           *vfs_list;
    struct vfs           *vfs_hash;
    ksema_t              vfs_reflock;
} vfs_t;
```

- 虚拟文件系统支持的操作。

```c
typedef struct vfsops {
    int  (*vfs_mount)(struct vfs *, struct vnode *, struct mount *);
    int  (*vfs_unmount)(struct vfs *, struct cred *);
    int  (*vfs_root)(struct vfs *, struct vnode **);
    int  (*vfs_statfs)(struct vfs *, struct statfs64 *);
    int  (*vfs_sync)(struct vfs *, short, struct cred *);
    int  (*vfs_getvid)(struct vfs *, struct vnode **, struct fid *);
    int  (*vfs_mountroot)(struct vfs *, struct vnode *, enum mountpoint);
    int  (*vfs_swapvp)(struct vfs *, struct vnode **, char *);
};
```

### 头文件 `<sys/vfs.h>`

## 13.3.1 文件系统切换表

下面所示的文件系统切换表是全范围文件系统类型表。加载到系统上的每种文件系统类型都可以在虚拟文件系统切换表中找到。文件系统切换表提供了文件系统名称（例如 `ufs`, `nfs`）的 ASCII 列表、初始化例程序以及该文件系统的 `vfs` 对象方法。`vfs` 对象的 `vfs_ftype` 字段是进入文件系统切换表的索引。

```c
/*
 * 文件系统类型切换。
 */
typedef struct vfssw {
    char *vfssw_name;      /* 类型名称字符串 */
    int (*vfssw_init) (struct vfssw, int);
    int              /* 初始化例程序 */
    struct vfsops *vfssw_vops;  /* 文件系统操作向量 */
    int              *vfs_flag;   /* 标志位 */
} vfssw;
```

### 头文件 `<sys/vfs.h>`

文件系统在首次加载时安装到文件系统切换表中，无论该类型的文件系统存在多少计数，每种类型的文件系统只有一个条目。虚拟文件系统切换的示例如下所示。每个槽位列出了文件系统名称，并告诉可以在哪里找到该系统的相对函数。
