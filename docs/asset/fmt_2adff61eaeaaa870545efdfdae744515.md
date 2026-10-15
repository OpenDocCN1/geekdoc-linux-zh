
文件 I/O 通常是文件系统实现中最困难区域之一。为了提高文件系统性能，这是一个花费大量时间的区域。在 Linux 中，只需极少的 I/O 时间即可提供完整工作的文件系统。Linux 中有很多通用函数供文件系统调用，以处理与页面缓存和缓冲区的所有交互。

第 8 章中的 2.2 Linux 内核描述了与页面缓存的部分交互。由于本章展示的是简化活动视图，因此没有描述缓存内部。相反，下面的章节显示了内核如何与 uds 出的 `ux_get_block()` 函数交互。该函数可以从文件读取数据或分配块并写入数据。

首先是 I/O 的主要入口点。它们通过 `file_operations` 结构导出：

```
struct file_operations ux_file_operations = {
	lseek:   generic_file_lseek,
	read:    generic_file_read,
	write:   generic_file_write,
	mmap:    generic_file_mmap,
};
```

因此，所有主要的文件 I/O 相关操作，文件系统都推给了 Linux 通文件 I/O 例程。对于任何映射文件交互的操作（无论是用户级映射还是处理页面缓存内的操作），情况也是如此。地址相关的操作为：

```
struct address_space_operations ux_aops = {
	readpage:  ux_readpage,
```

# 为 Linux 内核开发文件系统 371

```
writepage: block_sync_page,
prepare: ux_prepare_write,
commit: generic_commit_write,
bmap: ux_bmap;
```

对于此向量中定义的所有函数，uufs 还会调用通用的内核例程。例如，考虑 `ux_readpage()` 函数（第 976 到 980 行），它在这里也显示：

```
int
ux_readpage(struct file *file, struct page *page)
{
    return block_read_full(page, ux_get_block);
}
```

对于 `uxfs` 导出的每个函数，uufs 都会调用一个通用函数并传递 `ux_get_block()` 例程。在进入文件 I/O 的文件系统之前，在介绍接下来的三个部分中的每一个部分之前，首先展示 `ux_get_block()`（第 929 到 968 行）将很有帮助：

```
int
ux_get_block(struct inode *inode, long block,
    struct buffer_head *bh_result, int create)
```

当内核需要访问文件中尚未被缓存的部分时，就会调用 `ux_get_block()`。`block` 参数是文件内的逻辑块，其中块 0 映射到文件偏移量 0，块 1 映射到文件偏移量 512，依此类推。`create` 参数指示内核是需要读取还是写入文件。如果 `create` 为 0，内核正在从文件中读取。如果 `create` 为 1，文件系统将在 `block` 所引用的偏移量处分配存储。

以 `block` 为 0 的例，文件系统必须如下填充头头中的适当字段：

```
bh_result->b_dev = inode->i_dev;
bh_result->b_blocknr = ufs->i_addr[block];
```

内核随后将执行数据读取。在 `create` 为 1 的情况下，文件系统必须通过 `ux_block_alloc()` 分配一个新的数据块，并设置相应的 `i_addr[]` 槽来引用新块。一旦分配完成，在内核执行 I/O 操作之前，必须初始化 `buffer_head` 结构。

## 从普通文件读取

文件系统对于读取普通文件没有执行任何操作。在读取操作（`file_operations` 向量）的位置，文件系统指定了 `generic_file_read()` 函数。

# 372 UNIX 文件系统——演变、设计与实现

为了显示如何进入文件系统，在 `ux_get_block()` 上设置了断点，并通过运行 `cat program` 命令从 uufs 文件系统读取 `passwd` 文件。通过查看 `passwd` 的大小：

```
# ls -l /mnt/passwd
--rw-r--r-- 1 root      root          1203 Jul 24 07:51 /etc/passwd
```

将有三个数据块需要访问。当命中第一个断点时：

```
Breakpoint 1, ux_get_block (inode=0xcf23a420, block=0, bh_result=0xc94f4740, create=0)
  at ux_file.c:21
    struct super_block *sb = inode->i_sb;
(gdb) bt
#0 ux_get_block (inode=0xcf23a420, block=0, bh_result=0xc94f4740, create=0)
  at ux_file.c:21
    0xc01401b in block_read_full_page (page=0xc01250c0,
    get_block=0xd085551ba (ux_get_block) at buffer=0xc1781
    0xd085551ba in read_page (file=0xc01c9360, page=0xc01250c0)
  at ux_file.c:67
#3 0xc012e73 in generic_file_read (file=0xc01c9360,
    desc=0xc96d15c, actor=0xc012af0 <file_reader>
  at filemap.c:1401
#4 0xc012ec72 in generic_file_read (file=0xc01c9360, buf=0x804eb28 **,
    count=4096, ppos=0xc01c9380 at filemap.c:1594
#5 0xc013d7c8 in sys_read (fd=3, buf=0x804eb28 **, count=4096)
  at read_write.c:162
0xc0107d3b in system_call ()
```

这里有两个区间点。第一个是调用 `ux_readpage()`。操作页缓存的例程可以在 `mm/filemap.c` 中找到。第二个是调用 `ux_get_block()`。因为由于文件系统大小的 I/O 倍数，调用了 `block_read_full_page()` 函数来填充页。在读取文件的情况下，只有三个 512 字节的块，还不足以填满整个页（4KB）。内核必须读取尽可能多的，然后填充页的剩余部分。传递给 `ux_get_block()` 的 `block` 参数为 0，因此文件系统将初始化从文件中读取的前 512 字节。当下次命中断点时：

```
Breakpoint 1, ux_get_block (inode=0xcf23a420, block=1, bh_result=0xc94f4e0, create=0)
  at ux_file.c:21
    struct super_block *sb = inode->i_sb;
(gdb) bt
#0 ux_get_block (inode=0xcf23a420, block=1,
    bh_result=0xc94f4e0, create=0)
  at ux_file.c:21
```

# 为 Linux 内核开发文件系统 373

1 0xc010b1f in block_read_full_page (page=0xc125fc0)，内核传递了 block 2，因此最后的 512 字节将从文件中读取。最后一次对 `ux_get_block()` 的调用所示：

(gdb) bt

#0 ux_get_block (inode=0xcf23a420, block=1,

    bh_result=0xc94f4e0, create=0)

  at ux_file.c:21

#1 0xc010b1f in block_read_full_page (page=0xc125fc0),

    get_block=0xd085551ba (ux_get_block) at buffer=0xc1781

#2 0xd08551ba in read_page (file=0xc01c9360, page=0xc01250c0)

    ux_file.0)

    at ux_file.c:67

对于写入普通文件，uufs 写入文件的机制与读取文件非常相似。

## 写入普通文件

文件系统对于写入普通文件没有执行任何操作。在写入操作（`file_operations` 向量）的位置，文件系统指定了 `generic_file_read()` 函数。
