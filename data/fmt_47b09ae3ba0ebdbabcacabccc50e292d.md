
| 4.5 | J1[3,6] | J1,3 |
| 5.5 | J1[3,6]; J2[2,10] | J1,3 |
| 6 | J1[4,8]; J2[2,10] | J1,4 |
| 7 | J2[2,10] | J2,2 |
| 8 | J1[5,10]; J2[2,10] | J1,5 |
| 9 | J2[2,10] | J2,2 |

例如，考虑一个包含两个任务的系统，它们都在时间 `t=0` 开始，因此它们的相位均为 0。`T1` 的周期为 2，执行时间为 1；`T2` 的周期为 5，执行时间为 2.5：

`T1 = (0, 2, 1)`

`T2 = (0, 5, 2.5)`

换句话说，两个任务有一半时间是活跃的，因此原则上它们合起来将使用 100% 的 CPU。因为任务是周期性的，只需要为 `T1` 和 `T2` 周期的最小公倍数计算调度方案，在本任务中为 `2*10`。调度方案所示。这是 EDF 的一个重要特性：只要总 CPU 占用率不超过 100%，它就能保证所有截止时间都能得到满足。换句话说，总可以创建一个有效的调度方案。

## 5.8 Linux 内核中的调度

Linux 内核支持两类调度：普通调度和实时调度。`sched(7)` 手页提供了良好的解释。关于调度，线程是主要的抽象，即调度器调度的是线程而不是进程。

每个线程都有关联的调度策略和静态调度优先级。调度器根据系统中所有线程的静态调度策略和优先级的知识做出决策。

### 树莓派上的 Linux 操作系统基础

目前（内核 4.14）有三种普通调度策略：`SCHED_OTHER`、`SCHED_IDLE` 和 `SCHED_BATCH`，以及三种实时策略：`SCHED_FIFO`、`SCHED_RR` 和 `SCHED_DEADLINE`。其中，`SCHED_OTHER`、`SCHED_FIFO` 和 `SCHED_RR` 是 POSIX 1003.1b 实时标准 [6] 要求的。

对于使用普通策略之一的线程，静态优先级不在调度决策中使用（设置为 0）。在一种实时策略下调度的进程具有范围从 1（低）到 99（高）的静态优先级值（因此，实时的静态优先级始终高于普通线程）。

调度器为每个静态优先级值维护一个可运行线程列表。为了确定下一个运行哪个线程，它会查找静态优先级最高的非空列表，并选择该列表头的线程。

调度策略决定了线程应插入到等优先级线程列表的什么位置以及它将如何移动到列表头部。

在 Linux 中，所有调度都是抢占式的：如果一个静态优先级更高的线程变为就绪状态，当前运行的线程将被抢占并返回到其优先级的运行列表中。调度策略决定了运行列表内部的排序。例如，对于优先级为 0 的运行列表（即普通调度类别 `SCHED_NORMAL`），可以有多多三种不同的策略来决定线程的排序。对于每个更高的静态优先级列表（实时），可以有一个或两个。

#### 5.8.1 用户优先级：niceness

`Niceness`（或 nice 值）是进程的动态优先级。`Niceness` 的范围从 -20（对进程最有利）到 19（对进程最不利），该值影响进程的调度方式，但不是直接影响。运行进程的 nice 值用户可以通过 `nice(1)` 命令或 `nice(2)` 系统调用来更改。我们将进一步看到不同的调度器如何使用这些值。

#### 5.8.2 任务控制块中的调度信息

如所述，任务控制块在 Linux 内核中通过 `include/linux/sched.h` 中的 `task_struct` 结构实现。让我们看看 `task_struct` 中存储的特定调度信息（为了简洁，已删除了其他字段）。

```
列表 5.8.1 task_struct 来自 include/linux/sched.h
struct task_struct {
    int rq;
    /* prio, static_prio; 调度时使用的优先级。变量 prio，用户的 nice 值可以转换为静态优先级以更好地扩展调度参数。 */
    int prio, static_prio, normal_prio;
    unsigned int rt_priority; // 用于实时
    const struct sched_class *sched_class; // 下文
    struct sched_entity se; // 下文
    struct rt_entity rt; // 用于实时
    struct dl_entity dl; // 用于 deadline
    /** 此进程使用的调度策略 */
    unsigned int policy;
};
```

该结构包含了许多与调度相关的结构。我们将在 CFS 和实时部分讨论 `sched_entity`、`rt_entity` 和 `dl_entity` 体。`sched_class` 类实际上是实际调度的接口：所有功能都在 `fair`、`idle`、`deadline` 各自类中实现。

```
列表 5.8.2 sched_class 来自 include/linux/sched.h
struct sched_class {
   const struct sched_class *next;
   void (*enqueue_task)(struct rq *rq, struct task_struct *p, int flags);
   void (*dequeue_task)(struct rq *rq, struct task_struct *p, int flags);
   void (*yield_task)(struct rq *rq);
   bool (*yield_to)(struct rq *rq, struct task_struct *p, bool preempt);
   void (*check_preempt_curr)(struct rq *rq, struct task_struct *p, int flags);
   struct task_struct (*pick_next_task)(struct rq *rq, struct task_struct *prev, struct rq *cpu);
   void (*put_prev_task)(struct rq *rq, struct task_struct *p);
   void (*set_cur_task)(struct rq *rq);
   void (*task_tick)(struct rq *rq, struct task_struct *p, int queued);
   void (*task_fork)(struct rq *rq, struct task_struct *p);
   void (*task_dead)(struct task_struct *p);
   void (*switched_from)(struct rq *this_rq, struct task_struct *task);
   void (*switched_to)(struct rq *this_rq, struct task_struct *task);
   void (*prio_changed)(struct rq *this_rq, struct task_struct *task, int oldprio);
   unsigned int (*get_rq_interval)(struct rq *rq, struct task_struct *task);
   void (*update_curr)(struct rq *rq);
};
```

因此，为了对进程 `p` 执行调度操作，调度器必须调用 `p->sched_class->name` 操作，并执行该进程特定调度类的相应操作。Linux 内核保留了一个每个 CPU 的运行队列（`struct rq`），其中按调度类包含不同的运行队列，所示（`sched.h`）。

```
列表 5.8.3 runqueue struct 来自 include/linux/sched.h
/*
 *  这是主要的、每个 CPU 的运行队列数据结构。
 */
struct rq {
    raw_spinlock_t lock;
    unsigned int nr_running;
#define CPU_LOAD_IDX_MAX
    unsigned long cpu_load[CPU_LOAD_IDX_MAX];
    struct load_weight load;
    unsigned long nr_load_updates;
    u64 nr_switches;
    struct cfs_rq cfs;
    struct rt_rq rt;
    struct dl_rq dl;
    struct task_struct *curr, *idle, *stop;
};
```

#### 5.8.3 Linux 内核中的进程优先级
