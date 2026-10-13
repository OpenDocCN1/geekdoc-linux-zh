
**Table 13-3** *Solaris 7 vnode Paging Functions* from `vm/pvn.h` *(Continued)*

| Function | Description |
|---|---|
| `pvn_write_kluster()` | Finds the contiguous range of dirty pages within the supplied offset and length. Returns a list of dirty locked pages ready to be written back. On return from `pvn_write_kluster()`, the caller typically sets up the write with `pageio_setup` for the returned offset and length, then initiates the write with `bdev_strategy()`. If the write is synchronous, then the caller should call `pvn_write_done()` to unlock the pages. If the write is asynchronous, then the `io_done` routine calls `pvn_write_done` when the write is complete. |
| `pvn_vplist_dirty()` | Finds all dirty pages in the page cache that have an offset greater than the supplied offset and calls the supplied `putpage()` routine. `pvn_vplist_dirty()` is often used to synchronize all dirty pages for a vnode when `vop_putpage` is called with a zero length. |

### 13.2.5 Block I/O on vnode Pages

The block I/O subsystem provides support for initiating I/O to and from vnode pages. The three functions, shown in Table 13-4, initiate I/O between a physical page and a device.

**Table 13-4** *Solaris 7 Paged I/O Functions* from `sys/bio.h`

| Function | Description |
|---|---|
| `bdev_strategy()` | Initiates an I/O on a page, using the block I/O device. |
| `pageio_done()` | Waits for the block device I/O to complete. |
| `pageio_setup()` | Sets up a block buffer for I/O on a page of memory so that it bypasses the block buffer cache by setting the `B_PAGEIO` flag and putting the page list on the `b_pages` field. |

## 13.3 The vfs Object

The vfs layer provides an administrative interface into the file system to support commands like mount and umount in a file-system-independent manner. The interface achieves independence by means of a virtual file system (vfs) object. The vfs object represents an encapsulation of a file system's state and a set of methods for each of the file system administrative interfaces. Each file system type provides its own implementation of the object. Figure 13.3 illustrates the vfs object.

![](img/220ae4af07df2fe8e5be69d27f885d1b_592_0.png)

**Figure 13.3** *The vfs Object*

Table 13-5 lists all the vfs interface methods.

**Table 13-5** *Solaris 7 vfs Interface Methods from `sys/vfs.h`*

| Method | Description |
|---|---|
| `vfs_mount()` | Mounts a file system on the supplied vnode. |
| `vfs_unmount()` | Unmounts the file system. |
| `vfs_root()` | Finds the root vnode for a file system. |
| `vfs_statvfs()` | Queries statistics on a file system. |
| `vfs_sync()` | Flushes the file system cache. |
| `vfs_vget()` | Finds a vnode that matches a unique file ID. |
| `vfs_mountroot()` | Mounts the file system on the root directory. |
| `vfs_swapvp()` | Not used. |

The vfs interface, with the relevant data structures from `sys/vfs.h`, is shown below.

```c
/*
 * Structure per mounted file system. Each mounted file system has
 * an array of operations and an instance record.
 *
 * The file systems are kept on a singly linked list headed by "rootvfs" and
 * terminated by NULL. File system implementations should not access this
 * list; it's intended for use only in the kernel's vfs layer.
 */
typedef struct vfs {
        struct vfs       *vfs_next;             /* next VFS in VFS list */
        struct vfsops    *vfs_op;               /* operations on VFS */
        struct vnode     *vfs_vnodecovered;     /* vnode mounted on */
        uint_t           vfs_flag;              /* flags */
        uint_t           vfs_bsize;             /* native block size */
        int              vfs_fstype;            /* file system type index */
        fsid_t           vfs_fsid;              /* file system id */
        caddr_t          vfs_data;              /* private data */
        dev_t            vfs_dev;              /* device of mounted VFS */
        ulong_t          vfs_bcount;            /* I/O count accounting */
        ushort_t         vfs_submounts;         /* immediate sub-mount count */
        struct vfs        *vfs_list;            /* sync list pointer */
        struct vfs        *vfs_hash;            /* hash list pointer */
        ksem_t           vfs_reflock;           /* mount/unmount/sync lock */
} vfs_t;

/*
 * Operations supported on virtual file system.
 */
typedef struct vfsops {
        int     (*vfs_mount)(struct vfs *, struct vnode *, struct mounta *,
                             struct cred *);
        int     (*vfs_unmount)(struct vfs *, struct cred *);
        int     (*vfs_root)(struct vfs *, struct vnode *);
        int     (*vfs_statvfs)(struct vfs *, struct statvfs *);
        int     (*vfs_sync)(struct vfs *, short, struct cred *);
        int     (*vfs_vget)(struct vfs *, struct vnode *, struct fid *);
        int     (*vfs_mountroot)(struct vfs *, enum whymountroot);
        int     (*vfs_swapvp)(struct vfs *, struct vnode **, char *);
} vfsops_t;
```

**Header File** `<sys/vfs.h>`

### 13.3.1 The File System Switch Table

The file system switch table, shown below, is a systemwide table of file system types. Each file system type that is loaded on the system can be found in the virtual file system switch table. The file system switch table provides an ASCII list of file system names (e.g., ufs, nfs), the initialization routines, and vfs object methods for that file system. The `vfs_fstype` field of the vfs object is an index into the file system switch table.

```c
/*
 * File system type switch table.
 */
typedef struct vfssw {
        char    *vsw_name;              /* type name string */
        int     (*vsw_init)(struct vfssw *);  /* init routine */
        struct vfsops *vsw_vfsops;      /* file system operations vector */
        int     vsw_flag;               /* flags */
} vfssw_t;
```

**Header File** `<sys/vfs.h>`

File systems install entries into the file system switch table when they are first loaded, usually during their initialization function. There is only one entry for each type of file system, regardless of how many mounts exist for that type of file system. An example of the virtual file system switch table is shown below. Each slot lists the name of the file system and tells where to find the relevant functions for that file system.

```c
struct vfssw vfssw[] = {
        "BADVFS",        NULL,        &vfs_strayops,  0,    /* invalid */
        "specfs",        specinit,    NULL,           0,    /* SPECS */
        "ufs",           ufsinit,     &ufs_vfsops,    0,    /* UFS */
        "fifofs",        fifoinit,    &fifo_vfsops,   0,    /* FIFOS */
        "namefs",        namefsinit,  &name_vfsops,   0,    /* NAMEFS */
        "proc",          procinit,    &proc_vfsops,   0,    /* PROCFS */
        "s5fs",          s5fsinit,    &s5_vfsops,     0,    /* S5FS */
        "nfs",           nfsinit,     &nfs_vfsops,    0,    /* NFS Ver 2 */
        "hsfs",          hsfsinit,    &hsfs_vfsops,   0,    /* HSFS */
        "lofs",          lofsinit,    &lo_vfsops,     0,    /* LOFS */
        "tmpfs",         tmpfsinit,   &tmp_vfsops,    0,    /* TMPFS */
        "fd",            fdinit,      &fd_vfsops,     0,    /* FDFS */
        "pcfs",          pcfsinit,    &pcfs_vfsops,   0,    /* PCFS */
        "swapfs",        swapinit,    &swap_vfsops,   0,    /* SWAPFS */
};
```

To dump the vfs switch table, issue the crash command, as shown below.

```text
# crash
dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> vfsw
FILE SYSTEM SWITCH TABLE SIZE = 29
SLOT  NAME      FLAGS
   1  specfs       0
   2  ufs          0
   3  fifofs       0
   4  namefs       0
   5  proc         0
   6  s5fs         0
```

The file system framework provides functions for accessing file systems in the file system switch table. These functions, described in Table 13-6, find file system entries, locate and load the file system modules for given types, and allocate new entries in the file system switch table.

**Table 13-6** *Solaris 7 vfs Support Functions from `<sys/vfs.h>`*

| Method | Description |
|---|---|
| `getvfs()` | Gets a pointer to the vfs that matches the supplied fsid. Used by the nfs server. |
| `vfs_getvfssw()` | Finds a vfssw entry by file system type name. Tries to autoload the file system if entry is not found. |
| `allocate_vfssw()` | Allocates an entry in the file system switch table for a given file type. |

### 13.3.2 The Mounted vfs List

The system starts with only one vfs object, the root file system, which is identified by the rootvfs kernel pointer. You can subsequently mount file systems by looking up the vfsops structure in the switch table and calling the mount operation for that file system. The mount operation initializes a new vfs object and links it to the rootvfs object by using the vfs_next structure in the object. Each time a new file system is mounted, its vfs structure is linked onto the chain. You
