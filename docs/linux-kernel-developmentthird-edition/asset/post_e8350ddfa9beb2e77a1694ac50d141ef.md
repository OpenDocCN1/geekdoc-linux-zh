
# Superblock Operations

The most important item in the superblock object is `s_op`, which is a pointer to the superblock operations table. The superblock operations table is represented by `struct super_operations` and is defined in `<linux/fs.h>`. It looks like this:

```c
struct super_operations {
    struct inode *(*alloc_inode)(struct super_block *sb);
    void (*destroy_inode)(struct inode *);
    void (*dirty_inode)(struct inode *);
    int (*write_inode)(struct inode *, int);
    void (*drop_inode)(struct inode *);
    void (*delete_inode)(struct inode *);
    void (*put_super)(struct super_block *);
    void (*write_super)(struct super_block *);
    int (*sync_fs)(struct super_block *sb, int wait);
    int (*freeze_fs)(struct super_block *);
    int (*unfreeze_fs)(struct super_block *);
    int (*statfs) (struct dentry *, struct kstatfs *);
    int (*remount_fs) (struct super_block *, int, char *);
    void (*clear_inode) (struct inode *);
    void (*umount_begin) (struct super_block *);
    int (*show_options)(struct seq_file *, struct vfsmount *);
    int (*show_stats)(struct seq_file *, struct vfsmount *);
    ssize_t (*quota_read)(struct super_block *, int, char *, size_t, loff_t);
    ssize_t (*quota_write)(struct super_block *, int, const char *, size_t, loff_t);
    int (*bdv_try_to_free_page)(struct super_block*, struct page*, gfp_t);
};
```

The code for creating, managing, and destroying superblock objects lives in `fs/super.c`. A superblock object is created and initialized via the `alloc_super()` function. When mounted, a filesystem invokes this function, reads its superblock off of the disk, and fills in its superblock object.

Each item in this structure is a pointer to a function that operates on a superblock object. The superblock operations perform low-level operations on the filesystem and its inodes.

When a filesystem needs to perform an operation on its superblock, it follows the pointers from its superblock object to the desired method. For example, if a filesystem wanted to write to its superblock, it would invoke:

```c
sb->s_op->write_super(sb);
```

In this call, `sb` is a pointer to the filesystem's superblock. Following that pointer into `s_op` yields the superblock operations table and ultimately the desired `write_super()` function, which is then invoked. Note how the `write_super()` call must be passed a superblock, despite the method being associated with one. This is because of the lack of object-oriented support in C. In C++, a call such as the following would suffice:

```c
sb.write_super();
```

In C, there is no way for the method to easily obtain its parent, so you have to pass it. Let's take a look at some of the superblock operations that are specified by `super_operations`:

- `struct inode * alloc_inode(struct super_block *sb)`
    - Creates and initializes a new inode object under the given superblock.
- `void destroy_inode(struct inode *inode)`
    - Deallocates the given inode.
- `void dirty_inode(struct inode *inode)`
    - Invoked by the VFS when an inode is dirtied (modified). Journaling filesystems such as ext3 and ext4 use this function to perform journal updates.
- `void write_inode(struct inode *inode, int wait)`
    - Writes the given inode to disk. The `wait` parameter specifies whether the operation should be synchronous.
- `void drop_inode(struct inode *inode)`
    - Called by the VFS when the last reference to an inode is dropped. Normal Unix filesystems do not define this function, in which case the VFS simply deletes the inode.
- `void delete_inode(struct inode *inode)`
    - Deletes the given inode from the disk.
- `void put_super(struct super_block *sb)`
    - Called by the VFS on umount to release the given superblock object. The caller must hold the `s_lock` lock.
- `void write_super(struct super_block *sb)`
    - Updates the on-disk superblock with the specified superblock. The VFS uses this function to synchronize a modified in-memory superblock with the disk. The caller must hold the `s_lock` lock.
- `int sync_fs(struct super_block *sb, int wait)`
    - Synchronizes filesystem metadata with the on-disk filesystem. The `wait` parameter specifies whether the operation is synchronous.
- `void write_super_lockfs(struct super_block *sb)`
    - Prevents changes to the filesystem, and then updates the on-disk superblock with the specified superblock. It is currently used by LVM (the Logical Volume Manager).
- `void unlockfs(struct super_block *sb)`
    - Unlocks the filesystem against changes as done by `write_super_lockfs()`.
- `int statfs(struct super_block *sb, struct statfs *statfs)`
    - Called by the VFS to obtain filesystem statistics. The statistics related to the given filesystem are placed in `statfs`.
- `int remount_fs(struct super_block *sb, int *flags, char *data)`
    - Called by the VFS when the filesystem is remounted with new mount options. The caller must hold the `s_lock` lock.
- `void clear_inode(struct inode *inode)`
    - Called by the VFS to release the inode and clear any pages containing related data.
- `void umount_begin(struct super_block *sb)`
    - Called by the VFS to interrupt a mount operation. It is used by network filesystems, such as NFS.

All these functions are invoked by the VFS, in process context. All except `dirty_inode()` may block if needed.

Some of these functions are optional; a specific filesystem can then set its value in the superblock operations structure to NULL. If the associated pointer is NULL, the VFS either calls a generic function or does nothing, depending on the operation.

# The Inode Object

The inode object represents all the information needed by the kernel to manipulate a file or directory. For Unix-style filesystems, this information is simply read from the on-disk inode. If a filesystem does not have inodes, however, the filesystem must obtain the information from wherever it is stored on the disk. Filesystems without inodes generally store file-specific information as part of the file; unlike Unix-style filesystems, they do not separate file data from its control information. Some modern filesystems do neither and store file metadata as part of an on-disk database. Whatever the case, the inode object is constructed in memory in whatever manner is applicable to the filesystem.

The inode object is represented by `struct inode` and is defined in `<linux/fs.h>`.

Here is the structure, with comments describing each entry:

```c
struct inode {
    struct list_head i_hash;             /* hash list */
    struct list_head i_list;             /* list of inodes */
    struct list_head i_sb_list;          /* list of superblocks */
    struct list_head i_dentry;           /* list of dentries */
    unsigned long i_ino;                /* inode number */
    atomic_t i_count;                   /* reference counter */
    unsigned int i_nlink;               /* number of hard links */
    uid_t i_uid;                        /* user id of owner */
    gid_t i_gid;                        /* group id of owner */
    kdev_t i_rdev;                      /* real device number */
    u64 i_version;                      /* versioning number */
    loff_t i_size;                      /* file size in bytes */
    seqcount_t i_size_seqcount;         /* serializer for i_size */
    struct timespec i_atime;            /* last access time */
    struct timespec i_mtime;            /* last modify time */
    struct timespec i_ctime;            /* last change time */
    unsigned int i_blkbits;            /* block size in bits */
    blkcnt_t i_blocks;                 /* file size in blocks */
    unsigned short i_bytes;            /* bytes consumed */
    umode_t i_mode;                    /* access permissions */
    spinlock_t i_lock;                 /* spinlock */
    struct rw_semaphore i_allocc_sem;  /* waits inside of i_sem */
    struct semaphore i_sem;            /* inode semaphore */
    struct inode_operations *i_op;     /* inode ops table */
    struct file_operations *i_fop;     /* default inode ops */
    struct super_block *i_sb;          /* associated superblock */
    struct file_lock *i_flock;         /* file lock list */
    struct address_space *i_mapping;    /* associated mapping */
    struct address_space i_data;        /* mapping for device */
    struct dquot *i_dquot[MAXQUOTAS];  /* disk quotas for inode */
    struct list_head i_devids;         /* list of block devices */
    union {
```
