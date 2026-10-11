cleaning up after a process and removing its process descriptor are separate. After the parent has obtained information on its terminated child, or signified to the kernel that it does not care, the child's task_struct is deallocated.

The wait(2) family of functions are implemented via a single (and complicated) system call, wait4(2). The standard behavior is to suspend execution of the calling task until one of its children exits, at which time the function returns with the PID of the exited child. Additionally, a pointer is provided to the function that on return holds the exit code of the terminated child.

When it is time to finally deallocate the process descriptor, release_task() is invoked. It does the following:

+   1. It calls \_exit\_signal(), which calls \_unhash\_process(), which in turn calls detach\_pid() to remove the process from the pidhash and remove the process from the task list.

+   2. \_exit\_signal() releases any remaining resources used by the now dead process and finalizes statistics and bookkeeping.

+   3. If the task was the last member of a thread group, and the leader is a zombie, then release_task() notifies the zombie leader's parent.

+   4. release_task() calls put_task_struct() to free the pages containing the process's kernel stack and thread\_info structure and deallocate the slab cache containing the task_struct.

At this point, the process descriptor and all resources belonging solely to the process have been freed.

# The Dilemma of the Parentless Task

If a parent exits before its children, some mechanism must exist to *adjust* any child tasks to a new process, or else parentless terminated processes would forever remain zombies, wasting system memory. The solution is to reparent a task's children on exit to *either* *another* *process* *in* *the* *current* *thread* *group* *or* if that fails, the init process. do_exit() calls exit\_notify(), which calls forget\_original\_parent(), which, in turn, calls *find\_new\_reaper()* to perform the reparenting:

```
static struct task_struct \*find_new_reaper(struct task_struct \*father)
{
    struct pid_namespace \*pid_ns = task_active_pid_ns(father);
    struct task_struct \*thread;

    thread = father;
    while_each_thread(father, thread) {
        if (thread->flags & PF_EXITING)
            continue;
        if (unlikely(pid_ns->child_reaper == father))

```