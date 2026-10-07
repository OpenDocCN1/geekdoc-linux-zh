The simple cases for lock acquisition through rw_enter() are the circumstances listed below:

+   - The write lock is wanted and is available.

+   - The read lock is wanted, the write lock is not held, and no threads are waiting for the write lock (rwrant is clear).

The acquisition of the write lock results in bit 2 getting set and the kernel thread pointer loaded in the upper bits. For a reader, the hold count (upper bits) is incremented. Conditions where the write lock is being held, causing a lock request to fail, or where a thread is waiting for a write lock, causing a read lock request to fail, result in a call to the rw_enter_sleep() function.

Important to note that the rw_enter() code sets a flag in the kernel thread used by the dispatcher code when establishing a thread's priority priority to preemption or changing state. We cover this in Chapter 6,"Kernel Memory". Briefly, the kernel thread structure contains a t_kpri_req (kernel priority request) field that is checked in the dispatcher code when a thread is about to be preempted (forced off the processor or when it is executing a higher priority thread becomes runnable) or when the thread is about to have its state changed. If the t_kpri_req flag is set, the dispatcher assigns a priority to the thread, such that when the thread resumes execution, it runs before threads in scheduling classes of lower priority (timeshare and interactive classes). More succively, the priority of a thread holding a write lock is set to a better priority to minimize the time of the lock.

Getting back to the rw_enter() flow: If the code falls through the simple case, we need to set up the kernel thread requesting the RW lock to block.

+   - rw_enter_sleep() establishes whether the calling thread is requesting a read or write lock and does another test to see if the lock is available. If it is, the caller gets the lock, the lockstat(1M) statistics are updated, and the code returns returns. If the lock is not available, the turnstile code is called to look up a turnstile in preparation for putting the calling thread to sleep.

+   - With a turnstile now available, another test is made on the lock availability. (Today's fast processors, and especially multiprocessor systems, it's quite possible that the thread holding the lock finished what it was doing and the lock became still held, the thread is set to a sleep state and on a turnstile.

+   - The RW lock structure will have the wait bit set for a reader waiting (forced to block because a writer has the lock) or the rwrant bit to signify that a thread wanting the write lock is blocking.

+   - The cpu_sysinfo structure for the processor maintains two counters for failures to get a read lock or write lock on the first pass: rw_rdfails and rw_wrfails. The appropriate counter is incremented just prior to the turnstile call; this action places the thread on a turnstile sleep queue.