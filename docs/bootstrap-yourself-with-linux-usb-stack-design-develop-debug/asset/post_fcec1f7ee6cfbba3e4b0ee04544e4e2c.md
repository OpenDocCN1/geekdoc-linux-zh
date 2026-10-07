
## Chapter 6 = Device File System

![](img/779a74a6577501a55983f193067274a3_88_0.png)

**Figure 6.1**
A simplistic view of VFS inside the Linux kernel.

## BOOTSTRAP ESSENTIALS: VIRTUAL FILE SYSTEM

In general, the Linux VFS framework provides an abstraction layer for the different file formats in the design. The Linux device model also uses the VFS framework to extend access to the devices onto the user space. The VFS framework uses four major data structure objects: entries, files, inodes, and super blocks. These data structures are the backbone of any VFS-based implementation.

**Note**

> The Virtual File System (VFS) is the more descriptive definition of VFS, because it switches between multiple file systems to seek information.

The super block data structure lies as the root of the file system. Any file system that is mounted is represented by a VFS `struct super_block` data structure. The definitions of the super block data structures are available as part of `include/linux/fs.h` `include/linux/fs.h` of the kernel source package. A super block data structure typically contains a pointer to super block operations, information on block size, identifiers to the block device, and file-specific information. The struct

### Bootstrap Essentials: Virtual File System

super_operations data structure provides methods to manage an inode, beyond methods that manage the super block and collect statistics.

```c
struct super_operations {
    struct inode *(alloc_inode)(struct super_block *sb);
    void (*destroy_inode)(struct inode);
    void (*dirty_inode)(struct inode);
    int (*write_inode)(struct inode *, struct writeback_control *wbc);
    int (*drop_inode)(struct inode);
    void (*delete_inode)(struct inode *);
    void (*put_super)(struct super_block);
    int (*sync_fs)(struct super_block *sb, int wait);
    int (*freeze_fs)(struct super_block);
    int (*unfreeze_fs)(struct super_block *);
    int (*statfs)(struct dentry *, struct kstatfs *);
    int (*remount_fs)(struct super_block *, int *, char *);
    void (*clear_inode)(struct inode *);
    void (*umount_begin)(struct super_block);
    int (*show_options)(struct seq_file *, struct vfs_mount *);
    int (*show_stats)(struct seq_file *, struct vfs_mount *);
#ifndef CONFIG_QUOTA
    size_t (*quota_read)(struct super_block *, int, char *, size_t, loff_t);
    size_t (*quota_write)(struct super_block *, int, const char *, size_t, loff_t);
#endif
};
```

```c
int (*bdev_try_to_free_page)(struct super_block *, struct page *);
```

The next important data structure is the inode or the index node, which may refer to a file or directory object. The inode holds file metadata information, such as the file length in bytes, file-related information, and ownership. This VFS inode objects are allocated by a slab allocator for the inode cache that the kernel maintains. The inode objects represent both data files and device files and sometimes are stored on a disk.

```c
struct inode_operations {
    int (*create)(struct inode *,struct dentry *,int, struct nameidata);
    struct dentry *(*lookup)(struct inode *,struct dentry *, struct nameidata *);
    int (*link) (struct dentry *,struct dentry *,struct dentry *);
    int (*unlink) (struct inode *,struct dentry *);
    int (*symlink) (struct inode *,struct dentry *,const char *);
    int (*mkdir) (struct inode *,struct dentry *,int);
    int (*rmdir) (struct inode *,struct dentry *);
    int (*mknod) (struct inode *,struct dentry *,int,dev_t);
    int (*rename) (struct inode *, struct dentry *);
    struct inode *, struct dentry *
    int (*read) (struct inode *, char __user *,int);
    void (*follow_link) (struct dentry *, struct nameidata *, void *);
    void (*put_link) (struct dentry *, struct nameidata *, void *);
    void (*truncate) (struct inode *, int);
    int (*permission) (struct inode *, int);
    int (*check_acl) (struct inode *, int);
    int (*setattr) (struct dentry *, struct iattr);
    int (*getattr) (struct vfsmount *,struct dentry *, struct kstat *);
    int (*setxattr) (struct dentry *, const char *,const void *,size_t,int);
    size_t (*getxattr)(struct dentry *, const char *, size_t);
    size_t (*listxattr)(struct dentry *, char *, size_t);
    int (*removattr_range) (struct dentry *, const char *);
    void (*truncate) (struct inode *, loff_t, loff_t);
    long (*allocate) (struct inode *inode, int mode, loff_t offset, loff_t len);
    int (*fiemap)(struct inode *, struct fiemap_extent_info *, u64 start, u64 len);
};
```

The next important data structure of a VFS framework is `file_operations`, which allows you to access the file.

```c
struct file_operations {
  struct module *owner;
  ssize_t (*read)(struct file *, char __user *, size_t, loff_t);
  ssize_t (*write)(struct file *, char __user *, size_t, loff_t);
  long (*seek)(struct file *, loff_t, int);
  int (*open)(struct inode *, struct file *);
  int (*release)(struct file *);
};
```
