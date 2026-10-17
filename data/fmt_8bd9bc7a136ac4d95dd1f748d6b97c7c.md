
`vm_stat` 中的统计项含义如下：`NR_FILE_DIRTY` 指明脏页的数量。`NR_FILE_MAPPED` 表示映射的页数。`NR_FILE_PAGES` 仅从进程上下文中修改。`NR_WRITEBACK` 以及 `NR_SLAB_RECLAIMABLE`、`NR_SLAB_UNCLAIMABLE`、`NR_PAGABLE`、`NR_NFS` 等是与 `pdflush` 机制执行的。

工作函数和参数的值被分配给 `pdflush_work` 的相应字段，并立即通过 `wake_up_process` 唤醒该线程。为了找到 `pdflush_work` 中的元素，内核知道它指的是哪个进程。

为了确保始终有足够的工作线程，内核在唤醒之前、移除当前实例后会检查 `pdflush_list` 是否为空。如果是，`last_empty_jiffs` 设置为当前系统时间。当线程终止时，内核利用此信息来检查没有空闲线程的期间 —— 它可以如所述启动一个新线程。

> `pdflush_list` 上一次为空的时间记录在全局变量 `last_empty_jiffs` 中。

## 17.7.2 写回控制

第二个数据结构持有控制写回的各种参数。上层使用它将关于如何写回的信息传递给底层（从上向下）：

```c
<writeback.h>

/* 一个告诉写回代码做什么的控制结构 */

struct writeback_control {

    struct backing_dev_info *bdi;      /* 如果为空，只写回 */

    enum writeback_sync_modes mode;

    unsigned long older_than_this;   /* 超过此的 */

    long nr_to_write;               /* 写多少页，并递减已写入 */

    long pages_aged;

    long range_start;

    long range_end;

    unsigned nonblocking;           /* 不要阻塞在队列上 */

    unsigned encountered_congestion;  /* 输出：队列满 */

    unsigned for_update;             /* 写回队列 */

    unsigned for_reclaim;             /* 从页分配器调用 */

    unsigned for_writepages;          /* 这是一个 writepages() 调用 */

    unsigned range_cyclic;           /* range_start 是循环的 */

};
```

该结构的含义如下：

- `bdi`：指向 `backing_dev_info` 结构，它总结了底层存储媒介的信息。这在第16章中简要讨论。我们在这里感兴趣两点：首先，该结构提供了一个变量来持有写回队列的状态（例如，当请求过多时可以信号拥塞），它允许没有（块设备）后端存储的内存文件系统加载——这类系统的写回操作没有意义。
- 模式区分了三种不同的同步模式：

```c
<writeback.h>

enum writeback_sync_modes {

    WB_SYNC_NONE,   /* 不等待任何内容 */

    WB_SYNC_ALL,    /* 等待所有映射 */

    WB_SYNC_HOLD,   /* 在 sys_sync() 时锁定 inode */

};
```

为了同步数据，内核需要向底层的块设备传递相应的写请求。对块设备的请求本质上是异步的。如果内核想要确保数据安全到达设备，它需要在发出请求后等待完成。这种行为在 `WB_SYNC_ALL` 时是强制的。等待写回完成是在下文讨论的 `sync_single_inode` 中执行；回想图 17-1，它位于机制的底部，负责将单个 inode 的同步工作委托给特定文件系统的方法。图 17 中标记了所有等待名为 `WB_SYNC_ALL` 调用的 inode 状态的函数。

请注意，带有 `WB_SYNC_ALL` 的回滚被称为数据完整性回滚。如果系统在这一机制完成后立即崩溃，则不会丢失数据，因为所有内容都已与底层块设备完成了同步。

如果使用 `WB_SYNC_NONE`，内核将发送请求，但立即继续剩余的同步工作。这种模式也被称为刷新回溯（flushing flashback）。

`WB_SYNC_HOLD` 是同步系统的一种特殊形式，其工作原理与 `WB_SYNC_NONE` 类似。具体的差异非常细微，将在第 17.15 节中讨论。

- 当内核执行写入时，它必须决定哪些缓存数据需要与底层存储进行同步。它使用 `older_than_this` 和 `nr_to_write` 元素来实现此目的。如果数据持续时间超过 `older_than_this` 指定的范围，则将其写回。

`older_than_this` 被定义为一个指针类型，这对于单个长值来说是不寻常的。它的数值可以通过适当的解引用来获取；如果指针为 NULL，则进行年龄检查，并且无论对象何时产生，都会对所有对象进行同步。将 `nr_to_write` 设置为 0 将禁用对预期写回页数量的上限限制。
