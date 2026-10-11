confirms it is not needed)

+   14. The child's `p->flags` are set according to the value of `clone_flags`; for plain `fork(2)`, this will be `p->flags = PF_FORKNOEXEC.`

+   15. The child's `pid` `p->pid` is set using the fast algorithm in `kernel/fork.c:get_pid()` (TODO: `lastpid_lock` spinlock can be made redundant since `get_pid()` is always called under big kernel lock from `do_fork()`, also remove `flags` argument of `get_pid()`, patch sent to Alan on 20/06/2000 – followup later).

+   16. The rest of the code in `do_fork()` initialises the rest of child's task structure. At the very end, the child's task structure is hashed into the `pidhash` hashtable and the child is woken up (TODO: `wake_up_process(p)` sets `p->state = TASK_RUNNING` and adds the process to the runq, therefore we probably didn't need to set `p->state` to `TASK_RUNNING` earlier on in `do_fork()`). The interesting part is setting `p->exit_signal` to `clone_flags & CSIGNAL`, which for `fork(2)` means just `SIGCHLD` and setting `p->pdeath_signal` to 0. The `pdeath_signal` is used when a process 'forgets' the original parent (by dying) and can be set/get by means of `PR_GET/SET_PDEATHSIG` commands of `prctl(2)` system call (You might argue that the way the value of `pdeath_signal` is returned via userspace pointer argument in `prctl(2)` is a bit silly – mea culpa, after Andries Brouwer updated the manpage it was too late to fix ;)

Thus tasks are created. There are several ways for tasks to terminate:

+   1. by making `exit(2)` system call;

+   2. by being delivered a signal with default disposition to die;

+   3. by being forced to die under certain exceptions;

+   4. by calling `bdflush(2)` with `func == 1` (this is Linux–specific, for compatibility with old distributions that still had the 'update' line in `/etc/inittab` – nowadays the work of update is done by kernel thread `kupdated.`

Functions implementing system calls under Linux are prefixed with `sys_`, but they are usually concerned only with argument checking or arch–specific ways to pass some information and the actual work is done by `do_` functions. So it is with `sys_exit()` which calls `do_exit()` to do the work. Although, other parts of the kernel sometimes invoke `sys_exit()` while they should really call `do_exit()`.

The function `do_exit()` is found in `kernel/exit.c`. The points to note about `do_exit()`:

+   * Uses global kernel lock (locks but doesn't unlock).

+   * Calls `schedule()` at the end, which never returns.

+   * Sets the task state to `TASK_ZOMBIE`.

+   * Notifies any child with `current->pdeath_signal`, if not 0.

+   * Notifies the parent with `current->exit_signal`, which is usually equal to SIGCHLD.

+   * Releases resources allocated by fork, closes open files etc.

+   * On architectures that use lazy FPU switching (ia64, mips, mips64) (TODO: remove 'flags' argument of `sparc, sparc64`, do whatever the hardware requires to pass the FPU ownership (if owned by current) to "none".

# 2.3 Linux Scheduler

The job of a scheduler is to arbitrate access to the current CPU between multiple processes. The scheduler is implemented in the 'main kernel file' `kernel/sched.c`. The corresponding header file `include/linux/sched.h` is included (either explicitly or indirectly) by virtually every kernel source file.