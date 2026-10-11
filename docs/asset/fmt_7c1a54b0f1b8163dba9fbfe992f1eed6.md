
```c
drivers/block/blk_rw_blk.c
1397 request_queue_t *blk_init_queue(request_fn, rfn, spinlock_t *lock)
1398 (
1399    request_queue_t *q;
1400    static int printed;

1402    q = blk_alloc_queue(GFP_KERNEL);
1403    if (!q)
1404      return NULL;

1406    if (blk_init_free_list(q))
1407      goto out_init;

1409 if (!printed) {
1410   printed = 1;
1411   printf("Using %s scheduler\n", chosen_elevator->elevator_name);
)
1414 if (elevator_init(q, chosen_elevator)) {
1415   goto out_elv;

1417   q->request_fn = rfn;
1418   q->back_merge_fn = back_merge_fn;
1419   q->front_merge_fn = front_merge_fn;
1420   q->merge_requests_fn = merge_requests_fn;
1421   q->prep_rq_fn = NULL;
1422   q->unplug_fn = generic_unplug_device;
1423   q->queue_flags = (1 << QUEUE_FLAG_CLUSTER);
1424   q->queue_lock = lock;

1426   blk_queue_segment_boundary(q, 0xffffffff);

1428   blk_queue_make_request(q, __make_request);
1429   blk_queue_max_segment_size(q, MAX_SEGMENT_SIZE);

1431   blk_queue_max_hw_segments(q, MAX_HW_SEGMENTS);
1432   blk_queue_max_phys_segments(q, MAX_PHYS_SEGMENTS);

1434   return q;
1435 out_elv:
1436   blk_cleanup_queue(q);
1437   out_init;
1438   kmem_cache_free(requestq_cachep, q);
1439   return NULL;
1440 }
```

# 第 1402 行

从内核内存中分配队列并清零其内容。

# 第 1406 行

初始化包含读取队列和写入队列的请求列表。

# 第 1414 行

将选定的电梯与此队列关联并初始化。

# 第 1417–1424 行

将特定的电梯函数与此队列关联。

## 5.2 设备

### 第 1426 行

该函数设置段合并的边界并检查其是否达到最小大小。

### 第 1428 行

该函数设置驱动程序从队列中获取请求的函数。它允许使用备用函数跳过队列。

### 第 1429 行

初始化合并段的上限限制。

### 第 1431 行

初始化物理设备可以处理的最大段数。

### 第 1432 行

初始化每个请求的最大物理段数。

`第 1429–1432` 行的值设置在 `include/linux/blkdev.h` 中。

### 第 1434 行

返回初始化的队列。

### 第 1435–1439 行

发生错误时清理内存的例程。

现在我们已经就绪并初始化了请求队列。

在探索通用设备层和通用块驱动程序之前，让我们快速追踪一下实现块设备 I/O 操作所经过的软件层。（参考图 5.4）。

在应用层面，应用程序启动了一个文件操作，如 `read()`。该请求由虚拟文件系统（VFS）层处理（第 4 章介绍），在 VFS 层找到文件的 `dentry` 结构，并通过 `inode` 结构调用文件的 `read()` 函数。VFS 层尝试在它的缓冲区缓存中查找请求的页面，但如果未命中，则调用文件系统处理器来获取相应的物理块。`inode` 与文件系统关联。

# 第 5 章 • 输入/输出

处理器，它与正确的文件系统关联。文件系统处理器调用请求队列实用程序，这些实用程序是通用块设备层的一部分，用于创建一个具有正确物理块和设备的请求。设备被放入请求队列中，该队列由通用块设备层维护。

## 5.2.3 示例：“通用”块驱动程序

我们现在来看下通用块设备层。参考图 5.4，它位于物理设备层之上，文件系统层之下。通用块设备层最重要的工作是维护请求队列及其相关的辅助例程。

我们首先通过 `register_blkdev(major, dev_name, fops)` 注册我们的设备。该函数接收请求的主设备号、块设备的名称（显示在 `/dev` 目录中），并返回指向文件操作结构体的指针。如果成功，它将返回所需的主设备。

接下来，我们创建 `gendisk` 结构体。

`include/linux/genhd.h` 中的函数 `alloc_disk(int minors)` 接收分区数量并返回指向 `gendisk` 结构体的指针。我们现在来看 `gendisk` 结构体：

```c
081 struct gendisk {
082    int major;                /* 驱动的主号 *
083    int first_minor;
084    int minors;
085    char disk_name[16];      /* 主驱动的名称 *
086    struct hd_disk *part;       /* (通过主索引) *
087    struct block_device_operations fops;
088    struct request_queue *queue;
089    void *private_data;
090    sector_t capacity;
091
092    int flags;
093    char devfs_name[64];     /* devfs 杂项 *
094    int number;              /* 同样的内容 */
095    struct device *driverfs;
096    struct kobject *kobj;
097
098    struct timer_rand_state *random;
099    int policy;
101  unsigned sync_io;    /* RAID */
102  unsigned long stamp, stamp_idle;
103  int in_flight;
104  #ifdef CONFIG_SMP
105    struct disk_stats *dkstats;
106  #else
107    struct disk_stats dkstats;
108  #endif
109  );
```

## 5.2 设备

`major_num` 字段通过 `register_blkdev()` 的结果进行填充。

硬盘的块设备可以处理多个物理驱动器。尽管这取决于驱动程序，但从设备号通常标记每个物理驱动器。`first_minor` 字段是第一个物理驱动器。

`disk_name`（例如 `hda` 或 `sdb`）是整个磁盘的文本名称。（磁盘内的分区命名为 `hda1`、`hda2` 等。）这些是物理磁盘设备内的逻辑磁盘。

`fops` 字段是初始化为文件操作结构体的 `block_device_operations`。文件操作结构体包含指向低级设备驱动程序中辅助函数的指针。这些函数是依赖于驱动程序的，因为它们并没有在每个驱动程序中实现。通常实现的文件操作有 `open`、`close`、`read` 和 `write`。第 4 章“内存管理”讨论了文件操作结构体。

`queue` 字段指向驱动程序必须执行的请求操作列表。稍后将讨论请求队列的初始化。

`private_data` 字段用于依赖驱动程序的数据。

`capacity` 字段应设置为驱动器的大小（单位为 512 字节扇区）。调用 `set_capacity()` 应提供此值。

`flags` 表示设备属性。对于硬盘驱动器，它是介质类型，例如 CD、可移动式等。

现在，我们来看下初始化请求队列涉及的内容。在队列已经声明的情况下，我们调用 `blk_init_queue(request_fn_proc, spinlock_t)`。该函数其第一个参数是代表文件系统调用的传输函数。`blk_init_queue()` 函数通过 `blk_alloc_queue()` 分配队列，然后初始化队列结构。`blk_init_queue()` 的第二个参数是一个与所有操作关联联的锁。

最后，为了让此块设备对内核可见，驱动程序必须调用 `add_disk()`：
