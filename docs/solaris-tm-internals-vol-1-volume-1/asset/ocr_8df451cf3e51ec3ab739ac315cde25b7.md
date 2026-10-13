which does not have processor sets, the global kernel preempt queue was maintained in a separate `disp_t` structure, `disp_kp_queue`.

A quick note on terminology before we proceed. A processor partition is essentially the same thing as a processor set. A user's view of a processor set is what the kernel references as a processor partition. A different abstraction exists for a possible future implementation, where some processor partitions are visible to the kernel but not visible to the user, so what users see as available processor sets may be different from the kernel's view of usable processor partitions. A default processor partition, which includes all available processors on the system, is created at boot time. As processor sets are created, processors configured into a user process set are removed from the default partition and added to the configured set. (Processor sets are discussed in “Kernel Processor Control and Processor Sets” on page 419.)

The kernel retains at least one processor for the default partition and does not allow all available processors to be configured into user-created processor sets. Kernel threads that are part of the operating system, such as the daemon threads created at boot time (Chapter 2), pageout, NFS server threads, etc., will not run on a user processor set. That's why a default partition is created at boot time and at least one processor is retained for the default partition. In practice, it is always prudent to assess processor requirements before allocating processor resources by means of processor sets. A system with sufficient processing power for bound application processes may run poorly if CPU resources for the kernel are inadequate.

Several dispatcher-related variables are embedded in each cpu structure.

+   - **cpu_disp** — An embedded `_disp` structure; the dispatch queue data for the processor, which contains the link to the actual per-processor queues.
+   - **cpu_runrun** — A preemption flag indicating that the thread currently running on the CPU will be preempted before switching back to user mode. The user preemption flag.
+   - **cpu_kprunrun** — Another preemption flag, kernel preemption, indicating that the thread should be preempted immediately or as soon as possible (e.g., return from an interrupt). The kernel preemption flag.
+   - **cpu_chosen_level** — The priority at which the CPU was chosen for scheduling a kthre​ad. Used by the dispatcher when selecting the next thread for execution.
+   - **cpu_dispthread** — A pointer to the kthread selected for execution on the CPU.
+   - **cpu_thread_lock** — A dispatcher lock on the current thread.
+   - **cpu_last_switch** — A time value: the last time the CPU switched execution to a new thread.

The dispatcher queue structure embedded in the cpu structure is where the per-CPU dispatch queue is rooted. It links to the per-priority dispatch queues