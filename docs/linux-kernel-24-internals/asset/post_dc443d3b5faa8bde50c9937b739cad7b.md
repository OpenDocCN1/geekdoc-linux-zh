
The tasks are hashed by their pid value and the above hashing function is supposed to distribute the elements uniformly in their domain (0 to PID_MAX-1). The hashtable is used to quickly find a task by given pid, using `find_task_pid()` inline from `include/linux/sched.h`:

```c
static inline struct task_struct *find_task_by_pid(int pid)
{
  struct task_struct *p, **htable = &pidhash[pid_hashfn(pid)];
  for (p = *htable; p && p->pid != pid; p = p->pidhash_next)
    ;
  return p;
}
```

The tasks on each hashlist (i.e. hashed to the same value) are linked by `p->pidhash_next/pidhash_prev` which are used by `hash_pid()` and `unhash_pid()` to insert and remove a given process into the hashtable. These are done under protection of the read–write spinlock called `tasklist_lock` taken for **WRITE**.

The circular doubly-linked list that uses `p->next_task/prev_task` is maintained so that one could go through all tasks on the system easily. This is achieved by the `for_each_task()` macro from `include/linux/sched.h`:

```c
#define for_each_task(p) \
  for (p = &init_task ; (p = p->next_task) != &init_task ; )
```

Users of `for_each_task()` should take `tasklist_lock` for **READ**. Note that `for_each_task()` is using `init_task` to mark the beginning (and end) of the list – this is safe because the idle task (pid 0) never exits.

The modifiers of the process hashtable or/and the process table links, notably `fork()`, `exit()` and `ptrace()`, must take `tasklist_lock` for **WRITE**. What is more interesting is that the writers must also disable interrupts on the local CPU. The reason for this is not trivial: the `send_sigio()` function walks the task list and thus takes `tasklist_lock` for **READ**, and it is called from `kill_fasync()` in interrupt context. This is why writers must disable interrupts while readers don't need to.

Now that we understand how the `task_struct` structures are linked together, let us examine the members of `task_struct`. They loosely correspond to the members of UNIX 'struct proc' and 'struct user' combined together.

The other versions of UNIX separated the task state information into one part which should be kept memory-resident at all times (called 'proc structure' which includes process state, scheduling information etc.) and another part which is only needed when the process is running (called 'u area' which includes file descriptor table, disk quota information etc.). The only reason for such ugly design was that memory was a very scarce resource. Modern operating systems (well, only Linux at the moment but others, e.g. FreeBSD seem to improve in this direction towards Linux) do not need such separation and therefore maintain process state in a kernel memory-resident data structure at all times.

The task_struct structure is declared in `include/linux/sched.h` and is currently 1680 bytes in size.

The state field is declared as:

```c
volatile long state;    /* -1 unrunnable, 0 runnable, >0 stopped */

#define TASK_RUNNING           0
#define TASK_INTERRUPTIBLE     1
#define TASK_UNINTERRUPTIBLE   2
#define TASK_ZOMBIE            4
#define TASK_STOPPED           8
#define TASK_EXCLUSIVE         32
```

Why is `TASK_EXCLUSIVE` defined as 32 and not 16? Because 16 was used up by `TASK_SWAPPING` and I forgot to shift `TASK_EXCLUSIVE` up when I removed all references to `TASK_SWAPPING` (sometime in 2.3.x).

The `volatile` in p->state declaration means it can be modified asynchronously (from interrupt handler):

- **TASK_RUNNING**: means the task is "supposed to be" on the run queue. The reason it may not yet be on the runqueue is that marking a task as TASK_RUNNING and placing it on the runqueue is not atomic. You need to hold the runqueue_lock read-write spinlock for read in order to look at the runqueue. If you do so, you will then see that every task on the runqueue is in TASK_RUNNING state. However, the converse is not true for the reason explained above. Similarly, drivers can mark themselves (or rather the process context they run in) as TASK_INTERRUPTIBLE (or TASK_UNINTERRUPTIBLE) and then call schedule(), which will then remove it from the runqueue (unless there is a pending signal, in which case it is left on the runqueue).
- **TASK_INTERRUPTIBLE**: means the task is sleeping but can be woken up by a signal or by expiry of a timer.
- **TASK_UNINTERRUPTIBLE**: same as TASK_INTERRUPTIBLE, except it cannot be woken up.
- **TASK_ZOMBIE**: task has terminated but has not had its status collected (wait(1)-ed for) by the parent (natural or by adoption).
- **TASK_STOPPED**: task was stopped, either due to job control signals or due to ptrace(2).
- **TASK_EXCLUSIVE**: this is not a separate state but can be OR-ed to either one of TASK_INTERRUPTIBLE or TASK_UNINTERRUPTIBLE. This means that when this task is sleeping on a wait queue with many other tasks, it will be woken up alone instead of causing "thundering herd" problem by waking up all the waiters.

Task flags contain information about the process states which are not mutually exclusive:

```c
unsigned long flags;    /* per process flags, defined below */
/*
 * Per process flags
 */
#define PF_ALIGNWARN       0x00000001      /* Print alignment warning msgs */
                                     /* Not implemented yet, only for 486*/
#define PF_STARTING        0x00000002    /* being created */
#define PF_EXITING         0x00000004    /* getting shut down */
#define PF_FORKNOEXEC      0x00000040    /* forked but didn't exec */
#define PF_SUPERPRIV       0x00000100    /* used super-user privileges */
#define PF_DUMPCORE        0x00000200    /* dumped core */
#define PF_SIGNALED        0x00000400    /* killed by a signal */
#define PF_MEMALLOC        0x00000800    /* Allocating memory */
#define PF_VWORK           0x00001000    /* Wake up parent in mm_release */
#define PF_USEDPU          0x00100000    /* task used PFU this quantum (SMP) */
```

The fields p->has_cpu, p->processor, p->counter, p->priority, p->policy and p->rt_priority are related to the scheduler and will be looked at later.

The fields p->mm and p->active_mm point respectively to the process' address space described by mm_struct structure and to the active address space if the process doesn't have a real one (e.g. kernel threads). This helps minimise TLB flushes on switching address spaces when the task is scheduled out. So, if we are scheduling-in the kernel thread (which has no p->mm) then its next->active_mm will be set to the prev->active_mm of the task that was scheduled-out, which will be the same as prev->mm if prev->mm != NULL. The address space can be shared between threads if CLONE_VM flag is passed to the clone(2) system call or by means of vfork(2) system call.

The fields p->exec_domain and p->personality relate to the personality of the task, i.e. to the way certain system calls behave in order to emulate the "personality" of foreign flavours of UNIX.

The field p->fs contains filesystem information, which under Linux means three pieces of information:

- root directory's dentry and mountpoint,
- alternate root directory's dentry and mountpoint,
- current working directory's dentry and mountpoint.

This structure also includes a reference count because it can be shared between cloned tasks when CLONE_FS flag is passed to the clone(2) system call.

The field p->files contains the file descriptor table. This too can be shared between tasks, provided CLONE_FILES is specified with clone(2) system call.

The field p->sig contains signal handlers and can be shared between cloned tasks by means of CLONE_SIGHAND.

## 2.2 Creation and termination of tasks and kernel threads

Different books on operating systems define a "process" in different ways, starting from "instance of a program in execution" and ending with "that which is produced by clone(2) or fork(2) system calls". Under Linux, there are three kinds of processes:

- the idle thread(s),
- kernel threads,
- user tasks.

The idle thread is created at compile time for the first CPU; it is then "manually" created for each CPU by means of arch-specific fork_by_hand() in arch/i386/kernel/smpboot.c, which unrolls the
