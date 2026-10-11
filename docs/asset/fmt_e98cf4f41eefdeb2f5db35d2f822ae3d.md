
```c
struct file_operations *f_op;

atomic_t f_count;

unsigned int f_flags;

mode_t f_mode;

loff_t f_pos;

unsigned long f_reada, f_rama, f_raend, f_ralen, f_rawin;

struct fown_struct f_owner;

unsigned int f_uid, f_gid;

int f_error;

unsigned long f_version;

/* needed for tty driver, and maybe others */

void *private_data;

};

extern spinlock_t files_lock;

#define file_list_lock() spin_lock(&files_lock);

#define file_list_unlock() spin_unlock(&files_lock);

#define get_file(x) atomic_inc(&(x)->f_count)

#define file_count(x) atomic_read(&(x)->f_count)

extern int init_private_file(struct file *, struct dentry *, int);
```

## 文件系统

```c
#define FL_POSIX            1

#define FL_FLOCK            2

#define FL_BROKEN           4    /* broken flock() emulation */

#define FL_ACCESS             8    /* for processes suspended by mandatory locking */

#define FL_LOCKD            16    /* lock held by rpc.lockd */

/*

 * The POSIX file lock owner is determined by

 * the "struct files_struct" in the thread group

 * (or NULL for no owner - BSD locks).

 *

 * Lockd stuffs a "host" pointer into this.

 */

typedef struct files_struct *fl_owner_t;

struct file_lock {

    struct file_lock *fl_next;    /* singly linked list for this inode */

    struct file_lock *fl_nextlink;/* doubly linked list of all locks */

    struct file_lock *fl_prevlink;/* used to simplify lock removal */

    struct file_lock *fl_nextblock; /* circular list of blocked processes */

    struct file_lock *fl_prevblock;

    fl_owner_t fl_owner;

    unsigned int fl_pid;

    wait_queue_head_t fl_wait;

    struct file *fl_file;

    unsigned char fl_flags;

    unsigned char fl_type;

    loff_t fl_start;

    loff_t fl_end;

    void (*fl_notify)(struct file_lock *);  /* unlock callback */

    void (*fl_insert)(struct file_lock *);  /* lock insertion callback */

    void (*fl_remove)(struct file_lock *);  /* lock removal callback */

    union {

        struct nfs_lock_info    nfs_fl;

    } fl_u;

};

/* The following constant reflects the upper bound of the file/locking space */

#ifndef OFFSET_MAX

#define INT_LIMIT(x)        (~-((x)1 << (sizeof(x)*8 - 1)))

#define OFFSET_MAX          INT_LIMIT(loff_t)

#endif

extern struct file_lock           *file_lock_table;

#include <linux/fcntl.h>

extern int fcntl_getlk(unsigned int, struct flock *);

extern int fcntl_setlk(unsigned int, unsigned int, struct flock *);

/* fs/locks.c */

extern void locks_remove_posix(struct file *, fl_owner_t);

extern void locks_remove_flock(struct file *);

extern struct file_lock *posix_test_lock(struct file *, struct file_lock *);

extern int posix_lock_file(struct file *, struct file_lock *, unsigned int);

extern void posix_block_lock(struct file_lock *, struct file_lock *);

extern void posix_unblock_lock(struct file_lock *);

struct fasync_struct {

	int 		magic;

	int 		fa_fd;

	struct fasync_struct 	*fa_next; /* singly linked list */

	struct file 		*fa_file;

};

struct nameidata {

	struct dentry *dentry;

	struct vfsmount *mnt;

	struct qstr last;

};

#define FASYNC_MAGIC 0x4601

extern int fasync_helper(int, struct file *, int, struct fasync_struct **);

#define DQUOT_USR_ENABLED		0x01 	/* User diskquotas enabled */

#define DQUOT_GRP_ENABLED		0x02 	/* Group diskquotas enabled */

struct quota_mount_options

{

	unsigned int flags;				/* Flags for diskquotas on this device */

	struct semaphore dquio_sem;		/* lock device while I/O in progress */

	struct semaphore dqoff_sem;		/* serialize quota_off() and quota_on()

						 on device */

	struct file *files[MAXQUOTAS];	/* fp's to quotafiles */

	time_t inode_expire[MAXQUOTAS];	/* expiretime for inode-quota */

	time_t block_expire[MAXQUOTAS];	/* expiretime for block-quota */

	char rsquash[MAXQUOTAS];		/* for quotas threat root as any other

					 user */

};

/*

	 * 	Unmount options

	 */

#define MNT_FORCE		0x00000001 	/* Attempt to forcibly unmount */

#include <linux/minix_fs_sb.h>
```
