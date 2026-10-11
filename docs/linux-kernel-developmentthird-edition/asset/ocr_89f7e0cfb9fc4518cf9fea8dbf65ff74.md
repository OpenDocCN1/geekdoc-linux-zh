A dynamically created completion variable is initialized via `init_completion()`. On a given completion variable, the tasks that want to wait call `wait_for_completion()`. After the event has occurred, calling `complete()` signals all waiting tasks to wake up. Table 10.9 has a listing of the completion variable methods.

Table 10.9  Completion Variable Methods

| Method | Description |
| :----- | :--------- |
| `init_completion(struct completion *)` | Initializes the given dynamically created Completion variable |
| `wait_for_completion(struct completion *)` | Waits for the given completion variable to be signaled |
| `complete(struct completion *)` | Signals any waiting tasks to wake up |

For sample usages of completion variables, see `kernel/sched.c` and `kernel/fork.c`. A common usage is to have a completion variable dynamically created as a member of a data structure. Kernel code waiting for the initialization of the data structure calls `wait_for_completion()`. When the initialization is complete, the waiting tasks are awakened via a call to `completion()`.

# BKL: The Big Kernel Lock

Welcome to the redheaded stepchild of the kernel. The Big Kernel Lock (BKL) is a global spin lock that was created to ease the transition from Linux's original SMP implementation to fine-grained locking. The BKL has some interesting properties:

+   - You can sleep while holding the BKL. The lock is automatically dropped when the task is unscheduled and reacquired when the task is rescheduled. Of course, this does not mean it is *always safe* to sleep while holding the BKL, merely that you *can* and you will not deadlock.
+   - The BKL is a recursive lock. A single process can acquire the lock multiple times and not deadlock, as it would with a spin lock.
+   - You can use the BKL only in process context. Unlike spin locks, you cannot acquire the BKL in interrupt context.
+   - New users of the BKL are forbidden. With every kernel release, fewer and fewer drivers and subsystems rely on the BKL.

These features helped ease the transition from kernel version 2.0 to 2.2. When SMP support was introduced in kernel version 2.0, only one task could be in the kernel at a time. Of course, now the kernel is quite finely threaded, we have come a long way. A goal of 2.2 was to allow multiple processors to execute in the kernel concurrently. The BKL