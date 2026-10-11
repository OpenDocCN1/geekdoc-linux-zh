
任务根据其 pid 值进行哈希，上述哈希函数旨在将这些元素均匀地分布在其定义域（0 到 PID_MAX-1）中。该哈希表用于通过给定的 pid 快速查找任务，使用来自 `include/linux/sched.h` 的内联函数 `find_task_pid()`：

```c
static inline struct task_struct *find_task_by_pid(int pid)
{
  struct task_struct *p, **htable = &pidhash[pid_hashfn(pid)];
  for (p = *htable; p && p->pid != pid; p = p->pidhash_next)
    ;
  return p;
}
```

每个哈希链（即哈希到相同值的任务）上的任务通过 `p->pidhash_next/pidhash_prev` 链接起来，它们由 `hash_pid()` 和 `unhash_pid()` 用于将给定进程插入或删除哈希表。这些操作在称为 `tasklist_lock` 的读写自旋锁保护下进行，该锁以**写（WRITE）**模式获取。

使用 `p->next_task/prev_task` 的循环双向链表得以维护，以便轻松遍历系统中的所有任务。这是通过 `include/linux/sched.h` 中的 `for_each_task()` 宏实现的：

```c
#define for_each_task(p) \
  for (p = &init_task ; (p = p->next_task) != &init_task ; )
```

使用 `for_each_task()` 的用户需要以**读（READ）**模式获取 `tasklist_lock`。请注意，`for_each_task()` 使用 `init_task` 来标记列表的开始（也是结束）——这是安全的，因为空闲任务（pid 0）永远不会退出。

修改进程哈希表或/和进程表链接的元素，特别是 `fork()`、`exit()` 和 `ptrace()`，必须以**写（WRITE）**模式获取 `tasklist_lock`。更有趣的是，写者还必须禁用本地 CPU 上的中断。这背后的原因并不简单：`send_sigio()` 函数遍历任务列表，因此以**读（READ）**模式获取 `tasklist_lock`，并且它是从中断上下文中由 `kill_fasync()` 调用的。这就是为什么写者在持有锁时必须禁用中断，而读者则不需要的原因。

既然我们理解了 `task_struct` 结构是如何链接在一起的，让我们来检查一下 `task_struct` 的成员。它们大致对应于 UNIX 中 'struct proc' 和 'struct user' 合并后的成员。

其他版本的 UNIX 将任务状态信息分离为两部分：一部分需要始终保持在内存中（称为 'proc 结构'，包含进程状态、调度信息等），另一部分仅在进程运行时才需要（称为 'u area'，包含文件描述符表、磁盘配额信息等）。这种丑陋设计的唯一原因是内存曾经是非常稀缺的资源。现代操作系统（好吧，目前只有 Linux，但其他操作系统，例如 FreeBSD 似乎也在朝 Linux 的方向改进）不需要这种分离，因此始终在内核内存驻留的数据结构中维护进程状态。

`task_struct` 结构在 `include/linux/sched.h` 中声明，当前大小为 1680 字节。

state 字段声明如下：

```c
volatile long state;    /* -1 unrunnable, 0 runnable, >0 stopped */

#define TASK_RUNNING           0
#define TASK_INTERRUPTIBLE     1
#define TASK_UNINTERRUPTIBLE   2
#define TASK_ZOMBIE            4
#define TASK_STOPPED           8
#define TASK_EXCLUSIVE         32
```

为什么 `TASK_EXCLUSIVE` 定义为 32 而不是 16？因为 16 被 `TASK_SWAPPING` 占用了，而我移除所有对 `TASK_SWAPPING` 的引用时（在 2.3.x 某个版本中）忘记将 `TASK_EXCLUSIVE` 向上移位。

p->state 声明中的 `volatile` 意味着它可以被异步修改（来自中断处理程序）：

- **TASK_RUNNING**：表示任务“应该”在运行队列上。它可能尚未进入运行队列的原因是将任务标记为 TASK_RUNNING 并将其放入运行队列这两个操作不是原子的。你需要以读模式持有 runqueue_lock 读写自旋锁才能查看运行队列。如果你这样做，你会看到运行队列上的每个任务都处于 TASK_RUNNING 状态。然而，由于上述原因，反之并不成立。同样，驱动程序可以将自身（或者更准确地说，它们运行的进程上下文）标记为 TASK_INTERRUPTIBLE（或 TASK_UNINTERRUPTIBLE），然后调用 schedule()，这会将其从运行队列中移除（除非有挂起的信号，如果是这种情况，它会保留在运行队列中）。
- **TASK_INTERRUPTIBLE**：表示任务正在睡眠，但可以被信号或定时器到期唤醒。
- **TASK_UNINTERRUPTIBLE**：与 TASK_INTERRUPTIBLE 相同，但不能被唤醒。
- **TASK_ZOMBIE**：任务已终止，但其状态尚未被父进程（自然父进程或通过收养的父进程）收集（即 wait(1)）。
- **TASK_STOPPED**：任务已被停止，原因是作业控制信号或 ptrace(2)。
- **TASK_EXCLUSIVE**：这不是一个独立的状态，但可以按位或（OR）到 TASK_INTERRUPTIBLE 或 TASK_UNINTERRUPTIBLE 中的任意一个。这意味着当此任务在一个有许多其他任务的等待队列上睡眠时，它将单独被唤醒，而不是通过唤醒所有等待者导致“惊群效应”问题。

任务标志包含有关进程状态的信息，这些状态不是互斥的：

```c
unsigned long flags;    /* per process flags, defined below */
/*
 * Per process flags
 */
#define PF_ALIGNWARN       0x00000001      /* Print alignment warning msgs */
                                     /* Not implemented yet, only for 486*/
#define PF_STARTING        0x00000002    /* being created */
#define PF_EXITING         0x00000004    /* getting shut down */
#define PF_FORKNOEXEC      0x00000040    /* forked but didn't exec */
#define PF_SUPERPRIV       0x00000100    /* used super-user privileges */
#define PF_DUMPCORE        0x00000200    /* dumped core */
#define PF_SIGNALED        0x00000400    /* killed by a signal */
#define PF_MEMALLOC        0x00000800    /* Allocating memory */
#define PF_VWORK           0x00001000    /* Wake up parent in mm_release */
#define PF_USEDPU          0x00100000    /* task used PFU this quantum (SMP) */
```

字段 p->has_cpu, p->processor, p->counter, p->priority, p->policy 和 p->rt_priority 与调度器相关，将在后面讨论。

字段 p->mm 和 p->active_mm 分别指向由 mm_struct 结构描述的进程地址空间，以及如果进程没有真实地址空间（例如内核线程）时的活动地址空间。这有助于在任务被调度出去时最小化切换地址空间时的 TLB 刷新。因此，如果我们正在调度入一个内核线程（没有 p->mm），那么它的 next->active_mm 将被设置为被调度出的任务的 prev->active_mm，如果 prev->mm != NULL，这将等同于 prev->mm。如果 clone(2) 系统调用传递了 CLONE_VM 标志，或者通过 vfork(2) 系统调用，地址空间可以在线程之间共享。

字段 p->exec_domain 和 p->personality 与任务的“个性”有关，即某些系统调用的行为方式，以模拟外部 UNIX 变体的“个性”。

字段 p->fs 包含文件系统信息，在 Linux 下意味着三个信息片段：

- 根目录的 dentry 和挂载点，
- 备用根目录的 dentry 和挂载点，
- 当前工作目录的 dentry 和挂载点。

该结构还包含一个引用计数，因为当 clone(2) 系统调用传递了 CLONE_FS 标志时，它可以在克隆任务之间共享。

字段 p->files 包含文件描述符表。如果 clone(2) 系统调用指定了 CLONE_FILES，这也可以在任务之间共享。

字段 p->sig 包含信号处理程序，并可以通过 CLONE_SIGHAND 在克隆任务之间共享。

## 2.2 任务和内核线程的创建与终止

不同的操作系统书籍对“进程”有不同的定义，从“正在执行的程序实例”开始，到“由 clone(2) 或 fork(2) 系统调用所产生的事物”结束。在 Linux 下，有三种类型的进程：

- 空闲线程，
- 内核线程，
- 用户任务。

空闲线程是为第一个 CPU 在编译时创建的；然后通过 arch/i386/kernel/smpboot.c 中特定的架构相关函数 fork_by_hand() 为每个 CPU“手动”创建，该函数展开

