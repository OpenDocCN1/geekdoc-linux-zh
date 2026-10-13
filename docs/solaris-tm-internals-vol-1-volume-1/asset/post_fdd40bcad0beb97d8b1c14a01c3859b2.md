
- The mutex is released and the code returns to the caller.
- If a writer is holding the lock or a write lock request is pending, the thread is set to block. The mutex is released, and the `cpu_sysinfo.rw_rdfails` counter is incremented.

  You can examine this counter with `mpstat(1M)`. The `sw` column displays the sum of the failed reader and failed writer lock attempts.
- The code tests the lock’s waiters field, which contains the ID of a turnstile if there are already waiters. No waiters means we must allocate a turnstile from the free pool; one or more waiters means we just need to locate the turnstile holding the other waiters and put the lock on that sleep queue.
- Before putting the thread on the turnstile and changing the thread state to sleep, the code tests the lock again (it may have been released by now). If it’s available, the path previously described for an available lock is taken. Otherwise, the turnstile block code is called to place the thread on the sleep queue.
- The priority inversion condition is tested for with the `pi_willto()` code, and the `swtch()` function is called for entry to the dispatcher.

The code flow for a writer lock request is similar.

- If the lock is not available, the `writewanted` bit is set.
- An existing turnstile is fetched if there are already waiters; otherwise, a new one is allocated, and the thread is placed on a sleep queue after the lock is rechecked to make sure it’s still unavailable. If it is available or was available when the code was first entered, the `holdcnt` field is set to −1 (the write lock), the owner field is set to the kernel thread ID of the caller, and the mutex is released (we grabbed that early on when the write code path was entered).
- An RW lock is released by a call to `rw_exit()`, which acquires the mutex when the function is entered. If a writer is releasing the lock, the owner and `holdcnt` fields in the lock are cleared and we check for any waiters.
- If there are threads sleeping on the lock, the turnstile is retrieved and the priority of the caller is reset if it was the beneficiary of priority inheritance.
- If a writer is waiting (`writewanted` is set), the writer thread is woken up. If there is more than one writer, the highest-priority writer gets the wakeup. Otherwise, with no writers waiting, all the readers are woken up.

  This always-favor-the-writer policy was changed in Solaris 2.6 and Solaris 7. For writers, only one thread gets the wakeup, whereas for readers, all waiting readers are woken up. This makes sense because with no writers, all the readers can get the lock (that’s how RW locks work, by design). Only one writer at a time can have the lock, so it only makes sense to wake one writer.
- If a reader is releasing the lock, the `holdcnt` field is decremented (one less reader) and writers are again favored for wakeup over readers if both exist. The code first checks to ensure that no other readers are holding the lock (`holdcnt` is 0), as it’s certainly possible for other readers to still have a read lock when one thread is releasing it.

Solaris 2.5.1 and earlier releases use a different wakeup policy, which was designed as an “always favor writers” policy. The code path when a thread was releasing a RW lock would basically look for waiting writers first and always grant the lock to a waiting writer, regardless of whether a reader or writer was releasing the lock and regardless of the priority of the readers versus the writers if both were waiting on the lock.

The final point to make here is that not only did the policy change in Solaris 2.6 and 7 with respect to the wakeup selection, but so did the method with which threads coming off the turnstile acquire the lock. In Solaris 2.5.1, the threads, once woken up, are scheduled, executed, and resumed in the `rw_enter()` to get the lock. Solaris 2.6 and Solaris 7 implement a direct handoff mechanism, where threads are given ownership of the lock before sleep queue removal and state change.

## 3.7 Turnstiles and Priority Inheritance

A turnstile is a data abstraction that encapsulates sleep queues and priority inheritance information associated with mutex locks and reader/writer locks. The mutex and RW lock code use a turnstile when a kernel thread needs to block on a requested lock. The sleep queues implemented for other resource waits do not provide an elegant method of dealing with the priority inversion problem through priority inheritance. Turnstiles were created to address that problem.

Priority inversion describes a scenario in which a higher-priority thread is unable to run because a lower priority thread is holding a resource it needs, such as a lock. The Solaris kernel addresses the priority inversion problem in its turnstile implementation, providing a *priority inheritance* mechanism, where the higher-priority thread can will its priority to the lower-priority thread holding the resource it requires. The beneficiary of the inheritance, the thread holding the resource, will now have a higher scheduling priority and thus get scheduled to run sooner so it can finish its work and release the resource, at which point the original priority is returned to the thread.

In this section, we assume you have some level of knowledge of kernel thread priorities, which are covered in Chapter 6, “The Kernel Dispatcher.” Because turnstiles and priority inheritance are an integral part of the implementation of mutex and RW locks, we thought it best to discuss them here rather than later. For this discussion, it is important to be aware of these points:

- The Solaris kernel assigns a global priority to kernel threads, based on the scheduling class they belong to.
- Kernel threads in the timeshare and interactive scheduling classes will have their priorities adjusted over time, based on three things: the amount of time the threads spend running on a processor, sleep time (blocking), and the case when they are preempted. Threads in the real-time class are fixed priority; the priorities are never changed regardless of runtime or sleep time unless explicitly changed through programming interfaces or commands.

The Solaris kernel implements sleep queues for the placement of kernel threads blocking on (waiting for) a resource or event. For most resource waits, such as those for a disk or network I/O, sleep queues, in conjunction with condition variables, manage the systemwide queue of sleeping threads. These sleep queues are covered in Chapter 6, “The Kernel Dispatcher.” This set of sleep queues is separate and distinct from turnstile sleep queues.

The implementation of turnstiles was changed substantially in Solaris 7, although the underlying premise and concepts are the same. We will begin with a look at the turnstile implementation in Solaris 7.

### 3.7.1 Solaris 7 Turnstiles

Figure 3.12 illustrates the Solaris 7 turnstiles. The rewrite of turnstiles in Solaris 7 resulted in a significant amount of code being removed, and some new, more efficient functions were developed.

Turnstiles are maintained in a systemwide hash table, `turnstile_table[]`, which is an array of `turnstile_chain` structures. Each entry in the array (each `turnstile_chain` structure) is the beginning of a linked list of turnstiles. The array is indexed via a hash function on the address of the synchronization object (the mutex or reader/writer lock), so locks that hash to the same array location will have a turnstile on the same linked list. The `turnstile_table[]` array is statically initialized at boot time.

![](img/220ae4af07df2fe8e5be69d27f885d1b_132_0.png)

**Figure 3.12** *Solaris 7 Turnstiles*

Each entry in the array has its own lock, `tc_lock`, so chains can be traversed concurrently. The turnstile itself has a different lock; each chain has an active list (`ts_next`) and a free list (`ts_free`). There are also a count of threads waiting on the sync object (`ts_waiters`), a pointer to the synchronization object (`ts_sobj`), a thread pointer linking to a kernel thread that had a priority boost through priority inheritance, and the sleep queues. Each turnstile has two sleep queues, one for readers and one for writers. (Threads blocking on a read/write lock are maintained on separate sleep queues.) The priority inheritance data is integrated into the turnstile, as opposed to being maintained in a separate data structure (which is what Solaris 2.6 and 2.5.1 do).

In Solaris 7, every kernel thread is born with an attached turnstile. That is, when a kernel thread is created by the kernel `thread_create()` routine, a turnstile is allocated for the kthread and linked to the kthread’s `t_ts` pointer. A kthread can block on only one lock at a time, so one turnstile is sufficient.

We know from the previous sections on mutex and RW locks that a turnstile is required if a thread needs to block on a synchronization object. Solaris 7 calls `turnstile_lookup()` to look up the turnstile for the synchronization object in the `turnstile_table[]`. Since we index the array by hashing on the address of the lock, if a turnstile already exists (there are already waiters), then we get the correct turnstile. If no threads are currently waiting for the lock, `turnstile_lookup()` simply returns a null value. If the blocking code must be called (recall from the previous sections that subsequent tests are made on lock availability before it is determined that the kthread must block), then
