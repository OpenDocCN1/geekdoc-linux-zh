# 2.3 Locking—Atomic Operations

spin_unlock(spinlock_t *my_spinlock) releases an acquired spinlock.
spin_unlock_irqrestore(spinlock_t *my_spinlock, unsigned long flags) releases the specified spinlock and allows interrupts, if there were any activated when the CPU status register was saved to the variable; otherwise it does not allow interrupts.
spin_unlock_irq(spinlock_t *my_spinlock) releases the specified spinlock and allows interrupts.

spin_unlock_bh(spinlock_t *my_spinlock) also releases the lock and allows-immediate processing of bottom halves.

The functions introduced above can be used to protect critical sections to avoid undesired side effects on the critical sections from occurring. The example shown in Figures 2-2 and 2-4 can be used as follows, where the use of a spinlock prevents undesired side effects:

```
#include <linux/spinlock.h>
spinlock_t *my_spinlock = SPIN_LOCK_UNLOCKED;
// Activity A
spin_lock(&my_spinlock);
skb_a->next = queue->next;
queue->next = skb_a;
spin_unlock(&my_spinlock);
...
// Activity B
spin_lock(&my_spinlock);
skb_b->next = queue->next;
queue->next = skb_b;
spin_unlock(&my_spinlock);
```

The following useful functions are available to handle spinlocks, in addition to the methods used to set and release spinlocks:

spin_is_locked(spinlock_t *my_lock) polls the current status of the lock, without changing it. For a set lock, a value unequal to zero is returned; for a free lock, zero is returned.
spin_trylock(spinlock_t *my_lock) sets the spinlock, if it is currently unoccupied; otherwise, the functions immediately returns a value unequal to zero.
spin_unlock_wait(spinlock_t *my_lock) waits for the lock to be released, if the lock is occupied, but the lock is not set.

# 2.3.3 Read–Write Spinlocks

Spinlocks represent a simple and useful element to protect parallel operations on common data structures from undesired side effects. However, they slow down the progress of activities, because these activities have to wait actively for locks to be released. Active