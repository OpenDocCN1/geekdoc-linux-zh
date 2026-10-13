
`dispadmin(1M)` command, for example, `dispadmin -c TS -g` will dump the current timeshare (TS) and interactive (IA) class dispatch table on your Solaris system. (TS and IA use the same dispatch table.)

```text
# dispadmin -g -c TS
# Time Sharing Dispatcher Configuration
RES=1000

# ts_quantum  ts_tqexp  ts_slpret  ts_maxwait  ts_lwait  PRIORITY LEVEL
    1000         0         50          0          50        #   0
     200         0         50          0          50        #   1


        ................................................

        40        48        58          0          59        #  58
        20        49        59       32000          59        #  59
```

Table 9-2 shows the default values for a selected group of timeshare/interactive priorities. In the interest of space and readability, we don’t list all 60 (0–59) priorities since we only need a representative sample for this discussion.

**Table 9-2** *Timeshare and Interactive Dispatch Table*

| RES | ts_globpri | ts_quantum | ts_tqexp | ts_slpret | ts_maxwait | ts_lwait | PRI |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 1000 | 0 | 200 | 0 | 50 | 0 | 50 | 0 |
|  | 5 | 200 | 0 | 50 | 0 | 50 | 5 |
|  | 10 | 160 | 0 | 51 | 0 | 51 | 10 |
|  | 11 | 160 | 1 | 51 | 0 | 51 | 11 |
|  | 15 | 160 | 5 | 51 | 0 | 51 | 15 |
|  | 20 | 120 | 10 | 52 | 0 | 52 | 20 |
|  | 25 | 120 | 15 | 52 | 0 | 52 | 25 |
|  | 30 | 80 | 20 | 53 | 0 | 53 | 30 |
|  | 35 | 80 | 25 | 54 | 0 | 54 | 35 |
|  | 40 | 40 | 30 | 55 | 0 | 55 | 40 |
|  | 45 | 40 | 35 | 56 | 0 | 56 | 45 |
|  | 50 | 40 | 40 | 58 | 0 | 59 | 50 |
|  | 55 | 40 | 45 | 58 | 0 | 59 | 55 |
|  | 59 | 20 | 49 | 59 | 32000 | 59 | 59 |

Each entry in the TS/IA dispatch table (each row) is defined by the `tsdpent` (time-share dispatch entry) data structure (from `/usr/include/sys/ts.h`), as shown below.

```c
/* time-sharing dispatcher parameter table entry
 */
typedef struct tsdpent {
        pri_t       ts_globpri;     /* global (class independent) priority */
        int         ts_quantum;     /* time quantum given to proc at this level */
        pri_t       ts_tqexp;       /* ts_utpri assigned when proc at this level */
                                    /* exceeds its time quantum */
        pri_t       ts_slpret;      /* ts_utpri assigned when proc at this level */
                                    /* returns to user mode after sleeping */
        short       ts_maxwait;     /* bumped to ts_lwait if more than ts_maxwait */
                                    /* secs elapse before receiving full quantum */
        short       ts_lwait;       /* ts_mdpri assigned if ts_dispwt exceeds */
                                    /* ts_tswait */
} tsdpent_t;
```

### Header File `<sys/ts.h>`

The RES and PRI columns are not defined in `tsdpent`. Those fields, along with the defined members in the structure table, are described below.

- **RES** — (resolution value) Interprets the `ts_quantum` column in the dispatch table. The reciprocal of RES determines the level of granularity in which the `ts_quantum` field will be displayed. As the value of RES increases, the `ts_quantum` column values also increase by the same order of magnitude. See `ts_quantum` below for more information.

- **PRI** — The class-dependent priority, not the systemwide global priority. The PRI column is derived as the row number in the dispatch table. The dispatch table is like any other generic table—it has rows and columns. Every row corresponds to a unique priority level within the scheduling class, and each column in the row contains values that determine the priority adjustments made on the thread running at that particular priority. This is not the same as `ts_globpri`.

- **ts_globpri** — The only table parameter (`tsdpent` structure member) that is not displayed in the output of the `dispadmin(1M)` command and also the only value that is not tunable. `ts_globpri` is the class-independent global priority that corresponds to the timeshare priority (column farthest to the right).

A given scheduling class within Solaris has a range of priorities beginning with 0, which represents the lowest priority for that class. The TS and IA classes have 60 priorities, range 0–59. The kernel implements a global priority scheme, such that every priority level available in every scheduling class can be uniquely identified with an integer value. Refer to Figure 9.2 on page 354 for a list of global priorities when all the bundled scheduling classes are loaded.

Since TS/IA is the lowest class, the kernel global priorities 0–59 correspond to the TS/IA class priorities 0–59. The kernel computes global priorities at boot time and will recompute if necessary if a new class is loaded into a running system. For example, referring again to Figure 9.2, if the RT class is not loaded, global priorities for interrupt threads will be 100–109, just above system (SYS). If the RT class gets loaded, the global priorities for RT become 100–159, and interrupt threads are bumped up to 160–169. `ts_globpri` sets the `t_pri` field for a timeshare kernel thread when priorities are reset and readjusted.

- **ts_quantum** — The time quantum; the amount of time that a thread at this priority is allowed to run before it must relinquish the processor. Be aware that the `ts_dptbl(4)` manual page, as well as other references, indicate that the value in the `ts_quantum` field is in ticks. A tick is a unit of time that can vary from platform to platform. On all UltraSPARC based systems, there are 100 ticks per second, so a tick occurs every 10 milliseconds. The value in `ts_quantum` is in ticks only if RES is 100. If RES is any other value, including the default value of 1000, then `ts_quantum` represents some fraction of a second, the fractional value determined by the reciprocal value of RES. With a default value of RES = 1000, the reciprocal of 1000 is .001, or one millisecond. Thus, by default, the `ts_quantum` field represents the time quantum for a given priority in milliseconds.

  From Table 9-2 on page 363, we see that priority 0 kthreads get 200 milliseconds (20 ticks), priority 10 kthreads get 160 milliseconds, etc. As a kthread’s priority gets better (higher global priority integer value), its time quantum is less. Lower (worse) priorities get larger time quantums, since they are scheduled to run less frequently. Changing the RES value by using the `-r` flag with `dispadmin(1M)`

  ```
  dispadmin -c TS -g -r 100
  ```

  causes the values in the `ts_quantum` column to change. For example, at priority 0, instead of a quantum of 200 with a RES of 1000, we have a quantum of 20 with a RES of 100. The fractional unit is different. Instead of 200 milliseconds with a RES value of 1000, we get 20 hundredths of a second, which is the same amount of time, just represented differently [20 × 0.010 = 200 × 0.001]. In general, it makes sense to simply leave the RES value at the default of 1000, which makes it easy to interpret the `ts_quantum` field as milliseconds.

- **ts_tqexp** — Time quantum expired. The new priority a thread is set to when it has exceeded its time quantum. From the default values in the TS dispatch table, threads at priorities 0–10 will have their priority set to 0 if they burn through their allotted time quantum of 200 milliseconds (160 milliseconds for priority 10 threads). As another example, threads at priority 50 have a 40 millisecond time quantum and will have their priority set to 40 if they use up their time.

- **ts_slpret** — The sleep return priority value. A thread that has been sleeping has its priority set to this value when it is woken up. These are set such that the thread will be placed at a higher priority (in some cases, substantially higher) so the thread gets some processor time after having slept (waited for an event, which typically is a disk or network I/O).

- **ts_maxwait** — Used in conjunction with `ts_lwait`. They attempt to compensate threads that have been preempted and have waited a (relatively) long time before using up their time quantum. When a thread begins execution, a field, called `ts_dispwait`, in the class-specific structure linked to the thread (Figure 9.3 on page 362) counts the number of seconds that have elapsed since the thread began executing. This value is not reset if the thread is preempted (must involuntarily relinquish the processor). Once a second, a kernel routine executes to increment the `ts_dispwait` field for all TS and IA class threads. If the value of the `ts_dispwait` field for the thread is greater than that of `ts_maxwait`, the thread priority is set to the value of `ts_lwait`, a higher priority for the thread since in this circumstance it must have been preempted and never had a chance to use its time quantum.

- **ts_lwait** — The new priority for a thread that has waited longer than `ts_maxwait` to use its time quantum. Interesting to note is that the default values in the TS and IA dispatch tables inject a 0 value in `ts_maxwait` for every priority except the highest priority (59). So, just one increment in the `ts_dispwait` field will cause the thread priority to be readjusted to `ts_lwait`, except for priority 59 threads. The net effect is that all but the highest-priority (59) timeshare threads have their priority bumped to the 50–59 range (`ts_lwait`) every second.

This process has the desirable effect of not penalizing a thread that is CPU-bound for an extended period of time. Threads that are CPU hogs will, over time, end up in the low 0–9 priority range as they keep using up their time quantum because of priority readjustments by `ts_tqexp`. Once a second, they’ll get bumped back up to the 50–59 range and will only migrate back down if they sustain their CPU-bound behavior.

Priority 59 threads are handled differently. These threads are already at the maximum (highest) priority for a timeshare thread, so there’s no way to bump their priority with `ts_maxwait` and make it better. The `ts_update()` routine, which is the kernel code segment that increments the `ts_dispwait` value and readjusts thread priorities by means of `ts_lwait`, reorders the linked list of threads on the dispatch queues after adjusting the priority. The reordering after the priority adjustment puts threads at the front of their new dispatch queue for that priority. The threads on the priority 59 linked list would end up reordered but still at the same priority.

Experimentation has shown that this approach has two results: some percentage of priority 59 threads never get processor time, and the threads that `ts_update()` puts on the front of the dispatch queue following adjustment get scheduled more frequently. When the `ts_maxwait` value is set to 32000 for priority 59, the queue is never reordered by `ts_update()` and every thread has a fair shot at getting scheduled.

You can apply user-supplied values to the dispatch tables by using the `dispadmin(1M)` command or by compiling a new `/kernel/sched/TS_DPTBL` loadable module and replacing the default module. The `ts_dptbl(4)` manual page provides the source and the instructions for doing this. Either way, any changes to the dis-
