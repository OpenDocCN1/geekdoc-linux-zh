
页面共享情况如图 6.29 所示。

![](img/f661d64b7eb54840fcb4d65765a4e933_351_0.png)

**图 6.30** 进程 A 准备 push。

**进程 A 准备 push 操作。** 我们假设进程 A 下一个执行，并且这是一个 push 操作。让我们看看会发生什么。
现在进程 A 程序的所有页面都是只读的。这意味着无论是代码占据的页面还是原始 push 对应的页面，只能执行读操作而不能执行写操作。然而，push 操作是一个写操作。在 push 过程中解析出相应的线性地址后，它必须映射到一个只读页，并产生“页写保护”（page write protect）中断。如图 6.30 所示。

**进程 A 的动作触发了页保护。** 当发生页保护时，缺页中断对应的函数是 `un_wp_page()` 函数。第一步是在主内存中申请一个空闲页（下文称为新页），为 push 栈位置的页的所有数据（下文称为原始页）制作备份。然后，我们将原始页的引用计数减 1。这是因为原始页中的数据将被备份到新页，进程 A 将去新页上操作数据，不再需要维护与原始页的关系，因此引用计数减去 1。

代码如下：

```c:mm/memory.c
void un_wp_page(unsigned long * table_entry)
{
    if (!(new_page = get_free_page())) // 获取一个新页
        return;

    if (old_page >= LOW_MEM)
        mem_map[MAP_NR(old_page)]--; // 页的引用计数减 1
    ....
}
```

![](img/f661d64b7eb54840fcb4d65765a4e933_352_0.png)

**图 6.31** 为进程 A 申请新页以存储 push 数据。

为进程 A 执行页写保护并申请新页后，内存的主要分布如图 6.31 所示。
值得注意的是，我们让原始页的引用计数减 1 而不是完全释放它。这是因为在操作系统中，所有资源可能被多个进程共享，例如文件节点、内存管理页等，因此需要通过引用计数来表示状态。当一个进程终止与它们的关系时，其他进程可能在做同样的事情；那么简单地“释放”是不妥的。

**将进程 A 的页表指向新的应用页。** 尽管已经申请了新页，但 A 页表中对应原始页的页表项仍然指向原始页。因为没有对应新页的页表项，所以无法找到物理地址。因此，它也让进程 A 页中指向原始页的页表项指向新页，并将属性从“只读”改为“可读可写”，进程 A 就就有处理新页中数据的了。
代码如下：

```c:mm/memory.c
void un_wp_page(unsigned long * table_entry)
{
    if (old_page >= LOW_MEM)
        mem_map[MAP_NR(old_page)]--;

    *table_entry = new_page | 7;
    // 7 的二进制形式是 111，意味着一个新页可以读和写。

    invalidate();
    copy_page(old_page, new_page);
}
```

![](img/f661d64b7eb54840fcb4d65765a4e933_353_0.png)

**图 6.32** 进程 A 的页表对应新的应用。

当此操作完成后，分配给 A 的新页如图 6.32 所示。

**将原始页的内容拷贝到进程 A 的新应用页。** 当一切就绪后，你可以将原始页的内容拷贝到新页。此操作后，进程 A 将在新页中完成 push 操作。

```c:mm/memory.c
void un_wp_page(unsigned long * table_entry)
{
    if (old_page >= LOW_MEM)
        mem_map[MAP_NR(old_page)]--;

    *table_entry = new_page | 7; // 进程 A
    invalidate();
    copy_page(old_page, new_page); // 在这里我们将原始页的数据拷贝到新页，让进程 A 使用
}
```

在拷贝操作后，新内存页中的存储情况、进程 A 应用如图 6.33 所示。

**进程 B 正在准备共享页的操作。** 在进程 A 完成后，进程 B 需要访问原始页。由于原始页是只读的，如果 B 尝试写入，也会触发缺页。这与进程 A 的机制相同。

**进程 B 的动作触发了页保护。** 当发生页保护时，缺页中断对应的函数是 `un_wp_page()` 函数。第一步是在主内存中申请一个空闲页（下文称为新页），为 push 栈位置的页的所有数据（下文称为原始页）制作备份。然后，我们将原始页的引用计数减 1。这是因为原始页中的数据将被备份到新页，进程 B 将去新页上操作数据，不再需要维护与原始页的关系，因此引用计数减去 1。

代码如下：

```c:mm/memory.c
void un_wp_page(unsigned long * table_entry)
{
    if (!(new_page = get_free_page())) // 获取一个新页
        return;

    if (old_page >= LOW_MEM)
        mem_map[MAP_NR(old_page)]--; // 页的引用计数减 1
    ....
}
```

设计缓冲区（buffer）能给系统的运行带来哪些好处？

我们认为这主要体现在两个方面：

1. 它形成了所有块设备的统一分布，使得操作系统的设计更加方便和灵活。
2. 它让块设备的文件操作运行得更高效。

第一个方面相对容易理解，而缓冲区是理解操作系统的难点之一。因此，在本章中，我们将通过多进程操作文件的两个示例，详细解释缓冲区设计是如何提高块设备文件操作的运行效率的。

在图 7.1 中，我们可以发现进程内存空间和缓冲区内存空间相同似乎存在一个问题。在进程内存空间和硬盘之间交换数据时增加一个缓冲区，只增加了内存中数据交接的时间，但这种数据交接并没有任何数据处理。它仅仅是简单的交接，应该只会增加 CPU 资源的消耗。为什么它比直接从硬盘交换数据还要快呢？

原因是缓冲区共享。在计算机中，内存与内存之间的数据交互速度比内存与硬盘之间快两个级。如果进程 A 从硬盘读取数据到缓冲区，进程 B 也需要读取这些数据，那么它就不需要从硬盘读取，而是可以直接从缓冲区读取。这样进程 B 读取该数据所需的时间只有进程 A 的约百分之一，效率提升了两个数量级。如果有进程 C、D、E 等进程都需要读取这些数据，整个计算机的效率将大大提高。这就是缓冲区共享的一种模型；意味着不同进程共享缓冲区中的相同数据。如果进程 A 读取数据、使用这些数据，并在一段时间后再次读取这些数据，而它仍然留在缓冲区中，进程 A 可以直接从缓冲区读取，而不需要花费硬盘时间。这是共享的另一种模式，即同一个进程在不同时间共享缓冲区中的数据。另一种是这两种模式的结合。我们上面分析的是读操作共享，这与写操作是类似的。

从分析中发现，如果我们想提高文件读写的整体效率，应该尽可能让缓冲区共享数据。如果想实现这一点，最有效的方法是让数据尽可能留在缓冲区中。

我们可以说，内核设计缓冲区的设计是为了确保数据交互的正确性，并让数据尽可能留在缓冲区中。在本章中，我们将通过多进程操作文件的两个示例，解释内核是如何实现数据尽可能留在缓冲区这一目标的。

## 7.2 缓冲区结构

缓冲区涉及进程、内存和文件。它包含大量复杂的代码，不容易理解。它是操作系统的难点之一。为了学习和掌握缓冲区设备，让我们先看缓冲区结构（图 7.2）。

在 Linux 中，为了支持缓冲区，设计了两个重要的管理信息：`buffer_head` 和 `request`。`buffer_head` 主要负责进程与缓冲区之间的数据交互。在确保数据交互正确的情况下，让数据尽可能留在缓冲区中。`request` 主要负责缓冲区与块设备之间的数据交互。在数据交互正确的情况下，让进程在缓冲区块中修改的数据尽快同步到块设备中。

![](img/f661d64b7eb54840fcb4d65765a4e933_359_0.png)

**图 7.2** 缓冲区、`buffer_head` 和 `request` 的模式图。

数据结构代码如下：

```c:include/linux/fs.h
struct buffer_head {
    char *b_data;                /* 指向数据块 (1024字节) */
    unsigned long b_blocknr;     /* 块号 */
    unsigned short b_dev;        /* 设备 (0 = free) */
    unsigned char b_update;      /* 0-clean, 1-dirty */
    unsigned char b_bd;          /* 使用此块 */
    unsigned char b_count;       /* 0-ok, 1-locked */
    unsigned char b_lock;
    struct task_struct *b_wait;
    struct buffer_head *b_prev;
    struct buffer_head *b_next;
    struct buffer_head *b_prev_free;
};

struct request {
```

```c:kernel/blk_drv/blk.h
struct request {
    int dev;                /* 无设备则为 -1 */
    int cmd;                /* READ 或 WRITE */
    int errors;
    unsigned long sector;
    unsigned long nr_sectors;
    char *buffer;
    struct task_struct *waiting;
    struct buffer_head *bh;
    struct request *next;
};
```

## 7.3 缓冲区的功能

`buffer_head`、`b_dev` 和 `request` 是重要的成员。`buffer_head`、`b_dev` 和 `request` 是支持缓冲区设备的重要成员。

### 7.3.1 确保数据交互的正确性

如果我们想确保数据交互的正确性，必须首先确保缓冲区块与指定的设备（dev）和块（block）绑定。这是因为 `buffer_head` 是缓冲区中此类结构的唯一实例，它用于管理缓冲区块与硬盘之间的数据交互。代码如下：

```c:fs/buffer.c
struct buffer_head *getblk(int dev, int block)
{
    // ... (实现细节)
}
```

当找到 `buffer_head` 时，发现缓冲区块留在缓冲区中是可能的，因为缓冲区块与硬盘之间的数据交互不在缓冲区中。

从代码中我们可以看到，申请一个新的时，它会锁定缓冲区块与硬盘之间的关系。这使得内核能够在进程方向确定文件位置，并切换到 `b_dev` 和 `b_blocknr`。当找到 `buffer_head` 时，发现缓冲区块留在缓冲区中是可能的，因为缓冲区块与硬盘之间的数据交互不在缓冲区中。

当读取文件时，内核通过指针计算文件数据内容所在的 `b_dev` 和 `b_blocknr`。

实现 `break()` 函数时，它不应直接处理磁盘的数据块。代码如下：

```c:fs/file_dev.c
int file_read(struct m_inode *inode, struct *filp, char *buf, int count) // 读取文件
{
    if (left < count == 0)
        return 0;

    while (left) {
        if (nr != bmap(inode, filp->f_pos) / BLOCK_SIZE) { // 通过文件偏移量指针，计算块号
            if (!bb == bread(inode->i_dev, nr)) // 在实际参数中 inode->i_dev 是
                break;
        } else {
            bb = NULL;
            nr = filp->f_pos % BLOCK_SIZE;
```
