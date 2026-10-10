also eliminates the hassle of using locks to protect a single integer variable from concurrent access.

The kernel also supports operators such as `set_bit()`, `clear_bit()`, and `test_and_set_bit()` to atomically engage in bit manipulations. Look at `include/asm-<your-arch>/atomic.h` for the atomic operators supported on your architecture.

# Reader–Writer Locks

Another specialized concurrency regulation mechanism is a reader–writer variant of spinlocks. If the usage of a critical section is such that separate threads either read from or write to a shared data structure, but don't do both, these locks are a natural fit. Multiple reader threads are allowed inside a critical region simultaneously. Reader spinlocks are defined as follows:

```
```c
rwlock_t myrwlock = RW_LOCK_UNLOCKED;

read_lock(&myrwlock);   /* Acquire reader lock */
/* ... Critical Region ... */
read_unlock(&myrwlock);  /* Release lock */
```
```

However, if a writer thread enters a critical section, other reader or writer threads are not allowed inside. To use writer spinlocks, you would write this:

```
```c
rwlock_t myrwlock = RW_LOCK_UNLOCKED;

write_lock(&myrwlock);    /* Acquire writer lock */
/* ... Critical Region ... */
write_unlock(&myrwlock);   /* Release lock */
```
```

Look at the IPX routing code present in `net/ipx/ipx_route.c` for a real-life example of a reader–writer spinlock. A reader–writer lock called `ipx_routes_lock` protects the IPX routing table from simultaneous access. Threads that need to look up the routing table to forward packets request reader locks. Threads that need to add or delete entries from the routing table acquire writer locks. This improves performance because there are usually far more instances of routing table lookups than routing table updates.

Like regular spinlocks, reader–writer locks also have corresponding irq variants—namely, `read_lock_irqsave()`, `read_lock_irqrestore()`, `write_lock_irqsave()`, and `write_lock_irqrestore()`. The semantics of these functions are similar to those of regular spinlocks.

Sequence locks or seqlocks, introduced in the 2.6 kernel, are reader–writer locks where writers are favored over readers. This is useful if write operations on a variable far outnumber read accesses. An example is the `jiffies_64` variable discussed earlier in this chapter. Writer threads do not wait for readers who may be inside a critical section. Because of this, reader threads may discover that their entry inside a critical section has failed and may need to retry:

```
```c
u64 get_jiffies_64(void) /* Defined in kernel/time.c */
{
 unsigned long seq;
 u64 ret;
 do {
  seq = read_seqbegin(&xtime_lock);
  ret = jiffies_64;
 } while (read_seqretry(&xtime_lock, seq));
 return ret;
}
```
```