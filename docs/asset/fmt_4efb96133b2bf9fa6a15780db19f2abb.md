
```c
struct sched_entity {

    struct load_weight       load;

    struct rb_node           run_node;

    struct list_head         group_node;

    unsigned int             on_rq;

    u64                      exec_start;

    u64                      sum_exec_runtime;

    u64                      vruntime;

    u64                      prev_sum_exec_runtime;

    u64                      last_wakeup;

    u64                      avg_overlap;

    u64                      nr_migrations;

    u64                      start_runtime;

    u64                      avg_wakeup;

/* many stat variables elided, enabled only if CONFIG_SCHEDSTATS is set */

};
```

调度实体结构嵌入在进程描述符 `struct task_struct` 中，作为一个名为 `se` 的成员变量。我们在第 3 章“进程管理”中讨论过进程描述符。

### 虚拟运行时间

`vruntime` 变量存储进程的虚拟运行时间，它是实际运行时间（即花费在运行上的时间）根据可运行进程数量进行归一化（或加权）后的结果。虚拟运行时间的单位是纳秒，因此 `vruntime` 与时钟 tick 解耦。虚拟运行时间用于帮助我们近似 CFS 所建模的“理想多任务处理器”。在这样理想的处理器中，我们不需要 `vruntime`，因为所有可运行进程都能完美地进行多任务处理。也就是说，在理想处理器上，具有相同优先级的所有进程的虚拟运行时间都是相同的——所有任务都获得了相等的、公平的处理器份额。由于处理器无法完美地进行多任务处理，我们必须依次运行每个进程，因此 CFS 使用 `vruntime` 来核算一个进程已经运行了多久，从而推断它还应再运行多久。

在 `kernel/sched_fair.c` 中定义的函数 `update_curr()` 负责管理这一核算过程：

```c
static void update_curr(struct cfs_rq *cfs_rq)
{
	struct sched_entity *curr = cfs_rq->curr;
	u64 now = rq_of(cfs_rq)->clock;
	unsigned long delta_exec;

	if (unlikely(!curr))
		return;

/*
 * Get the amount of time the current task was running
 * since the last time we changed load (this cannot
 * overflow on 32 bits);
*/

	delta_exec = (unsigned long)(now - curr->exec_start);

	if (!delta_exec)
		return;

	__update_curr(cfs_rq, curr, delta_exec);

	curr->exec_start = now;

	if (entity_is_task(curr)) {
		struct task_struct *curtask = task_of(curr);

		trace_sched_stat_runtime(curtask, delta_exec, curr->vruntime);

		cputick_charge(curtask, delta_exec);

		account_group_exec_runtime(curtask, delta_exec);
	}
}
```

`update_curr()` 计算当前进程的执行时间，并将该值存储在 `delta_exec` 中。然后，它将此运行时间传递给 `__update_curr()`，后者根据可运行进程数量对该时间进行加权。当前进程的 `vruntime` 随后增加该加权值：

```c
/*
 * Update the current task's runtime statistics. Skip current tasks that
 * are not in our scheduling class.
 */
static inline void
__update_curr(struct cfs_rq *cfs_rq, struct sched_entity *curr,
	unsigned long delta_exec)
{
	unsigned long delta_exec_weighted;
	schedstat_set(curr->exec_max, max((u64)delta_exec, curr->exec_max));

	curr->sum_exec_runtime += delta_exec;

	schedstat_add(cfs_rq, exec_clock, delta_exec);

	delta_exec_weighted = calc_delta_fair(delta_exec, curr);

	curr->vruntime += delta_exec_weighted;

	update_min_vruntime(cfs_rq);
}
```

`update_curr()` 由系统定时器定期调用，并且在进程变为可运行或阻塞（从而变得不可运行）时也会被调用。通过这种方式，`vruntime` 成为了特定进程运行时间的准确度量，并指示下一个应该运行哪个进程。

### 进程选择

在上一节中，我们讨论了在理想且完美多任务的处理器上，所有可运行进程的 `vruntime` 将是相同的。在现实中，我们无法完美地进行多任务处理，因此 CFS 尝试使用一条简单的规则来平衡进程的虚拟运行时间：当 CFS 决定下一个要运行的进程时，它选择具有最小 `vruntime` 的进程。事实上，这正是 CFS 调度算法的核心：选择具有最小 `vruntime` 的任务。仅此而已！本小节其余部分描述了如何实现选择具有最小 `vruntime` 的进程。

CFS 使用**红黑树**来管理可运行进程的列表，并高效地找到具有最小 `vruntime` 的进程。红黑树在 Linux 中被称为 `rbtree`，是一种自平衡二叉搜索树。我们在第 6 章中将具体讨论自平衡二叉搜索树以及红黑树。目前，如果你对此不熟悉，只需知道红黑树是一种数据结构，它存储任意数据的节点，由特定的键标识，并且能够高效地根据给定的键进行搜索。（具体来说，获取由给定键标识的节点的时间复杂度是总节点数的对数级。）

### 选取下一个任务

让我们从以下假设开始：我们有一个红黑树，其中填充了系统中所有可运行的进程，每个节点的键是该可运行进程的虚拟运行时间。我们将很快看到如何构建该树，但在此假设我们已经拥有它。给定这棵树，CFS 希望下一个运行的进程（即具有最小 `vruntime` 的进程）就是树中的最左侧节点。也就是说，如果你从树根开始，沿着左子节点向下走，并继续向左移动直到到达叶子节点，你就能找到具有最小 `vruntime` 的进程。（再次提醒，如果你不熟悉二叉搜索树，不要担心。只需知道这个过程是高效的。）CFS 的进程选择算法可以概括为“运行 `rbtree` 中最左侧节点所表示的进程”。执行此选择的函数是 `_pick_next_entity()`，定义在 `kernel/sched_fair.c` 中：

```c
static struct sched_entity *_pick_next_entity(struct cfs_rq *cfs_rq)
{
    struct rb_node *left = cfs_rq->rb_leftmost;
    if (!left)
        return NULL;
    return rb_entry(left, struct sched_entity, run_node);
}
```
