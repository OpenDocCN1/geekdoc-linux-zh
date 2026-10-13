
In a running system, and the use of a lock per list allows multiple kernel routines to traverse different lists at the same time (see Figure 9.4).

![](img/220ae4af07df2fe8e5be69d27f885d1b_412_0.png)

**Figure 9.4** *tsproc Structure Lists*

### 9.2.1 Dispatch Queues

Every processor on the system has its own dispatch queue (actually, a queue of queues), and per-processor scheduling information is maintained in the data structures that describe the processors in the kernel (the CPU structures). Data structures make up the actual dispatch queues, which provide the linkage to the lists of runnable threads on the system and state information for each queue. Threads in the TS, IA, and SYS classes are placed on the per-processor dispatch queues.

A separate queue is maintained for threads that are runnable at a priority high enough to cause a kernel preemption. The Solaris kernel is, for the most part, pre-emptable, such that a processor executing in kernel (system) mode can be pre-empted so a higher-priority thread can run. Currently, the global dispatch priorities for RT class threads and interrupt threads are above SYS and can generate a kernel preemption. Since interrupt threads do not actually go on a dispatch queue, only unbound RT class threads are placed on the kernel preempt (`kp_preempt`) queue. There is one such queue systemwide on systems that do not have processor sets configured. A kernel preempt queue is created when a processor set is configured, so there is a per-processor set `kp_preempt` queue, plus one for the default processor set. Since the kernel will not allow every available processor on a system to be placed in a processor set, the number of kernel preempt queues on a system will always be the number of processor sets configured, plus 1. Without processor sets configured, there is one `kp_preempt` queue systemwide. We discuss preemption later in more detail.

The creation of the dispatch queues occurs at boot time during the Solaris system initialization. A kernel dispatcher initialization routine, `dispinit()`, is called from the architecture-specific startup code, which builds the kernel preemption queue and the per-cpu dispatch queues. The kernel data structures that make up the complete dispatch queue picture are the `cpu`, `disp_queue_info`, `_disp`, and `dispq` structures, as shown in Figure 9.5 on page 374. It is during the dispatcher initialization that the default processor set's preemption queue (`cp_kp_queue`) is maintained. In Solaris 2.5.1, which does not have processor sets, the global kernel preempt queue was maintained in a separate `disp_t` structure, `disp_kp_queue`.

A quick note on terminology before we proceed. A processor partition is essentially the same thing as a processor set. A user's view of a processor set is what the kernel references as a processor partition. A different abstraction exists for a possible future implementation, where some processor partitions are visible to the kernel but not visible to the user, so what users see as available processor sets may be different from the kernel's view of usable processor partitions. A default processor partition, which includes all available processors on the system, is created at boot time. As processor sets are created, processors configured into a user processor set are removed from the default partition and added to the configured set. (Processor sets are discussed in “Kernel Processor Control and Processor Sets” on page 419.)

The kernel retains at least one processor for the default partition and does not allow all available processors to be configured into user-created processor sets. Kernel threads that are part of the operating system, such as the daemon threads created at boot time (Chapter 2), pageout, NFS server threads, etc., will not run on a user processor set. That's why a default partition is created at boot time and at least one processor is retained for the default partition. In practice, it is always prudent to assess processor requirements before allocating processor resources by means of processor sets. A system with sufficient processing power for bound application processes may run poorly if CPU resources for the kernel are inadequate.

Several dispatcher-related variables are embedded in each cpu structure.

- **cpu_disp** — An embedded `_disp` structure; the dispatch queue data for the processor, which contains the link to the actual per-processor queues.
- **cpu_runrun** — A preemption flag indicating that the thread currently running on the CPU will be preempted before switching back to user mode. The user preemption flag.
- **cpu_kprunrun** — Another preemption flag, kernel preemption, indicating that the thread should be preempted immediately or as soon as possible (e.g., return from an interrupt). The kernel preemption flag.
- **cpu_chosen_level** — The priority at which the CPU was chosen for scheduling a kthread. Used by the dispatcher when selecting the next thread for execution.
- **cpu_dispthread** — A pointer to the kthread selected for execution on the CPU.
- **cpu_thread_lock** — A dispatcher lock on the current thread.
- **cpu_last_switch** — A time value: the last time the CPU switched execution to a new thread.

The dispatcher queue structure embedded in the cpu structure is where the per-CPU dispatch queue is rooted. It links to the per-priority dispatch queues maintained for each processor. Within each processor dispatch queue, separate linked lists of runnable kthreads are maintained for every priority level, except realtime lists. Unbound realtime threads are maintained on the global kp_queue. If processor sets are configured, then a kernel preempt queue is configured for each processor set.

Other data the dispatcher needs for queue management and thread scheduling maintained in the dispatch queue structure includes the following.

- **disp_lock** — A synchronization lock to protect fields in the structure.
- **disp_npri** — The number of priority levels in the queue.
- **disp_q** — The pointer to the dispatch queue (pointer to a dispq_t structure).
- **disp_q_limit** — Another pointer to a dispq_t structure, set to point to the end of the queue.
- **disp_qactmap** — A bitmap indicating which queues actually have runnable threads in them. Using the bitmap in conjunction with **disp_nrunpri** and **disp_nrunnable**, the dispatcher code can traverse the queues with extreme speed and efficiency, searching for the best runnable thread.
- **disp_maxrunpri** — The priority of the highest-priority thread on the queue.
- **disp_max_unbound_pri** — The priority of the highest-priority unbound thread on the queue.
- **disp_nrunnable** — Total number of runnable threads on the queue.
- **disp_cpu** — A pointer back to the cpu structure that owns this queue.

The dispatch queue entry itself is a small, three-member data structure, defined as a dispq_t structure. It contains a pointer to the first thread on the queue (dq_first), a pointer to the last thread on the queue (dq_last), and a count of kthreads on the queue (dq_sruncnt). Each per-priority queue maintains a count of threads on the queue, and the sum of all per-priority queues is represented in disp_nrunnable.

Finally, there's the disp_queue_info structure. An array of these structures is created at boot time, one for each processor on the system. Each array member (disp_queue_info structure) contains a pointer to one per-processor dispatch queue (disp_t) embedded in the cpu structure. There are two additional disp_t pointers, olddispq and newdispq, and storage space for an old and new queue bitmap field, oldqctmap and newqctmap, for queue manipulation and maintenance. The number of global priorities in the queue is also maintained in oldnglobpris. As we move through the algorithmic flow of the dispatcher code, we'll see how these structures and members are used. Figure 9.5 provides the big picture.
