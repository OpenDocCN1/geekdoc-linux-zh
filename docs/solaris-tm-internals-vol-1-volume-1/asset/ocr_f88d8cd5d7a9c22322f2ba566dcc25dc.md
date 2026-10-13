If you take a look at `/usr/include/sys/sobject.h`, you’ll find a definition for a synchronization object operations structure.

```
```c
typedef struct __sobj_ops {
        syncobj_t *sobj_type;
        kthread_t *(*sobj_owner)();
        void (*sobj_unsleep)(kthread_t *);
        void (*sobj_change_pri)(kthread_t *, pri_t, pri_t *);
} sobj_ops_t;
```
```

# Header File `<sys/sobject.h>`

This is a generic structure that is used for all types of synchronization objects supported by the operating system. Note the enumerated types in the same header file; they describe mutex locks, reader/writer locks, semaphores, condition variables, etc. Essentially, this object provides a placeholder for a few routines specific to the synchronization object that may require invocation while the kernel thread is sleeping. In the case of condition variables (our example), the sobj_ops structure is populated with the address of the cv_owner(), cv_unsleep(), and cv_change_pri() functions, with the sobj_type field set to SOBJ_CV. The address of this structure is what the kthread’s sobj_ops field is set to in the cv_block() code.

With the kthread’s wait channel and synchronization object operations pointers set appropriately, the correct sleep queue is located by use of the hashing function on the condition variable address to index into the sleepq_head array. Next, the cv_waiters field in the condition variable is incremented to reflect another kernel thread blocking on the object, and the thread state is set to TS_SLEEP. Finally, the sleepq_insert() function is called to insert the kernel thread into the correct position (based on priority) in the sleep queue. The kthread is now on a sleep queue in a TS_SLEEP state, waiting for a wakeup.

# 9.3.4 The Wakeup Mechanism

For every cv_wait() (or variant) call on a condition variable, a corresponding wakeup call uses cv_signal(), cv_broadcast(), or cv_unsleep(). In practice, cv_unsleep() is not called in current versions of Solaris. cv_signal() wakes up one thread, and cv_broadcast() wakes up all threads sleeping on the same condition variable. Here is the sequence of wakeup events.

+   - The cv_broadcast() function simply locates the address of the sleep queue by invoking the hash function on the address of the condition variable, which was passed to cv_broadcast() as an argument, clears the cv_waiters field in the condition variable (all the threads are getting a wakeup, so the condition variable should reflect zero threads waiting on the condition variable), and calls sleepq_wakeall_chan().