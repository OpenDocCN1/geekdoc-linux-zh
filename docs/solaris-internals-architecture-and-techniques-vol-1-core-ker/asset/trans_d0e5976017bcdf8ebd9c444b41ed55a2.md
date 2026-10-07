

## 5.3.6 地址空间管理

Solaris 内核实现了一个中央地址管理子系统，内核的其他部分会调用该子系统。地址空间模块是段驱动程序（segment drivers）的封装，因此子系统不需要知道内存范围使用的是哪个段驱动程序。图 5.7 所示的地址空间对象从进程地址空间链接，并包含指向段空间（segment space）的指针。

![](img/a86367b95bf21add858c99948ac951c6_182_0.png)

图 5.7 地址空间

地址空间子系统管理以下功能：

- 地址空间的复制（用于 `fork()`）
- 地址空间的销毁（用于 `exit()`）
- 在地址空间内创建新段
- 从地址空间中移除段
- 地址空间的页保护的设置与管理
- 地址空间的页缺异常路由
- 地址空间的页锁定和建议（advice）
- 地址空间的监视点（watchpoints）管理

请记住，进程和内核子系统会调用地址空间子系统来管理它们的地址空间。地址空间子系统由一组函数组成，这些函数用于执行上述列表的功能。尽管该子系统有很多入口点，但其实现相当简单，因为大多数函数只需查找操作需要作用于哪个段，然后路由到相应的段驱动程序。

调用 `as_alloc()` 函数会创建一个地址空间，因为 `as_alloc()` 只会被调用一次——在系统启动并创建 `init` 进程时。在 `init` 进程创建后，所有的地址空间都是通过复制 `init` 进程创建的。`fork()` 系统调用转而调用 `as_dup()` 函数在创建新进程时复制进程的地址空间，整个地址空间配置（包括栈和堆）在此时被复制。

此时 `fork()` 的行为略有所不同。它不是调用 `as_dup()` 来替换地址空间，而是通过借用父进程现有的地址空间创建一个新进程。如果目标是调用 `exec()`，那么 `fork` 函数非常有用，因为它节省了复制地址空间的精力（而这些空间在调用 `exec()` 后会被丢弃）。在子进程使用地址空间期间，父进程会被挂起，直到调用 `exec()`。一旦进程创建，地址空间对象就会被分配并设置。Solaris 7 中地址空间对象的结构所示：

```
struct as {
    kmutex_t contents;      /*保护结构中的某些字段 */
    uchar_t *flags;          /* as 属性 */
    uchar_t *vbits;          /* 用于收集统计 */
    kcondvar_t *cv;          /* 被 rangelock 使用 */
    struct *ha;              /* has 结构 */
    struct *hrm;             /* ref 和 mod 位 */
    c_addr_t *ulimit;         /* as 中最大的允许地址 */
    union {
        struct seg *seglist; /* 地址空间的最后一个段 */
        sel_spath *spath;     /* skiplist 中最后的搜索路径 */
    } cache;
    krtwlock_t lock;         /*保护 .cache 下的字段 */
    int nwpage;            /* 被监视的页数 */
    struct page *wa_pages;  /* 被监视的页 (procs) */
    struct seg *segs;       /* 此地址空间中的段 */
    size_t size;             /* 地址空间的大小 */
    struct *tail;            /* 段列表中的最后一个元素 */
    uint *defines;           /* 段列表中的元素; #defs */
    uchar_t *larep;          /* segs 的表示; #defines */
    uchar_t *hilevel;       /* a segs skiplist 中的最高层 */
    uchar_t *unused;         /* 映射已更改，重建为 objectdir */
    uchar_t *updated;        /* 对象目录 (procs) */
    vnode t **objectdir;
    size_t asizer;          /* 对象目录的大小 */
};
```

## 头文件 <vm/as.h>

## 虚拟地址空间

地址空间异常处理在地址空间子系统中执行；某些异常由通用地址空间代码处理，另一些则被重定向到段处理器。当发生页缺异常时，Solaris 陷阱处理器（trap handlers）调用 `as_fault()` 函数，该函数查找页缺异常是由哪个段引起的。当发生页缺异常时，Solaris 陷阱处理器调用 `as_fault()` 函数，该函数查找页缺异常是由哪个段引起的。

表 5-2 Solaris 7 地址空间

| 方法 | 描述 |
| :--- | :--- |
| as_add() | 在范围内创建一个段。 |
| as_alloc() | 创建一个新的地址空间。 |
| as_clearwatch() | 清除地址空间的所有监视点。 |
| as_ctl() | 控制该地址的段。 |
| as_dup() | 复制地址空间。 |
| as_exec() | 替换地址空间。 |
| as_fault() | 处理页缺异常。 |
| as_findseg() | 查找包含地址的段。 |
| as_free() | 销毁地址空间。 |
| as_gap() | 在范围内查找洞。 |
| as_memid() | 返回段的唯一 ID。 |
| as_prot() | 获取地址当前的保护属性。 |
| as_map() | 将文件映射到地址空间。 |
| as_memory() | 返回 [base, len) 内由“真实内存”支持的范围。 |
| as_pagelock() | 锁定地址空间页。 |

表 5-2 Solaris 7 地址空间函数（续）

| 方法 | 描述 |
| :--- | :--- |
| as_pageclaim() | 从空列表中检索页。 |
| as_pagelock() | 解锁地址空间页。 |
| as_rangebroadcast() | 唤醒所有等待地址空间变量的线程。 |
| as_rangelock() | 锁定地址范围的页。 |
| as_rangeunlock() | 解锁地址范围的页。 |
| as_rangewait() | 等待地址空间可用虚拟地址。 |
| as_setat() | 查找包含地址的段。 |
| as_setprot() | 设置从 addr + size 开始的间隔保护。 |
| as_setwatch() | 为地址设置监视点。 |
| as_swapout() | 将地址空间相关的页交换到次级存储。 |
| as_unmap() | 从地址空间取消映射段。 |

