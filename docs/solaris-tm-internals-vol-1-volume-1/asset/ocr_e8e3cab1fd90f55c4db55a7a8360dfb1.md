The generic kernel sleep queue functions are invoked indirectly through macros defined in the turnstile header file; for example, insertion of the thread on a sleep queue is done through the `TSTILE_INSERT` macro, which calls the kernel `sleepq_insert()` function.

+   - When `sleepq_insert()` completes, the kernel thread resides in the sleep queue associated with the turnstile. A kernel thread can be blocked only on one, and no more than one, synchronization object at any time, so `t_ts` will either be a NULL pointer or a pointer to one turnstile.

All that remains to be done is the priority inheritance check to determine if the thread holding the lock is at a lower (worse) priority than the thread requesting the lock (the one that was just placed on a turnstile sleep queue).

+   - The kernel `pi_willto()` function is called to check the priority of the lock owner against the thread waiting.

+   - If the owner priority is greater than the waiter priority, we do not have a priority inversion condition and the code just bails out.

+   - If the waiter priority is greater (a better priority) than the owner, we do have a priority inversion condition; then, the priority of the lock owner is set to the priority of the waiter.

+     - The `t_epri` field of the kernel thread is used for inherited priorities. A non-null value in `t_epri` results in the inherited priority of the thread being used the next time the lock owner's priority is adjusted (when we enter the dispatcher through an explicit call to the `swtch()` function).

At this point, the turnstile has been set, with the waiting thread on the turnstile’s sleep queue, and a potential priority inversion problem has been checked for a priority inheritance if needed.

+   - The kernel now enters the dispatcher through the `swtch()` function to resume scheduling threads.

+   - When a thread has finished working in the protected data region, it calls the appropriate lock exit routine (`mutex_exit()` or `rw_exit()`) to free the lock, which in turn triggers the wakeup mechanism if threads are awaiting for the lock.

+   - The release function checks the waiters field maintained in the synchronization object.
+   
+     As with mutex and RW locks, the decision on which thread to wake up or whether to wake all the waiting threads varies depending on the synchronization object and the version of the Solaris kernel. We examined what happens in each circumstance in the sections on mutex and RW locks.

The turnstile support functions used in Solaris 2.5.1 are `t_release()` for waking a single thread and `t_release_all()` for waking all the threads. Solaris 2.6 uses macros instead (e.g., `TSTILE_WAKENONE`), which have the same net effect. That is, the macros result in entering the generic sleep queue code, which has a corre-