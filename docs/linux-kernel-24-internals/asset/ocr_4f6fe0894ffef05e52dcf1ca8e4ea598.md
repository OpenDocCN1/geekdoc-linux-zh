CPUs. This is where spinlocks are useful for.

There are three types of spinlocks: vanilla (basic), read–write and big–reader spinlocks. Read–write spinlocks should be used when there is a natural tendency of 'many readers and few writers'. Example of this is access to the list of registered filesystems (see *fs/super.c*). The list is guarded by the `file_systems_lock` read–write spinlock because one needs exclusive access only when registering/unregistering a filesystem, but any process can read the file `/proc/filesystems` or use the `sysfs(2)` system call to force a read–only scan of the `file_systems` list. This makes it sensible to use read–write spinlocks. With read–write spinlocks, one can have multiple readers at a time but only one writer and there can be no readers while there is a writer. Btw, it would be nice if new readers would not get a lock while there is a writer trying to get a lock, i.e. if Linux could correctly deal with the issue of potential writer starvation by multiple readers. This would mean that readers must be blocked while there is a writer attempting to get the lock. This is not currently the case and it is not obvious whether this should be fixed – the argument to the contrary is – readers usually take the lock for a very short time so should they really be starved while the writer takes the lock for potentially longer periods?

Big–reader spinlocks are a form of read–write spinlocks heavily optimised for very light read access, with a penalty for writes. There is a limited number of big–reader spinlocks – currently only two exist, of which one is used only on sparc64 (glocal irq) and the other is used for networking. In all other cases where the access pattern does not fit into any of these two scenarios, one should use basic spinlocks. You cannot block while holding any kind of spinlock.

Spinlocks come in three flavours: *plain*, *_irq()* and *_bh()*.

+   1.  Plain `spin_lock()/spin_unlock()`: if you know the interrupts are always disabled or if you do not race with interrupt context (e.g. from within interrupt handler), then you can use this one. It does not touch interrupt state on the current CPU.
+   2.  `spin_lock_irq()/spin_unlock_irq()`: if you know that interrupts are always enabled then you can use this version, which simply disables (on lock) and re–enables (on unlock) interrupts on the current CPU. For example, `rtc_read()` uses
+   
+       ```text
+       spin_lock_irq(&rtc_lock)  (interrupts are always enabled inside read())
+       whilst
+       rtc_interrupt() uses
+       spin_lock(&rtc_lock)  (interrupts are always disabled inside
+       interrupt handler).
+       ```
+       
+       Note that `rtc_read()` uses `spin_lock_irq()` and not the more generic `spin_lock_irqsave()` because on entry to any system call interrupts are always enabled.
+   3.  `spin_lock_irqsave()/spin_unlock_irqrestore()`: the strongest form, to be used when the interrupt state is not known, but only if interrupts matter at all, i.e. there is no point in using it if our interrupt handlers don't execute any critical code.

The reason you cannot use plain `spin_lock()` if you Race against interrupt handlers is because if you take it and then an interrupt comes in on the same CPU, it will busy wait for the lock forever: the lock holder, having been interrupted, will not continue until the interrupt handler returns.

The most common usage of a spinlock is to access a data structure shared between user process context and interrupt handlers:

```
```text
spinlock_t my_lock = SPIN_LOCK_UNLOCKED;

my_ioctl()
{
          spin_lock_irq(&my_lock);
          /* critical section */
}
```
```