# Introduction to the Linux Operating System

```
#if CONFIG_SMP
next->has_cpu = 1;
next->processor = this_cpu;
#endif
spin_unlock_irq(&runqueue_lock);

if (prev == next)
    goto same_process;
#if CONFIG_SMP
/*
* we maintain the per-process 'last schedule' value.
* (this has to be recalculated even if we reschedule to
* (the same process) Currently this is only used on SMP,
* and it's approximate, so we do not have to maintain
* it while holding the runqueue spinlock.
* */
sched_data->last_schedule = get_cycles();
/*
* We drop the scheduler lock early (it's a global spinlock),
* thus we have to lock the previous process from getting
rescheduled during switch_to();
 */
#endif /* CONFIG_SMP */
```

# 2.11 The scheduler iv: linux/kernel/sched.c

```
kstat.context_svctch();
/*
there are 3 processes which are affected by a context switch:
prev == ... => (last => next)

It's the 'most previous' 'prev' that is on next's stack,
but prev is set to (the just run) 'last' process by switch_to().
This might sound slightly confusing but makes tones of sense.

prepare_switch({
    struct sched_mm *mm = next->mm;
    struct sched_mm *oldmm = prev->active_mm;
    if (mm) {
        if (next->active_mm) BUG();
        next->active_mm = oldmm;
        atomic_inc(&oldmm->mm_count);
        enter_lazy_tlb(oldmm, next, this_cpu);
    } else {
        if (next->active_mm != mm) BUG();
        switch_mm(oldmm, mm, next, this_cpu);
    }
}
if (!prev->mm) {
```