
同样重要的是一点是，内核只需要担心生成全局 PID。全局命名空间中的所有其他 ID 类型将映射到 PID，因此不需要生成（例如）全局 TGID 或 SID。

在第二步中，与其直接使用 `pid_ns`，内核还可以使用这些辅助函数之一：

- `pid_vnr` 返回从其所属命名空间中看到的 PID。
- `pid_nr` 获取从 `init` 进程中看到的全局 PID。

这两者都依赖于 `pid_ns` 并自动选择合适的级别：全局 PID 对应 0，本地 PID 对应 `pid->level`。

内核提供了几个辅助函数来处理描述的步骤：

```
kernel/pid.c
pid_t task_pid_ns(struct task_struct *task, struct pid_namespace *ns)
pid_t task_tgid_ns(struct task_struct *task, struct pid_namespace *ns)
pid_t task_pgrp_ns(struct task_struct *task, struct pid_namespace *ns)
pid_t task_session_ns(struct task_struct *task, struct pid_namespace *ns)
```

由于父命名空间共享子命名空间中的 PID，但反之则不然，内核必须确保当前命名空间小于或等于生成本地 PID 的级别。

## 生成 PID

除了 PID 外，内核还负责提供一种机制来生成尚未分配的唯一 PID。在这种情况下，PID 类型之间的差异可以忽略忽略，因为唯一的标识符只针对 PID 生成。正如我们在下文讨论 `fork` 和 `clone` 时所看到的，在后续章节中，术语 PID 再次指的是进程标识符。

为了跟踪哪些 PID 已经分配且仍然空闲，内核使用了一个位图，其中每个 PID 由一个位标识。PID 的值通过其在位图中的位置获取。

分配空闲 PID 本质是在位图中查找第一个值为 0 的位，并将该位设置为 1。相反，释放 PID 可以通过将相应的位从 1 切换为 0 来实现。操作通过以下函数实现：

```
kernel/pid.c
static int alloc_pidmap(struct pid_namespace *ns)
```

以及

```
kernel/pid.c
static fast void free_pidmap(struct pid_namespace *ns, int pid)
```

它们的实现在此无关，但显然它们必须按命名空间运行。

当创建一个新进程时，它可能在多个命名空间中可见。对于每个命名空间，都必须生成一个本地 PID。这在 `alloc_pid` 中处理：

```
kernel/pid.c
struct pid *alloc_pid(struct pid_namespace *ns)
{
  struct pid *pid;
  enum pid_type type;
  int i, nr;
}
```

# 第 2 章：进程管理与调度

```c
struct pid_namespace *tmp;
struct upid *upid;

tmp = ns;
for (i = ns->level; i >= 0; i--) {
    nr = alloc_pidmap(tmp);
    pid->numbers[i].nr = nr;
    pid->numbers[i].ns = tmp;
    tmp = tmp->parent;
}
pid->level = ns->level;
```

内核从进程创建时的命名空间级别开始，向下到达初始的全局命名空间，并为每个代码创建一个 PID。`struct pid` 中包含的所有 upid 都被新生成的 PIDs 填充。每个 upid 实例都必须放在 PID 哈希表中：

```c
kernel/pid.c
for (i = ns->level; i >= 0; i--) {
    upid = &pid->numbers[i];
    hlist_add_head_rc(&upid->pid_chain,
        &pid_hash[pidhashn(upid->nr, upid->ns)]);
}

return pid;
```

## 2.3.4 任务关系

除了 ID 链接产生的关系外，内核还负责管理基于 Unix 进程创建模型建立的“家族关系”。在此背景下，使用了以下术语：

- 如果进程 A fork（派生）生成进程 B，则 A 被称为父进程，B 被称为子进程。⁶
- 如果进程 B 再次 fork 生成另一个进程 C，则 A 和 C 之间的关系有时被称为祖父与孙子关系。
- 如果进程 A 派生了多次，生成了多个子进程 B1, B2, ..., Bn，则 Bi 进程之间的关系被称为兄弟关系。

图 2-16 以图形形式展示了可能的各种。

`task_struct` 数据结构提供了两个链表头来帮助实现这些关系：

```c
<sched.h>
struct task_struct {
    struct list_head children; /* 我的子进程列表 */
    ...
```

> ⁶与家庭不同，一个进程只有一个父进程。

```c
    struct list_head sibling; /* 在父进程子进程列表中的链接 */
}
```

- `children` 是该进程所有子元素列表的链表头。
- `siblings` 用于将兄弟进程相互链接。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_95_0.png)

图 2-6：进程之间的家族关系。

新的子进程被放在 `siblings` 列表的*开头*，这意味着可以重构 fork 的时间顺序。

## 2.4 进程管理系统调用

在本节中，我描述了 `fork` 和 `exec` 系统调用族的实现。通常情况下，这些调用并不由应用程序直接发出，而是通过中间层——C 标准库来调用的，该库负责与内核进行通信。

从用户模式切换到内核模式的方法随架构而异。在附录 A 中，我描述了用于在这两种模式之间切换的机制，并解释了用户空间和内核空间之间如何交换参数。目前，将内核视为第 1 章中简要提到的、C 标准库所使用的“程序库”即可。

### 2.4.1 进程复制

用于复制进程的传统 Unix 系统调用是 `fork`。然而，它并不是 Linux 实现的唯一调用——事实上，有：

> ^7 2.4.2 之前的内核版本有三个辅助函数：`younger_sibling`、`older_sibling` 和 `eldest_child`，它们为访问列表和元素提供了某些帮助。它们被用于进程调试输出，由于一直并不有用，已被移除。补丁 Ingo Molnar 注意到相应的代码是内核中最旧元素，并对此做了了说明。这导致另一位著名的开发者以 `Linux sn'` Torvalds 的名签署了该补丁……

- 1. `fork` 是一个重量级调用，因为它创建了父进程的完整副本，然后作为子进程执行。为了减少与此调用相关的代价，Linux 使用了下文讨论的写复制（copy-on-write）技术。
- 2. `vfork` 类似于 `fork`，但不会创建父进程数据的副本。相反，它在父进程之间共享数据。这节省了大量的 CPU 时间（如果其中一个进程操作了共享数据，另一个会自动感知）。
`vfork` 设计用于子进程立即执行 `exec` 系统调用以加载新程序的情况。内核还保证父进程在子进程退出或启动新程序之前会被阻塞。

引用手册页 `vfork(2)`，“Linux 回顾过去是相当遗憾的。由于 `fork` 使用了写复制，`vfork` 的速度优势不再适用，以前应该避免使用它。”
- 3. `clone` 生成线程，并允许对父进程和子进程之间具体哪些元素被共享、哪些被复制做出决定。

### 写复制 Copy on Write

内核使用写复制（COW）技术来防止在 `fork` 执行时复制父进程的所有数据。这种技术利用了进程通常只使用内存中一小部分页的特性。

- 1. 大量的 RAM 是一种稀缺资源。
- 2. 复制操作耗时很长。

COW 机制允许内核延迟复制页。当调用 `fork` 时，内核通常会为子进程创建父进程每个内存的相同副本。

- 1. 大量的 RAM，一种稀缺资源。
- 2. 复制操作耗时很长。

COW 机制允许内核尽可能地延迟页的复制。

- 1. 大量的 RAM，一种稀缺资源。
- 2. 复制操作耗时很长。

COW 机制允许内核尽可能地延迟页的复制。
