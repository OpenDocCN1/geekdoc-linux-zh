

# kthread 内核进程

用于从现有内核线程生成新的内核线程的接口（在 `<linux/kthread.h>` 中声明）为：

```c
struct task_struct *kthread_create(int (*threadfn)(void *data),
                                   void *data,
                                   const char namefmt[],
                                   ...);
```

新任务由 `kthreadd` 内核进程通过 `clone()` 系统调用创建。新进程将执行 `threadfn` 函数，该函数接收 `data` 参数。进程将被命名为 `namefmt`，它接受变参列表中的 `printf` 风格的格式化参数。进程以不可运行状态创建；除非通过 `wake_up_process()` 显式唤醒，否则它不会开始运行。可以使用单一函数 `kthread_run()` 创建并使进程可运行：

```c
struct task_struct *kthread_run(int (*threadfn)(void *data),
                                void *data,
                                const char namefmt[],
                                ...);
```

这个例程被实现为一个宏，它简单调用了 `kthread_create()` 和 `wake_up_process()`：

```c
#define kthread_run(threadfn, data, namefmt, ...) \
({ \
    struct task_struct *k; \
    k = kthread_create(threadfn, data, namefmt, ## __VA_ARGS__); \
    if (!IS_ERR(k)) \
        wake_up_process(k); \
    k; \
})
```

启动后，内核线程将继续存在，直到它调用 `do_exit()` 或内核的其他部分调用 `kthread_stop()` 并传入 `kthread_create()` 返回的 `task_struct` 结构的地址：

```c
int kthread_stop(struct task_struct *k);
```

我们将在后续章节中更详细地讨论特定的内核线程。

# 进程终止

令人遗憾但也必须面对的是，进程最终会消亡。当进程终止时，内核会释放该进程拥有的资源，并通知其子进程的父母该子进程已死亡。

通常，进程销毁是自发的。当进程调用 `exit()` 系统调用时发生，无论是显式地在准备终止时调用，还是在任何程序的 `main` 子例程返回时隐式调用（即 C 编译器在 `main()` 返回后放置了一个对 `exit()` 的调用）。进程也可能非自愿终止。当进程接收到无法处理或忽略的信号或异常时发生。无论进程如何终止，大部分工作由 `do_exit()` 处理：

1.  它在 `task_struct` 的 `flags` 成员中设置 `PF_EXITING` 标志。
2.  它调用 `get_timer_sync()` 来移除任何内核定时器。返回时，保证没有定时器排队，也没有定时器处理器正在运行。
3.  如果启用了 BSD 进程记账，`do_exit()` 调用 `acct_update_integrals()` 来写出处置信息。
4.  它调用 `exit_mm()` 来释放该进程持有的 `mm_struct`。如果没有其他进程使用此地址空间——即地址空间未被共享——内核随后将其销毁。
5.  它调用 `exit_sem()`。如果进程在队列中等待 IPC 信号量，则在此处出队。
6.  然后它调用 `exit_files()` 和 `exit_fs()` 分别减少与文件描述符和文件系统数据相关的对象的使用计数。如果使用计数中任何一个达到零，则对象不再被任何进程使用，并被销毁。
7.  它将任务的退出代码（存储在 `task_struct` 的 `exit_code` 成员中）设置为由 `exit()` 或强制终止的内核机制提供的代码。退出代码存储在此处，以便父进程可选地检索。
8.  它调用 `exit_notify()` 向任务的父进程、任务任何子进程的父进程、线程组中的另一个线程或 init 进程发送信号，并将任务的退出状态（存储在 `task_struct` 结构中的 `exit_state`）设置为 `EXIT_ZOMBIE`。
9.  `do_exit()` 调用 `schedule()` 切换到新进程（参见第 4 章）。由于进程现在不可调度，这是任务将永远执行的最后一段代码。`do_exit()` 永远不会返回。

此时，与任务相关的所有对象（假设任务是唯一使用者）已被释放。任务*不可运行*（并且不再有地址空间供其运行），处于 `EXIT_ZOMBIE` 退出状态。它占用的唯一内存是其内核栈、`thread_info` 结构和 `task_struct` 结构。任务退出的唯一目的是向父进程提供信息。父进程检索到信息或通知内核它不感兴趣后，进程持有的剩余内存将被释放并返回给系统使用。

# 移除进程描述符

在 `do_exit()` 完成后，已终止进程的进程描述符仍然存在，但进程已成为僵尸且无法运行。如前所述，这使得系统能够在子进程终止后获取关于它的信息。因此，清理进程和其进程描述符移除是两个独立的动作。在父进程获取已终止子进程的信息，或向内核表示它不关心之后，子进程的 `task_struct` 被释放。

`wait(2)` 函数族通过单个（且复杂的）系统调用 `wait4(2)` 实现。标准行为是挂起调用任务的执行，直到其某个子进程退出，此时函数返回已退出子进程的 PID。此外，提供一个指针给该函数，在返回时持有已终止子进程的退出代码。

当最终释放进程描述符时，调用 `release_task()`。它执行以下操作：

1.  它调用 `exit_signal()`，进而调用 `unhash_process()`，再调用 `detach_pid()` 从 `pidhash` 中移除进程，并从任务列表中移除进程。
2.  `exit_signal()` 释放现已死亡的进程使用的任何剩余资源，并最终化统计和记账。
3.  如果任务是线程组的最后一个成员，且领导者是僵尸，则 `release_task()` 通知僵尸领导者的父进程。
4.  `release_task()` 调用 `put_task_struct()` 释放包含进程内核栈和 `thread_info` 结构的页面，并释放包含 `task_struct` 的 slab 缓存。

此时，进程描述符和仅属于该进程的所有资源已被释放。

# 无父进程任务的困境

如果父进程在其子进程之前退出，必须存在某种机制来*调整*任何子任务到一个新进程，否则无父进程且已终止的进程将永远保持僵尸状态，浪费系统内存。解决方案是在退出时将任务的子进程重新分配给*线程组中的另一个* *进程*，如果失败，则分配给 init 进程。`do_exit()` 调用 `exit_notify()`，进而调用 `forget_original_parent()`，再调用 `find_new_reaper()` 执行重新分配：

```c
static struct task_struct *find_new_reaper(struct task_struct *father)
{
    struct pid_namespace *pid_ns = task_active_pid_ns(father);
    struct task_struct *thread;

    thread = father;
    while_each_thread(father, thread) {
        if (thread->flags & PF_EXITING)
            continue;
        if (unlikely(pid_ns->child_reaper == father))
            break;
        thread = NULL;
    }
    if (thread) {
        pid_ns->child_reaper = thread;
        return thread;
    }

    if (unlikely(pid_ns->child_reaper == father)) {
        write_unlock_irq(&tasklist_lock);
        if (unlikely(pid_ns == &init_pid_ns))
            panic("Attempted to kill init!");

        zap_pid_ns_processes(pid_ns);
        write_lock_irq(&tasklist_lock);
        /*
         * We can not clear ->child_reaper or leave it alone.
         * There may by stealth EXIT_DEAD tasks on ->children,
         * forget_original_parent() must move them somewhere.
         */
        pid_ns->child_reaper = init_pid_ns.child_reaper;
    }
    return pid_ns->child_reaper;
}
```

此代码试图查找并返回进程线程组中的另一个任务。如果线程组中没有其他任务，它查找并返回 _init_ 进程。既然找到了适合子进程的新父进程，每个子进程都需要被定位并重新分配给 _reaper_：

```c
reaper = find_new_reaper(father);
list_for_each_entry_safe(p, n, &father->children, sibling) {
    p->real_parent = reaper;
    if (p->parent == father) {
        BUG_ON(p->ptrace);
        p->parent = p->real_parent;
    }
    reparent_thread(p, father);
}
```

然后调用 `exit_ptrace()` 对 _ptraced_ 子进程列表执行相同的重新分配：

```c
void exit_ptrace(struct task_struct *tracer)
{
    struct task_struct *p, *n;
    LIST_HEAD(ptrace_dead);

    write_lock_irq(&tasklist_lock);
    list_for_each_entry_safe(p, n, tracer->ptraced, ptrace_entry) {
        if (!__ptrace_detach(tracer, p))
            list_add(&p->ptrace_entry, &ptrace_dead);
    }
    /*
     * Now move the list of reparented processes to a new reaper
     */
    reaper = find_new_reaper(tracer);
    while (!list_empty(&ptrace_dead)) {
        p = list_first_entry(&ptrace_dead, struct task_struct, ptrace_entry);
        list_del(&p->ptrace_entry);
        p->ptrace = 0;
        p->parent = reaper;
        list_add(&p->sibling, &reaper->ptraced);
    }
    write_unlock_irq(&tasklist_lock);
}

