+   4. `ts_dispwait` is set to 0. A user mode priority is calculated, setting the `ts_umpri` value, which is then used as an index into the TS/IA dispatch table to establish the thread’s actual dispatch priority.
+   5. `t_pri` is determined by the `ts_globpri` (global priority) value in the indexed table location (5).

![](bbox=[0.27, 0.236, 0.809, 0.464])

*Figure 9.7 Setting a Thread’s Priority Following `fork()`*

The calculation of the user mode priority (between steps 2 and 3), which is done whenever a TS/IA thread priority adjustment is required, is simple arithmetic, summing the `ts_cpupri`, `ts_upri`, and `ts_boost` values. `ts_boost` is used for IA class threads as a means of boosting the priority by a value of 10. `ts_umpri` is set to the sum of `ts_cpupri`, `ts_upri`, `ts_boost` and is tested against some boundary values; it cannot be greater than the maximum TS/IA class priority, 59, or less than 0.

The other relevant step taken in the fork return code is the setting of the `ts_timeleft` and `ts_dispwait` fields in the kthread’s `tsproc` structure. `ts_timeleft` tracks execution time when the kthread is running on a processor and is decremented in the clock tick handler (if the thread is actually running on a processor, of course). When `ts_timeleft` counts down to 0, the kthread has used its time quantum and is context-switched off the processor. `ts_dispwait` tracks how much time the thread has spent sitting on a dispatch queue, waiting to get context-switched onto a processor for execution. For all threads on a dispatch queue, `ts_dispwait` is updated once a second by the `ts_update()` thread, which is run out of the callout queue from the clock interrupt handler (more on this in a minute).

When the priority work has been done and `t_pri` in the kernel thread has a valid dispatch priority, the thread is ready to be placed on a dispatch queue; such placement is ultimately done by one of the dispatcher queue management functions, `setfrontdq()` or `setbackdq()`. How these functions work and whether a