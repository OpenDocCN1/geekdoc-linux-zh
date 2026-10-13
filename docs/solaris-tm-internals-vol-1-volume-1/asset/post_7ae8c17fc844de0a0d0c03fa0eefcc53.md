
![](img/220ae4af07df2fe8e5be69d27f885d1b_415_0.png)

### Figure 9.5 *Solaris Dispatch Queues*

### 9.2.2 Thread Priorities

The operating system uses a global priority scheme to assign priorities to kernel threads; the priorities are derived from a dispatch table according to the scheduling class the thread belongs to. As we saw, each scheduling class has a range of priorities assigned to it. As scheduling classes load into the system, the kernel must ensure that every priority level across all loaded scheduling classes has a unique priority number.

The range of priorities for the TS/IA class is 0–59, which corresponds to global priorities 0–59 since the TS/IA class is the lowest class on the system. SYS priorities range from 0–39 and are assigned global priorities 60–99 since the SYS class sits directly above the TS/IA class. If the RT class is not loaded, interrupt priorities range 0–9, occupy global priorities 100–109. Thus, without the RT class loaded, there is a total of 110 (0–109) global priorities. When the RT class (range 0–39) loads, the interrupt thread priorities are bumped up to global priorities 160–169, and the RT global priority range is 100–159. This protocol is represented in Figure 9.2 on page 354 and Table 9-1 on page 351.

During dispatcher initialization, the kernel calculates the maximum SYS global priority value and the total number of global priorities as scheduling classes are loaded. These values are recalculated if scheduling classes are loaded following initialization, for example, if the RT class is loaded sometime after the system has been booted. The calculated values are stored in the system var structure’s v_nglobpris and v_maxsyspri field.

```text
# /etc/crash
> dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> v
.
.
v_nglobpris: 170
v_maxsyspri: 99
.
.
```

Newly created threads inherit their priority and scheduling class from the parent process (parent thread, actually—remember, nonthreaded processes have one LWP/kthread pair). Recall from the previous chapter, the forkwp() kernel routine calls thread_create(), which in turn calls thread_create(). thread_create() is passed as arguments a thread state (TS_STOPPED—the initial state of a kthread) and priority, which is established from the calling thread. The other applicable kthread structure members are initialized toward the end of the forkwp() code, including the allocation of the class-specific data structure (e.g., tsproc). Entry into the class-specific fork routine through CL_FORK() completes the setup of the dispatcher data for the new thread, initializing the class data structure for the thread and putting it on the linked list of class structures.

The kernel thread structure fields relevant to thread priorities are t_pri, which is the actual global dispatcher priority for the thread, t_epri, which reflects an inherited priority, and `t_kpri_req`, which is a flag to indicate to the dispatcher that a SYS priority is requested for the thread. Other per-thread priority-related data is maintained in the class-specific data structure linked to the kthread: `tsproc` for TS/IA threads, `rtproc` for RT threads. For TS/IA threads, the kernel provides a facility for user-level priority adjustments, similar in concept to the traditional `nice(1)` command. Unix systems provided a `nice(1)` command that allowed users to adjust the priority of the processes they owned. Non-root users could only make their own process priorities worse (they could be nice to the other users of the system), and root could make priorities better with `nice(1)`. Solaris supports `nice(1)` today for compatibility, but the proper way to apply user-level priorities to threads is to use `priocntl(1)` command. Issuing `priocntl(1)` with the `-l` (lowercase l) flag displays the range of user priorities.

```text
# priocntl -l
CONFIGURED CLASSES
===================

SYS (System Class)

TS (Time Sharing)
        Configured TS User Priority Range: -60 through 60

IA (Interactive)
        Configured IA User Priority Range: -60 through 60

RT (Real Time)
        Maximum Configured RT Priority: 59
```

The user priority ranges shown in the preceding `priocntl(1)` command output clearly do not reflect the range of priorities for the TS/IA class from a kernel perspective. The user priority facility allows a user to move a process or thread priority in a positive (better) or negative (worse) direction. The priority value specified on the command line can be as high as 60 (maximum potential priority) or as low as -60 (lowest possible priority). A priority value specified on a `priocntl(1)` command line does not become the process’s or thread’s actual global dispatch priority (as seen with `ps(1)`, e.g., `ps -Lc`), but rather is used by the dispatcher code to adjust a kernel thread’s priority. A user-supplied priority will alter the global dispatcher priority of the thread in one direction or another, depending on the value specified.

For RT class threads or processes, the valid range of priorities is 0–59; the `priocntl(1)` output shown above indicates a maximum value of 59. The RT class does not support the notion of user mode priorities. Priority tweaking of RT threads involves simply specifying a priority value in the RT class range; then, that value will be directly reflected in the global dispatch priority of the process. For example, the global priority range for RT is 100–159, where global priority 100 corresponds to RT priority 0, global priority 120 corresponds to RT priority 19, and so on.

So, below, we used `priocntl(1)` to start a program in real time and specified a priority.

```text
# priocntl -e -c RT -p 59 ./hog &
1016
# ps -Lcc
  PID  LWP  CLS  PRI TTY      TIME CMD
 1016    1   RT  159 pts/2  0:03 hog
 1015    1   TS   48 pts/2  0:00 sh
 1017    1   TS   48 pts/2  0:00 ps
```

We specified a priority value of 59 on the command line. Note the actual global dispatch priority of the process we started is 159. This value results from the kernel turning the specified priority into a global dispatch priority. In the case of RT processes and threads, the kernel uses the user-supplied RT priority value as an index into the RT dispatch table to retrieve the corresponding global dispatch priority, as illustrated in Figure 9.6.

![](img/220ae4af07df2fe8e5be69d27f885d1b_418_0.png)

An invocation of the `priocntl(1)` command to execute a process as a real-time process defaults to the base RT class priority, which is 0, resulting in a global dispatch priority of 100—the value in the 0th entry in the real-time dispatch table (rt_dptbl). The example in Figure 9.6 specifies a value of 59, and the kernel will plug into the rt_pri field of the thread's rtproc structure and use as an index in the dispatch table, rt_dptbl. The corresponding value is used to set the thread's actual global dispatch priority, 159, in this example. A kernel thread_change_pri() function is called to set the dispatcher priority in the kthread's t_pri field.

User-settable priorities for RT threads is the easy case, which is why we talked about that first. The SYS class is even easier: user-level tweaking of SYS class thread priorities does not exist, period. Which brings us back to TS/IA class threads. First, a quick note before we move on. Kernel threads in the same process can run at different scheduling classes and priorities. A multithreaded process can have LWP/kthread pairs in the TS, IA, SYS, and RT class. The priocntl(1) command, however, does not provide that level of granularity for control. priocntl(1) provides for scheduling class and priority control only on a per-process level, not per LWP/kthread. The priocntl(2) system call has facilities for specifying an LWP ID versus a PID, so code can alter scheduling classes and priorities of the LWP/kthread level.

Several fields in the tsproc structure support the implementation of user mode priorities for TS threads: ts_umpri, the user priority within the TS class range; ts_upri, the user priority value; ts_uprilim, a boundary (limit) on user priority values; and ts_cpupri, the kernel component of user priorities. ts_cpupri exists essentially to give the kernel some control over user-adjusted priorities (think of it as a throttle). It is used in conjunction with the user priority, ts_umdpri, to index into the TS dispatch table to set new values for both ts_cpupri and the thread's actual priority, t_pri. The ts_uprilim field exists to enable users to place their own throttle in user mode priorities.

The dispatcher uses these values in the kernel for boundary checking on user-supplied priorities and for adjusting a thread’s priority as a result of the priocntl() call. Once user priorities are set, they remain in use for subsequent thread priority adjustments. ts_cpupri is set to 29 when the LWP/kthread is initialized; ts_upri and ts_uprilim are initialized to 0. Without an explicit priocntl(1) or priocntl(2) command issued on a process or kthread, the user mode priorities do not factor in to the normal priority adjustments done during the execution life of a kernel thread. If an LWP/kthread has a user priority set and issues a fork(), then the new process LWP/kthread inherits the user-supplied values from the parent thread.

RT class thread priorities are fixed, as opposed to TS/IA thread priorities, which are adjusted in many places during the life of a thread: after initialization on return from a fork(), when a thread is made runnable by ts_setrun(), upon sleep and wakeup, upon return from a trap, during clock tick processing, prior to a context switch, and during a regular thread update that is executed through the callout queue feature from the clock interrupt handler. The actual priority adjustment is, in some cases, contingent on a conditional test in the code, for example, has a thread been waiting to get on a dispatch queue for an inordinate amount of time? We’ll look at some examples to illustrate the mechanics of establishing a thread's priority, starting with TS and IA class threads.

Refer to Figure 9.7, which illustrates the following sequence.

- 1. After the creation and initialization of the LWP/kthread (fork()), a fork return function is called to set the kthread’s priority and place it on a dispatch queue. The inherited ts_cpupri value indexes into the TS dispatch table (1).
- 2. It creates a new ts_cpupri value that is based on the ts_tqexp value in the indexed table location.
- 3. The ts_timedleft value is set on the basis of the allotted time quantum for the priority level.
