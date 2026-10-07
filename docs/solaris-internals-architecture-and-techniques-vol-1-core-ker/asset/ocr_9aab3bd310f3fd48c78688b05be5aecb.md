# Turnstles and Priority Inheritance

and RW lock code use a turnstile when a kernel thread needs to block on a requested lock. The sleep queues implemented for other resource waits do not provide an elegant method of dealing with the priority inversion problem through priority inheritance. Turnstles were created to address that problem.

Priority inversion describes a scenario in which a higher-priority thread is unable to run because a lower-priority thread is holding a resource it needs, as a lock. The Solaris kernel addresses the priority inversion problem in its turnstile implementation, providing a priority inheritance mechanism, where the higher-priority thread can will its priority to the lower-priority thread holding the resource it requires. The beneficiary of the inheritance, the thread holding the resource, will now have a higher scheduling priority and thus get to run sooner so it can finish its work and release the resource, at which point the original priority is returned to the thread.

In this section, we assume you have some level of knowledge of kernel thread priorities, which are covered in Chapter 6 "Kernel Memory." Because turnstiles and priority inheritance are an integral part of the implementation of mutex and RW locks, we thought it best to discuss them here rather than later. For this discussion, it is important to be aware of these points:

+   - The Solaris kernel assigns a global priority to kernel threads, based on the scheduling class they belong to.
- Kernel threads in the timeshare and interactive scheduling classes will have their priorities adjusted over time, based on three things: the amount of time they spend running on a processor; sleep time (blocking), and the case when they are preempted. Threads in the real-time class are fixed priority; the priorities are never changed regardless of runtime or sleep time unless explicitly changed through programming interfaces or commands.

The Solaris kernel implements sleep queues for the placement of kernel threads blocking (waiting for) a resource or event. For most resource waits, such as for a disk or network I/O, sleep queues, in conjunction with condition variables, manage the systemwide queue of sleeping threads. These sleep queues are covered in Chapter 6, "Kernel Memory." This set of sleep queues is separate and distinct from turnstile sleep queues.

The implementation of turnstiles was changed substantially in Solaris 7, although the underlying premise and concepts are the same. We will begin with a look at the turnstile implementation in Solaris 7.

# 3.7.1 Solaris 7 Turnstiles

Figure 3.12 illustrates the Solaris 7 turnstiles. The rewrite of turnstiles in Solaris 7 resulted in a significant amount of code being removed, and some new, more efficient functions being develo.