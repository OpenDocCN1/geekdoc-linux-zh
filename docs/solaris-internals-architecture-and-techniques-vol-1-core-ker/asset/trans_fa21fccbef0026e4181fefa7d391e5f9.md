

接口通过虚拟文件系统（vfs）对象实现独立性。vfs 对象代表了文件系统状态的封装，以及针对每个文件系统管理接口的一组方法。每种文件系统类型都提供该对象的自己的实现。图 13.3 展示了 vfs 对象。

| struct vfs | |
| --- | --- |
| vfs_next | struct vsops |
| vfs_fstype | vfs_mount () |
| vfs_op | vfs_mount () |
| | vfs_root () |
| | vfs_statvfs () |
| | vfs_sync () |
| v_data | vfs_getget () |
| | vfs_mountroot () |

图 13.3 vfs 对象

表 13-5 列出了所有的 vfs 接口方法。

# 表 13-5 来自 sys/vfs.h 的 Solaris 7 vfs 接口方法

| 方法 | 描述 |
| --- | --- |
| vfs_mount () | 在提供的 vnode 上挂载文件系统。 |
| vfs_unmount () | 卸载文件系统。 |
| vfs_root () | 查找文件系统的根 vnode。 |
| vfs_statvfs () | 查询文件系统的统计信息。 |
| vfs_sync () | 刷新文件系统缓存。 |
| vfs_vget () | 查找匹配唯一文件 ID 的 vnode。 |
| vfs_mountroot () | 在根目录上挂载文件系统。 |
| vfs_swapvp () | 未使用。 |

vfs 接口及其 sys/vfs.h 中的相关数据结构如下所示。

# 542

# 文件系统框架

```
* 每个挂载文件系统的结构。每个挂载的文件系统都包含
* 一个操作数组和一个实例记录。

* 文件系统保存在一个以 "rootvfs" 开头的单链表中，
* 并以 NULL 结束。文件系统实现不应访问此
* 列表；它仅供内核的 vfs 层使用。
*/
typedef struct {
    struct vfs *vfs_next;      /* VFS 列表中的下一个 */
    struct vfsops *             /* VFS 上的操作 */
    struct vnode *              /* 发现的 vnode */
    uint_t  vfs_flag;           /* 标志 */
    uint_t  vfs_size;           /* 原生块大小 * */
    int      vfs_type;          /* 文件系统类型索引 */
    int      vfs_id;            /* 文件系统 ID */
    char     caddr;
    dev_t    dev;             /* 挂载的 VFS 设备 */
    uint_t  vfs_bount;         /* I/o 计数 (统计) */
    uint_t  vfs_amounts;       /* 中间挂载计数 */
    struct vfs *vfs_list;      /* 同步列表指针 */
    struct vfs *vfs_hash;      /* 哈希列表指针 */
    struct vfs *vfs_reflock;   /* 挂载/卸载/同步锁 */
} ksema_t;
/*
* 在虚拟文件系统上的操作。
```

```
typedef struct vfsops {
    int (*vfs_mount)(struct vfs *, struct vnode *, struct mount *,
                     struct cred *);
    int (*vfs_unmount)(struct vfs *, struct vfs);
    int (*vfs_root)(struct vfs *, struct vnode *);
    int (*vfs_statvfs)(struct vfs *, struct statfs64 *);
    int (*vfs_sync)(struct vfs *, struct cred *);
    int (*vfs_getnode)(struct vfs *, struct vnode *, struct fid *);
    int (*vfs_mountpoint)(struct vfs *, enum whymountpoint);
    int (*vfs_swapv)(struct vfs *, struct vnode *, char *);
};
```

# 13.3.1 文件系统切换表 <sys/vfs.h>

下所示的文件系统切换表是全系统范围的文件系统类型表。加载到系统上的每种文件系统类型都可以在虚拟文件系统切换表中找到。文件系统切换表提供了该系统文件名的 ASCII 列表（例如 ufs, nfs）、初始化例程以及 vfs 对象方法。vfs 对象的 vfs_ctype 是指向文件系统切换表的索引。

```
* 文件系统切换表。
typedef struct vsw {
    char *vsw_name;            /* 类型名称字符串 */
    int (*vsw_init)(struct vfs *, int); /* 初始化例程 */
    struct vfsops *vsw_vfsops;  /* 文件系统操作向量 */
    int vsw_flag;               /* 标志 */
} vsw_t;
```

# 头文件 <sys/vfs.h>

文件系统在第一次加载时（通常在初始化函数期间）会将所有条目安装到文件系统切换表中。无论该类型的文件系统存在多少个挂载，每种类型只有一个条目。虚拟文件系统切换表的示例所示。每个槽位列出了文件系统的名称，并告知在何找到该系统的相对函数。

```
struct vfs vfssw[] = {
    "BADVFS",   &vfs_strayops, 0, /* 无效 */
    "specfs",  NULL,          /* SPEFS */
    "ufs",      &vfs_vfsops, 0, /* UFS */
    "fifofs",   &vfs_vfsops, 0, /* FIFOS */
    "namefs",   &namefs_vfsops, 0, /* NAMEFS */
    "proc",     &sproc_vfsops, 0, /* PROC */
    "nfs",      &nfs_vfsops,  0, /* NFS */
    "hfsfs",     &hfs_vfsops, 0, /* HSFS */
    "lofs",     &lofs_vfsops, 0, /* LOFS */
    "tmpfs",    &tmpfs_vfsops,  0, /* TMPFS */
    "fd",       &fd_vfsops, 0, /* FDS */
    "pcfs",     &pcfs_vfsops, 0, /* PCFS */
    "swapfs",  &swapfs_vfsops, 0, /* SWAPFS */
};
```

要转储 vfs 切换表，执行所示所示：

```
# crash
dumpfile = /dev/mem, namelist = /dev/ksym, outfile = stdout
# vfs
FILE TABLE SIZE = 29
SLOT NAME FLAGS
1 specfs 0
2 ufs    0
3 fifos  0
4 namefs 0
5 proc    0
```

文件系统框架提供了访问切换表的函数。这些函数见表 13-6，用于查找文件系统条目、加载指定的文件系统模块并在切换表中分配新条目。

# 表 13-6 来自 <sys/vfs.h> 的 vfs 支持函数

| 方法 | 描述 |
| --- | --- |
| getvfs() | 获取匹配指定 fsid 的 vfs。供 nfs 服务器使用。 |
| vfs_getvfsw() | 查找对应的 vfs 条目。如果未找到则尝试自动加载文件系统。 |
| allocate_vfsw() | 为指定类型在切换表中分配条目 |

# 13.3.2 挂载的 vfs 列表

系统从一个 vfs 对象开始，根文件系统通过 rootvfs 指针识别。你可以通过查找切换表中的 vfsops 结构并调用该系统的挂载操作来挂载文件系统。挂载操作初始化一个新的 vfs 对象并使用对象中的 vfs_next 结构将其链接到 rootvfs。每当挂载一个新的文件系统时，其 vfs 结构都会链接到链表中。你可以从 rootvfs 开始并沿着 vfs_next 链（如图 13.4 所示）获取挂载的文件系统列表。![](img/a86367b95bf21add85c9948ac951c6_589_0)

图 13.4 挂载的 vfs 列表

系统框架提供了表 13-7 中的函数，用于从挂载系统列表中搜索、添加和删除。

# 表 13-7 Solaris vfs 支持函数

| 方法 | 描述 |
| --- | --- |
| vfs_add() | 文件系统挂载函数调用，用于挂载到现有挂载点。例如，vfs_mountroot() 方法使用此调用来挂载和卸载根。 |
| vfs_remove() | 从链表中移除 vfs 对象。通常在卸载根覆盖时调用。 |
| vfs_lock() | 锁定整个文件系统。 |
| vfs_unlock() | 解锁整个文件系统。 |
| vfs_make_fsid() | 文件系统调用，从设备生成文件系统 ID。 |
| getvfs() | 获取匹配指定 fsid 的 vfs。仅供 nfs 服务器使用。 |
| vf_to_stf() | 将 vfs 标志映射到 statfs 标志。 |

要显示文件系统 vfs 对象列表，执行如下所示 crash 命令。

```
# crash
dumpfile = /dev/mem, namelist = /dev/ksym, outfile = stdout
# vfs
FSTYP BSZ MAJ/MIN FSID      VNCOVERED      HDATA      BCOUNT FLAG
ufs 8192 118,104 1d8e96e8 0 3000067888 00000000 0 notr
lfs 8192 65,0 10400000 300032b9f9b8 30002965f9be 0 00000000
names 1024 179,0 2c000000 3000311f5a60 300011ff4440 0 00000000 nolk
lfs 8192 65,0 10400000 300032b9f9b8 30002965f9be 0 00000000
lfs 8192 65,0 10400000 300032b9f9b8 30002965f9be 0 00000000
```

