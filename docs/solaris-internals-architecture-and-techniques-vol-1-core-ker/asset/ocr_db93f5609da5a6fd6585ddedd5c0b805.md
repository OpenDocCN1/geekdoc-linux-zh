# 88

# Kernel Synchronization Primitives

able when the code was first entered, the holdcnt field is set to -1 (the write lock), the owner field is set to the kernel thread ID of the caller, and the mutex is released (we grabbed that early on when the write code path was entered).

+   * An RW lock is released by a call to rw_exit(), which acquires the lock when the function is entered. If a writer is releasing the lock, the owner field and holdcnt fields in the lock are cleared and we check for waiters.
* If there are threads sleeping on the lock, the turnstile is retrieved and the priority of the caller is reset if it was the beneficiary of priority inheritance.
* If a writer is writing (writanted is set), the writer is woken up. If there is more than one writer, the highest-priority writer gets the wakeup. With no writers waiting, all the readers are woken up.

This always-favor-the-writer policy was changed in Solaris 2.6 and Solaris 7. For writers, only one thread gets the wakeup, whereas for readers, all waiting readers are woken up. This makes sense because with no writers, all the readers can get the lock (that's how RW works, by design). Only one writer at a time can have the lock, so it only makes sense to wake one reader.

+   * If a reader is releasing the lock, the holdcnt field is decremented (one less reader) and writers are again favored over readers if both exist. The code first checks to ensure that no other readers are holding the lock (holdcnt is 0), as it's certainly possible for other readers to still have a lock when one thread is releasing it.

Solaris 2.5.1 and earlier releases use a different wakeup policy, which was designed as an "always favor writers" policy. The code path when a thread was releasing an RW lock would basically wake up writers first and always grant the lock to a waiting writer, regardless of whether a reader or writer was releasing the lock or regardless of the priority of the readers versus the writers both waiting on the lock.

The final point to make here is that not only did the policy change in Solaris 2.6 and 7 with respect to the wakeup selection, but so did the method with threads coming off the turnstile acquire the lock. In Solaris 2.5.1, the threads, woken up are scheduled, executed and resumed with rw_enter() to get the lock. Solaris 2.6 and Solaris 7 implement a direct handoff mechanism, where threads are given ownership of the lock before sleep queue removal and state change.

# 3.7 Turnstiles and Priority Inheritance

A turnstile is a data abstraction that encapsulates sleep queues and priority inheritance information associated with mutex locks and reader/writer locks. The mutex