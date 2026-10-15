
428–429 它们提供了当前（发送端）进程的 `pid` 和 `uid`。

431–437 如果参数 `info` 的值为 1，则它是由内核发送的内核信号。所有字段均为默认值，但 `si_code` 例外，该字段指示信号是从内核的某个地方发送的（这些 `si_code` 值参见第 17.1.5.4 节）。

438–440 提供了指向 `struct siginfo` 的有效指针。

439 将此信息从 `struct siginfo` 拷贝到 `struct sigqueue_info`。该函数描述第 18.1.3.3 节。

442–443 此测试仅在系统内存不足且无法在第 415 行为 `struct sigqueue_info` 分配空间时执行。如果以下所有条件均为真，则不会尝试在没有其信息的情况下投递它，且函数返回 `EAGAIN`：

- 它是一个实时信号（第一个条件）
- 提供了有效的 `struct siginfo`（第二个和第三个条件）
- 它不是从用户模式发送的（第四个条件）。

451 这一行在所有其他情况下执行。它设置目标进程信号掩码中相应的位并返回（`sigaddset()` 函数参见第 17.2.1.1 节）。

## 18.1.3.3 拷贝 siginfo 数据

当信号被入队以处理 `struct siginfo` 中提供的数据时，这些数据被拷贝到 `struct sigqueue` 的 `info` 字段中。该函数见图 18.10，`<asm/siginfo.h>`。

```c
219 static inline void copy_siginfo(siginfo_t*to, siginfo_t*from)
220 {
221     if (from->si_code < 0)
222         memcpy(to, from, sizeof(siginfo_t));
223     else
224         memcpy(to, from, sizeof(int)+sizeof(from));
227 }
```

图 18.10 将 `siginfo` 数据拷贝到队列条目；参数是发送者提供的 `struct siginfo`。如果 `si_code` 为负数，则它是标准的 `siginfo_t`（17.1.5），直接 `memcpy` 即可。否则，我们拷贝联合体的当前成员。

## 18.1.3.4 通知信号到达

当一个未阻塞的信号发布到一个进程时，如果进程处于睡眠状态，则应该被唤醒并移动到运行队列。实现该函数的见图 18.11，`kernel/signal.c`。该函数期望调用者持有 `sigmask_lock`，并且在获取时已禁用本地中断。

```c
466 static inline void signal_up(struct task_struct *t)
467 {
468     t->sigpending=1;
469 
#ifdef CONFIG_SMP
481     spin_lock(&runqueue_lock);
482     if (t->has_cpu && t->processor != smp_processor_id(t))
483         smp_send_reschedule(t->processor);
484     spin_unlock(&runqueue_lock);
485 #endif
486 
487     if (t->state&TASK_INTERRUPTIBLE) {
488         wake_up(t);
489     return;
491 }
```

图 18.11 通知信号到达

468 在进程的 `task_struct` 中设置一个标记表示有一个挂起的信号。

470–485 这段代码仅在 SMP 有效；目标进程可能实际上在另一个处理器（CPU）上运行。

481–484 取出运行队列，以便我们在读取时目标进程无法更改信息。代码中的注释接受如果进程实际上处于更改中间，这可能会触发错误的 CPU —— 这样做唯一的危害是额外的（轻量级）处理器间中断。

482 如果目标进程实际上正在运行，且位于与当前进程不同的处理器上，这排除了进程自发信号的情况。`smp_processor_id()` 来自节 7.2.1.4。

483 在其他 CPU 上强制调度以便注意到新信号（函数参见第 13.5.1 节）。

487–490 如果目标进程正在睡眠，我们使用第 4.7.5 节的函数唤醒它，将其状态更改为 `TASK_RUNNING` 并移动到运行队列。当调度器最终交给 CPU 时，它将处理此信号。

## 18.2 其他发送函数

本节考虑了若干函数，它们在经过初步处理后发送信号。它们最终都会调用 `send_sig_info()` 来发送一个或多个信号。

## 18.2.1 强制投递信号

有时需要强制进程接收一个它标记为忽略或阻塞的信号。图 18.12 `kernel/signal.c` 中的函数正是这么这么的。

```c
560 int
561 force_sig_info(int sig, struct siginfo *info, struct task_struct *t)
562 {
563     unsigned long flags;
564 
565     spin_lock_irqsave(&t->sigask_lock, flags);
566     if (t->sig==NULL) {
567         spin_unlock_irqrestore(&t->sigask_lock, flags);
568         return -ESCH;
569     }
```

```c
570 if (t->sig_action[sig-1].sa.sa_handler == SIG_IGN) {
571 t->sig_action[sig-1].sa.sa_handler = SIG_DFL;
572 delset(&blocked, sig);
573 recalc_sigpending(t);
574 spin_unlock_irqrestore(&t->sigask_lock, flags);
575 
577 return send_sig_info(sig, info, t);
578 }
```

图 18.12 强制投递信号；指向 `struct siginfo` 的指针，以及指向目标进程 `task_struct` 的指针。

565–575 由于函数将写入目标进程的阻塞掩码，因此它获取一个自旋锁以防止同时进行任何其他处理。中断安全的自旋锁宏在第 12.8.1 节中描述过。

566–569 如果目标进程是僵尸，我们释放锁并恢复中断状态。然后返回 `ESRCH`（无此类进程）。

571–572 如果进程将信号的处理程序设置为 `SIG_IGN`，我们将其改为 `SIG_DFL` 以执行默认操作。

573 将此特定的信号标记为未阻塞，以防它被阻塞。该函数位于第 17.2.1.1 节。

574 该函数（来自第 18.3.2 节）更新 `task_struct` 的 `sigpending` 字段，以便此信号被注意到。

577 现在调用发送信号的普通函数（描述第 18.1.1 节），并返回它提供的任何状态值。

## 18.2.2 向组中的所有进程发送信号

有一个特殊函数向组中的所有进程发送信号。这用于键盘控制字符，例如 CTRL-C 和 CTRL-Z；见图 18.13，来自 `kernel/signal.c`。

```c
585 int
586 kill_pg_info(int sig, struct siginfo *info, pid_t pgrp)
587 {
588     int retval = -EINVAL;
589 if (pgrp > 0) {
590     struct task_struct *p;
591 
592     retval = -ESRCH;
593     read_lock(&task_list_lock);
594     for_each_task(p) {
```

```c
595    if (p->pgrp == pgrp) {
596        int err = send_sig_info(sig, info, p);
597        if (retval)
598            retval = err;
599    }
600    }
601    read_unlock(&tasklist_lock);
602    }
603    return retval;
604 }
```

# 其他信号发送函数
