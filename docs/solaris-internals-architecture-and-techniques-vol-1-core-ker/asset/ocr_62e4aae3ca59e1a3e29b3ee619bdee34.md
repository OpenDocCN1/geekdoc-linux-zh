# Processes, Threads, and Scheduling

15

![](bbox=[0.115, 0.076, 0.843, 0.442])

The kernel dispatcher manages run queues of runnable kernel threads, and it schedules kernel threads onto available processors according to priority and scheduling class.

Figure 1.3 Kernel Threads, Processes, and Lightweight Processes

# 1.4.1 Two-Level Thread Model

Although it is relatively inexpensive to switch between multiple threads within a process, it is still relatively expensive to create and destroy threads. In addition, each kernel thread within a process requires a lightweight process containing a stack that consumes kernel resources. For these reasons, an additional level of thread management is implemented within each process to manage user threads, as shown in Figure 1.4

![](bbox=[0.115, 0.698, 0.843, 0.915])

User threads are scheduled onto LWPs so that they can execute.

Figure 1.4 Two-Level Thread Model