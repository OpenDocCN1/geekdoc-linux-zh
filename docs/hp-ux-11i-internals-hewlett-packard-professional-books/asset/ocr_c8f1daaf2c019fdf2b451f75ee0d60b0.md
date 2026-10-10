seconds, the system will panic. Semaphores can be held indefinitely.
* If the system tries to get a spinlock and finds it already locked, it will busy wait. It will do no other work until the spinlock is free. If it tries to get a semaphore and finds it locked, it can put the current process to sleep and switch to another process.
* A process can sleep while holding a semaphore. Processes that are holding spinlocks are not allowed to sleep.

Let’s look into the details of spinlocks first.

# Spinlocks

Listing 12.3 is the structure that represents a spinlock.

# **Listing 12.3 Spinlock structure**

```
```
struct lock {
volatile uintptr_t sl_lock;
volatile uintptr_t sl_owner;
char *sl_name_ptr;
volatile uint16_t sl_flag;
volatile uint16_t sl_next_cpu;
uint32_t sl_arena_alloc_flag;
};
```
```

This structure is also typed as lock_t, you'll see lock_t used more commonly than struct lock.

The first word in the structure, sl_lock, is the one that indicates whether or not the lock is currently locked. If sl_lock is zero, then the spinlock is locked. If it is nonzero, it is not locked. When it is not locked, this field should contain the per-processor data pointer (PPDP) of the processor that had it last. (Remember that the PPDP is also the address of the mpinfo structure for that processor)

The second field, sl_owner, does the opposite of sl_lock. When the spinlock is locked, this field contains the PPDP of the owner. When it is unlocked, it contains zero.

sl_name_ptr is a pointer to a character string containing the name of the spinlock. Each spinlock is given a name when it is allocated. Prior to HP-UX release 11.1, this pointer had to be left-shifted two bits before it was used. Starting with 11.1, the pointer can be used as is.

You might wonder why we use zero to indicate locked. It seems more logical that a zero would be unlocked and nonzero would be locked. The answer comes from the PA-RISC architecture. In order to implement any kind of locking mechanism, the hardware must provide an atomic operation for testing a value and setting the value. By atomic, we mean that it is a single operation—the test and the set must both happen. The instruction can't be interrupted partway through. Many hardware architectures implement a Test and Set instruction. On PA-RISC this operation is done with the Load and Clear Word (LDCW) instruction.