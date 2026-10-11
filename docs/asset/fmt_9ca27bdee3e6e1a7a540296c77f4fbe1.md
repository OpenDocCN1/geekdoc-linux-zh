
```
457             desc->status |= IRQ_DISABLED;

458             mask_irq(irq);

/* 这是一个真实的中断，我们必须处理它，

所以我们跳转到 out */

goto out;

}

status &= ~IRQ_PENDING; /* 我们提交（开始）处理它 */

if ((status & IRQ_CPU))

    status = IRQ_INPROGRESS; /* 我们正在处理它 */

}

desc->status = status;
```
```
for (;;)
    spin_unlock(&desc->lock);
    handle_irq_event(irq, regs, action);
    spin_lock(&desc->lock);
}
if (likely(!(desc->status & IRQ_PENDING)))
    break;
desc->status &= ~IRQ_PENDING;
}
out:
desc->status &= ~IRQ_INPROGRESS;
```

第 432 行：从参数中获取 IRQ 并访问适当的 `irq_desc`。

第 435 行：获取 IRQ 描述符的自旋锁，以防不同的 CPU 同时访问同一个中断。

第 436 行：向硬件发送确认。硬件随后做出响应，在当前中断完成之前防止处理更多此类型的中断。

第 441–443 行：`IRQ_REPLAY` 和 `IRQ_WAITING` 标志被清除。在这种情况下，`IRQ_REPLAY` 表示 IRQ 之前丢失并正在重发。`IRQ_WAITING` 表示 IRQ 正在被测试（两种情况都在讨论范围内）。在单处理器系统中，`IRQ_PENDING` 标志被设置，表示我们提交处理中断。

## 3.8 异步执行流

第 450 行：这段代码检查我们不处理中断的情况。如果设置了 `IRQ_DISABLED` 或 `IRQ_INPROGRESS`，我们可以跳过这段代码。设置 `IRQ_DISABLED` 标志是因为，我们不希望系统对正在处理的特定 IRQ 线做出响应。`IRQ_INPROGRESS` 表示中断正在被处理器处理。这用于多处理器系统中的第二个处理器尝试触发相同中断的情况。

第 451–462 行：在这里，我们检查处理程序是否存在。如果不存在，我们跳出并跳转到第 498 行的 `out` 标签。

第 463–465 行：此时，我们已经清除了不服务中断的三个条件，因此我们提交处理中断。`IRQ_INPROGRESS` 标志被设置，`IRQ_PENDING` 标志被清除。

## 处理 PPC 定时器中断

如 `timer_init()` 所示，递减器被硬编码为 0x900。我们可以假设已经达到了终点计数，并在此时调用了 `arch/ppc/kernel/time.c` 中的处理函数 `timer_interrupt()`。

这里是 `timer_interrupt()` 函数：

```
arch/ppc/kernel/time.c
145 void timer_interrupt(struct pt_regs * regs)
146 {
```

# 170 第3章 • 进程：执行的主要模型

```
...
152 if (atomic_read(&ppc_n_lost_interrupts) != 0)
153 do_IRQ(regs);
154
155 irq_enter();
...
159 if (!user_mode(regs))
160 ppc_do_profile(instruction_pointer(regs));
...
165 write_seqlock(&xtime_lock);
166
167 do_timer(regs);
...
189 if (ppc_md.set_rtc_time(xtime.tv_sec+1 + time_offset) == 0)
...
195 write_sequnlock(&xtime_lock);
...
198 set_dec(next_dec);
208 irq_exit();
209 )
```

第 152 行

如果丢失了中断，返回并调用 0x900 处的外部处理程序。

第 159 行

为了内核路由进行内核性能分析。

第 165 和 195 行

锁定此代码块。

第 167 行

此代码与 x86 定时器中断（接将介绍）使用的函数相同。

第 189 行

更新 RTC（实时时钟）。

第 198 行

重启减计数器以处理下一次中断。

第 208 行

从中断返回。被中断的代码现在恢复正常运行，直到下一次中断的发生。

## 3.8 异步执行流

### 处理 x86 系统定时器中断

当中断被激活时（在我们的示例中，PIT 计数到 0 并激活了 IRQ0），中断控制器会激活一根进入处理器的中断线。`entry.S` 中的汇编代码有一个入口点，对应于 IDT 中的每个描述符。IRQ0 是第一个外部中断，向量 32，代码随后准备好跳转到 `entry.S` 跳转表中的第 32 号入口点。

```
arch/i386/kernel/entry.S
385 vector=0
386 ENTRY(irq_entries_start)
387 .rept NR_IRQS
388 ALIGN
389 1: pushl $vector-256
390 jump common_interrupt
391 .data
392 .long lb
393 .text
394 vector=vector+1
395 .endr
396
397 ALIGN
398 common_interrupt:
399 SAVE_ALL
400 call do_IRQ
401 jump ret_from_intr
```

这段代码是一段精妙的汇编魔法。重复结构 `rept`（位于第 387 行）及其结束语句（第 395 行）在编译时创建了中断跳转表。注意，此代码块被重复创建，由第 389 行推入堆栈的向量号会递减。通过推入向量，内核代码现在知道它在中断发生时正在处理哪一个 IRQ。

当我们停止对 x86 代码的追踪时，代码跳转到跳转表中正确的入口点并将 IRQ 保存到堆栈上。代码跳转到第 398 行的通用处理程序，并在第 400 行调用 `do_IRQ()`（`arch/i386/kernel/irq.c`）。该函数与 `ppc_irq_dispatch_handler()` 几乎相同，后者在“处理 PowerPC 外部中断向量”节中已描述过，因此我们在此不再重复。

根据传入的 IRQ，`do_irq()` 函数访问 `irq_desc` 的相应元素，并跳转到动作结构体链中的每个处理程序。在这里，我们终于到达了 PIT 的实际处理函数：`timer_interrupt()`。参见来自来自 `time.c` 的代码段。保持与源文件相同的顺序，该处理程序从第 274 行开始：

```
arch/i386/kernel/time.c
274 irqreturn_t timer_interrupt(int irq, void *dev_id, struct pt_regs *regs)
275 (

    287 do_timer_interrupt(irq, NULL, regs);
    ...
    290 return IRQ_HANDLED;
    )
```

这是系统定时器中断处理程序的入口点。

这是对 `do_timer_interrupt()` 的调用。

```
arch/i386/kernel/time.c
208 static inline void do_timer_interrupt(int irq, void *dev_id,
209 struct pt_regs *regs)
210 (

    227 do_timer_interrupt_hook(regs);
    ...
    250 )
```

```
include/asm-i386/mach-default/do_timer.h
016 static inline void do_timer_interrupt_hook(struct pt_regs *regs)
017 {
018     do_timer(regs);
    ...
025     x86_do_profile(regs);

030 )
```

## 第 18 行

这是调用 `do_timer()` 的地方。该函数执行更新系统时间的大部分工作。

## 第 25 行

`x86_do_profile()` 程序查看 `eip` 寄存器以获取中断前运行的代码。随着时间的推移，这些数据指示了进程运行的频率。

此时，系统定时器中断从 `do_irq()` 返回到 `entry.s` 进行系统维护，被中断的线程恢复。

正如之前讨论过的，系统定时器是 Linux 操作系统的心脏。虽然我们在本章中将定时器作为中断的示例，但它的用途贯穿整个操作系统。

## 总结
