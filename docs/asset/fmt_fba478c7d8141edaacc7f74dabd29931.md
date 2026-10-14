
```c
579 void update_process_times(int user_tick)
580 {
581     struct task_struct *p=current;
582     int cpu = smp_processor_id(current),system=user_tick^1;
583 
584     update_one_process(p, user_tick, system, cpu);
585     if (p->pid) {
586         if (-p->counter<=0) {
587             p->counter=0;
588             p->need_resched=1;
589         }
590         if (p->nice>0)
591             kstat.per_cpu_nice[cpu]+=user_tick;
592         else
593             kstat.per_cpu_system[cpu]+=user_tick;
594 
595 }else if (local_bb_count(cpu)||local_irq_count(cpu)>1)
596     kstat.per_cpu_system[cpu]+= system;
597 }
```

图15.3 当前进程的定时器中断处理

- 参数 `user_tick` 表示正在计入的是用户态 (1) 还是内核态 (0) 的滴答。

- 此函数接收一个指向当前进程 `task_struct` 的指针。

- 获取运行此代码的 CPU 标识符（ID）。`smp_processor_id()` 宏在第 7.2.1.4 节描述过。系统变量（`system`）初始化为 `user_tick` 的反值。如果 CPU 在上一个滴答中处于内核态，则 `system` 应该为 1。如果 `user_tick` 为 1，则表示它上一个滴答处于用户态，因此 `system` 应该 0。

- 使用第 15.1.3.2 节中的函数更新当前进程的统计信息。

- 如果处理的是进程 0（空进程，null process），则跳转到第 595 行。空进程没有量子片，因此无需检查它，也无法通过 `nice` 降低其优先级。

- 递减当前进程的量子片。

- 如果为负数（即在递减之前为 0），则将其重置为 0。

- 如果已过期，我们为该进程设置 `need_resched` 标志。

- 590–593 行更新 CPU 统计信息。此行根据进程优先级是否已低于默认值（通过 `nice` 降低），向 `per_cpu_nice[]` 或 `per_cpu_user[]` 增加一个用户滴答。如果是内核态滴答，则会增加整个 `kstat` 结构体（该结构体在第 7.2.4.1 节中定义）。

- 594 行在任何情况下，都会向 `per_cpu_system[]` 增加一个滴答。如果是用户态滴答，则不增加。

- 595–596 行如果空进程正在运行，且该 CPU 代码正在处理两个半部分（halves）或本地中断，如果是系统态滴答，则更新 `per_cpu_system[]`，这样如果空进程恰好在为系统工作，则会将该费用记在系统头上。这些宏在第 16.5.1.2 节中描述。

## 15.1.3.2 更新单个进程的统计信息

上一个进程处理了统计信息的更新。图15.4所示的来自 `kernel/timer.c` 的函数更新当前进程的统计信息，包括虚拟定时器和分析定时器（profiling timers）。

```c
566 void update_one_process(struct task_struct *p,
567     unsigned long user, unsigned long system, int cur)
568 {
569     p->per_cpu_utime[cpu] += user;
570     p->per_cpu_stime[cpu] += system;
571     do_process_times(p, user, system);
572     do_it_virt(p, user);
573     do_it_prof(p);
574 }
```

图15.4 更新进程统计信息和时间

- 567 行 `user` 将为 1 且 `system` 为 0，或反之，取决于定时器中断发生在用户态还是内核态。

- 569–573 行此代码增加了在该 CPU 上使用的用户时间或系统时间的运行总和。

- 571 行 `do_process_times()` 函数检查该进程是否超过了 CPU 限制（见第 15.1.3.3 节）。

- 572–573 行最后会检查任何虚拟定时器或分析定时器是否过期（这些函数分别见第 15.1.3.4 和第 15.1.3.5 节）。

## 15.1.3.3 检查限制

除了量子片外，每个进程都被赋予了在其生命周期内可以使用的最大 CPU 时间（秒为单位），以防止失控进程占用 CPU。CPU 使用实际上有两个限制：软限制（`rlim_cur`）和硬限制（`rlim_max`）。当超过软限制时，进程会收到 `SIGCPU`。当超过硬限制时，会发送 `SIGKILL`。图15.5所示的来自 `kernel/timer.c` 的函数检查该进程是否超过了 CPU 限制。

定时器中断处理

```c
522 static inline void do_process_times(struct task_struct *p,
523     unsigned long user, unsigned long system)
524 {
525     unsigned long pseecs;
526
527     psesecs = (p->utime += user);
528     psesecs += (p->stime += system);
529     if (psesecs > p->rlim[CPU].rlim_cur){
530         if (!pseecs%HZ)
531             send_sig(SIGCPU, p, 1);
532
533         if (psesecs / HZ > p->rlim[CPU].rlim_max)
534             send_sig(SIGKILL, p, 1);
535 }
```

图15.5 检查用户时间和系统时间

- 522–523 行第一个参数是指向目标进程 `task_struct` 的指针。两个 `user` 和 `system` 是在用户态或系统态花费的时间，将要加入。其中一个为 1，另一个为 0。

- 527 行如果是用户态滴答，则更新进程描述符的 `utime` 字段。任何情况下，我们将用户时间加入 `pseecs`。

- 528 行如果是系统态滴答，则更新进程描述符的 `stime` 字段。任何情况下，我们将系统时间加入 `pseecs`，这是到目前为止的总时间（以滴答为单位）。

- 529–536 行将滴答除以 `HZ`（`HZ` 是每秒滴答数），此代码仅在超过软限制时执行。

- 531–535 行每当使用一秒 CPU 时间时发送 `SIGCPU`。`pseecs %HZ` 的值每秒一次为0。`send_sig()` 函数在第 18.2.7 节描述。进程可以捕获此信号，例如打印警告消息。

- 534–535 行当超过限制时，进程会被 `SIGKILL` 以被杀死。

## 15.1.3.4 更新虚拟定时器

Linux 提供了多种机制，允许进程请求定期发送信号。其中之一是虚拟定时器，它只计算进程在用户态花费的时间。它发送 `SIGALRM`。`task_struct` 中的 `it_virt_incr` 字段包含该定时器信号之间的间隔（以滴答测量）；相应的 `it_virt_value` 字段包含定时器的当前值。图15.6所示的来自 `kernel/timer.c` 的函数更新并检查虚拟定时器的过期。

```c
539 static inline void do_it_virt(struct task_struct* p, unsigned long ticks)
{
    unsigned long it_virt=p->it_virt_value;
    if (it_virt) {
        it_virt -= ticks;
        if (!it_virt) {
            it_virt = p->it_virt_incr;
            send_sig(SIGALRM, p, 1);
        }
    }
    p->it_virt_value = it_virt;
}
```

图15.6 检查虚拟间隔定时器的过期

- 539 行 `ticks` 参数指定上一个滴答是在用户态 (1) 还是系统态 (0)。虚拟间隔定时器只计算用户态花费的时间。可以认为此测试应该由调用者（`update_one_process()`，第 15.1.3.2 节）完成。
