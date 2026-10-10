This is a candidate for being implemented as a kernel thread for the following reasons:

+   • It’s a background task because it has to wait for asynchronous events.

+   • It needs access to kernel data structures because the actual detection of events is done by other parts of the kernel.

+   • It has to invoke a user mode helper program, which is a time-consuming operation.

# Built-In Kernel Threads

To see the kernel threads (also called *kernel processes*) running on your system, run the `ps` command. Names of kernel threads are surrounded by square brackets:

```
bash> ps -ef

UID          PID    PPID  C STIME TTY          TIME CMD
root            1       0  0 22:36 ?        00:00:00 init [3]
root            2       0  0 22:36 ?        00:00:00 [kthread/d]
root            3       2  0 22:36 ?        00:00:00 [ksoftirqd/0]
root            4       2  0 22:36 ?        00:00:00 [events/0]
root           38       2  0 22:36 ?        00:00:00 [pdflush]
root           39       2  0 22:36 ?        00:00:00 [pdflush]
root           29       2  0 22:36 ?        00:00:00 [khubd]
root          695       2  0 22:36 ?        00:00:00 [kjournald]
...
root         3914       2  0 22:37 ?        00:00:00 [nfsd]
root         3915       2  0 22:37 ?        00:00:00 [nfsd]
...
root         4015    3364  0 22:55 tty3     00:00:00 -bash
root         4066     4015 0 22:59 tty3     00:00:00 ps -ef
```

The *ksoftirqd/O/J* kernel thread is an aid to implement *softirqs*. Softirqs are raised by interrupt handlers to request “bottom half” processing of portions of the handler whose execution can be deferred. We take a detailed look at bottom halves and softirqs in Chapter 4, “Laying the Groundwork,” but the basic idea here is to allow as little code as possible to be present inside interrupt handlers. Having small interrupt handlers reduces interrupt-off times in the system, resulting in lower latencies. *Ksoftirqd*’s job is to ensure that a high load of softirqs neither starves the softirqs nor overwhelms the system. On *Symmetric Multi Processing* (SMP) machines where multiple thread instances can run on different processors in parallel, one instance of *ksoftirqd* is created per CPU to improve throughput (*ksoftirqd/n*, where *n* is the CPU number).

The *events/n* threads (where *n* is the CPU number) help implement *work queues*, which are another way of deferring work in the kernel. Parts of the kernel that desire deferred execution of work can either create their own work queue or make use of the default *events/n* worker thread. Work queues are also dissected in Chapter 4.

The task of the *pdflush* kernel thread is to flush out dirty pages from the page cache. The page cache buffers accesses to the disk. To improve performance, actual writes to the disk are delayed until the *pdflush* daemon writes out dirtied data to disk. This is done if the available free memory dips below a threshold, or if the page has remained dirty for a sufficiently long time. In 2.4 kernels, these two tasks were respectively performed by separate kernel threads, *bdflush* and