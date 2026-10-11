# Adding Processes to the Tree

Now let's look at how CFS adds processes to the rbtree and caches the leftmost node. This would occur when a process becomes runnable (wakes up) or is first created via fork(), as discussed in Chapter 3. Adding processes to the tree is performed by enqueue_entry():

```
static void
enqueue_entry(struct cfs_rq *cfs_rq, struct sched_entity *se, int flags)
{

      /*
       * Update the normalized runftime before updating min_vruntime
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

This function updates the runtime and other statistics and then invokes __enqueue_entry() to perform the actual heavy lifting of inserting the entry into the red-black tree:

```
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
```