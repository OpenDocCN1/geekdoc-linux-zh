
# Mutex Locks

The algorithm described in the previous paragraphs is summarized in pseudocode below.

```
mutex_vector_enter(){
    if (lock is a spin lock)
        lock_set_spi() /* enter spin-lock specific code path */
        increment cpu_sysinfo.ademters.
    spin_loop:
        if (lock is not owned)
            mutex_trylock() /* try to acquire the lock */
            if (lock is acquired)
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
            block /* the sleep queue associated with the turnstile */
bottom:
    updatelockstatistics
```
```

When a thread has finished working in a lock-protected data area, it calls the mutex_exit() to release the lock. The entry point is implemented in assembly and handles the simple case of freeing an adaptive lock with no waiters. With no threads waiting the lock, it is a simple matter of clearing the lock fields (m owner) and returning. The C language function mutex_vector_exit() is entered from mutex_exit() for anything but the simple case.

In the case of a spin lock, the lock is cleared and the processor is returned to the PIL level it was running at prior to entering the lock code. For adaptive locks, a waiter must be selected from the turnstile (if there is more than one waiter), its state changed from sleeping to running, and placed on a patch queue that it can execute and get the lock. If the thread releasing the lock was the beneficiary of priority inheritance, meaning that it had its priority improved when a calling thread with a better priority was not able to get the lock then the thread releasing the lock will have its priority reset to what it was prior to the inheritance. Priority inheritance is discussed in "Turnstiles and Priority Inheritance" on page 88.

When an adaptive lock is released, the code clears all the waiters in m owner and calls the turnstile to wake up all the waiters. Readers familiar with sleep/wakeup mechanisms of operating systems have likely heard of a behavior known as the thundering herd problem, a situation where many threads have been blocking for the same resource are all woken up at the same time and make a dash for the resource (a mutex in this case)—like a herd of large beasts running toward the same object. System behavior tends to go from a relatively small queue to a large run queue (all the threads we woken up and made runnable) and high CPU utilization until a thread gets the resource, at which point a bunch of threads are sleeping again, the run queue normalizes, and CPU utilization flattens out. This is a generic behavior that can occur on any operating system.

The wakeup mechanism used when mutex_vector_exit() is called in Solaris 7 may seem like an open invitation to thundering herds, but in practice it turns not to be a problem. The main reason is that the blocking for threads waiting for a mutex is rare; most of the threads will spin. If a blocking situation do arise, it typically does not reach a point where many threads are blocked on the mutex—one of the characteristics of the thundering herd problem is resource contention resulting in a lot of sleeping threads. The kernel code segments that implement mutex locks are, by design, short and fast, so locks are not held for long. That code requires longer lock-hold times uses a reader/writer write lock, which provides mutual exclusion semantics with a selective wakeup algorithm. There are, of course, other reasons for choosing reader/writer locks over mutex locks, the most obvious being to allow multiple readers to see the protected data.

In the following sections, we differentiate the implementation of mutexes in Solaris 2.5.1 and 2.6. As we said, Solaris 2.5.1 are similar to the previously described Solaris 7 behavior, especially in the area of lock acquisition (mutex_enter()). The more salient differences exist in the lock release algorithm, and associated wakeup behavior.

## 3.5.2.1 Solaris 2.6 Mutex Implementation Differences

First, an examination of the lock structures, as illustrated in Figure 3.6.

![](img/a86367b95bf21add858c99948ac951c6_123_0.png)

Figure 3.6 Solaris 2.6 Mutex

Solaris 2.6 defines all possible mutex lock types within the same structure. The spin lock is the same as for Solaris 7, with the addition of a type field. The adaptive mutex has more fields, which are fairly self-descriptive. m owner lock is the same as m owner in Solaris 7; it is the lock itself, and the value represents the thread ID of holder when the lock is held. m waiters stores the turnstile ID of a waiting kernel thread, and m wlock is a dispatcher lock (see "Dispatcher Locks" on page 96) that synchronizes access to the m waiters field in the mutex. m_type describes the lock type (adaptive or spin).

The structure differs also, the basic algorithm and implementation assembly and C are essentially the same in Solaris 2.6 for lock acquisition (mutex_enter()). The difference exists in the sleep mechanism–turnstile implementation has been improved in Solaris 7. These differences are in the interfaces and subroutines to facilitate turnstile allocation and priority inheritance. (See "Turnst and Priority Inheritance" on page 88).

On the lock release side, Solaris 2.6 implements routines for releasing spin locks and adaptive locks: mutex_vector_exit() and mutex_adaptive_release(), respectively. When an adaptive lock with waiting threads is released, the 2.6 code wakes only the thread with the highest priority. If multiple threads of the same (high-est) priority are waiting for the same lock, the thread waiting longest is selected.

## 3.5.2.2 Solaris 2.5.1 Mutex Implementation Differences

The data structure of Solaris 2.5.1 looks very much like that of Solaris 2.6. It has another possible instantiation of an adaptive lock, m_adaptive2, which combines the lock owner and lock bits in the same field of the adaptive mutex data structure, as illustrated in Figure 3.7.

![](img/a86367b95bf21add858c99948ac951c6_124_0.png)

Figure 3.7 Solaris 2.5.1 Adaptive Mutex

The implementation of the mutex code in Solaris 2.5.1 is quite different from the other releases, although algorithmically the behavior is essentially the same. Solaris 2.5.1 defines a mutex operations vector array. Each element in the array is a mutex_ops structure, one for each type of mutex defined in Solaris 2.5.1. The array is indexed according to the lock type and the function call. The design is such that specific functions handle lock operations for each of the different types of mutex locks. Common entry points into the mutex code pass control to the lock-specific functions by switching through the operations, as determined by the lock type and function offset. This is illustrated in Figure 3.8.

![](img/a86367b95bf21add858c99948ac951c6_125_0.png)

Figure 3.8 Solaris 2.5.1 Mutex Operations Vectoring

Solaris 2.5.1 implements a wakeup method similar to that of Solaris 2.6 when an adaptive mutex is released with waiting threads; the highest priority waiter is selected for wakeup and should get ownership of the lock. It is, of course, possible for another thread to come along and acquire the lock before the wakeup is completed, the newly awakened thread is not guaranteed to get the lock.

Finally, note that the lockstat utility was first implemented in Solaris 2.6 and thus is not part of the 2.5.1 release.

## 3.5.2.3 Why the Mutex Changes in Solaris 7

We wanted to avoid getting mired in subtle differences that would not add real value to the text, but at the same time we want to point out relevant differences in implementations. The subsections describing the implementation differences across releases serve two purposes. The first and most obvious is completeness, to meet our goal of covering multiple Solaris releases. Second, and even more compelling, we see the evolution and refinements that have gone into the lock code from release to release. The actual lock manipulation and turnstiles code follow the same trend shown in the data structures—scaled down, leaner, and more efficient.
