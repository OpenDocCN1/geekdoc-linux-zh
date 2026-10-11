
## PV Status
available / allocatable
total PE / Free PE: 131 / 131

### PV Name (#): /dev/sdl1 (7)
PV Status: available / allocatable
total PE / Free PE: 131 / 131

### PV Name (#): /dev/sdj1 (8)
PV Status: available / allocatable
total PE / Free PE: 125 / 125

### PV Name (#): /dev/sdk1 (9)
PV Status: available / allocatable
total PE / Free PE: 537 / 537

```bash
# create a linear physical volume with all space of the volume group
lvcreate -l 100%FREE my_first_vg
lvcreate -- performing automatic backup of my_first_vg
lvcreate -- logical volume /dev/my_first_vg/lvol1 successfully created
```

```bash
# create an ext2fs on newly created logical volume
mkfs /dev/my_first_vg/lvol1
mkfs 1.10, 24-Apr-97 for EXr2 FS 0.5b, 95/08/09
Linux ext2 file system format
File system label:
3235840 inodes, 12939264 blocks
646963 blocks (5.00%) reserved for the super user
First data block=1
Block size=1024 (log=0)
Fragment size=1024 (log=0)
1580 block groups
8192 blocks per group, 8192 fragments per group
2048 inodes per group
Superblock backups stored on blocks:
8193, 16385, 24577, 32769, 40961, 49153, 57345, 65537, 73729,
81921, 90113, 98305, 106497, 114689, 122881, 131073, 139265,
147457,
Writing superblocks and file system accounting information: done
0.66 user 26.55 system 3:06.62 elapsed 14% CPU (0 avgtext+0 avgdata
0 maxresident)k
0 inputs+0 outputs (97 major+522 minor)pagefaults 0 swaps
```

```bash
# and mount it (not very exciting :) )
mount /dev/my_first_vg/lvol1 /mnt
```

### Data Structures—include/linux/fs.h

```c
#ifndef _LINUX_FS_H
#define _LINUX_FS_H

/**
 * This file has definitions for some important file table
 * structures etc.
 */

#include <linux/config.h>
#include <linux/linkage.h>
#include <linux/limits.h>
#include <linux/wait.h>
#include <linux/types.h>
#include <linux/vfs.h>
#include <linux/net.h>
#include <linux/kdev_t.h>
#include <linux/ioctl.h>
#include <linux/list.h>
#include <linux/dcache.h>
#include <linux/stat.h>
#include <linux/cache.h>
#include <linux/stddef.h>
#include <linux/string.h>

#include <asm/atomic.h>
#include <asm/bitops.h>

struct poll_table_struct;

/**
 * It's silly to have NR_OPEN bigger than NR_FILE, but you can change
 * the file limit at runtime and only root can increase the per-process
 * nr_file rlimit, so it's safe to set up a ridiculously high absolute
 * upper limit on files-per-process.
 *
 * Some programs (notably those using select()) may have to be
 * recompiled to take full advantage of the new limits.
 */

/* Fixed constants first: */
#undef NR_OPEN
#define NR_OPEN (1024*1024) /* Absolute upper limit on fd num */
#define INR_OPEN 1024       /* Initial setting for nr_file rlimits */

#define BLOCK_SIZE_BITS 10
#define BLOCK_SIZE (1<<BLOCK_SIZE_BITS)

/* And dynamically-tunable limits and defaults: */
extern int max_files, nr_files, nr_free_files;
extern int max_super_blocks, nr_super_blocks;

#define NR_FILE 8192 /* this can well be larger on a larger system */
#define NR_RESERVED_FILES 10 /* reserved for root */
#define NR_SUPER 256

#define MAY_EXEC 1
#define MAY_WRITE 2
#define MAY_READ 4

#define FMODE_READ 1
#define FMODE_WRITE 2

#define READ 0
#define WRITE 1
#define READA 2 /* read-ahead - don't block if no resources */
#define SPECIAL 4 /* For non-blockdevice requests in request queue */

#define WRITEA 5 /* raw write - don't play with buffer lists */

#define NIL_FILP ((struct file *)0)
#define SEL_IN 1
#define SEL_OUT 2
#define SEL_EX 4

/* public flags for file_system_type */
#define FS_REQUIRES_DEV 1
#define FS_NO_DCACHE 2 /* Only dcache the necessary things. */
#define FS_NO_PRELIM 4 /* prevent preloading of entries, even if
                      * FS_NO_DCACHE is not set.
                      */

/*
 * These are the fs-independent mount-flags: up to 16 flags are supported
 */
#define MS_RDONLY 1 /* Mount read-only */
#define MS_NOSUID 2 /* Ignore suid and sgid bits */
#define MS_NODEV 4 /* Disallow access to device special files */
#define MS_NOEXEC 8 /* Disallow program execution */
#define MS_SYNCHRONOUS 16 /* Writes are synced at once */
#define MS_REMOUNT 32 /* Alter flags of a mounted FS */
#define MS_MANDLOCK 64 /* Allow mandatory locks on an FS */
#define S_QUOTA 128 /* Quota initialized for file/directory/symlink */
#define S_APPEND 256 /* Append-only file */
#define S_IMMUTABLE 512 /* Immutable file */
#define MS_NOSYMTIME 1024 /* Do not update access times. */
#define MS_NODIRATIME 2048 /* Do not update directory access times */

#define MS_ODD_RENAME 32768 /* Temporary stuff; will go away as soon
                           * as nfs_rename() will be cleaned up
                           */

/*
 * Flags that can be altered by MS_REMOUNT
 */
#define MS_RMT_MASK      (MS_RDONLY|MS_NOSUID|MS_NODEV|MS_NOEXEC| \
                         MS_SYNCHRONOUS|MS_MANDLOCK|MS_NOATIME|MS_NODIRATIME)

/**
 * Magic mount flag number. Has to be or-ed to the flag values.
 */
#define MS_MGC_VAL 0xC0ED0000  /* magic flag number to indicate "new" flags */
#define MS_MGC_MSK 0xFFF0000   /* magic flag number mask */

/*
 * Note that nosuid etc flags are inode-specific: setting some file-system
 * flags just means all the inodes inherit those flags by default. It might be
 * possible to override it selectively if you really wanted to with some
 * ioctl() that is not currently implemented.
 *
 * Exception: MS_RDONLY is always applied to the entire file system.
 *
 * Unfortunately, it is possible to change a filesystems flags with it mounted
 * with files in use. This means that all of the inodes will not have their
 * i_flags updated. Hence, i_flags no longer inherit the superblock mount
 * flags, so these have to be checked separately. -- rmk@arm.uk.linux.org
 */
#define __IS_FLG(inode,flg) (((inode)->i_sb && (inode)->i_sb->s_flags & (flg)) \
                           || (inode)->i_flags & (flg))

#define IS_RDONLY(inode) (((inode)->i_sb) && ((inode)->i_sb->s_flags & MS_RDONLY))

#define IS_NOSUID(inode)                 __IS_FLG(inode, MS_NOSUID)
#define IS_NODEV(inode)                  __IS_FLG(inode, MS_NODEV)
#define IS_NOEXEC(inode)                 __IS_FLG(inode, MS_NOEXEC)
#define IS_SYNC(inode)                   __IS_FLG(inode, MS_SYNCHRONOUS)
#define IS_MANDLOCK(inode)               __IS_FLG(inode, MS_MANDLOCK)

#define IS_QUOTANIT(inode)               ((inode)->i_flags & S_QUOTA)
#define IS_APPEND(inode)                 ((inode)->i_flags & S_APPEND)
#define IS_IMMUTABLE(inode)              ((inode)->i_flags & S_IMMUTABLE)
#define IS_NOATIME(inode)                __IS_FLG(inode, MS_NOATIME)
#define IS_NODIRATIME(inode)             __IS_FLG(inode, MS_NODIRATIME)

/* the read-only stuff doesn't really belong here, but any other place is
   probably as bad and I don't want to create yet another include file. */

#define BLKROSET    _IO(0x12,93) /* set device read-only (0 = read-write) */
#define BLKROGET    _IO(0x12,94) /* get read-only status (0 = read_write) */
#define BLKRPART    _IO(0x12,95) /* re-read partition table */
#define BLKGETSIZE  _IO(0x12,96) /* return device size */
#define BLKFLSBUF   _IO(0x12,97) /* flush buffer cache */
#define BLKRASET    _IO(0x12,98) /* Set read ahead for block device */
#define BLKRRASE    _IO(0x12,99) /* Get current read ahead setting */
#define BLKPASRA    _IO(0x12,100)/* set filesystem (mm/filemap.c) read-ahead */
#define BLKPASRG    _IO(0x12,101)/* get filesystem (mm/filemap.c) read-ahead */
#define BLKSECTSET  _IO(0x12,102)/* set max sectors per request (ll_rw_blk.c) */
#define BLKSECTGET  _IO(0x12,103)/* get max sectors per request (ll_rw_blk.c) */
```
