# # Preemption and Context Switching

Context switching, the switching from one runnable task to another, is handled by the `context_switch( )` function defined in `kernel/sched.c`. It is called by `schedule( )` when a new process has been selected to run. It does two basic jobs:

+   - Calls `switch_mm( )`, which is declared in `<asm/mmu_context.h>`, to switch the virtual memory mapping from the previous process's to that of the new process.
+   - Calls `switch_to( )`, declared in `<asm/system.h>`, to switch the processor state from the previous process's to the current's. This involves saving and restoring stack information and the processor registers and any other architecture-specific state that must be managed and restored on a per-process basis.

The kernel, however, must know when to call `schedule( )`. If it called `schedule( )` only when code explicitly did so, user-space programs could run indefinitely. Instead, the kernel provides the `need_resched` flag to signify whether a reschedule should be performed (see Table 4.1). This flag is set by `scheduler_tick( )` when a process should be preempted, and by `try_to_wake_up( )` when a process that has a higher priority than the currently running process is awakened. The kernel checks the flag, sees that it is set, and calls `schedule( )` to switch to a new process. The flag is a message to the kernel that the scheduler should be invoked as soon as possible because another process deserves to run.

Table 4.1	Functions for Accessing and Manipulating need_resched

| Function | Purpose |
| :--- | :--- |
| `set_task_need_resched( )` | Set the need_resched flag in the given process. |
| `clear_task_need_resched( )` | Clear the need_resched flag in the given process. |
| `need_resched( )` | Test the value of the need_resched flag; return true if set and false otherwise. |

Upon returning to user-space or returning from an interrupt, the `need_resched` flag is checked. If it is set, the kernel invokes the scheduler before continuing.

The flag is per-process, and not simply global, because it is faster to access a value in the process descriptor (because of the speed of current) and high probability of it being cache hot) than a global variable. Historically, the flag was global before the 2.2 kernel. In 2.2 and 2.4, the flag was an int inside the task_struct. In 2.6, it was moved into a single bit of a special flag variable inside the thread_info structure.

# ## User Preemption

User preemption occurs when the kernel is about to return to user-space, `need_resched` is set, and therefore, the scheduler is invoked. If the kernel is returning to user-space, it