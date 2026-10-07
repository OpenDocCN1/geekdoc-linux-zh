+   Thus, the new ts_cpupri value is 18th, which also becomes the ts_udmpri when the user mode priority is calculated—ts_upri and ts_boost are zero values (no user priority, and it's a TS class thread, so no priority boost).

+   The global dispatch priority at index location 18 is 17, so the kthread's initial (t_pri) is 17, with a 120 clock time quantum (derived by using ts_cpupri as an index).

+   When 120 ticks are gone and ts_tifeleft has clicked down to 0, we'll essentially repeat the steps to get the new priority.

+   ts_cpupri is now 18, the ts_tqexp value at the corresponding location is 7, the new ts_cpupri value is 7, which again becomes ts_udmpri after the user mode priority is calculated.

+   The global dispatch priority at the 7th array location is 6, so the kthread's priority after its time quantum will go from 17 to 6, a worse priority. Its time quantum is larger, at 160 clock ticks, so it will wait longer to run but get more clock ticks when it executes. The behavior is consistent with the targeted behavior of timeshare class threads. As threads get more execution time, their priority is worsened; as spend more time waiting to run, their priority is improved.

The second case we'll look at centers around kthread sleep and wakeup. Specifics of the sleep queue implementation and wakeup mechanism are discussed in the next section, but we can still examine the priority component of these states without detracting from either discussion.

+   The ts_sleep() function handles the preparation of a TS/IA class thread for sleep. The code tests the t_kpri_req flag (kernel priority requested), which will be set if the thread is holding a kernel RW lock or an exclusive package lock on a memory page when the sleep function is invoked. If t_kpri_req is set, the thread priority, t_pri, is set to 100, the lowest SYS class priority, which puts it above all TS/IA class priorities.

+   The kthreadTSFRI flag is set to indicate that it is a SYS priority. If a kernel priority has not been requested for the thread, the ts_sleep() tests the ts_diswait value (how long the thread has been waiting on a dispatcher queue) against the ts_maxwait value in the dispatch table, indexed by ts_udmpri, which will index the same row to retrieve the global priority for the last time it was. The test looks something like this.

```
if (kthread->tsproc.ts_diswait == ds_dtpbl(ts_udmpri).ts_maxwait)
```

That condition is true if the thread has been waiting a relatively long time for processor cycles.

+   The priority is recomputed, as previously described, the ts_cpupri value is set from the ts_slpret (sleep return priority) column in the TS/IA dispatch table, and not the ts_tqexp column, as was the