
### 18.4.2 递交给被跟踪进程的待处理信号

图 18.25 显示的代码来自 `arch/i86/kernel/signal.c`，当进程被跟踪且被处理的信号不是 `SIGKILL` 时才会执行。即使进程被跟踪，`SIGKILL` 仍然杀死它。

```c
if ((current->ptrace & PT_TRACED) && signr != SIGKILL) {
    current->exit_code = signr;
    current->state = TASK_STOPPED;
    notify_parent(current, SIGCHLD);
    schedule();

    if (!(signr == current->exit_code)) {
        continue;
    }
    current->exit_code = 0;
}

    if (signr == SIGSTOP) {
        continue;
    }

    if (signr != info.si_signo) {
        info.si_signo = signr;
        info.si_errno = 0;
        info.si_code = SI_USER;
        info.si_pid = current->pptr->pid;
        info.si_uid = current->pptr->uid;
    }

    if (sigismember(&current->blocked, signr)) {
        send_sig_info(signr, &info, current);
        continue;
    }
}
```

图 18.25 递交给被跟踪进程的待处理信号

- 604–606：在当前进程 `sigmask_lock` 的保护下，我们找到队列中的第一个信号。中断安全的自旋锁宏在第 12.8 节中描述。
- 605：`dequeue_signal()` 函数将在第 18.5 节中描述。它返回下一个信号的数量以及 `info` 中信号的信息。
- 608–609：如果队列中没有信号，则跳出循环到达该行。这在第一次循环时通常发生。
- 613–616：这是将控制权交给跟踪进程。
- 613：正在处理信号的数量放在当前进程的 `exit_code` 字段中。这让跟踪进程知道哪个信号是待处理的。
- 614：其状态改为 `TASK_STOPPED`。
- 615：然后通知其父进程（调试进程）。`notify_parent()` 函数在第 18.2.6 节中检查过。它通过发送 `SIGCHLD` 让父进程知道子进程的状态发生了。
- 616：最后调用调度器。这会将当前进程从运行队列中移除。虽然调度器可能不会立即运行跟踪进程，但最终会运行，并且在此进程再次运行之前（因为它的状态是 `TASK_STOPPED`）。
- 619–620：当跟踪进程运行并将状态改回 `TASK_RUNNING` 后，此进程切回时将从这里开始。复制 `exit_code` 允许跟踪进程更改要处理的信号。如果跟踪进程取消了该信号，它会在 `exit_code` 中放入零。在这种情况下，该信号可以被忘记，我们再次通过循环检查是否有待处理信号。
- 621：否则，调试器希望此进程处理该信号。使用 `exit_code` 从调试器传回信息有点不常规。我们清除它以防以后引起混淆。
- 624–625：如果处理的信号是 `SIGSTOP`，我们直接忽略它。毕竟，进程刚刚停止并重启。我们再次通过循环检查是否有待处理信号。

### 18.4.3 忽略信号

当到达图 18.26 显示的代码时，无论从何处，都有需要处理的信号。现在我们正在检查，重点在于确定如何处理它。这段代码处理默认被忽略的信号。

```c
ka = &current->sig->action[sig-1];
if (ka->sa.sa_handler == SIG_IGN) {
    if (sig != SIGCHILD)
        continue;
while (sys_wait4(-1, NULL, WNOHANG, NULL) > 0)
    "nothing";
}
```

**图 18.26** 处理器被设置为 `SIG_IGN` 的信号

`643` 此处为我们正在处理的信号设置了指向 `k_sigaction` 结构体的本地指针。它包含了关于如何处理该信号的信息。

`645—650` 只有当处理器为 `SIG_IGN` 时，才会执行这段代码。

`645—646` 对于 `SIGCHLD` 以外的任何信号，我们都会跳过循环。由于处理器是 `SIG_IGN`，所以我们直接这样做。

如果它是 `SIGCHLD`，则意味着该进程的一个子进程已经退出。为了对其进行清理，我们调用了 `wait4`（见第 9.3 节）。第一个参数指定了与子进程的同步。第二个参数是一个指向 `int` 的指针，子进程的状态信息将写入其中。在这种情况下，当前进程只感兴趣于消除僵尸进程，因此在此处放置了 `NULL`。第三个参数指定不等待尚未退出的子进程。第四个参数是一个结构体指针，在这种情况下不需要。成功后，此函数返回子进程的 `pid`，因此如果有子进程在等待，这将会选取一个僵尸进程并允许它安息而去。`while` 循环考虑了多个子进程退出的可能性；它每次循环都会进行清理。当没有（进一步的）僵尸进程时，`wait4()` 返回 `0`，循环终止。

`650` 在任何情况下，我们都会回到主循环并检查下一个信号。

## 18.4.4 信号的默认处理

图 18.27 所示的代码只有在处理器为 `SIG_DFL` 时才会执行。

```c
if (ka->sa.sa_handler == SIG_DFL) {
    int exit_code = signr;
    if (current->pid==1)
        continue;
}
switch (signr) {
    case SIGCONT: case SIGCHLD: case SIGWIN:
        continue;
    case SIGSTOP: case SIGTTIN: case SIGGTTOU:
        if (is_orphaned_pgrp(current->pgrp))
            continue;
    case SIGSTOP:
        struct signal_t *sig =
            current->state = TASK_STOPPED;
            current->exit_code = signr;
            sig = current->p_ptr->sig;
        if (sig &&
sig-t;action[SIGCHLD-1].sa.sa_flags&SA_NOCLDSTOP))
```

## 发布与递送信号

```
675 notify_parent(current, SIGCHLD);
676 schedule();
677 continue;
678 case SIGQUIT: case SIGILL: case SIGTRAP
case SIGABRT: case SIGFPE: case SIGSEV
case SIGBUS: case SIGSYS: case SIGXFSZ
if (coredump, regs)) exit_code |= 0x80ndef:
sigaddset(&current->pending->signal, signr);
recalc_sigpending(current);
current->flags |= PF_SIGNALED;
do_exit(exit_code); }
```

图 18.27 处理器为 `SIG_DFL` 的信号

此句设置了一个本地 `exit_code`，用于存储正在处理的信号编号。该值可能会在 `684` 行处更新，并持续到 `691` 行。

注意，`init`（1 号进程）是一个特殊进程：它不会接收它不想处理的信号。它的默认操作是忽略信号。无论由于无意还是故意，你无法通过 `SIGKILL` 杀死 `init`。我们再次回到循环并检查下一个信号。

使用此 `switch` 语句，不同的信号或信号组被赋予不同的默认处理方式。

这些信号的默认处理只是忽略它们。我们循环并检查下一个信号。

这些是终端控制信号。如果该进程所属的进程组是孤儿进程（即没有控制终端），我们就忽略该信号并继续循环。`is_orphaned_ppgrp` 函数在第 9.2.3.2 节中描述过。否则，我们进入下一个 `case`。这里没有 `break` 语句。
