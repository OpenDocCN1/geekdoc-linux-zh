# TCP/IP and Linux Protocol Implementation

# Figure 2.9 The scheduler iii: linux/kernel/sched.c

```
/ move an exhausted RR process to be last... */
if (prev->policy == SCHED_RR)
    goto move_rr_last;
move_rr_back:
    switch (prev->state) {
        case TASK_INTERRUPTIBLE:
            if (signal_pending(prev)) {
                prev->state = TASK_RUNNING;
                break;
            }
            default:
                del_from_runqueue(prev);
            case TASK_RUNNING:
    }
    prev->need_resched = 0;
/*
 * this is the scheduler proper:\ */
```

```
repeat_schedule:
    /* Default process to select.. */
    next = idle_task(this_cpu);
    c = -1000;
    if (prev->state == TASK_RUNNING)
        goto still_running;
```

```
still_running_back:
    list_for(tmp, &runqueue_head) {
        p = list_entry(tmp, struct task_struct, run_list);
        if (can_schedule(p, this_cpu))
```

# Figure 2.10 The scheduler iv: linux/kernel/sched.c

```
int weight = goodness(p, this_cpu, prev->active_mm);
if (weight > c)
    c = weight, next = p;
```

```
/* Do we not need to re-calculate counters? */
if (!c)
    goto recalculate;
/*
 * from this point on nothing can prevent us from
 * switching to the next task, save this fact in
 * sched_data.\ */
sched_data->curr = next;
```