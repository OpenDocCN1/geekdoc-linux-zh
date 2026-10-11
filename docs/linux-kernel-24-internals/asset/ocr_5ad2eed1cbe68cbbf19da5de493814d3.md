The tasks are hashed by their pid value and the above hashing function is supposed to distribute the elements uniformly in their domain (0 to PID_MAX-1). The hashtable is used to quickly find a task by given pid, using `find_task_pid()` inline from `include/linux/sched.h`:

```
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

```
#define for_each_task(p) \n  for (p = &init_task ; (p = p->next_task) != &init_task ; )
```

Users of `for_each_task()` should take `tasklist_lock` for **READ**. Note that `for_each_task()` is using `init_task` to mark the beginning (and end) of the list – this is safe because the idle task (pid 0) never exits.

The modifiers of the process hashtable or/and the process table links, notably `fork()`, `exit()` and `ptrace()`, must take `tasklist_lock` for **WRITE**. What is more interesting is that the writers must also disable interrupts on the local CPU. The reason for this is not trivial: the `send_sigio()` function walks the task list and thus takes `tasklist_lock` for **READ**, and it is called from `kill_fasync()` in interrupt context. This is why writers must disable interrupts while readers don't need to.

Now that we understand how the `task_struct` structures are linked together, let us examine the members of `task_struct`. They loosely correspond to the members of UNIX 'struct proc' and 'struct user' combined together.

The other versions of UNIX separated the task state information into one part which should be kept memory-resident at all times (called 'proc structure' which includes process state, scheduling information etc.) and another part which is only needed when the process is running (called 'u area' which includes file descriptor table, disk quota information etc.). The only reason for such ugly design was that memory was a very scarce resource. Modern operating systems (well, only Linux at the moment but others, e.g. FreeBSD seem to improve in this direction towards Linux) do not need such separation and therefore maintain process