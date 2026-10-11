
```c
1641 bdev_cache_init ()
fs/block_dev.c
290   void __init bdev_cache_init(void)
291   {
292     int err;
293     bdev_cachep = kmem_cache_create("bdev_cache",
294         sizeof(struct bdev_inode),
295         0,
296         SLAB_HWCACHE_ALIGN|SLAB_RECLAIM_ACCOUNT,
297         init_once,
298         NULL);
299 if (!bdev_cachep)
300   panic("Cannot create bdev_cache SLAB cache");
301   err = register_filesystem(&bd_type);
302   if (err)
303     panic("Cannot create bdev pseudo-fs");
304     bd_mnt = kernel_mount(&bd_type);
305     err = PTR_ERR(bd_mnt);
306     if (IS_ERR(bd_mnt))
307       panic("Cannot create bdev pseudo-fs");
308     blockdev_superblock = bd_mnt->mnt_sb; /* For writeback */
309 )
```

第 293–298 行

创建 `bdev_cache` SLAB 缓存，它持有 `bdev_inodes`。

第 301 行

注册 `bdev` 特殊文件系统。它的定义如下：

```c
fs/block_dev.c
294 static struct file_system_type bd_type = {
295   name = "bdev",
296   get_sb = bd_get_sb,
297   kill_sb = kill_anon,
298 };
```

如你所示，`bdev` 特殊文件系统的 `file_system_type` 结构只有两个例程：一个用于获取系统的超级块，另一个用于移除。在这里可能会疑惑为什么块设备被注册为文件系统。在第 6 章中，我们看到技术上不是文件系统的可以使用内核结构；它们没有挂载点，块设备是使用 VFS 结构的伪文件系统实例。作为 `bdev`，这些特殊文件系统通常为应用程序定义了有限的字段。

第 304–308 行

调用 `kernel_mount()` 设置所有与挂载相关的 VFS 结构并返回 `vfsmount` 结构。（有关将全局变量 `bd_mnt` 指向 `vfsmount` 以及将 `blockdev_superblock` 指向它的更多信息，见第 6 章。）

此函数初始化了字符设备对象：

```c
1642 chrdev_tree_init
fs/chrdev_dev.c
void __init chrdev_dev_init(void)
{
    433     subsystem_init(&cdev_subsys);
434     cdev_map = kobj_map_init(base_probe, &cdev_subsys);
435 }
```

### 8.5.27 调用 `radix_tree_init()`

第 476 行

2.6 Linux 内核使用 radix树来管理页缓存中的页。在这里我们只需初始化用于存储页缓存 radix树的连续内核空间：

```c
lib/radix-tree.c
798 void __init radix_tree_maxindex(void)
799 {
800     radix_tree_node_cache = kmem_cache_create("radix_tree_node",
801     sizeof(struct radix_tree_node), 0,
802     SLAB_PANIC, radix_tree_ctor, NULL);
803     radix_tree_maxindex();
804     hotcpu_notifier(radix_tree_callback, 0);
```

注意 `radix_tree_init()` 如何分配页缓存空间以及 `radix_tree_maxindex()` 如何配置 radix树数据。`hotcpu_notifier()`（第 804 行）指的是 Linux 2.6 热插拔 CPU 的能力。当 CPU 被热插拔时，内核调用 `radix_tree_callback()`，

```c
lib/radix-tree.c
768 static int radix_tree_maxindex(void)
769 {
770     unsigned int i;
771
772     for (i = 0; i < ARRAY_SIZE(height_to_maxindex); i++)
773     height_to_maxindex[i] = __maxindex(i);
774 }
```

尝试清理与热插拔 CPU 关联的页缓存部分。

### 8.5.28 调用 `signals_init()`

第 477 行

`kernel/signal.c` 中的 `signals_init()` 初始化了内核信号队列：

```c
fs/buffer.c
2565 void __init signals_init(void)
2566 {
2567   sigqueue_cache =
2568     kmem_cache_create("sigqueue",
2569             sizeof(struct sigqueue),
2570             alignof(struct sigqueue),
2571             0, NULL, NULL);
2572   if (!sigqueue_cache)
2573     panic("signals_init(): cannot create sigqueue SLAB cache");
2574   }
```

第 2567–2571 行

为 `sigqueue` 分配 SLAB 内存。

### 8.5.29 调用 `page_writeback_init()`

第 479 行

`page_writeback_init()` 初始化控制脏页写磁盘的值。脏页不会立即写磁盘；它们在经过一段时间后或内存中有一定数量或百分比的页标记为脏后会被写入。此函数尝试确定触发后台写入和专用写入之前必须变脏的最佳数量。后台脏页写入消耗的处理器资源比专用脏页写入少得多：

```c
mm/page-writeback.c
488 /*
489 * 如果机器具有较大的 highmem:lowmem 比例，则缩小默认
    default
490 * 脏内存阈值：允许过多的脏 highmem 产生
491 * 过量的 bufferheads。
492 */
493 void __init page_writeback_init(void)
494 {
495     long buffer_pages = nr_free_buffer_pages();
496     long correction;
497
498     total_pages = nr_free_pagecache_pages();
499
500     correction = (100 * 4 * buffer_pages) / total_pages;
501
502     if (correction < 100) {
503     dirty_background_ratio *= correction;
504     dirty_background_ratio /= 100;
505     vm_dirty_ratio *= correction;
506     vm_dirty_ratio /= 100;
507 }
508     mod_timer(&wb_timer, jiffies + (dirty_writeback_centisecs * HZ) / 100);
509     set_ratelimit();
510     register_cpu_notifier(&ratelimit_nb);
511 }
```

## 8.5 起始：start_kernel() 511
