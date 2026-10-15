
## 3.8 异步执行流

第 81–84 行

函数调用 `setup_irq(0, &irq0)` 将包含处理函数 `timer_interrupt()` 的 `irq` 结构体放入与 `irq0` 关联的共享中断队列中。

这段代码的作用与为通用处理程序调用 `request_irq()` 类似（那些未在内核初始化时加载的处理程序）。定时器中断的初始化代码通过一种快捷方式将处理程序直接放入 `irq_desc{ ...}`。运行时代码在 `irq.c` 中使用了 `disable_irq()`、`enable_irq()`、`request_irq()` 和 `free_irq()`。这些程序都是处理 IRQ 的工具程序，并在某一点访问 `irq_desc` 结构体。

## 中断时间

对于 PowerPC 而言，递减器是处理器内部的，并且在 `0x900` 处有自己的中断向量。这与 x86 架构形成对比，在 x86 中，PIT 是来自中断控制器的外部中断。PowerPC 的外部控制器位于向量 `0x500`。如果系统定时器基于本地 APIC，x86 架构也会类似的情况。

表 3.10 和 3.11 分描述了 x86 和 PPC 架构的中断向量表。

### 表 3.10

x86 中断向量表

| 向量数/IRQ | 说明 |
| :--- | :--- |
| 0 | 除错 (Divide error) |
| 1 | 调试扩展 (Debug extension) |
| 2 | 非掩器中断 (NMI interrupt) |
| 3 | 断点 (Breakpoint) |
| 4 | INTO 检测的溢出 |
| 5 | 范围越界 (BOUND range exceeded) |
| 6 | 无效指令 (Invalid opcode) |
| 7 | 设备不可用 (Device not available) |
| 8 | 双重故障 (Double fault) |

#### 表 3.10 续

| 向量数/IRQ | 说明 |
| :--- | :--- |
| 9 | 协处理器段溢出（预留） |
| 10 | 无效任务状态段 |
| 11 | 段不存在 (Segment not present) |
| 12 | 栈故障 (Stack fault) |
| 13 | 一般保护 (General protection) |
| 14 | 页面异常 (Page fault) |
| 15 |（Intel 预留。请勿。） |
| 16 | 浮点数错误 |
| 17 | 对齐检查 (Alignment check) |
| 18 | 机器检查 (Machine check*) |
| 19–31 |（Intel 预留。请勿。） |
| 32–255 | 可掩码中断 |

### 表 3.11

PPC 中断向量偏移量

| 偏移量（十六进制） | 中断类型 |
| :--- | :--- |
| 00000 | 预留 |
| 00100 | 系统重置 (System reset) |
| 00200 | 机器检查 (Machine check) |
| 00300 | 数据存储 (Data storage) |
| 00400 | 指令存储 (Instruction storage) |
| 00500 | 外部 (External) |
| 00600 | 对齐 (Alignment) |
| 00700 | 程序 (Program) |
| 00800 | 浮点数不可用 |
| 00900 | 递减器 (Decrementer) |

#### 表 3.11 续

| 偏移量（十六进制） | 中断类型 |
| :--- | :--- |
| 00A00 | 预留 |
| 00B00 | 预留 |
| 00C00 | 系统调用 (System call) |
| 00D00 | 跟踪 (Trace) |
| 00E00 | 浮点辅助 (Floating point assist) |
| 00E10 | 预留 |
| ... | ... |
| 00FFF | 预留 |
| 01000 | 预留，具体实现相关 |
| ... | ... |
| 02FFF |（中断向量位置结束） |

注意这两种架构之间的相似性。这些表代表硬件。Intel 异常中断向量表的软件接口是本章之前提到的中断描述符表 (`IDT`)。

随着我们的进行，我们可以看到 Intel 架构如何通过 IRQ 处理硬件中断：跳转到 `entry.s` 中的一个跳转表，然后跳转到调用门（描述符），最后才执行到处理程序代码。图 3.19 说明了这一点。

![](img/6525157588f931c50a65c5a42af9a432_192_0.png)

## 第 3 章 进程：执行的主要模型

相反，PowerPC 向量到内存中的特定偏移量，那里存在跳转到相应处理程序的代码。正如我们接下来看到的，`head.S` 中的 PPC 跳跃表是通过在内存中固定的方式进行索引的。图 3.20 说明了这一点。

![](img/6525157588f931c50a65c5a42af9a432_193_0.png)

图 3.20
PPC 中断流

当我们探索 PPC 外部（偏移量 `0x900`）和定时器（偏移 `0x500`）中断处理程序时，这将变得更加清晰。

## 处理 PPC 外部中断向量

如前所述，当发生外部中断时，处理器会跳转到地址 `0x500`。对 `head.S` 文件中的 `EXCEPTION()` 宏进行进一步研究，我们可以看到以下代码被链接并加载，它映射到偏移量 `0x500` 处的此内存区域。该架构跳转表与 x86 `IDT` 具有相同的效果：

```
arch/ppc/kernel/head.S

453     /* 外部中断 */

454     EXCEPTION(0x500, HardwareInterrupt, do_IRQ, EXC_FER_LITE)
```

```
arch/ppc/kernel/irq.c

510     void do_IRQ(struct pt_regs *regs)

511     {

512     int irq, first = 1;

513         irq_enter();

523         while ((irq = ppc_get_irq(regs)) >= 0) {

524             ppc_irq_dispatch_handler(regs, irq);

525             first = 0;

526

527     if (irq != -2 && first)

528     /* 非 SMP 安全的 */

529             ppc_spurious_interrupts++;

530         irq_exit();

531 }
```

第 513–530 行：指示抢占代码处于硬件中断。

第 523 行：从中断控制器读取等待中断并转换为 IRQ 号。

第 524 行：`ppc_irq_dispatch_handler()` 处理中断。我们详细查看此函数。`ppc_irq_dispatch_handler()` 函数与 x86 的 `do_irq()` 函数几乎相同：

```
arch/ppc/kernel/irq.c

428 void ppc_irq_dispatch_handler(struct pt_regs *regs, int irq)

429 {

430     int status;

431     struct irq_action *action;

432     irq_desc_t *desc = irq_desc + irq;

433

434     atomic_this_cpu_irqs(irq)++;

435     spin_lock(&desc->lock);

436     ack_irq(irq);

..

441     int status = desc->status & ~(IRQ_REPLAY | IRQ_WAITING);

442     if (!(status & IRQ_CPU))

443         status = IRQ_PENDING; /* 我们想要处理它 */

..

449     action = NULL;

450     if (likely(status & (IRQ_DISABLED | IRQ_INPROGRESS))) {

451         action = desc->action;

452         if (action && !action->handler) {

453             ppc_spurious_interrupts++;

454             printk(KERN_DEBUG, "Unhandled interrupt %x,%d\n", irq);

455             /* 我们不能在这里禁用中断，会导致死锁 */

456             ++desc->depth;
```
