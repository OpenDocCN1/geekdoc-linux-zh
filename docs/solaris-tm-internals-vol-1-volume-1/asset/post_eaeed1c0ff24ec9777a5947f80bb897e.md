
![](img/220ae4af07df2fe8e5be69d27f885d1b_387_0.png)

**Figure 8.25** *Process and Session Structure Links*

Figure 8.25 provides two illustrations. The top diagram shows some detail of the data structures and links for a simple case of a login session with two process groups. One process group has only one process, the login shell. The other process group has three processes. They all link to the session structure, which connects to the device and device driver through the `s_vp` vnode pointer. The session leader is the login shell, and the session ID is the PID of the login shell.

The lower illustration is a broader view, encapsulating a login session (a session) with a shell process in its own process group, plus three additional process groups. One process group is in the foreground, thus attached to the control terminal, receiving characters typed and able to write to the terminal screen. Job control shells use a `^Z` (Control-Z) key sequence to place a foreground process/process group in the background. A SIGTSTP signal is sent to all the processes in the group, and the processes are stopped. If a process sets up a signal handler and catches SIGTSTP, the handler is invoked and governs the process behavior.

The session leader (e.g., the shell) handles the communication link to the control terminal by using library calls that translate `ioctl()` routines into the STREAMS subsystem. (The character device drivers in Solaris for serial terminals and pseudoterminals are STREAMS based.) The Solaris C library includes `tcsetpgrp(3)` and `tcgetpgrp(3)` interfaces for setting and getting the process group ID for a control terminal.

When processes or process groups are moved from the background into the foreground, the session leader issues a `tcsetpgrp(3)` call to direct the control terminal to the new foreground process. The `tcsetpgrp(3)` call results in an `ioctl()` call into the tty/pty driver code with the `TIOCSPGRP` flag, which in turn enters the STREAMS subsystem, calling the `strsetpgrp()` function (STREAM set process group). The data structures associated with the control terminal include a STREAM header structure, `stdata`, which contains a pointer to a PID structure for the foreground process group. When a new process or process group is placed into the foreground, the `pgrp` pointer is set to reference the PID structure of the process group leader in the new foreground process group. In this way, the control terminal is dynamically attached to different process groups running under the same session.

The signal mechanism in the kernel that delivers signals to groups of processes is the same code used for other signal delivery. A `pgsignal()` (process group signal) interface is implemented in the kernel. The function follows the pointers that link processes in a process group and calls the generic `sigtoproc()` function in each pass through the loop, causing the signal to be posted to each process in the process group.

## The Solaris Kernel Dispatcher

In the previous chapter, we discussed (among other things) the creation and termination of processes and the LWPs and kernel threads within the process. Now we'll talk about what happens in between creation and termination: the scheduling and execution phase, managed by the Solaris kernel dispatcher (a.k.a. scheduler).

The framework on which the Solaris 2.X scheduler is built is rooted in the Unix SVR4 scheduler, which represents a complete rework of the traditional Unix scheduler. The rework incorporated the notion of a scheduling class, which defines the scheduling policies and systemwide priority range for kernel threads in a particular scheduling class. The implementation of dispatch tables for storing the parameters used by the scheduler code was introduced. For each scheduling class, there exists a table of values and parameters the dispatcher code uses for establishing the priority of a kernel thread, which ultimately drives the thread's placement on a dispatch queue—the Solaris queues of runnable threads waiting for an available processor.

In this chapter, we examine the implementation of the kernel scheduler, or dispatcher, in Solaris. We discuss the scheduling classes, the dispatch tables, and the kernel functions that provide the dispatcher infrastructure, including the kernel thread priority scheme and priority algorithms. We take a look at sleep queues and the kernel sleep/wakeup facilities. Finally, we discuss innovative features in the kernel, such as scheduler activations.

### 9.1 Overview

The Solaris kernel scheduler provides a rich set of features and innovations that contribute significantly to the speed and scalability of the operating system. The Solaris kernel is preemptive; that is, the execution of an operating system kernel thread, or user thread, can be preempted if a higher priority thread becomes runnable. This feature minimizes dispatch latency and is a key component to the implementation of the real-time scheduling class. The preemption mechanism is applied across the entire range of system priorities. In general, if a thread of a higher (better) priority than all threads currently executing becomes runnable, a preemption will occur, forcing the executing thread to relinquish the processor so the higher priority thread can run.

The process of moving a kernel thread on and off a processor (CPU) is referred to as **context switching**, and the Solaris kernel tracks both *involuntary* context switches and *voluntary* context switches. An involuntary context switch occurs when a thread is preempted (because a better priority thread has transitioned to the runnable state) or when an executing kernel thread uses up its allotted time quantum. Voluntary context switches result from a thread executing a blocking system call, such as a file read, where the thread will be context-switched off the processor and placed on a sleep queue. When the event a thread is sleeping (blocking) for occurs, a wakeup mechanism notifies the thread and places it back on a run queue, where it will be scheduled onto a processor, based on its global priority as compared to other runnable threads.

Additionally, a scalable queuing mechanism is employed for runnable threads. Rather than implementing a single, monolithic queue to hold all runnable threads systemwide, the Solaris kernel creates a set of dispatch queues for every processor on a system. Access to the per-processor queues is synchronized by means of locks that exist at the queue level (as opposed to a single dispatch queue lock), providing concurrency on queue manipulation functions.

The Solaris kernel dispatcher implements additional features that enhance the overall usability and flexibility of the operating system:

- **Scheduling classes.** Kernel threads have a scheduling class and priority. Different scheduling classes provide different scheduling policies and priority boundaries.
- **Intuitive priority scheme.** Higher priorities are better priorities (the traditional Unix implementation was so designed that low priorities were better priorities). The kernel defines a range of global priorities, 0–169. Within that global priority range, a given scheduling class is assigned a subset of the total number of global priorities, as shown in Figure 9.1.

![](img/220ae4af07df2fe8e5be69d27f885d1b_392_0.png)

**Figure 9.1** *Global Priority Scheme and Scheduling Classes*

The priority assignments for each scheduling class are shown in Table 9-1.

**Table 9-1** *Scheduling Class Priority Ranges*

| Class Priority Range | Global Priority Range | Scheduling Class |
|---|---|---|
| 0 – 59 | 000 – 059 | Timeshare (TS) and Interactive (IA) |
| 0 – 39 | 060 – 099 | System (SYS) |
| 0 – 9 | 100 – 109 | Interrupt threads (not really a scheduling class) if the RT class is *not* loaded |
| 0 – 59 | 100 – 159 | Realtime (RT) |
| 0 – 9 | 160 – 169 | Interrupt threads if the RT class is loaded |

- **Real-time support.** Solaris now provides support for real-time applications, which require a predictable, bounded dispatch latency (the elapsed time between the time when a thread needs to run and the time when it actually begins executing on a processor).
- **Table-driven scheduler parameters.** You can now “tune” the dispatcher for specific application requirements by altering the values in the dispatch table for a particular scheduling class. Note that altering the dispatch table values can dramatically affect the behavior of an application, some-
