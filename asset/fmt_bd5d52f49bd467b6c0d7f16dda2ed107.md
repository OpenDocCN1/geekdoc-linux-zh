
* Derek Atkins <warlord@MIT.EDU> 1994-10-20

 */

```c
struct iattr {
    unsigned int      ia_valid;
    umode_t           ia_mode;
    uid_t             ia_uid;
    gid_t             ia_gid;
    loff_t            ia_size;
    time_t            ia_atime;
    time_t            ia_mtime;
    time_t            ia_ctime;
    unsigned int      ia_attr_flags;
};
```

/*
 * 以下是 inode 属性标志定义
 */

```c
#define ATTR_FLAG_SYNCRONOUS 1 /* 同步写入 */
#define ATTR_FLAG_NOTIME 2 /* 不更新时间 */
#define ATTR_FLAG_APPEND 4 /* 仅追加文件 */
#define ATTR_FLAG_IMMUTABLE 8 /* 不可变文件 */
#define ATTR_FLAG_NODIRATIME 16 /* 不更新目录时间 */
```

/*
 * 用于磁盘配额和挂载结构的头文件包含。
 */

```c
#include <linux/quota.h>
#include <linux/mount.h>
```

/*
 * C 语言类型声明的美妙之处。
 */

```c
struct page;
struct address_space;

struct address_space_operations {
    int (*writepage)(struct dentry *, struct page *);
    int (*readpage)(struct dentry *, struct page *);
    int (*prepare_write)(struct file *, struct page *, unsigned, unsigned);
    int (*commit_write)(struct file *, struct page *, unsigned, unsigned);
    /* 不幸的是，这个临时方案是 FIBMAP 所必需的。请勿使用 */
    int (*bmap)(struct address_space *, long);
};

struct address_space {
    struct list_head pages; /* 页链表 */
    unsigned long nrpages; /* 页数 */
    struct address_space_operations *a_ops; /* 方法 */
    void *host; /* 所有者：inode、block_device */
    struct vm_area_struct *i_mmap; /* 映射列表 */
    spinlock_t i_shared_lock; /* 保护上述内容的自旋锁 */
};

struct block_device {
    struct list_head bd_hash;
    atomic_t bd_count;
    /* struct address_space bd_data; */
    dev_t bd_dev; /* 不是 kdev_t - 它是搜索键 */
    atomic_t bd_openers;
    const struct block_device_operations *bd_op;
    struct semaphore bd_sem; /* 打开/关闭互斥量 */
};

struct inode {
    struct list_head i_hash;
    struct list_head i_list;
    struct list_head i_dentry;
    unsigned long i_ino;
    unsigned int i_count;
    kdev_t i_dev;
    umode_t i_mode;
    nlink_t i_nlink;
    uid_t i_uid;
    gid_t i_gid;
    kdev_t i_rdev;
    loff_t i_size;
    time_t i_atime;
    time_t i_mtime;
    time_t i_ctime;
    unsigned long i_blksize;
    unsigned long i_blocks;
    unsigned long i_version;
    struct semaphore i_sem;
    struct semaphore i_zombie;
    struct inode_operations *i_op;
    struct file_operations *i_fop; /* former ->i_op->default_file_ops */
    struct super_block *i_sb;
    wait_queue_head_t i_wait;
    struct file_lock *i_flock;
    struct address_space *i_mapping;
    struct address_space i_data;
    struct dquot *i_dquot[MAXQUOTAS];
    struct pipe_inode_info *i_pipe;
    struct block_device *i_bdev;
    unsigned long i_state;
    unsigned int i_flags;
    unsigned char i_sock;
    atomic_t i_writecount;
    unsigned int i_attr_flags;
    __u32 i_generation;
    union {
        struct minix_inode_info minix_i;
        struct ext2_inode_info ext2_i;
        struct hpfs_inode_info hpfs_i;
        struct ntfs_inode_info ntfs_i;
        struct msdos_inode_info msdos_i;
        struct umsdox_inode_info umsdox_i;
        struct isofs_inode_info isofs_i;
        struct nfs_inode_info nfs_i;
        struct sysv_inode_info sysv_i;
        struct affs_inode_info affs_i;
        struct ufs_inode_info ufs_i;
        struct efs_inode_info efs_i;
        struct romfs_inode_info romfs_i;
        struct coda_inode_info coda_i;
        struct smb_inode_info smbfs_i;
        struct hfs_inode_info hfs_i;
        struct adfs_inode_info adfs_i;
        struct gnx4_inode_info gnx4_i;
        struct bfs_inode_info bfs_i;
        struct udf_inode_info udf_i;
        struct ncp_inode_info ncpfs_i;
        struct proc_inode_info proc_i;
        struct socket socket_i;
        struct usbdev_inode_info usbdev_i;
        void *generic_ip;
    } u;
};
```

/* Inode state bits.. */

```c
#define I_DIRTY 1
#define I_LOCK 2
#define I_FREEING 4
#define I_CLEAR 8

extern void __mark_inode_dirty(struct inode *);

static inline void mark_inode_dirty(struct inode *inode)
{
    if (!(inode->i_state & I_DIRTY))
        __mark_inode_dirty(inode);
}

struct fown_struct {
    int pid; /* pid or -pgrp where SIGIO should be sent */
    uid_t uid, eid; /* uid/euid of process setting the owner */
    int signum; /* posix.1b rt signal to be delivered on IO */
};

struct file {
    struct list_head f_list;
    struct dentry *f_dentry;
    struct vfsmount *f_vfsmnt;
```
