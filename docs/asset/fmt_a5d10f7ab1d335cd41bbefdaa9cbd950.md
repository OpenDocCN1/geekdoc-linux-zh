
```
1304 void __init_sched_init(void)
1305 {
1310     int cpu=smp_processor_id();
1311     int nr;
1312
1313     init_task.processor = cpu;
1314
1315     for(nr = 0; nr < PIDHASH_SZ; nr++)
1316        pidhash[nr] = NULL;
1317
1318     init_timervecs();
1319
1320     init_bh(TIMER_BH, timer_bh);
1321     init_bh(QUEUE_BH, tqueue_bh);
1322     init_bh(IMMEDIATE_BH, immediate_bh);

1327     atomic_inc(&init_mm.mm_count);
1328     enter_lazy_tlb(&init_mm, current, cpu);
1329 }
```

图 1.6 初始化调度器的函数

这找到当前处理器的 ID，在本例中是启动处理器。`smp_processor_id()` 宏是特定特定的（参见第 7.2.1.4 节）。

这将 ID 放入 `task_struct` 的 `processor` 字段中，该字段已由编译器静态设置（参见第 3.3.2 节）。

1315–1316 如第 3.2 节所述，哈希表初始化为 NULL 值。

1318 `init_timervecs()` 函数用于设置内部定时器子系统，将在第 5.3.1.3 节中描述。

1320–1322 最后设置了中断处理程序的下半部（bottom halves）。大多数操作系统将中断的处理分为两部分。有一些必须立即完成的紧急工作，以及可以稍后完成的较不紧急的工作。1327–1328 这两行涉及内存管理，将在后续介绍。

### 1.3.3 启动空闲进程

其余部分内容被拆分为一个独立的函数 `rest_init()`。这是与架构无关的代码（参见 1.7）。

```
530 static void rest_init(void)
531 {
532     kernel_thread(init, NULL,
533     unlock_kernel();
534     CLONE_FS | CLONE_FILES | CLONE_SIGNAL;
535     current->need_resched = 1;
536     cpu_idle();
537 }
```

> 图 1.7 设置空闲进程

532 该函数将在第 5.5 节描述，创建一个线程并安排其运行。在此之前内核拥有独占控制权。

533 通过在 `task_struct` 中设置此标志，进程向调度器信号它愿意放弃 CPU。

534 该函数在第 3.4 节描述，进入无限循环。执行进程进程变为空闲进程，但因为它在第 534 行设置了 `need_resched` 标志，调度器可以随时抢占它。

# 在 Linux 中表示进程

操作系统需要跟踪进程。与所有软件系统一样，它使用数据结构来表示它处理的对象。对于当前管理的每个进程，操作系统都维护一个进程描述符或进程控制块。在 Linux 中这就是 `task_struct`，定义在 `<linux/sched.h>` 中。每个进程分配一个 `task_struct`。它包含了进程所需的所有数据，无论它是否运行。操作系统保证始终将信息留在内存中。这可能是内核中最重要的数据结构，因此将在本章中进行详细检查。在某种意义上，它是书的其余部分的目录。

`task_struct` 中的许多字段与进程管理有关，因此每个字段将在相应章节的对应位置进行处理：当我们以后检查内核如何处理它们时，它们的目的将变得更加清晰。其他字段不在本书的范围内。处理内存管理或输入输出就是明显的例子。由于这是考虑它们的唯一地方，因此将进行更详细的介绍。

字段没有按照逻辑顺序排列——它们似乎是生长在那里的。源文件中的注释将这个大结构划分为若干易于管理的部分，这里也将遵循相同的划分。

## 2.1 位于开头的重要字段

图 2.1 显示了 `task_struct` 开头的几个字段。这些字段在汇编程序（如 `arch/i386/kernel/entry.S`）中通过偏移量而不是名称访问。这意味着无论其他部分发生什么变化，它们始终位于结构开头的相同相对位置。

```c
281 struct_task_struct {
285    volatile long      state;
286    unsigned long      flags;
287    int                sigpending;
288    mm_segment_t      addr_limit;

292    struct exec_domain  *exec_domain;
293    volatile long      need_resched;
294    unsigned long      ptrace;
296    int                lock_depth;
```

图 2.1 task_struct 中的硬编码字段

### 2.1.1 第 285 行：state

首先注意 `state` 被声明为 `volatile`。这是对编译器的警告，告知其该值可能会被异步改变（例如，中断处理程序可能会将进程从等待状态变为可运行状态），优化器不要移除任何引用该变量的看似冗余的语句。

任何进程都可以处于几种状态之一，如图 2.2 所示，定义自 `<linux/sched.h>`。正值意味着由于某种原因该进程没有运行。

```c
86  #define TASK_RUNNING       0
87  #define TASK_INTERRUPTIBLE  1
88  #define TASK_UNINTERRUPTABLE 2
89  #define TASK_ZOMBIE        4
90  #define TASK_STOPPED       8
```

图 2.2 state 字段的可能值

`TASK_RUNNING` 应用于当前运行的进程或任何准备就绪的进程。这些进程维护在一个名为运行队列（runqueue）的链表中（第 4.8 节）。

当处于 `TASK_INTERRUPTIBLE` 状态时，进程处于睡眠状态。它维护在一个名为等待队列（wait queue，见第 4 章）的链表中，但它可以被信号唤醒。信号在第 17–19 章介绍。

在 `TASK_UNINTERRUPTABLE` 状态下，进程在等待队列上睡眠，但它正在等待可能很快发生的事件，因此在被唤醒之前不会持有任何信号。

`TASK_ZOMBIE` 状态指的是已终止但尚未从系统中完全移除的进程。这种进程在 Unix 术语中被称为僵进程（zombie）。Unix 中的每个进程都有一个父进程，即创建它的进程。当进程终止时，它可以将信息传回父进程，通常表示其终止的原因，无论是正常还是异常。此类信息存储在 `task_struct` 的 `exit_code` 中，将在第 2.3 节看到。因此，在进程终止后，该进程的 `task_struct` 继续存在，直到父进程使用 `wait()` 系统服务收集信息。之后，进程的所有痕迹都会消失。第 9 章处理进程终止。

- 90 有时进程管理器会完全停止一个进程。如果这不是终止，而是将其挂起一段不确定的时间。这种情况发生的两种常见情况是：进程失去了与控制终端的联系；或者它的执行正在被另一个进程（调试器）跟踪，并且在执行完每个指令后被停止，以便检查其状态。进程的停止和启动是通过信号实现的，这些将在第 17–19 章中检查。当进程像这样被停止时，它的状态为 `TASK_STOPPED`。

注意，更改进程状态并将其从一个队列移动到另一个队列并不一定是原子操作。

### 2.1.2 第 286 行：flags

这是一个位域，记录了关于进程状态的各种感兴趣的项目。该字段中的单独位表示进程生命周期中的不同里程碑。这些位定义如图 2.3 所示，定义自 `<linux/sched.h>`。它们是互斥的；但可以同时设置多个一个位。
