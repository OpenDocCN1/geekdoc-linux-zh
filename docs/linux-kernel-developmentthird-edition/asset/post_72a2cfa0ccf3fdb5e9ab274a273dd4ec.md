
## Dentry Operations

The dentry_operations structure specifies the methods that the VFS invokes on directory entries on a given filesystem.

The dentry_operations structure is defined in <linux/dcache.h>:

```c
struct dentry_operations {
  int (*d_revalidate) (struct dentry *, struct nameidata *);
  int (*d_hash) (struct dentry *, struct qstr *);
  int (*d_compare) (struct dentry *, struct qstr *, struct qstr *);
  int (*d_delete) (struct dentry *);
  void (*d_release) (struct dentry *);
  void (*d_iput) (struct dentry *, struct inode *);
  char *(*d_dname) (struct dentry *, char *, int);
};
```

The methods are as follows:

- `int d_revalidate(struct dentry *dentry, struct nameidata *)`

  Determines whether the given dentry object is valid. The VFS calls this function whenever it is preparing to use a dentry from the dcache. Most filesystems set this method to `NULL` because their dentry objects in the dcache are always valid.

- `int d_hash(struct dentry *dentry, struct qstr *name)`

  Creates a hash value from the given dentry. The VFS calls this function whenever it adds a dentry to the hash table.

- `int d_compare(struct dentry *dentry, struct qstr *name1, struct qstr *name2)`

  Called by the VFS to compare two filenames, `name1` and `name2`. Most filesystems leave this at the VFS default, which is a simple string compare. For some filesystems, such as FAT, a simple string compare is insufficient. The FAT filesystem is not case-sensitive and therefore needs to implement a comparison function that disregards case. This function requires the `dcache_lock`.

- `int d_delete(struct dentry *dentry)`

  Called by the VFS when the specified dentry object's `d_count` reaches zero. This function requires the `dcache_lock` and the dentry's `d_lock`.

- `void d_release(struct dentry *dentry)`

  Called by the VFS when the specified dentry is going to be freed. The default function does nothing.

- `void d_iput(struct dentry *dentry, struct inode *inode)`

  Called by the VFS when a dentry object loses its associated inode (say, because the entry was deleted from the disk). By default, the VFS simply calls the `iput()` function to release the inode. If a filesystem overrides this function, it must also call `iput()` in addition to performing whatever filesystem-specific work it requires.

## The File Object

The final primary VFS object that we shall look at is the file object. The file object is used to represent a file opened by a process. When we think of the VFS from the perspective of user-space, the file object is what readily comes to mind. Processes deal directly with files, not superblocks, inodes, or dentries. It is not surprising that the information in the file object is the most familiar (data such as access mode and current offset) or that the file operations are familiar system calls such as `read()` and `write()`.

The file object is the in-memory representation of an open file. The object (but not the physical file) is created in response to the `open()` system call and destroyed in response to the `close()` system call. All these file-related calls are actually methods defined in the file operations table. Because multiple processes can open and manipulate a file at the same time, there can be multiple file objects in existence for the same file. The file object merely represents a process's view of an open file. The object points back to the dentry (which in turn points back to the inode) that actually represents the open file. The inode and dentry objects, of course, are unique.

The file object is represented by `struct file` and is defined in `<linux/fs.h>`. Let's look at the structure, again with comments added to describe each entry:

```c
struct file {
    union {
        struct list_head  fu_list;	/* list of file objects */
        struct rcu_head	fu_rcuhead;	/* RCU list after freeing */
    } f_u;
    struct path		f_path;		/* contains the dentry */
    struct file_operations	*f_op;	/* file operations table */
    spinlock_t		f_lock;		/* per-file struct lock */
    atomic_t		f_count;	/* file object's usage count */
    unsigned int	f_flags;		/* flags specified on open */
    mode_t		f_mode;		/* file access mode */
    loff_t		f_pos;		/* file offset (file pointer) */
    struct fown_struct	f_owner;	/* owner data for signals */
    const struct cred	*f_cred;	/* file credentials */
    struct file_ra_state	f_ra;		/* read-ahead state */
    u64			f_version;	/* version number */
    void		*f_security;	/* security module */
    void		*private_data;	/* tty driver hook */
    struct list_head      f_ep_links;     /* list of epoll links */
    spinlock_t            f_ep_lock;      /* epoll lock */
    struct address_space  *f_mapping;      /* page cache mapping */
    unsigned long         f_mnt_write_state; /* debugging state */
};
```

Similar to the dentry object, the file object does not actually correspond to any on-disk data. Therefore, no flag in the object represents whether the object is dirty and needs to be written back to disk. The file object denotes pointer to its associated dentry object via the `f_dentry` pointer. The dentry in turn points to the associated inode, which reflects whether the file itself is dirty.

## File Operations

As with all the other VFS objects, the file operations table is quite important. The operations associated with `struct file` are the familiar system calls that form the basis of the standard Unix system calls.

The file object methods are specified in `file_operations` and defined in `<linux/fs.h>`:

```c
struct file_operations {
  struct module *owner;
  loff_t (*llseek) (struct file *, loff_t, int);
  ssize_t (*read) (struct file *, char __user *, size_t, loff_t *);
  ssize_t (*write) (struct file *, const char __user *, size_t, loff_t *);
  ssize_t (*aio_read) (struct kiocb *, const struct iovec *,
        unsigned long, loff_t);
  ssize_t (*aio_write) (struct kiocb *, const struct iovec *,
        unsigned long, loff_t);
  int (*readdir) (struct file *, void *, filldir_t);
  unsigned int (*poll) (struct file *, struct poll_table_struct *);
  int (*ioctl) (struct inode *, struct file *, unsigned int,
        unsigned long);
  long (*unlocked_ioctl) (struct file *, unsigned int, unsigned long);
  long (*compat_ioctl) (struct file *, unsigned int, unsigned long);
  int (*mmap) (struct file *, struct vm_area_struct *);
  int (*open) (struct inode *, struct file *);
  int (*flush) (struct file *, fl_owner_t id);
  int (*release) (struct inode *, struct file *);
  int (*fsync) (struct file *, struct dentry *, int datasync);
  int (*aio_fsync) (struct kiocb *, int datasync);
  int (*fasync) (int, struct file *, int);
  int (*check) (struct file *, int, struct file_lock *);
  ssize_t (*sendpage) (struct file *, struct page *,
        int, size_t, loff_t, int);
  unsigned long (*get_unmapped_area) (struct file *,
        unsigned long,
        unsigned long, unsigned long, unsigned long);
  int (*check_flags) (int);
  int (*flock) (struct file *, int, struct file_lock *);
  size_t (*splice_write) (struct pipe_inode_info *,
        struct file *,
        loff_t *,
        size_t,
        unsigned int);
  ssize_t (*splice_read) (struct file *,
        loff_t *,
        struct pipe_inode_info *,
        size_t,
        unsigned int);
  int (*setlease) (struct file *, long, struct file_lock **);
};
```

Filesystems can implement unique functions for each of these operations, or they can use a generic method if one exists. The generic methods tend to work fine on normal Unix-based filesystems. A filesystem is under no obligation to implement all these methods—although not implementing the basics is silly—and can simply set the method to `NULL` if not interested.

Here are the individual operations:

- **`loff_t llseek(struct file *file, loff_t offset, int origin)`**

  Updates the file pointer to the given offset. It is called via the `lseek()` system call.

- **`ssize_t read(struct file *file, char *buf, size_t count, loff_t *offset)`**

  Reads `count` bytes from the given file at position `offset` into `buf`. The file pointer is then updated. This function is called by the `read()` system call.

- **`ssize_t aio_read(struct kiocb *iocb, char *buf, size_t count, loff_t offset)`**

  Begins an asynchronous read of `count` bytes into `buf` of the file described in `iocb`. This function is called by the `aio_read()` system call.

- **`ssize_t write(struct file *file, const char *buf, size_t count, loff_t *offset)`**

  Writes `count` bytes from `buf` into the given file at position `offset`. The file pointer is then updated. This function is called by the `write()` system call.
