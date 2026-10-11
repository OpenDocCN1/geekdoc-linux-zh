
`close_on_exec_init`持有一个位域，用于跟踪那些在`exec()`时需要关闭的文件描述符。

### 6.3.2.4 open_fds_init

`open_fds_init`持有一个位域，用于跟踪已打开的文件的文件描述符。

### 6.3.2.5 fd_array

`fd_array`数组指针指向前32个打开的文件描述符。`fs_struct`结构通过`INIT_FILES`宏初始化。

```
include/linux/init_task.h
6 #define INIT_FILES \
7 {
8 .count = ATOMIC_INIT(1),
9 .file_lock = SPIN_LOCK_UNLOCKED,
10 .max_fds = NR_OPEN_DEFAULT,
11 .max_fdset = _FD_SETSIZE,
12 .next_fd = 0,
13 .fd = &init_files.fd_array[0],
14 .close_on_exec = &init_files.close_on_exec_init,
15 .open_fds = &init_files.open_fds_init,
16 .close_on_exec_init = { { 0, 0 } },
17 .open_fds_init = { { 0, 0 } },
18 .fd_array = { NULL, }
19 }
```

图 6.11 展示了`fs_struct`初始化后的样子。

> 有关内存区域（memory zones）更多信息请参见第 4 章。

换出（写回磁盘）以释放内存。区域列表中的每个页都有指向`address_space`的指针。每个`address_space`都有一个指向`address_space_operations`结构的指针。通过调用`address_space_operation`结构中的`set_dirty_page()`函数可以将页面标记为脏页。图 6.12 展示了这种依赖关系。

![](img/6525157588f931c50a65c5a42af9a432_358_0.png)

图 6.12

页缓存与区域

### 6.4.1 address_space 结构

页缓存的核心是`address_space`对象。让我们仔细观察它。

```
include</linux/fs.h>
struct address_space {
    struct inode *host; /* 所有者：inode, 块设备 */
    struct radix_tree_root page_tree; /* 所有页的基数树 */
    spinlock_t lock; /* 保护它的自旋锁 */
    unsigned long nrpages; /* 总页数 */
    pgoff_t writeback_index;/* 回写从这里开始 */
    struct address_space_operations *a_ops; /* 方法实现 */
333 struct prio_tree_root i_immap; /* 私有映射的树 */
334 unsigned int i_immap_writable;/* VM_SHARED 映射计数 */
335 struct list_head  i_immap_nonlinear;/* VM_NONLINEAR 映射列表 */
336 spinlock_t      i_immap_lock; /* 保护树，计数列表 */
337 atomic_t        truncate_count; /* 处理与 truncate 的竞态条件 */
338 unsigned long flags; /* 标志位 */
339 struct          backing_dev; /* 后端设备信息 */
340 spinlock_t      lock; /* 保护页锁 */
341 struct list_head      list; /* 列表 */
342 struct address_space *mapping; /* 映射 */
343 };
```

被换出（写回磁盘）以释放内存。区域列表中的每个页都有一个指向`address_space`的指针。每个`address_space`都有一个指向`address_space_operations`结构的指针。通过调用`address_space_operation`结构中的`set_dirty_page()`函数可以将页面标记为脏页。图 6.12 展示了这种依赖关系。

![](img/6525157588f931c50a65c5a42af9a432_358_0.png)

图 6.12

页缓存与区域

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。

`address_space`结构包含了`address_space_operations`结构。
