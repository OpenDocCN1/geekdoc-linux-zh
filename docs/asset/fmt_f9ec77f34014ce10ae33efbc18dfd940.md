
```c
323    static int signal_type(int sig, struct signal_struct *signals)
324    {
325        unsigned long handler;
326
327        if (!signals)
328            return 0;
329
330        handler = (unsigned long) signals[sig-1].sa_handler;
331        if (handler > 1)
332            return 1;
333
335        if (handler == 1)
336            return sig == SIGCHLD;

339    switch (sig) {
342    case SIGCONT: case SIGWINCH:
343    case SIGCHLD: case SIGUSR:
344        return 0;
347    case SIGSTOP: case SIGTTIN: case SIGTO:
348        return 1;
351    default:
352        return -1;
353 }
354 }
```

**图 18.7** 确定信号类型以及目标进程 `task_struct` 的指针。

323 参数是信号数。

327–328 如果指向目标进程 `task_struct` 的指针为 NULL，则意味着是一个僵尸进程。该信号可以被忽略，因此我们返回 0。

330 这获取为指定信号的处理程序指针的本地副本。

331–332 如果指针大于大于1，则安装了有效的处理程序，不应被忽略。我们返回 1。

335–336 如果指针值为 1，则它被设置为 `SIG_IGN`。然而，有一个例外：SIGCHLD 信号不能忽略。如果是 SIGCHLD，我们返回 1；否则返回 0。注意 SIGCHLD 是非常特殊的信号；如果设置为 `SIG_IGN`，它实际上并没有被忽略，而是自动收割；如果设置为 `SIG_DFL`，POSIX 强制将其忽略。

339–343 此段代码仅在指针值小于 1 时执行。这意味着它被设置为 `SIG_DFL`。

342–344 这四个信号的默认动作是忽略它们，因此我们返回 0，意味着忽略。它们具有某些隐式行为。

351–352 对于所有其他情况，我们返回 -1。调用者（第 18.1.2.5 节）绝会区分零和非零。

## 18.1.3 向目标进程投递信号

作为第 18.1.1 节讨论的发送过程的一部分，信号必须投递给目标进程。这是本节的主题。有一个基础函数和一个由它调用的系列子函数。

### 18.1.3.1 投递信号

所有处理的核心是图 18.8 所示的函数，来自 `kernel/signal.c`。每当发送信号时，`send_sig_info()` 都会调用它。

```
493 static int deliver_signal(int sig, struct siginfo *info,
494     struct task_struct *t)
495     int retvval = send_signal(sig, info, &t->pending);
497     if (!retvval && !sigismember(&t->blocked, sig))
499         signal_wake_up(t);
501     return retvval;
502 }
```

**图 18.8** 投递信号

493 参数是待发送的信号数、额外信息的指针以及目标进程 `task_struct` 的指针。

495 这种发送信号的低级函数在第 18.1.3.2 节中描述。第三个参数是目标进程 `pending` 字段的指针。这是唯一受影响的字段。如果成功投递信号，则返回 0，否则返回指示原因的错误代码。

497–498 如果 `send_signal()` 调用成功（0），且信号未被阻塞，则我们唤醒进程处理该信号，以防它处于睡眠状态。`sigismember()` 宏在第 17.2.1 节中描述过。

498 `signal_wake_up()` 函数将在第 18.1.3.4 节中讨论。

500 这是第 495 行 `send_signal()` 返回的成功或失败值。该值被传递给信号发送者。

### 18.1.3.2 发送信号

实际上向另一个进程发送信号的低级函数（即第一个实际操作目标进程 `task_struct` 的函数）如图 18.9 所示，来自 `kernel/signal.c`。

```
33 atomic_t    nr_queued_signals;
34 int           max_queued_signals = 1024;
```

## 发布与投递信号

```c
416     }
417 
418 if(q) {
419     atomic_inc(&nr_queued_signals);
420     q->next = NULL;
421     *signals->tail = q;
422     signals->tail = &q->next;
423     switch ((unsigned long)info) {
424         case 0:
425             q->info.si_sign = sig;
426             q->info.si_errno = 0;
427             q->info.si_code = SI_USER;
428             q->info.si_pid = current->pid;
429             q->info.si_uid = current->uid;
430             break;
431         case 1:
432             q->info.si_sign = sig;
433             q->info.si_errno = 0;
434             q->info.si_code = SI_KERNEL;
445             q->info.si_pid = 0;
436             q->info.si_uid = 0;
437             break;
438         default:
439             copy_siginfo(&q->info, info);
440             break;
441     }
442 } else if (sig == SIGRTMIN && info &&
443 (unsigned long)info != 1 && info->si_code != SI_USER) {
448     return -EAGAIN;
449     }
450 
451     sigaddset(&signals->signal, sig);
452     return 0;
453 }
```

图 18.9 发送信号

33 当信号在所有进程中队列时，存在一个系统级的信号队列限制。

34 任何时刻可以队列信号的总数有一个系统级限制，位于 `max_queued_signals` 中，初始化为 1024。

402 参数分别是待发送的信号编号、指向额外信息的指针，以及指向目标进程中 `struct sigpending` 的指针。

404 此指针需要初始化为 `NULL`。如果第 414 行的条件为假，则不会分配队列条目。如果指针在第 418 行仍为 `NULL`，则只有在满足以下条件时，414–416 任何时刻可队列信号总数的系统级限制未被超出，尝试为队列条目分配内存

## 发布信号

为队列条目分配内存（参见第 5.2.1 节，关于 `atomic_read()` 宏）。

418–441 这一块代码仅在内存管理器能够为另一个 `struct sigqueue_info` 分配足够空间时执行。

419 这增加了队列信号的全局计数器（该函数参见第 5.2.5 节）。

420 由于这将是队列中的最后一个条目，我们将它的前向指针设置为 `NULL`。

421 该进程信号队列的尾部指针指向上一个最后一个条目的 `next` 字段（该字段为 `NULL`）。此赋值更改了之前的最后一个条目，使其指向这个新条目。

422 信号队列的尾部指针设置为此新条目的 `next` 字段。

423 这检查了作为参数传递的指针 `info`。有三种可能：

424–440 如果它是一个 `NULL` 指针，则信号是由用户发送的，调用者没有额外信息要传递给目标进程。我们用默认值填充新分配的 `struct sigqueue_info` 的相应字段。

425 这是正在发送的信号编号。

426 未提供错误号，因此默认为 0。

427 这标识了由用户通过系统服务发送的信号（这些 `si_code` 值参见第 17.1.5.4 节）。
