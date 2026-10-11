```
```
struct pipe_inode_info *i_pipe; /* pipe information */
struct block_device *i_bdev; /* block device driver */
struct cdev *i_cdev; /* character device driver */
};
unsigned long i_notify_mask; /* directory notify mask */
struct dnotify_struct *i_dnotify; /* dnotify */
struct list_head dnotify_watches; /* dnotify watches */
struct mutex i_dnotify_mutex; /* protects dnotify_watches */
unsigned long i_state; /* state flags */
unsigned long dirtied_when; /* first dirtying time */
unsigned int i_flags; /* filesystem flags */
atomic_t i_writecount; /* count of writers */
void *i_security; /* security module */
void *i_private; /* fs private pointer */
};
```
```

An inode represents each file on a filesystem, but the inode object is constructed in memory only as files are accessed. This includes special files, such as device files or pipes. Consequently, some of the entries in `struct inode` are related to these special files. For example, the `i_pipe` entry points to a named pipe data structure, `i_bdev` points to a block device struct pointer, and `i_cdev` points to a character device structure. These three pointers are stored in a union because a given inode can represent only one of these (or none of them) at a time.

It might occur that a given filesystem does not support a property represented in the inode object. For example, some filesystems might not record an access timestamp. In that case, the filesystem is free to implement the feature however it sees fit; it can store zero for `i_atime`, make `i_atime` equal to `i_mtime`, update `i_atime` in memory but never flush it back to disk, or whatever else the filesystem implementer decides.

# # Inode Operations

As with the superblock operations, the `inode_operations` member is important. It describes the filesystem’s implemented functions that the VFS can invoke on an inode. As with the superblock, inode operations are invoked via

`i->i_op->truncate(i)`

In this call, `i` is a reference to a particular inode. In this case, the `truncate()` operation defined by the filesystem on which `i` exists is called on the given inode. The `inode_operations` structure is defined in `<linux/fs.h>`:

```
```
struct inode_operations {
    int (*create) (struct inode *,struct dentry *,int, struct nameidata *);
    struct dentry * (*lookup) (struct inode *,struct dentry *, struct nameidata *);
    int (*link) (struct dentry *,struct inode *,struct dentry *);
    int (*unlink) (struct inode *,struct dentry *);
    int (*symlink) (struct inode *,struct dentry *,const char *);
```
```