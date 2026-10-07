
+   In Solaris 7, sleep_wakeall_chan() traverses the linked list of kernel threads waiting on that particular condition variable and, for each kthread, calls sleep_pq_unlink(). sleep_pq_unlink() removes the kthread from the sleep queue linked list, adjusts the pointers (t_prifront, t_prback) and returns to sleep_wakeall_chan().

+   On the return to sleep_wakeall_chan(), the kthread's t_chan and t_sobj_ops fields are cleared, and the scheduling-class-specific wakeup code is called.

For TS/IA threads, the code is ts_wakeup(); for RT threads, it is rt_wakeup(). In Solaris 2.5 and Solaris 2.6, the queue is a singly linked list, with the t_link pointer in the kthread.

Solaris 2.5 and Solaris 2.6 do not have a sleep_unlink() function, so sleep_wakeall_chan() removes each thread from the list and sets the thread's t_link, t_chan, and t_sobj_ops fields to NULL.

+   cv_signal() locates the correct index in the sleep_head array by hashing on the address of the condition variable, decrements the cv_waiters field in the condition variable by 1, since only one thread is getting a wakeup, and calls sleep_wakeone_chan().

+   ts_wakeup() puts the kernel thread back on a dispatch queue so it can be executed on a processor.

Threads that have a kernel mode priority (as indicated by the TSPRI flag in the class-specific data structure, which is set in ts_sleep() if a SYS priority is assigned) are placed on the front of the appropriate dispatch queue. IA class threads will also result in setfrontdq() being called; otherwise, setbackdq() is called to place the kernel thread at the back of the dispatch queue.

+   Threads that are not at a SYS priority are tested to see if they've waited longer for a shot at getting scheduled than the time set in the ts_maxwait field in the dispatch table for thread's priority level.

If the thread has been waiting an inorder time to run (if wait > dispatch_table[priority].diswait), then the thread's priority is recalculated, using the ts_slpret value from the dispatch table. This is essentially the same logic used in ts_sleep() and gives a priority boost to threads that have spent an amount of time on the sleep queue.

It is in the dispatcher queue insertion code (setfrontdq(), setbackdq()) that the thread is switched from SLEEP to TS_RUN. It's also in functions that we determine if the thread we just placed on a queue is of higher priority than the currently running thread and if so, a preemption. At this point, the kthread has been woken up and is sitting on a dispatch queue, ready to get text-switched onto a processor when the dispatcher swch() function runs and the newly inserted thread is selected for execution.

# Scheduler Activations

## 9.4 Scheduler Activations

We made several references to scheduler activations in the preceding text and highlighted the preemption control feature in the thread priority descriptions. Scheduler activations were added to the kernel dispatcher of Solaris 2.6 to address several deficiencies in the two-level threads architecture of Solaris and to provide a facility for short-term preemption control by a process. (This section and any previous references to scheduler activations do not apply to Solaris 2.5.1; they apply only to Solaris 2.6 and Solaris 7).

The two levels in the design refer to user-level threads and the underlying kthread/LWP. We use the term LWP from this point forward when discussing the kernel level, and we use threads to refer to a user thread created from the threads library. User-level threads are scheduled within the framework of the threads library—the user threads actually participate in their own scheduling through preemption points and internal threads routines. User threads are, by design, not visible to the kernel. The priority of a user thread has no bearing on the scheduling or priority of an LWP linked to the thread for execution.

Prior to Solaris 2.6, there was no facility for communication between the threads scheduler and the kernel dispatcher (see Figure 9.16), and thus no correlation between the priority of a user thread and the priority of the underlying LWP. This problem could be circumvented to some extent by the use of bound threads, where every user thread was bound to a LWP, and priority control facilities (pcnt(1M)) managed execution priorities at the LWP level.

![](img/a86367b95bf21add858c99948ac951c_452_0.png)

Figure 9.16 Two-Level Threads Model

Other problems existed in the area of synchronization primitives used by threaded programs. At the user levels, the use of mutex locks and other synchronization mechanisms were prone to priority inversion problems. We described how priority inheritance addressed this problem in the kernel for kernel synchronization primitives. There was no means by which an inheritance scheme could be implemented at the user levels, since the priority information of the LWP was not readily available to the library code. This lack of LWP state information at the threads library level made the implementation of adaptive locks impossible.

Finally, keeping a sufficient pool of LWPs available to a threaded user would have the resource needed to execute when they were not easily solved. Solaris 2.5.1 and previous releases provide a SIGWAITING signal generated by the kernel when all the LWPs in a process are blocked and a special signal handler creates more LWPs for the process. In Solaris 2.5.1 (and previous releases), sigwaiting creates more LWPs for the process.

### 9.4.1 User Activation

Scheduler activations provide a facility for communication between the user-level threads and the kernel. This is achieved through the use of doors, which allow a user-level thread to call a function in the kernel and vice-versa. The door mechanism is a fast and efficient way to pass messages between user and kernel space.

The kernel uses scheduler activations to manage the scheduling of threads. When a thread blocks, the kernel sends a scheduler activation to the user-level thread library, which then decides which thread to run. When a thread is unblocked, the kernel sends another scheduler activation to the library to wake the thread.

### 9.4.2 LWP Pool Activation

LWP pool activation refers to the fast and efficient replenishment of LWPs to a threaded process that has all LWPs in a blocking or sleeping state, potentially leaving runnable threads without an execution resource. This condition is tested for and handled when the condition variables are entered to put an LWP/kthread to sleep.
