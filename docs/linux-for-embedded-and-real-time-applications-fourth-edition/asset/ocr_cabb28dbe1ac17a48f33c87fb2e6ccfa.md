scheduling policies must have a priority greater than 0. Thus, a process scheduled with SCHED_FIFO or SCHED_RR will preempt any running normal process when it becomes ready.

A SCHED_FIFO process runs until it blocks or it yields. SCHED_RR is a minor variation on SCHED_FIFO that adds time slicing. If a SCHED_RR process exceeds its time slice it is placed at the back of its priority queue.

cyclictest has options to lock memory (-m) and to give its threads a higher priority (-p n). On my system, running cyclictest with a priority of 90 and a load of 20 kept the maximum latency down to about 12 milliseconds.

Locking memory did not improve things, which probably means there is no swapping going on anyway.

# ## Two Approaches

OK, so Linux is not real-time. What do we do about it? Well, there are at least two very different approaches to giving Linux deterministic behavior.

# ### Preemption Improvement

One approach is to modify the Linux kernel itself to make it more responsive. This primarily involves introducing additional preemption points in the kernel to reduce latency. An easy way to do this is to make use of the “spinlock” macros that already exist in the kernel to support symmetric multi-processing (SMP). In an SMP environment spinlocks prevent multiple processors from simultaneously executing a critical section of code on shared memory. In a uni-processor environment the spinlocks simply lock out the scheduler.

The preemption improvement strategy starts by turning the spinlocks into priority inheritance mutexes. This work of introducing preemption points in the kernel has been ongoing since late in the 2.4 series development. Mainline kernels these days implement three different preemption models, one of which is selected at build time as a configuration parameter:

+   * **No Forced Preemption (Server):** This is the traditional Linux preemption model, intended to maximize throughput. This is the preferred model for server applications. System call returns and interrupts are the only preemption points.
+   * **Voluntary Kernel Preemption (Desktop):** This option reduces the latency of the kernel by adding more “explicit preemption points” to the kernel code, at the cost of slightly lower throughput. In addition to explicit preemption points, system call returns and interrupt returns are still implicit preemption points.