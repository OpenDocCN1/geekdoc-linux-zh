# 20 Chapter 2 The Kernel Structure

# 2.3.2 Spinlocks

Spinlocks are also busy wait locks because of the way they work. When a critical section begins and the lock—in this case the spinlock—has already been set, then the processor waits actively until the lock is removed. This means that the processor continues locking the variable in a continuous loop until the locking variable is released by the locking activity.

Though this wastes computing time because the processor seems to continually test the locking variable "meaninglessly," it can prove more effective to continually test the lock for a brief moment and then it can enter the critical section upon its release rather than calling the scheduler and grant the computing time to another activity. A lot of time can elapse until the waiting activity will get its turn after the lock's release. In addition, a change of activity caused by calling the scheduler could eventually take more computing time than a brief wait in the busy wait loop. For we observe the principle that spinlocks represent the best locking method for small critical points (i.e., with short locking times).

In the Linux kernel, spinlocks are implemented by the variable spinlock_t, which consists of a single integer locking variable. To use a spinlock, you have to create and initialize the spinlock_t structure, in the following example:

```
#include <linux/spinlock.h>
spinlock_t my_spinlock = SPIN_LOCK_UNLOCKED;
/* You can also use spinlock_init(&my_spinlock) instead of an assignment in the definition. */
```

You can now use a set of different functions to request, set or release spinlocks. Each of these functions is especially suited for certain application cases. First, let's look at how we set a spinlock:

+   - spin_lock(spinlock_t *my_spinlock) tries to set the spinlock my_spinlock. If it is not free, we have to wait or test until it is released. The free spinlock is then returned immediately.
- spin_lock_irsave(spinlock_t *my_spinlock, unsigned long flags) works similarly to spin_lock(), but it additionally prevents interrupts and stores the current value of the CPU status register in the variable flags.
- spin_lock_irq(spinlock_t *my_spinlock) works similarly to spin_lock_irq(), which does not store the value of the CPU status register. It assumes that interrupts are already being prevented.
- Similar to spin_lock(), spin_lock_bh(*my_spinlock) tries to set the lock, but it prevents bottom halves (see Section 2.2.5) from running at the same time.

The following functions can be used to mark the end of the critical section, depending on the application. Each of them releases an occupied spinlock.