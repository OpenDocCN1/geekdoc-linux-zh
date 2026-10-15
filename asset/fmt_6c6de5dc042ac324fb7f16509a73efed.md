
`ext2_readpage()` 调用了 `mpage_readpage()`，这是一个通用的文件系统调用，但它传递了特定文件系统函数 `ext2_get_block()`。通用文件系统函数 `mpage_readpage()` 期望第二个参数是一个 `get_block()` 函数。每个文件系统实现了特定于其格式的 I/O 函数；`get_block()` 将地址空间的逻辑块映射到特定布局中的设备块。让我们来看 `mpage_readpage()` 的细节：

```c
fs/mpage.c

358 int mpage_readpage(struct page *page, get_block_t get_block)

359 {

360     struct bio *bio = NULL;

361     sector_t last_block_in_bio = 0;

362

363     bio = do_mpage_readpage(page, 1,

364         &last_block_in_bio, get_block);

365     if (bio)

366         mpage_bio_submit(READ, bio);

367     return 0;

368 }
```

### 第 360–361 行

我们为 `bio` 结构分配空间，地址空间使用该结构来管理我们正尝试从设备读取的页面。

### 第 363–364 行

调用 `do_mpage_readpage()`，它将逻辑页面转换为由实际页面和块组成的 `bio` 结构。`bio` 结构跟踪与块 I/O 关联的信息。

### 第 365–367 行

我们将新创建的 `bio` 结构发送到 `mpage_bio_submit()` 并返回。让我们花一点时间回顾（高级概述）目前 `read` 函数的流程：

- 1. 使用来自 `read()` 调用的文件描述符定位文件指针，从中获取 `inode`。
- 2. 文件系统层检查内存页缓存是否存在与给定 `inode` 对应的页面或多个页面。
- 3. 如果没有找到页面，文件系统使用特定文件系统驱动将文件的请求部分转换为给定设备上的 I/O 块。
- 4. 我们在页缓存地址空间为页面分配空间，并创建一个 `bio` 结构，将新页面与块设备上的扇区连接。

`mpage_readpage()` 是创建 `bio` 结构并将从页缓存新分配的页面连接到 `bio` 结构的函数。然而，页面中尚未存在数据。这是因为文件系统需要块设备驱动来与设备进行实际交互。这是通过 `mpage_bio_submit()` 中的 `submit_bio()` 完成的：

```c
fs/mpage.c

90 struct bio *mpage_bio_submit(int rw, struct bio *bio)

91 {

92     bio->bi_end_io = mpage_end_read;

93     if (rw == WRITE)

94         bio->bi_end_io = mpage_end_write;

95     submit_bio(rw, bio);

96     return NULL;

97 }
```

### 第 90 行

需要注意的是 `mpage_bio_submit()` 通过 `rw` 参数处理读取和写入调用。它提交了一个 `bio` 结构，在读取情况下它是空的，需要填充；在写入情况下，`bio` 结构是填充好的，块设备驱动将复制内容。

### 第 92–94 行

如果正在进行读取或写入，我们就设置在 I/O 结束时调用的函数。

### 第 95–96 行

我们调用 `submit_bio()` 并返回 `NULL`。记得 `mpage_readpage()` 不处理 `mpage_bio_submit()` 的返回值。

`submit_bio()` 是 Linux 内核通用块设备驱动的一部分。

```c
drivers/block/11_rw_blk.c

2433 void submit_bio(int rw, struct bio *bio)

2434 {

2435 int count = bio_sectors(bio);

2436

2437 BIO_BUG_ON(!bio->bi_size);

2438 BIO_BUG_ON(!bio->bi_io_vec);

2439 bio->rw = rw;

2440 if (rw & WRITE)

2441 mod_page_state(pgpgout, count);

2442 else

2443 mod_page_state(pgpgin, count);

2444

2445 if (unlikely(block_dump)) {

2446 char *bdevname[BDEVNAME_SIZE];

2447 printk(KERNEL_DEBUG "%s:%d: %s block Lu on %s\n",

2448 current->comm, current->pid,

2449 (rw & WRITE) ? "WRITE" : "READ",

2450 (unsigned long long)bio->bi_sector,

2451 bdevname(bio->bi_bdev, b));

2452 }
```

```c
2452  }

2453

2454  generic_make_request(bio);

2455  )
```

第 2433–2443 行

这些调用允许某些调试：设置 `bio` 结构的读/写属性，并执行一些页状态清理工作。

第 2445–2452 行

这些行处理了罕见的块转储（block dump）情况。会抛出一个调试信息。

第 2544 行

`generic_make_request()` 包含了主要功能，并使用特定块设备驱动的请求队列来处理块 I/O 操作。

`generic_make_request()` 的内联内容非常有启发性：

```c
drivers/block/ll1_rw_blk.c

2336 * generic_make_request() 的调用者必须确保 bi_io_vec

2337 * 已设置以描述内存缓冲区，并且 bi_dev 和 bi_sector

2338 * 已设置以描述设备地址，并且

2339 * bi_end_io 和可选的 bi_private 已设置以描述

2340 * 应该如何发出完成通知。
```

在这些阶段，我们构建了 `bio` 结构，因此 `bio_vec` 结构被映射到第 2337 行提到的内存缓冲区，并且 `bio` 结构也用设备地址参数进行了初始化。如果你想进一步在块驱动程序中追踪读取操作，请参阅第 5 章中的“块设备概述”部分，该部分描述了块设备驱动如何处理请求以及其设备的特定硬件限制。图 6.18 展示了 `read()` 系统调用如何跨越内核功能层。

在块设备驱动读取了实际数据并将其放入 `bio` 结构之后，我们所追踪的代码开始回溯。页缓存（page cache）中新分配的页被填充，它们的引用被传回 VFS 层，并复制到原始 `read()` 调用指定的指定的用户区域。

368

第 6 章 • 文件系统

![](img/6525157588f931c50a65c5a42af9a432_395_0.png)

图 6.18
`read()` 自上而下的遍历

然而，我们听到你在提问：“这不只是故事的一半吗？如果我们想写而不是读呢？”

我们希望这些描述能让你大致清楚，`read()` 调用通过 Linux 内核的路径与 `write()` 用的路径是相似的。然而，我们现在概述一些差异。

## 6.5 VFS 系统调用与文件系统层

### 6.5.4 write()

`write()` 调用以与 `read()` 调用相同的方式映射到 `sys_write()`，然后映射到 `vfs_write()`：

```c
fs/read_write.c

244 ssize_t vfs_write(struct file *file, const char __user *buf, size_t count,
      loff_t *pos)

245

{

259     ret = file->f_op->write(file, buf, count, pos);
```

`vfs_write()` 使用通用的 `file_operations` `write` 函数来确定要使用哪种特定的文件系统层。在我们 ext2 的示例中，这是通过 `ext2_file_operations` 结构翻译的：

```c
fs/ext2/file.c

42 struct file_operations ext2_file_operations = {

43     .llseek      = generic_file_llseek,
```
