
```c
#define BMAP_IOCT 1 /* 已废弃 - 保留以兼容旧代码 */

#define FBMAP _IO(0x00,1) /* bmap 访问 */

#define FGETBSZ _IO(0x00,2) /* 获取用于 bmap 的块大小 */

#ifdef _KERNEL_

#include <asm/semaphore.h>

#include <asm/byteorder.h>

extern void update_atime (struct inode *);

#define UPDATE_ATIME(inode) update_atime (inode)

extern void buffer_init(unsigned long);

extern void inode_init(void);

extern void file_table_init(void);

extern void dcache_init(void);

/* 缓冲区状态位 */

#define BH_Uptodate 0 /* 如果缓冲区包含有效数据，则为 1 */

#define BH_Dirty 1 /* 如果缓冲区已脏，则为 1 */

#define BH_Lock 2 /* 如果缓冲区已加锁，则为 1 */

#define BH_Req 3 /* 如果缓冲区已失效，则为 0 */

#define BH_Mapped 4 /* 如果缓冲区有磁盘映射，则为 1 */

#define BH_New 5 /* 如果缓冲区是新的且尚未写出，则为 1 */

#define BH_Protected 6 /* 如果缓冲区受保护，则为 1 */

/*

 * 尽量将最常用字段保持在单个缓存行内（16 字节）

 * 以提升性能。这种排列顺序在 32 位处理器上

 * 尤其有益。

 *

 * 前 16 字节用于在块哈希链表上进行搜索

 * 时使用的数据（例如 getblk() 及其相关函数）。

 *

 * 后 16 字节用于 LRU 缓冲区扫描，

 * 由 sync_buffers() 和 refill_freelist() 使用。-- sct

 */

struct buffer_head {

 /* 第一个缓存行： */

 struct buffer_head *b_next; /* 哈希队列链表 */

 unsigned long b_blocknr; /* 块号 */

 unsigned short b_size; /* 块大小 */

 unsigned short b_list; /* 该缓冲区所在的链表 */

 kdev_t b_dev; /* 设备（B_FREE = 空闲） */

 atomic_t b_count; /* 使用此块的用户数 */

 kdev_t b_rdev; /* 实际设备 */

 unsigned long b_state; /* 缓冲区状态位图（见上文） */

 unsigned long b_flushtime; /* 应当写出（脏）缓冲区的时间 */

 struct buffer_head *b_next_free;/* LRU/空闲链表连接 */

 struct buffer_head *b_prev_free;/* 缓冲区的双向链表 */

 struct buffer_head *b_this_page;/* 同一页内缓冲区组成的循环链表 */

 struct buffer_head *b_reqnext; /* 请求队列 */

 struct buffer_head **b_pprev; /* 哈希队列的双向链表 */

 char * b_data; /* 指向数据块的指针（512 字节） */

 struct page *b_page; /* 该 bh 映射到的页 */

 void (*b_end_io)(struct buffer_head *bh, int uptodate); /* I/O 完成回调 */

 void *b_dev_id;

 unsigned long b_rsector; /* 实际缓冲区在磁盘上的位置 */

 wait_queue_head_t b_wait;

 struct kiobuf * b_kiobuf; /* 拥有此 I/O 的 kiobuf */

 };

 typedef void (bh_end_io_t)(struct buffer_head *bh, int uptodate);

 void init_buffer(struct buffer_head *, bh_end_io_t *, void *);

 #define __buffer_state(bh, state) ((bh)->b_state & (1UL << BH_##state)) != 0

 #define buffer_uptodate(bh) __buffer_state(bh,Uptodate)

 #define buffer_dirty(bh) __buffer_state(bh,Dirty)

 #define buffer_locked(bh) __buffer_state(bh,Lock)

 #define buffer_req(bh) __buffer_state(bh,Req)

 #define buffer_mapped(bh) __buffer_state(bh,Mapped)

 #define buffer_new(bh) __buffer_state(bh,New)

 #define buffer_protected(bh) __buffer_state(bh,Protected)

 #define bh_offset(bh) ((unsigned long) (bh)->b_data & ~PAGE_MASK)

 extern void set_bh_page(struct buffer_head *bh, struct page *page, unsigned long offset);

 #define touch_buffer(bh) set_bit(PG_referenced, &bh->b_page->flags)

 #include <linux/pipe_fs_i.h>

 #include <linux/minix_fs_i.h>

 #include <linux/ext2_fs_i.h>

 #include <linux/hfs_fs_i.h>

 #include <linux/nfs_fs_i.h>

 #include <linux/msdos_fs_i.h>

 #include <linux/umsdos_fs_i.h>

 #include <linux/iso_fs_i.h>

 #include <linux/nfs_fs_i.h>

 #include <linux/sysv_fs_i.h>

 #include <linux/affs_fs_i.h>

 #include <linux/uifs_fs_i.h>

 #include <linux/efs_fs_i.h>

 #include <linux/coda_fs_i.h>

 #include <linux/romfs_fs_i.h>

 #include <linux/smb_fs_i.h>

 #include <linux/hfs_fs_i.h>

 #include <linux/adfs_fs_i.h>

 #include <linux/qnx4_fs_i.h>

 #include <linux/bfs_fs_i.h>

 #include <linux/udf_fs_i.h>

 #include <linux/ncp_fs_i.h>

 #include <linux/proc_fs_i.h>

 #include <linux/usdev_fs_i.h>

 /*

 * 属性标志。这些值应进行按位或运算，

 * 以判断哪些内容已变更！

 */

 #define ATTR_MODE      1

 #define ATTR_UID       2

 #define ATTR_GID       4

 #define ATTR_SIZE      8

 #define ATTR_ATIME     16

 #define ATTR_MTIME     32

 #define ATTR_CTIME     64

 #define ATTR_ATIME_SET 128

 #define ATTR_MTIME_SET 256

 #define ATTR_FORCE     512 /* 非变更，而是强制变更 */

 #define ATTR_ATTR_FLAG 1024

 /*

 * 这是 Inode 属性结构，用于 notify_change()。

 * 它使用上述定义作为标志，

 * 以识别哪些值发生了变化。

 * 通过这种方式，文件系统只需关注

 * 它所关心的属性值即可。本质上，

 * 这些是 VFS 层可以请求 FS 层变更的属性。

 *
 */
```
