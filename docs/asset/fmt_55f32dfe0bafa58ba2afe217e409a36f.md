
优先级数组结构体的字段如下：

- `nr_active`。一个用于跟踪优先级数组中持有任务数量的计数器。
- `bitmap`。这用于跟踪数组内的优先级。`bitmap` 的实际长度取决于系统中 `unsigned long` 的大小。它始终足够存储 `MAX_PRIO` 位，但可能更长。
- `queue`。一个存储任务列表的数组。每个列表持有特定优先的任务。因此，`queue[0]` 存储所有优先级为 0 的任务指针列表，`queue[1]` 存储所有优先级为 1 的任务指针列表，依此类推。

# 第 3 章 进程：执行的主要模型

| struct runqueue |
| :--- | :--- | :--- |
| prio_array_t *active | spinlock_t lock | task_t *curr, *idle |
| prio_array_t *expired | unsigned long nr_running | init best_expired_prio |
| prio_array_t *arrays[0] | | |
| int nr_active | unsigned long bitmap [BITMAP_SIZE] |
| struct list_head_queue [MAX_PRIO] | | |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | ... | 138 | 139 | 140 |
| A | B | | | | | | | X | Y | ... | Z |
| (优先级为 0 的任务指针队列) | | | | | | | | | | | | | |
| (优先级为 138 的任务指针队列) | | | | | | | | | | | | | |

| prio_array_t *arrays[1] |
| :--- |
| int nr_active | unsigned long bitmap [BITMAP_SIZE] |
| struct list_head_queue [MAX_PRIO] | | |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | ... | 138 | 139 | 140 |
| D | E | | | | | | | U | V | ... | W |
| (优先级为 0 的任务指针队列) | | | | | | | | | | | | | |
| (优先级为 138 的任务指针队列) | | | | | | | | | | | | | |

图 3.12
运行队列中的优先级数组

在对运行队列组织方式有了基础理解后，我们现在开始在单 CPU 系统上跟踪任务通过调度器。

## 3.6.2 从等待或激活中唤醒

回想当进程调用 `fork()` 时，会创建一个新进程。如前所述，调用 `fork()` 的进程称为父进程，新进程称为子进程。新创建的进程需要调度以访问 CPU。这是通过 `do_fork()` 函数实现的。

`do_fork()` 中有两行处理调度器相关的代码涉及唤醒进程。在 `linux/kernel/fork.c` 第 1184 行调用的 `copy_process()` 调用函数 `sched_fork()`，该函数初始化了插入调度器运行队列的操作。在 `linux/kernel/fork.c` 第 1222 行调用的 `wake_up_forked_process()` 获取初始化的进程并将其插入运行队列。将初始化和插入分离，是为了允许新进程在被调度之前被杀死或通过终止终止。只有当进程被创建、成功初始化且没有待处理信号时，它才会被调度。

### 3.6.2.1 sched_fork(): 为新派生进程进行调度器初始化

`sched_fork()` 函数执行调度器为新派生进程所需的基础设施设置：

```c
kernel/sched.c
719 void sched_fork(task_t *p)
720 {
721   /*
722    * 我们在这里将进程标记为运行状态，但尚未实际
723    * 将其插入运行队列。这保证了
724    * 没有人会真正运行它，信号或其他外部
725    * 事件也无法唤醒并将其插入运行队列。
726    */
727   p->state = TASK_RUNNING;
728   INIT_LIST_HEAD(&p->run_list);
729   p->array = NULL;
730   spin_lock_init(&p->lock);
```

该函数通过将状态设置为 `TASK_RUNNING` 将进程标记为运行（第 727 行）。初始化 `run_list`（第 728 行），并将 `array` 设置为 `NULL`（第 729 行）。初始化锁（第 730 行）。

# 第 3 章 进程：执行的主模型

```c
953 else {
954     p->prio = current->prio;
955     list_add_tail(&p->run_list, &current->run_list);
956     p->array = current->array;
957     p->array->nr_active++;
958     rq->nr_running++;
959 }
960 task_rq_unlock(rq, &flags);
```

第 930–934 行
调度器执行的第一件事是锁定运行队列（run queue）结构。对运行队列的任何修改都必须在持有锁的情况下进行。如果进程没有被标记为 `TASK_RUNNING`，我们还会抛出一个 bug 警告，这应该归功于 `sched_fork()` 中的初始化（见前文所示 `kernel/sched.c` 中的第 727 行）。

第 948 行
`effective_prio()` 函数修改进程的静态优先级。它返回一个在 100 到 139 之间的优先级（`MAX_RT_PRIO` 到 `MAX_PRIO-1`）。根据进程之前的 CPU 使用情况和睡眠时间，进程的静态优先级可以在两个方向上最多修改 5，但它始终保持在这个范围内。从命令行来看，我们说的是进程的 `nice` 值，其范围可以从 +19 到 -20（最低到最高优先级）。`nice` 值为 0 对应静态优先级 120。

## 3.6 跟踪进程：基础调度器的构建

第 749 行
进程的 CPU 属性被设置为当前 CPU。

第 951–960 行
该代码块的概述是：新进程（或子进程）从其父进程（即 `current`）复制调度信息，然后将自己插入到运行队列适当的位置。我们已经完成了对运行队列的修改，因此我们解锁了它。接下来的段落和图 3.13 将详细讨论这一点。

![](img/6525157588f931c50a65c5a42af9a432_158_0.png)

图 3.13
运行队列插入

指针数组指向运行队列中的优先级数组。如果当前进程没有指向优先级数组，则意味着当前进程已完成或处于睡眠状态。在这种情况下，当前进程的 `run_list` 字段不在运行队列的优先级数组的队列中，这意味着 `list_add_tail()` 操作（第 955 行）将失败。相反，我们使用 `_activate_task()` 插入新创建的进程，该函数将新进程添加到队列中，而不将其标记为 `task` 进行引用。

在正常情况下，当当前进程在运行队列上等待 CPU 时间时，该进程被添加到优先级数组中 `p->prio` 槽位的队列中。被添加的数组的进程计数器 `nr_active` 会加1，运行队列的进程计数器 `nr_running` 也会加1。最后，我们解锁运行队列锁。

当前进程未指向运行队列优先级数组的情况，对于理解调度器如何管理运行队列和优先级数组属性非常有帮助。

```c
kernel/sched.c
366 static inline void _activate_task(task_t *p, runqueue_t *rq)
367 {
368     enqueue_task(p, rq->active);
369     rq->nr_running++;
370 }
```

`_activate_task()` 将给定的进程 `p` 置于运行队列 `rq` 的活动优先级数组上，并增加运行队列 `nr_running` 字段，该字段是运行队列上进程总数的计数器。

```c
kernel/sched.c
311 static void enqueue_task(struct task_struct *p, prio_array_t *array)
312 {
313     list_add_tail(&p->run_list, array->queue + p->prio);
314     __set_bit(p->prio, array->bitmap);
315     array->nr_active++;
316     p->array = array;
317 }
```
