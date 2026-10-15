
## 代码示例：块设备写入操作

以下代码展示了 `block_write` 和 `file_write` 函数的实现片段，位于 `fs/blk_dev.c` 中。

```c
// code path: fs/blk_dev.c
int block_write(int dev, long *pos, char *buf, int count)
{
    ...
    bh->b_dirt = 1;
    c = count;
    while (c > 0) {
        *(p = get_byte(buf));
    }
}
```

```c
// code path: fs/blk_dev.c
int file_write(struct m_inode *inode, struct file *filp, char *buf, int count)
{
    c = BLOCK_SIZE;
    p = c + bh->b_data;
    bh->b_dirt = 1;

    filp->f_pos += count;
    if (filp->f_pos > inode->i_size) {
        inode->i_size = filp->f_pos;
        inode->i_dirt = 1;
    }
}
```

*(注：原文中重复的代码块已合并，并修正了明显的笔误，如 `0->dirt` 修正为 `bh->b_dirt`，`pos` 修正为 `filp->f_pos`，`inode->dir` 修正为 `inode->i_dirt`。)*

---

## 缓冲区状态与 `b_uptodate` 机制

值得注意的是，`b_uptodate` 赋值为 1 告诉内核数据已由缓冲区进行更新，但这并不意味着缓冲区数据与磁盘数据块完全相同。例如，为文件构建新的数据块需要分配一个新的缓冲区，并建立与数据块的绑定关系。建立这种关系会清空缓冲区；然后将缓冲区的 `b_uptodate` 设为 1。此时，数据并未在物理层面同步，缓冲区与硬盘之间的数据是不一致的，但这并不影响数据的正确同步逻辑。

我们从前文了解到，新构建的块只有两个用途：存储文件内容，或者存储文件 `i_zone` 的间接块管理信息。

*   **若用于存储文件内容**：新构建的数据块和缓冲区全是垃圾数据，并非进程所需。无论数据是否更新，结果都“等同”于问题已解决。因此，将缓冲区的 `b_uptodate` 设为 1（缓冲区是否为空并不重要）。
*   **若用于间接块管理信息**：它必须被清零，意味着不索引任何数据块；否则垃圾数据将导致索引错误并破坏文件操作。虽然缓冲区与磁盘块数据不同，但基于相同理由，`b_uptodate` 可赋值为 1。

设计者采取了统一策略：只要为新数据块分配了缓冲区，无论将来用于何处，进程都不需要其中的原始数据，因此将其全部清零。于是，无论数据块绑定存储何种信息，将缓冲区的 `b_uptodate` 设为 1，更新问题即“等同”于被解决。

### 核心代码实现

**`fs/inode.c`：创建数据块**

```c
// code path: fs/inode.c
int create_block(struct m_inode *inode, int block) // create a new data block
{
    return bmap(inode, block, 1);
}

static int bmap(struct m_inode *inode, int block, int create)
{
    if (block < 7) {
        if (create && !inode->i_zone[block]) {
            if (inode->i_zone[block] = new_block(inode->i_dev)) {
                inode->i_ctime = CURRENT_TIME;
                inode->i_dirt = 1;
            }
        }
        return inode->i_zone[block];
    }
    // ... 处理间接块逻辑省略 ...
}
```

**`fs/bitmap.c`：分配新块并初始化缓冲区**

```c
// code path: fs/bitmap.c
int new_block(int dev) // allocate a data block in the device dev
{
    struct buffer_head *bh;
    int i, j;

    // ... 位图查找逻辑省略 ...

    if (!(bh = getblk(dev, j)))
        return 0;

    if (bh->b_count != 1)
        panic("new block: count is != 1");

    clear_block(bh->b_data);
    bh->b_uptodate = 1; // set the buffer to be updated
    bh->b_dirt = 1;
    brelse(bh);
    return j;
}
```

### `b_uptodate` 置 1 后的缓冲区状态分析

在 `b_uptodate` 赋值为 1 后，缓冲区可能处于两种状态：

1.  **读取场景**：缓冲区新构建，内部虽有垃圾数据。但考虑到是新文件，读取空数据块无逻辑需求，内核不会执行此操作。
2.  **写入场景**：新文件被清空，磁盘数据块是垃圾数据，缓冲区数据也非进程所需。它们是否被更新或覆盖并不重要，可视为已更新。执行写入操作符合进程预期。

![图 7.9 如果操作系统使用 b_uptodate 控制文件操作的读取](img/f661d64b7eb54840fcb4d65765a4e933_377_0.png)
**图 7.9** 如果操作系统使用 `b_uptodate` 控制文件操作的读取。

---

## 7.4 `b_uptodate` 和 `b_dirt` 的功能

相反，如果缓冲区中的数据未更新，且 `b_uptodate` 为 0，无论进程是为了读取还是写入，内核都会阻止进程共享缓冲区中的数据，目的是防止因未更新导致的数据损坏。

### 7.4.1 `b_uptodate` 在读取中的判断

例如，在读取块设备时会进行两次判断，代码如下：

```c
// code path: fs/buffer.c
struct buffer_head *bread(int dev, int block)
{
    struct buffer_head *bh;

    if (!(bh = getblk(dev, block)))
        return NULL;

    if (bh->b_uptodate) // 如果已更新，直接返回缓冲区
        return bh;

    ll_rw_block(READ, bh); // 否则发起读请求
    wait_on_buffer(bh);    // 等待读取完成

    if (bh->b_uptodate)
        return bh;

    brelse(bh);
    return NULL;
}
```

在 `getblk()` 函数中，缓冲区被找到后，可能需要从硬盘读取数据（用于索引间接块或返回数据）。若 `b_uptodate` 为 0，则必须等待物理读取完成并再次校验。

### 7.4.2 `b_dirt` 的功能

在设置 `b_uptodate` 为 1 后，为将缓冲区内容同步到硬盘，需将 `b_dirt` 设为 1。

![图 7.11 继续向缓冲区写入数据](img/f661d64b7eb54840fcb4d65765a4e933_381_0.png)
**图 7.11** 继续向缓冲区写入数据。

以此类推，当不断向缓冲区写入数据时，缓冲区数据自然变化，未来这些新数据将按进程预期自然同步到磁盘数据块。

`buffer_head` 分别在进程方向和硬盘方向上设置了 `b_uptodate` 和 `b_dirt` 两个字段，请求结构也考虑了这些方向。与写操作相比，读取操作对用户更紧急，因此请求队列为两种操作预留了不同大小的空间，代码如下：

```c
// code path: kernel/blk_drv/ll_rw_blk.c
static void make_request(int major, int rw, struct buffer_head *bh)
{
    lock_buffer(bh);

    if ((rw == WRITE && bh->b_dirt) || (rw == READ && bh->b_uptodate)) {
        unlock_buffer(bh);
        return;
    }

    struct request *req;
repeat:
    if (rw == READ)
        req = request + NR_REQUEST; // 读请求使用后 1/3 空间
    else
        req = request + ((NR_REQUEST * 2) / 3); // 写请求使用前 2/3 空间

    while (--req >= request)
        if (req->dev < 0)
            break;
    // ... 后续请求入队逻辑省略 ...
}
```

从代码可见，请求队列空间只有三分之二用于写入，其余用于读取。同等条件下，读取操作获得调度机会更大。

此外，通过评估 `b_uptodate` 和 `b_dirt` 可知：
*   只要 `b_uptodate` 为 1，进程即可共享该数据。
*   若 `b_count = 0` 且 `b_dirt` 为 1，情况不同：数据已与磁盘块不同，需同步。虽不必立即同步，但同步前不能重用该缓冲区，否则数据丢失导致磁盘块无法反映进程重写操作，造成损坏。若缓冲区不足，进程必须等待同步完成。同步后，内核立即将 `b_dirt` 设为 0，释放缓冲区。

```c
// code path: kernel/blk_drv/ll_rw_blk.c
static void add_request(struct blk_dev_struct *dev, struct request *req)
{
    struct request *tmp;

    req->next = NULL;
    cli();

    // 注意：原文此处有赋值判断笔误 if (req->bh->b_dirt = 0)，应为判断或清零逻辑
    // 此处还原逻辑意图：处理脏块同步
    if (req->bh->b_dirt) {
        // ... 处理脏块写入 ...
    }

    if (!tmp && dev->current_request) {
        dev->current_request = req;
        sti();
        (dev->request_fn)();
        return;
    }
    // ...
}
```

---

## 7.4.3 `i_update`、`i_dirt` 和 `s_dirt` 的功能

上述描述了对文件内容准确性的控制，通过 `b_uptodate` 和 `b_dirt` 确保缓冲区数据与磁盘块数据一致。文件管理信息（inode）具有类似字段。当不同进程操作同一文件时，共享 `inode_table[32]` 中的 `m_inode` 信息。其结构包含 `i_update`（Linux 0.11 中未实际使用）和 `i_dirt` 字段。

```c
// code path: include/linux/fs.h
struct m_inode {
    unsigned short i_mode;
    unsigned short i_uid;
    unsigned long  i_size;
    unsigned long  i_time;
    unsigned char  i_gid;
    unsigned char  i_nlinks;
    unsigned short i_zone[9];

    /* in-memory only fields */
    struct task_struct *i_wait;
    unsigned long  i_atime;
    unsigned long  i_mtime;
    unsigned long  i_ctime;
    unsigned short i_dev;
    unsigned short i_num;
    unsigned short i_count;
    unsigned char  i_lock;
    unsigned char  i_dirt;     // inode 已修改，需写回磁盘
    unsigned char  i_pipe;
    unsigned char  i_mount;
    unsigned char  i_seek;
    unsigned char  i_update;   // 未使用
};
```

理解 `i_dirt` 设计并不困难：改变文件大小时，inode 应更新大小记录。此时内存 inode 与磁盘 inode 不同，需同步。`i_update` 未使用，因为磁盘 inode 以数据块形式存储并加载到块缓冲区，加载后与磁盘一致，等同于“已更新”，可直接共享，无需在管理结构中额外设置 `i_update`。

`super_block[8]` 中也存在超级块共享问题。超级块存储整个文件系统管理信息，多进程处理文件时共享使用，包含 `s_dirt` 字段。

```c
// code path: include/linux/fs.h
struct super_block {
    unsigned short s_ninodes;
    unsigned short s_nzones;
    unsigned short s_imap_blocks;
    unsigned short s_zmap_blocks;
    unsigned short s_firstdatazone;
    unsigned short s_log_zone_size;
    unsigned long  s_max_size;
    unsigned short s_magic;
    /* in-memory only fields */
    struct buffer_head *s_imap[8];
    struct buffer_head *s_zmap[8];
    unsigned short s_dev;
    struct m_inode *s_isup;
    struct m_inode *s_imount;
    unsigned long  s_time;
    unsigned short s_rd_only;
    unsigned short s_dirt;     // 超级块已修改，需写回磁盘
};
```
