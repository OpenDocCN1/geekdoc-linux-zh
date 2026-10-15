
请注意，`_pick_next_entity()` 实际上并不遍历树来寻找最左侧节点，因为该值由`rb_leftmost`缓存。虽然遍历树以找到最左侧节点是高效的——对于 N 个节点，如果树是平衡的，则为 $O(\log N)$——但缓存最左侧节点甚至更简单。该函数的返回值是 CFS 下一个运行的进程。如果该函数返回`NULL`，则表示没有最左侧节点，因此树中没有节点。在这种情况下，没有可运行的进程，CFS 将调度空闲任务。

### 向树中添加入进程

接下来，让我们看看 CFS 如何将进程添加到红黑树中并缓存最左节点。当进程变为可运行状态（唤醒）或通过`fork()`首次创建时，就会发生这种情况，正如第 3 章所讨论的那样。向树中添加入进程是通过`enqueue_entry()`执行的：

```c
static void
enqueue_entry(struct cfs_rq *cfs_rq, struct sched_entity *se, int flags)

{
    /*
     * Update the normalized run time before updating min_vruntime
     * through calling update_curr().
     */

    if (!(flags & ENQUEUE_WAKEUP) || (flags & ENQUEUE_MIGRATE))
        se->vruntime += cfs_rq->min_vruntime;

    /*
     * Update run-time statistics of the `current'.
     */

    update_curr(cfs_rq);

    account_entity_enqueue(cfs_rq, se);

    if (flags & ENQUEUE_WAKEUP) {
        place_entity(cfs_rq, se, 0);
        enqueue_sleeper(cfs_rq, se);
    }

    update_stats_enqueue(cfs_rq, se);
    check_sched(cfs_rq, se);

    if (se != cfs_rq->curr)
        __enqueue_entity(cfs_rq, se);
}
```

该函数更新运行时间及其他统计数据，然后调用`__enqueue_entity()`来执行将条目插入红黑树的主要繁重工作：

```c
/*
 * Enqueue an entity into the rb-tree:
 */
static void __enqueue_entity(struct cfs_rq *cfs_rq, struct sched_entity *se)

{
    struct rb_node **link = &cfs_rq->tasks_timeline.rb_node;
    struct rb_node *parent = NULL;
    struct sched_entity *entry;
    s64 key = entity_key(cfs_rq, se);
    int leftmost = 1;
    /*
     * Find the right place in the rbtree:
     */
    while (*link) {
        parent = *link;
        entry = rb_entry(parent, struct sched_entity, run_node);
        /* We don't care about collisions. Nodes with
         * the same key stay together.
         */
        if (key < entry_key(cfs_rq, entry)) {
            link = &parent->rb_left;
        } else {
            link = &parent->rb_right;
            leftmost = 0;
        }
    }

    /*
     * Maintain a cache of leftmost tree entries (it is frequently
     * used):
     */
    if (leftmost)
        cfs_rq->rb_leftmost = &se->run_node;

    rb_link_node(&se->run_node, parent, link);
    rb_insert_color(&se->run_node, &cfs_rq->tasks_timeline);
}
```

让我们分析一下这个函数。`while()`循环的主体遍历树以搜索匹配的键，该键是插入进程的`vruntime`。根据平衡树的规则，如果键小于当前节点的键，则向左子节点移动；如果键大于当前节点的键，则向右子节点移动。如果它曾经向右移动，即使只有一次，它就知道插入的进程不能成为新的最左节点，并将`leftmost`设置为零。如果它只向左移动，`leftmost`保持为一，我们就有了一个新的最左节点，可以通过将`rb_leftmost`设置为插入的进程来更新缓存。当我们将自身与一个在移动方向上没有子节点的节点进行比较时，循环终止；此时`link`为`NULL`，循环终止。离开循环后，函数在父节点上调用`rb_link_node()`，将插入的进程标记为新的子节点。函数`rb_insert_color()`更新树的自平衡属性；我们将在第 6 章中讨论着色。

### 从树中移除进程

最后，让我们看看 CFS 如何从红黑树中移除进程。当进程阻塞（变为不可运行）或终止（不再存在）时，会发生这种情况：

```c
static void
dequeue_entity(struct cfs_rq *cfs_rq, struct sched_entity *se, int sleep)

{
    /*
     * Update run-time statistics of the `current'.
     */
    update_curr(cfs_rq);
    update_stats_dequeue(cfs_rq, se);
    clear_buddies(cfs_rq, se);

    if (se != cfs_rq->curr)
        __dequeue_entity(cfs_rq, se);

    account_entity_dequeue(cfs_rq, se);
    update_min_vruntime(cfs_rq);

    /*
     * Normalize the entity after updating the min_vruntime because the
     * update can refer to the ->curr item and we need to reflect this
     * movement in our normalized position.
     */
    if (!sleep)
        se->vruntime -= cfs_rq->min_vruntime;
}
```

与向红黑树添加进程类似，实际工作由辅助函数`__dequeue_entity()`执行：

```c
static void __dequeue_entity(struct cfs_rq *cfs_rq, struct sched_entity *se)

{
    if (cfs_rq->rb_leftmost == &se->run_node) {
        struct rb_node *next_node;

        next_node = rb_next(&se->run_node);
        cfs_rq->rb_leftmost = next_node;
    }

    rb_erase(&se->run_node, &cfs_rq->tasks_timeline);
}
```
