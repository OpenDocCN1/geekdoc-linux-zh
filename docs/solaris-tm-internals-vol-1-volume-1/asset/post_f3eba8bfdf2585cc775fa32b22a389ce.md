
the code places the kernel thread on a turnstile (sleep queue) and changes the thread's state to sleep. That effectively concludes the sequence of events in `mutex_vector_enter()`.

Dropping out of `mutex_vector_enter()`, either the caller ended up with the lock in attempting to acquire, or the calling thread is on a turnstile sleep queue associated with the lock. In either case, the `lockstat(1M)` data is updated, reflecting the lock type, spin time, or sleep time as the last bit of work done in `mutex_vector_enter()`.

`lockstat(1M)` is a kernel lock statistics command that was introduced in Solaris 2.6. It provides detailed information on kernel mutex and reader/writer locks.

The algorithm described in the previous paragraphs is summarized in pseudocode below.

```
mutex_vector_enter()
    if (lock is a spin lock)
        lock_set_spl() /* enter spin-lock specific code path */
        increment cpu_syncinfo.adjustments
spin_loop:
    if (lock is not owned)
        mutex_trylock() /* try to acquire the lock */
        if (lock acquired)
            goto bottom
        else
            continue /* lock being held */
    if (lock owner is running on a processor)
        goto spin_loop
    else
        lookup turnstile for the lock
        set waiters bit
        if (lock owner is running on a processor)
            drop turnstile
            goto spin_loop
        else
            block /* the spin / sleep queue associated with the turnstile */

bottom:
    update lockstat statistics
```

When a thread has finished working in a lock-protected data area, it calls the `mutex_exit()` code to release the lock. The entry point is implemented in assembly language and handles the simple case of freeing an adaptive lock with no waiters. With no threads waiting for the lock, it's a simple matter of clearing the lock fields (`m_owner`) and returning. The C language function `mutex_vector_exit()` is entered from `mutex_exit()` for anything but the simple case.

In the case of a spin lock, the lock field is cleared and the processor is returned to the PIL level it was running at prior to entering the lock code. For adaptive locks, a waiter must be selected from the turnstile (if there is more than one waiter), have its state changed from sleeping to runnable, and be placed on a dispatch queue so it can execute and get the lock. If the thread releasing the lock was the beneficiary of priority inheritance, meaning that it had its priority improved when a calling thread with a better priority was not able to get the lock, then the thread releasing the lock will have its priority reset to what it was prior to the inheritance. Priority inheritance is discussed in “Turnstiles and Priority Inheritance” on page 89.

When an adaptive lock is released, the code clears the waiters bit in `m_owner` and calls the `turnstile` function to wake up all the waiters. Readers familiar with sleep/wakeup mechanisms of operating systems have likely heard of a particular behavior known as the *thundering herd* situation, where many threads that have been blocking for the same resource are all woken up at the same time and make a mad dash for the resource (a mutex in this case)—like a herd of large, four-legged beasts running toward the same object. System behavior tends to go from a relatively small run queue to a large run queue (all the threads have been woken up and made runnable) and high CPU utilization until a thread gets the resource, at which point a bunch of threads are sleeping again, the run queue normalizes, and CPU utilization flattens out. This is a generic behaviour that can occur on any operating system.

The wakeup mechanism used when `mutex_vector_exit()` is called in Solaris 7 may seem like an open invitation to thundering herds, but in practice it turns out not to be a problem. The main reason is that the blocking case for threads waiting for a mutex is rare; most of the time the threads will spin. If a blocking situation does arise, it typically does not reach a point where very many threads are blocked on the mutex—one of the characteristics of the thundering herd problem is resource contention resulting in a lot of sleeping threads. The kernel code segments that implement mutex locks are, by design, short and fast, so locks are not held for long. Code that requires longer lock-hold times uses a reader/writer write lock, which provides mutual exclusion semantics with a selective wakeup algorithm. There are, of course, other reasons for choosing reader/writer locks over mutex locks, the most obvious being to allow multiple readers to see the protected data.

In the following sections, we differentiate the implementation of mutexes in Solaris 2.5.1 and 2.6. As we said, Solaris 2.5.1 and 2.6 are similar to the previously described Solaris 7 behavior, especially in the area of lock acquisition (`mutex_enter()`). The more salient differences exist in the lock release algorithm, and associated wakeup behavior.

## 3.5.2.1 Solaris 2.6 Mutex Implementation Differences

First, an examination of the lock structures, as illustrated in Figure 3.6.

![](img/220ae4af07df2fe8e5be69d27f885d1b_120_0.png)

Solaris 2.6 defines all possible mutex lock types within the same structure. The spin lock is the same as for Solaris 7, with the addition of a type field. The adaptive mutex has more fields, which are fairly self-descriptive. m_owner_lock is the same as m_owner in Solaris 7; it is the lock itself, and the value represents the kthread ID of the holder when the lock is held. m_waiters stores the traversal ID of a waiting kernel thread, and m_wlock is a dispatcher lock (see “Dispatcher Locks” on page 97) that synchronizes access to the m_waiters field in the mutex. m_type describes the lock type (adaptive or spin).

The structure differences aside, the basic design and implementation of assembly and C code are essentially the same in Solaris 2.6 for lock acquisition (mutex_enter()). The differences exist in the sleep mechanism—the turnstile implementation has been improved in Solaris 7. These differences are in the interfaces and subroutines called to facilitate turnstile allocation and priority inheritance. (See “Turnstiles and Priority Inheritance” on page 89.)

On the lock release side, Solaris 2.6 implements separate routines for releasing spin locks and adaptive locks: mutex_vector_exit() and mutex_adaptive_release(), respectively. When an adaptive lock with waiting threads is released, the 2.6 code wakes only the thread with the highest priority. If multiple threads of the same (highest) priority are waiting for the same lock, the thread waiting longest is selected.

## 3.5.2.2 Solaris 2.5.1 Mutex Implementation Differences

The data structure of Solaris 2.5.1 looks very much like that of Solaris 2.6. It has another possible instantiation of an adaptive lock, m_adaptive2, which combines the lock owner and lock bits in the same field of the adaptive mutex data structure, as illustrated in Figure 3.7.

![](img/220ae4af07df2fe8e5be69d27f885d1b_121_0.png)

Figure 3.7 *Solaris 2.5.1 Adaptive Mutex*

The implementation of the mutex code in Solaris 2.5.1 is quite different from the other releases, although algorithmically the behaviour is essentially the same. Solaris 2.5.1 defines a mutex operations vector. Each element in the array is a mutex_ops structure, one structure for each type of mutex defined in Solaris 2.5.1. The array is indexed according to the lock type and the function called. The design is such that specific functions handle lock operations for each of the different types of mutex locks. Common entry points into the mutex code pass control to the lock-specific functions by switching through the operations array, as determined by the lock type and function offset. This is illustrated in Figure 3.8.

![](img/220ae4af07df2fe8e5be69d27f885d1b_121_1.png)

Figure 3.8 *Solaris 2.5.1 Mutex Operations Vectoring*

Solaris 2.5.1 implements a wakeup method similar to that of Solaris 2.6 when an adaptive mutex is released with waiting threads; the highest priority waiter is
