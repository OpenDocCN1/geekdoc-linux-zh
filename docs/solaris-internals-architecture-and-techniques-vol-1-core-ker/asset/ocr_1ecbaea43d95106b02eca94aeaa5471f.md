underlying file system containing the vnode is. For example, to read from a file without knowing that it resides on a UFS file system, the kernel would simply call the file-system-independent macro for read(), VOP_READ(), which would call the vop_read() method of the vnode, which in turn calls the UFS function, ufs_read(). A sample of a vnode macro from sys/vnode. is shown below.

```
#define VOP_READ(vpp, mode, cr) \
(*(vpp))->v_opop->vop_read(vpp, mode, cr)
```

# Header File <sys/vnode.h>

The structure of a vnode in Solaris can be found in sys/vnode.h and is shown below. It defines the basic interface elements and provides other information contained in the vnode.

```
typedef struct vnode {
    kmut_t      v_lock;         /* protects vnode fields */
    ushort_t    v_flag;          /* vnode flags (see below) */
    uint        v_count;         /* reference count *
n    struct vfs  *v_mountee;    /* ptr to vfs mounted here */
    struct vnodeops *v_op;      /* vnode operations * */
    struct vfs   *v_fsap;        /* ptr containing VFS */
    struct data *v_stream;      /* associated stream * */
    struct page  v_pages;        /* vnode pages list * */
    enum vtype v_type;         /* vnode type * */
    dev_t       v_device;       /* device (VCHR, VLBK) */
    caddr_t     v_data;         /* private data for fs * */
    struct filock v_locks;      /* ptr to filock list * */
    struct shlocklist *v_shlocks; /* ptr to shlock list * */
    kcondvar_t  v_cv;           /* synchronization locking */
} vnode;
```

# 13.2.1 vnode Types

Solaris has specific vnode types for files. The v type field in the vnode structure indicates the type of vnode, as described in Table 13-1.

# Table 13-1 Solaris7 vnode types from sys/vnode.h

| Type | Description |
| --- | --- |
| VNON | No type |
| VREG | Regular file |
| VDIR | Directory |
| VLBK | Block device |
| VCHR | Character device |
| VLNK | Hard link |
| VFIPO | Named pipe |
| VDOOR | Doors interface |
| VPROC | procfs node |