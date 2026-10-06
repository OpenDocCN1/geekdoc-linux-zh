# 2.3 Locking—Atomic Operations 19

they are normally implemented by variables, which manage the status of locks (i.e., they remember how many activities there are currently in a critical section.

This means that, first of all, the status of locking variables has to be checked and then set, before entry into a critical section. In a processor, this generally adds up to two machine commands to be executed, one after the other. It can now happen that a situation like the one described can occur exactly between these two machine commands (i.e., the activity is interrupted and another activity of the kernel changes the state of variables). For this reason, atomic test and set machine commands are required to support critical sections. Modern processors support these commands and many more (It would go beyond the scope of this book to describe each one in detail).

Some of these atomic operations, as well as useful operations to manipulate single bits or integer variables, which are often useful to handle protocol headers, are listed in the following examples.Another benefit of these atomic operations is that no additional locks are required for their operations. They run in single (very fast) machine command.

```
test_and_set_bit(nr, void *addr) sets the bit with number nr in the unsigned long variables of the pointer addr.The previous value of the bit is returned as value.
test_clear_bit(nr, void *addr) deletes the specified bit and also returns that bit's previous value.
test_change_bit(nr, void *addr) inverts bit nr and resets it to its original value.
set_bit(nr, void *addr) sets the bit with number nr at address addr.
clear_bit(nr, void *addr) deletes the specified bit.
change_bit(nr, void *addr) inverts bit nr.
test_bit(nr, void *addr) returns the current values of the bits.
```

# Integer Operations

Operations can also be run atomically on integers. To do this, however you have to use the atomic_t data type, which corresponds to the int data type in all supported architectures.

+   * atomic_set(atomic_t *var, int i) sets the value to i.
* atomic_read(atomic_t *var) reads the variables.
* atomic_add_sub(int i, atomic_t *var) adds or subtracts.
* atomic_inc/atomic_dec(atomic_t *var) adds or subtracts in increments of 1.
* atomic_..._test(...):see Bit Operations.

All of these operations are implemented by one single machine command. However, critical sections cannot be reduced to one single command, but consist of several operations. Using the atomic bit or integer operations introduced in this section, you can implement locks to protect larger ranges for exclusive access. These spinlocks and semaphores are introduced in the following subsections.