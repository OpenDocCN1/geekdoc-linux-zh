
### 7.4.3 进程 `nice` 值与时间片计算

每个进程的 `task_struct` 中都有一个 `nice` 字段，可以通过 `nice()` 系统服务设置。该字段中的值指示了进程的优先级。该值的范围从 -20（高优先级进程）到 +19（最低优先级进程）。该宏将进程的 `nice` 值转换为时钟节拍的时间片大小。计算的第一部分 `20-(nice)` 产生从 40（最高优先级）到 1（最低优先级）的数值。然后该值通过 `TICK_SCALE()` 宏进行缩放，结果取决于中断时钟的频率。对于较慢的时钟，它除以 4 或 2；对于较的时钟，它乘以 2 或 4。最后加的 1 保证了无论优先级多低，或中断时钟有多慢，时间片至少为 1 个节拍。

## 7.4.4 记录分配的中央处理器单元

图 7.20 显示了来自 `<linux/sched.h>` 的简单函数在 `task_struct` 中记录特定进程已分配了一个 CPU。

```c
553 #define task_has_cpu(tsk) ((tsk)->cpu_runnable !=~0UL)
```

```c
556 static inline void task_set_cpu(struct task_struct *tsk,
557                                     unsigned int cpu)
557 {
558     tsk->processor = cpu;
559     tsk->cpu_runnable = 1UL << cpu;
560 }
```

> 图 7.20 记录已分配了一个计算单元

如果进程未分配 CPU：

- 在 `processor` 字段中记录分配的 CPU 编号。
- 在 `cpu_runnable` 中设置对应于分配进程的位。所有其他位都被清零。

## 7.5 上文切换

在第 7.3 节考虑调度器时，我们将讨论分为两个主要部分。其中最后一部分是进程之间的上下文切换。调度器的这部分主要涉及更改机器的内存上下文（见第 7.3.5 节）。它将切换栈和寄存器的工作交给两个例程。这里有许多步骤需要在此检查。首先，我们有一个通过切换栈指针来准备工作的宏。然后我们有一个实际完成上下文切换的函数。运行中进程执行的第一段代码确保它正愉快地休息，并向系统的其余部分宣布它实际上让出了 CPU。

被切换出的进程的 `task_struct` 结构体。此输入参数必须位于 `EBX` 寄存器中。它是参数 2 的别名。

### 7.5.2 切换计算机处理单元上下文

图 7.22 显示了来自 `arch/i386/kernel/process.c` 的代码将任务从 `prev_p` 切换到 `next_p`。当此函数被调用时，调度器已经在新进程的栈上运行了。

```c
679 void __switch_to(struct task_struct *prev_p, struct task_struct *next_p)
680 {
681     struct thread_struct *prev = &prev_p->thread,
682     *next = &next_p->thread;
683     struct tss_struct *tss = init_tss+smp_processor_id();
684
685     lazy_fpu(prev);
689
690     tss->esp0 = next->esp0;
696
697     asm volatile("movl%%fs,%0" :="m"((int *)&prev->fs));
698     asm volatile("movl%%gs,%0" :="m"((int *)&prev->gs));
702
703     loadsegment(fs, next->fs);
704     loadsegment(gs, next->gs);
708
709     if (next->debugreg[7]) {
710         loaddebug(next, 0);
711         loaddebug(next, 1);
712         loaddebug(next, 2);
713         loaddebug(next, 3);
714         /* no 4 and 5 */
715         loaddebug(next, 6);
716         loaddebug(next, 7);
717     }
718
719     if (prev->ioperm || !next->ioperm) {
720         if (next->ioperm) {
728
729             memcpy(tss->io_bitmap, next->io_bitmap,
730                             IO_BITMAP_SIZE*sizeof(unsigned long));
731             tss->bitmap = IO_BITMAP_OFFSET;
732         } else {
738
739             tss->bitmap = INVALID_IO_BITMAP_OFFSET;
740     }
741 }
```

图 7.22 实际的上下文切换器

- 679 参数是指上一个和下一个进程的 `task_struct` 的指针。
- 681–682 这些行获取了每个 `task_struct` 中 `thread` 字段的局部指针。
- 683 这获取了与当前 CPU 对应的 `tss` 字段的局部指针（见第 7.2.3.2 节）。
- 685 检查该进程是否使用了浮点单元（FPU）（该函数见第 11.10.2.2 节）。
- 690 这将进入进程线程的栈指针拷贝到 `tss` 结构体中相应的字段中，覆盖该处的原有值。
- 696–697 这在上一个进程的线程中保存 `FS` 和 `GS` 硬件寄存器。不需要保存 `ES` 和 `DS`，因为它们是内核内部的段。
- 702–703 这从新进程的线程中恢复 `FS` 和 `GS` 硬件寄存器值。该宏来自第 19.6.2 节。
- 708–716 如果新进程保存的 `debugreg[7]`（调试控制寄存器）指示有有效信息，则从线程结构中加载硬件调试寄存器。`loaddebug()` 函数见第 7.5.3 节。
- 718–739 这段代码仅在旧进程或新进程的 `ioperm` 有效时执行，这表示允许进程直接访问 IO 端口。这实际上是 IO 器的职责。
- 728–730 如果新进程的 `ioperm` 字段有效，则将 `io_bitmap` 字段从 `thread_io_bitmap` 拷贝到 `tss` 中。
- 730 `tss` 的 `thread` 字段被设置为上一行刚刚拷贝的 `io_bitmap` 字段的偏移量。
- 738 如果上一个进程设置了 `ioperm` 字段但当前进程没有，则执行此行。它在 `tss` 中设置了一个未对齐的位图偏移，指向段的边界，这当进程尝试使用 IO 端口指令时会导致 `SIGSEGV`。随后任何对 `sys_ioperm()` 的调用将正确设置位图。
- 740 该函数以一种异常方式终止。栈上的返回地址没有指向调用者。事实上，此函数从未被“调用”，而是跳转到了 `switch_to()` 的第 23 行（见第 7.5.1 节）。因为它被声明为标准的 C 函数，编译器在它的末尾生成了一个 `RET` 指令。当执行此指令时，它从栈中弹出一个值到 `EIP` 寄存器。这个值在 `switch_to()` 的第 22 行被推入栈中，指向恢复新进程的指令。

#### 7.5.3 加载调试寄存器

图 7.23 显示的来自 `arch/i386/kernel/process.c` 的宏将一个值从内存加载到调试寄存器之一中。

```c
651 #define loaddebug(thread,register)
652     asm volatile("movl%0,db" % register \
653     : /* no output */
654     :r (thread->debugreg[register]))
```

图 7.23 加载调试寄存器

- 651 参数是指要加载值的线程结构指针，以及寄存器编号。
- 652 这条机器指令将参数 0 移动到指定的寄存器。注意它在寄存器名前加上了 "db"。
- 654 唯一的操作数是线程结构中的 `debugreg[]` 数组元素，由寄存器指定。

#### 7.5.4 上文切换后的清理

图 7.24 显示的 `__schedule_tail()` 函数位于 `kernel/sched.c`。它在 `schedule()` 的第 698 行上下文切换后立即调用（见 7.3.5）。这意味着它是进程切换到 CPU 时执行的第一段代码。`prev` 指针指向被切换出的进程。大部分代码对于单处理器情况是微不足道的。
