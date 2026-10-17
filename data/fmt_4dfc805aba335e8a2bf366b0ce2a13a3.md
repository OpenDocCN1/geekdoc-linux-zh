
```c
204 struct mm_struct{
205     *mmap;
206     struct vm_area_struct  mm_rb;
207     root_t                  *mmap_cache;
208     struct vm_area_struct  *pgd;
209     pgd_t                   mm_users;
210     atomic_t               mm_count;
211     atomic_t               _count;
212     int                    map_count;
213     struct rw_semaphore    mmap_sem;
214     spinlock_t              page_table_lock;
215     struct list_head        mmlist;

220    unsigned long           start_code, end_code,
221    unsigned long           start_data, end_data;
222    unsigned long           start_brk, brk, stack_start,
                         arg_start, arg_end, env_start,
                                 env_end;

223    unsigned long           rss, total_vm, locked_vm;
unsigned long def_flags;
unsigned long cpu_vm_mask;
unsigned long swap_address;
unsigned dumpable:1;
mm_context_t context;
};
```

图 2.7 内存控制信息

- 205 这是一个链表头，链表中的结构表示进程地址空间中的区域。
- 206 表示进程区域的结构也排列成树，以提高查找速度。该字段是该树的根。
- 207 这是一个指向最近访问区域的指针。
- 208 这是一个指向物理页表的指针。

### 第 322 行：sleep_time

该字段包含进程从运行队列中移除或进入睡眠的时间。这是另一个与调度器相关的字段，将在第 4.8.3 节中讨论。

### 第 324 行：next_task, prev_task

这些是后向和前向指针，将整个 `task_struct` 结构体链表连接在一起。请注意，这两个指针都是直接指针，指向相应的 `task_struct`。该列表由 `init_task` 作头（见第 3.3.1 节）。

### 第 325 行：active_mm

该字段的值通常与 `mm` 相同。但对于没有独立地址空间的内核线程（其 `mm` 字段为 `NULL`），该字段指向代表其正活跃使用的地址的 `mm_struct`。当调度器切换进一个内核线程时，它将其 `active_mm` 字段设置为刚刚切换出的进程的 `mm` 字段。它用于最小化地减少转换备备缓冲区（TLB）的刷新（见第 7.3.5 节）。

### 第 326 行：local_pages

这包含一个 `struct page` 链表，代表分配给此进程的所有页帧。

### 第 327 行：allocation_order

指定内存管理器在分配页帧时使用的阶数。

### 第 327 行：nr_local_pages

这是以 `local_pages` 为头的列表中的页面数量。

## 2.3 通用进程信息

`task_struct` 中的下一块信息松散地聚集在“通用进程状态信息”标题下，如图 2.8 所示。

```c
330 struct linux_binfmt      *binfmt;
331 int                        exit_code, exit_signal;
332 int                        pdeath_signal;
333
334 unsigned long             personality;
335 int                        did_exec:1;
336 pid_t                     pid;
337 pid_t                     pgrp;
338 pid_t                     tty_old_pgrp;
339 pid_t                     session;
```

## 通用进程信息

```c
340 pid_t               tgid:
341
342 int                 leader:
348 struct task_struct    *opptr, *pptr, *cptr,
                                     *pysptr, *ososptr;
349 struct list_head      thread_group;
352 struct task_struct      *pidash_next;
353 struct task_struct      **pidash_pprev;
354
355 wait_queue_head_t     *wait_chldexit;
356 struct completion      *vfork_done;
357 unsigned long          rt_priority;
358 unsigned long          it_real_value, it_prof_value,
                                     it_virtual;
359 unsigned long          it_real_incr, it_prof_incr,
                                     it_virt_incr;
360 struct timer_list     real_timer;
361 struct tms            times;
362 unsigned long         start_time;
363 long                  per_cpu_utime[NR_CPUS],
                                     per_cpu_stime[NR_CPUS];
```

**图 2.8** `task_struct` 中的进程状态信息

### 第 330 行：binfmt

Linux 可以运行编译为各种可执行格式的程序，例如 .out 和 ELF。`struct linux_binfmt` 结构体包含一组指向函数的指针，用于加载和操作正在执行的程序所编码的特定二进制格式。这些函数分别用于加载可执行文件、加载共享库以及写入核心文件。再次强调，这是一个指针字段，因为信息存在于系统列表中。该列表在启动时建立，每个支持的格式都有一个条目，如下：

- a.out：主要为了向后兼容而存在
- ELF：广泛用于可执行文件和共享库；Linux 的原生格式；
- iX86：在 Alpha 上运行 Intel 二进制文件，就就像它们是原生 Alpha 二进制文件一样；这似乎意味着其中一种解释方式，或者是即时翻译；
- Java：通过自动运行 Java 解释器来执行 Java .class 文件；
- Misc：主要通过魔数（magic number）工作，并可以配置为识别新的魔数；
- Script：shell或其他解释型脚本，如 Perl 或 Python。

二进制格式实际上是文件管理器的关注点，这里将不再进一步处理。

### 第 331 行：exit_code

当进程终止时返回给父进程的信息在 `exit_code` 中。该字段将在第 9.1 节处理进程终止时讨论。

### 第 331 行：exit_signal

如果进程是由信号终止的，那么 `exit_signal` 字段包含该信号的编号。

### 第 332 行：pdeath_signal

当任何子死亡时发送给此进程的信号定义在 `pdeath_signal` 中。它由函数 `forget_original_parent()` 发送（见第 9.2.2 节）。

### 第 334 行：personality

Linux 进程可以执行为不同版本的 Unix 编译的程序。当前程序对应的版本记录在 `personality` 中。通常，该值是 `PER_LINUX` (0)。关于个性（personality）的完整讨论请参见第 21 章，包括不同的可能性。

### 第 335 行：did_exec
