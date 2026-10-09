![](bbox=[0.16, 0.08, 0.86, 0.3])

# Common Real-Time Kernel Requirements

By now you understand what real-time means and what role it plays in processing external events. Now we can look at more detailed requirements a software system must meet in order to qualify as real-time. There are many types of real-time, as we have seen, and therefore many types of systems that qualify in different ways as real-time systems. But certain concepts run through all of them.

# A Fine-Grained Preemptible Kernel

Because real-time behavior is a matter of reacting early enough and properly to internal and external events, a real-time kernel has to be able to switch as soon as possible from a low-priority context to a high-priority task that needs attention. The time this takes is called the *preemption granularity*, and the longest time that could be spent waiting for a pending rescheduling to take place defines the worst-case dispatch latency of a kernel.

This issue has already been addressed by different patches to the Linux 2.4 series, which introduce opportunities for task scheduling in the kernel code. Previously, a new task could be scheduled only upon exit from the kernel context—that is, as long as the kernel was handling activities required by a system call or another user space request, the kernel wouldn’t stop in order to allow a new task to run.

Probably the best-known approach to a preemptible kernel, called the *preemptible kernel* support, was instituted by Robert Love while he was at Montavista. This was merged into the mainline kernel during the 2.5 development phase and is now available as a standard feature of Linux 2.6. It offers significantly better preemptibility on average. On the other hand, the concurrence between tasks is still suboptimal, because kernel preemption remains globally disabled as long as any task on the system holds any exclusive resource, even if no other task could compete for the same resource. As a consequence of this, only the average latency shows some improvement, but