
ties for specifying LWP ID versus a PID, so code can alter scheduling classes and priorities at the LWP/kthread level.

Several fields in the tsproc structure support the implementation of user mode priorities for TS threads: ts_umdpri, the user priority within the TS class range; ts_upri, the user priority; ts_uplim, a boundary (limit) on user priority values; and ts_cpup, the kernel component of user priorities exists essentially to give the kernel some control over user-adjusted priorities (think of it as a throttle). It is used in conjunction with the user priority, ts_umdpri, to index into the dispatch table to set new values for both ts_cpup and the thread's actual priority, t_pri. The ts_uplim field enables users to place their throttle on user mode priorities.

The dispatcher uses these values in the kernel for boundary checking on user-supplied priorities and for adjusting a thread's priority as a result of the priority(1). Once priorities are set, they remain for subsequent priority adjustments. ts_cpup is set to 29 when the LWP/kthread is initialized; ts_upri and ts_uplim are initialized to 0. Without explicit prioritycnt(1) or procnt(2) command issued on a process or kthread, the user mode priorities do not factor in the normal priority adjustments done during the execution of a kernel thread. If an LWP/kthread has a user priority set and issues a fork(), then the new LWP/kthread inherits the user-supplied values from the parent thread.

RT class threads are fixed, as opposed to TS/IA priorities, which are adjusted in many places during the life of a thread: after initialization on return from a fork(), when a thread is made runnable by ts_setrun(1), upon sleep and wakeup, upon return from a trap, during clock ticking, prior to a context switch, and during a regular thread update that is executed through the callback queue for the interrupt handler. The actual priority adjustment is, in some cases, contingent on a conditional test in the code, for example, a thread has been waiting to get on a dispatch queue for an amount of time? We will look at examples to illustrate the mechanics of establishing a thread's priority, starting with TS and IA class threads.

Refer to Figure 9.7, which illustrates the following sequence.

- 1. After creation and initialization of the LWP/kthread(fork()), a fork return function is called to set the kthread's priority and place it on the dispatch table (1).
2. It creates a new ts_cpupri value that is based on the ts_tqexp value in the indexed table location.
3. The ts_timeleft value is set on the base of the allotted time quantum for the priority level.
4. ts_diswait is set to 0. A user priority is calculated, setting the ts_umdpri value, which is used as an index into the TS/IA dispatch table to establish the thread's actual priority,

## The Kernel Dispatcher

5. t_pri is determined by the ts_globpri (global priority) value in the indexed table location (5).

![](img/a86367b95bf21add858c99948ac951c6_418_0.png)

Figure 9.7 Setting a Thread's Priority Following fork()

The calculation of the user mode priority (between steps 2 and 3), which is done whenever a TS/IA thread priority adjustment is required, is simple arithmetic, ming the ts_cpupri, ts_upri, and ts_boost values. ts_boost is used for IA class threads means of boosting the priority by a value of 10. ts_umdpri is set to the sum of ts_cpupri, ts_upri, and ts_boost and is tested against some bound values; it cannot be greater than the maximum TS/IA priority, or less than 0.

The other relevant step taken in the return code is the setting of the ts_timeleft and ts_dispatch fields in the kthread's tsproc structure. ts_timeleft tracks execution time when the kthread is running on processor or is decremented in the clock tick handler (if the thread is actually running on processor, of course). When ts_timeleft counts down to 0, the kthread has its quantum and is context-switched off the processor. ts_dispatch tracks how much the thread has spent switching on dispatch queue, waiting context-switched onto a processor for execution. For all threads on dispatch queue, ts_dispatch is updated once by the ts_update() thread, which is out of clock interrupt handler (more on this in the minute).

When the priority work has been done and t_pri in the kernel has a valid dispatch priority, the thread is ready to be placed on dispatch queue; placement is ultimately done by one of the dispatcher management functions, setfrontdq() or setbackdq(). How these functions work and whether kthread ends up at the front or back of queue matters.

## Solaris Kernel Dispatcher

Once a kthread is off and running, it can go through state changes that determine how priority adjustments are made. A typical thread spends time executing, gets interrupted, gets preempted, issues a blocking system call calling the thread to be placed on sleep queue, and forth. Class-specific functions are called appropriately as dictated by the dispatcher-related values in the thread's tsproc structure. For example, if a thread burns through its allotted time quantum in the dispatch table (Figure 9.7, step 3), the kthread is switched off the processor and given a new priority.

The scheduling-class-specific clock tick is called from each CPU that has running on it. When the ts_tick() function is invoked, the timeleft value is decremented and tested. If ts_timeleft reaches 0, the time quantum has expired for the kthread. This is the case for TS/IA threads that are not at SYS priority are time sliced. Assuming an expired time quantum, the code tests to see if scheduler activation has been turned on for the thread, in the form of preemption control.

The use of preemption control in application code is illustrated in the following pseudocode:

```
mutex_t mylock;
mutex_init(&mylock);
schedctl_init();

schedctl_start();
mutex_lock(&mylock);

do work while holding the mutex

mutex_unlock(&mylock);
schedctl_stop();
```

## Kernel Dispatcher

Without activation on preemption control, there's a greater possibility that the kthread will be forced to surrender the processor before it is able to free the lock. Think of preemption control as a means of telling the dispatcher "I'm about to grab a critical resource, so grant me a little extra time."

Getting back to the ts_tick() code, we entered the main segment of ts_tick() because the kthread was not running at a SYS priority and its time quantum has expired. If preemption control has been turned on for the kthread, it allows an extra couple of ticks to execute, and ts_tick() is finished with the thread. There is a limit to how many additional clock ticks a thread with preemption control turned on will be given. If that limit has been exceeded, the kernel sets a flag such that the thread will get one more time slice and on the next pass through ts_tick(), the preemption control test will fail and normal processing will be done. In this way, the kernel does not allow scheduler activation to keep the thread running indefinitely. If the requirement is that the thread must stay on the processor indefinitely, the RT class should be used.

Regular TS/IA task processing involves adjusting the priority in the way priority is set in the fork return code (Figure 9.7 on page 373). ts_cpu is used as an index in the TS dispatch table and assigned a new value that is based on ts_tqexp from the indexed location. The user mode priority calculates, ts_diswait is set to 0, and a new dispatcher priority is derived from the TS/IA dispatch table. The new priority is based on the global priority value in the table row corresponding to ts_udmpri, which is used as the dispatch array index. What differs between the ts_tick() handler and the fork return scenario is that the thread's priority is not set directly in ts_tick(), but rather in a thread_change_pri() function. A change in a thread priority may warrant a change in its position on a queue; thread_change_pri() handles such a case. In the fork return, we are dealing with a new thread that has not yet been on a queue, so it's not an issue.

By design for TS/IA class threads, the adjusted priority in the preceding scenario will end up being other than the thread was previously. If a thread consumed its entire time quantum, it gets a worse priority to allow other threads a better opportunity to obtain processor time. You can test this behavior by plugging in some actual values, walking through the adjustment sequence as we described it, and figuring where the thread's priority lands after the thread uses a full quantum.

Here's a quick example, assuming a simple case of no user priority.

- - A thread starts with a ts_cpu value of 29, which puts it right in the middle of the TS/IA priority range (which we are assuming is the default value of 29 was chosen). The ts_tqexp value at table location 29 (the 28th row, because the count starts at 0) is.
