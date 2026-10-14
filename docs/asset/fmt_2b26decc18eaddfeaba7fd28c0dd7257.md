
```
386 /* 此任务的 CPU 特定状态 */
387     struct thread_struct thread;
388 /* 文件系统信息 */
389     struct fs_struct *fs;
384 struct sem_undo *semundo;
385 struct sem_queue *semsleeping;
```

**图 2.13** `task_struct` 中的杂项信息

# 在 Linux 中表示进程

## 2.7 环境变量

图 2.14 所示的三个字段包含了关于进程状态的大量信息。

```
390 /* 打开文件信息 */
391 struct files_struct *files;
```

**图 2.14** 易变环境与输入输出

### 环境变量与输出

#### 第 380 行：`link_count`, `total_link_count`

解析当前文件名时遇到的递归符号链接数量存储在 `link_count` 中。连续符号链接的数量维护在 `total_link_count` 中。

#### 第 381 行：`tty`

`tty_struct` 代表分配给进程的终端。当终端打开时，与终端相关的所有状态都在这里。如果没有终端（例如是后台进程），则该字段为 NULL。注意这是一个指针字段；多个进程可以共享同一个终端。

#### 第 382 行：`locks`

此字段指示进程持有的文件锁数量。这些在进程终止时必须归还。

#### 第 384 行：`semundo`

`semundo` 字段指向 System V 信号量的列表，当此进程终止时，可能对它们进行撤销操作。

#### 第 385 行：`semsleeping`

当进程在 System V 信号量上挂起时，`semsleeping` 指向进程挂起的特定信号量等待队列。

### 第 387 行：线程

在 Linux 中，“task”（任务）”、“process”（进程）和“thread”（线程）这些术语之间没有本质区别。然而，源代码似乎需要“thread”这一标识符来处理特定架构细节。图 2.15 来自 `<asm-i386/processor.h>`，显示了用于 i386 架构的 `thread_struct`。它包含了进程进行上下文切换时必须保存的所有状态信息。上下文切换始终在内核态发生。在进入内核之前，大多数硬件寄存器的值已经保存。因此，通常该结构体包含了进程进入内核时未保存的某些寄存器的值，以及特定架构的信息。

```c
365 struct thread_struct {
366     unsigned long          esp0;
367     unsigned long          eip;
368     unsigned long          esp;
369     unsigned long          fs;
370     unsigned long          gs;
371
372     unsigned long          debugreg[8];
373
374     unsigned long          cr2, trap_no, error_code;
375
376     union i387_union      i387;
377
378     struct vm86_struct *vm86_info;
379     unsigned long          screen_bitmap;
380     unsigned long          v86flags, v86mode, saved_esp;
381     int                    ioperm;
382     unsigned long          io_bitmap[IO_BITMAP_SIZE+1];
383 };
```

**图 2.15** `thread_struct` 尽管声明为 `unsigned long`，但此字段实际上包含一个指向栈底（栈顶）的指针。在使用之前，它总是会被强制转换为特定数据类型的指针。这些是标准的 i386 寄存器。i386 架构有八个寄存器，当处理器在上下文切换期间发生异常时，会保存状态信息。

### 易变环境与输入输出

`CR2` 寄存器用于存储导致页错误的地址。通用中断处理程序将其正在处理的陷阱（trap）数量保存在 `trap_no` 中。浮点寄存器值会被保存。结构本身见图 2.16。这些字段仅当处理器因调用 `vm86()` 服务运行在 8086 模式时有效。这些字段的使用将在第 23.4 节中详细讨论。

`vm86_info` 是一个指向 `struct vm86_struct` 的指针，包含了在 vm86 模式下运行时所需的信息（见 24.1）。该字段中的每个位代表一个内存区域页。如果相应的页已调入，则该位被置位。`v86flags` 字段由 Linux 在 vm86 模式下管理（见 24.2）。`v86mask` 定义了处理器类型。`saved_esp` 字段用于在切换到 vm86 模式时保存 `esp0` 的副本。这些字段定义了该进程可以访问的 I/O 地址。书中将不再进一步讨论这些字段。

图 2.16 来自 `<asm-i386/processor.h>`，显示了用于存储 FPU 信息的的数据结构。不同模型 FPU 的不同格式在随后的图中描述。

```c
324 union i387_union {
325     struct i387_fsave_struct fsave;
326     struct i387_fxave_struct fxsave;
327     struct i387_soft_struct soft;
328 };
```

**图 2.16** 浮点寄存器值。标准 i387 FPU 需要保存的信息见图 2.17，来自 `<asm-i386/processor.h>`。

```c
282 struct i387_fsave_struct {
283     long cwd;
284     long swd;
285     long twd;
286     long fip;
287     long fcs;
288     long foo;
289     long fos;
290     long st_space[20];
291     long status;
292 };
```

**图 2.17** 标准 FPU 寄存器。FPU 的控制字寄存器保在这里。FPU 的状态寄存器保在这里。保在这里的标签字（tag word）指示哪些 FPU 寄存器包含有效数据。浮点指令指针是一个 48 位寄存器。32 位偏移量保存在 `fip` 中，16 位段选择符保存在 `fcs` 中。浮点操作数是一个 48 位寄存器。32 位偏移量保存在 `foo` 中，16 位段选择符保存在 `fos` 中。这涉及到保存八个浮点寄存器，每个宽度为 10 字节。

后期的 FPU 模型（如 Pentium 处理器中所示）更强大，需要保存更多的状态。图 2.18 来自 `<asm-i386/processor.h>`，显示了用于保存这些额外状态的数据结构。显然，它与之前的图有很多重叠。毕竟，这是该图的扩展。

```c
294 struct i387_fxave_struct {
295     unsigned short cwd;
296     unsigned short swd;
297     unsigned short twd;
298     unsigned short fop;
299     long fp;
300     long fcs;
301     long foo;
302     long fos;
303     long mxcsr;
304     long reserved;
305     long st_space[32];
306     long xmm_space[32];
307     long padding[56];
308 } __attribute__((aligned(16)));
```

**图 2.18** 扩展浮点单元寄存器。这些字段在上述描述了图 2.17 的第 286–289 行，但请注意它们现在是 `unsigned short`。这是合理的，因为它们只是 16 位的寄存器。执行的最后一个非控制指令的前两个字节存储在最后一个指令操作码寄存器中并保在这里。这些字段在上述描述了图 2.17 的第 286–289 行。

这是 `MXCSR` 寄存器，它为对 XMM 寄存器的操作提供了控制和状态位。八个 FPU 寄存器每个仍然是 10 字节宽，但为了更好地对齐，位于 16 字节边界上。还有 8 个 XMM 寄存器，每个 16 字节宽。这是为了未来的扩展。每个 `struct i387_fxave_struct` 都对齐在 16 字节边界。用于维护状态的结构见图 2.19。

```c
310     struct i387_fsave_struct fsave;
311     struct i387_fxave_struct fxsave;
312     struct i387_soft_struct soft;
313 };
```
