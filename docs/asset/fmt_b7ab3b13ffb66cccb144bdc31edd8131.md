
如果中断发生前处理器处于虚拟 8086 模式，则有额外工作要做。这段代码在第 224 行。

此操作的效果是将 `EDX` 寄存器清零。这是为调用 `do_signal()` 准备第二个参数。

`do_signal` 函数的原型在 `arch/i386/kernel/signal.c` 中给出：

```
asmlinkage int FASTCALL(do_signal(struct pt_regs *regs,sigset_t *oldset));
```

`FASTCALL` 宏在 `<linux/kernel.h>` 中定义为：

```
#define FASTCALL(x) __attribute__((regparam(3)))
```

这意味着 `do_signal()` 具有 `regparam(3)` 属性，也就是说编译器通过 `EAX`、`EDX` 和 `ECX` 传递三个整数。由于在第 217 行将 `ESP` 拷贝到 `EAX`，第一个参数是栈指针，解释为指向 `struct pt_regs`。这是合理的，因为最后入栈的是寄存器，其格式由 `struct pt_regs` 指定。由于 `EDX` 在第 219 行被清零，第二个参数为 0，解释为指向 `sigset_t`，因此这是一个空指针。函数不期望第三个参数，因此 `ECX` 中的值是无关的。`do_signal()` 函数本身在第 18.4.1 节中描述。

这把控制权交回返回路径 `restore_all`，回到图 10.32 的第 210 行。

此宏在第 1.2.2.1 节中描述过。

如果在中断发生时处理器运行在 8086 模式下，会出现复杂情况。

`save_v86_state()` 函数来自第 24.8.2 节，顾其名。它被定义为 `FASTCALL`，调用一个参数，指向 `struct kernel_vm86_regs` 的指针。该指针在 `EAX` 中，实际上，栈指针已经在那里了。它从栈上拷贝值到线程结构的 `vm86_info` 字段中。整个虚拟 8086 模式区域将在第 23.4 节中处理。

# 从中断中返回

227–229 这些代码与保护模式下的代码相似，位于第 219–221 行。

## 10.6.4 重新调度当前进程

如果当前进程在中断后无法继续，则执行图 10.36 中的代码，来自 `entry.S`。

```
258 reschedule:
259 call SYMBOL_NAME(schedule)
260 jmp ret_from_sys_call
```

**图 10.36** 当前进程需要重新调度

258 如果当前进程需要重新调度，我们从图 10.32 的第 207 行跳转到这里。

259 `schedule()` 函数是主调度器，如第 7.3 节所述。

260 当进程下次发生上下文切换时，会执行此跳转（见第 10.6.1 节）。

## 10.6.5 总结

整个 10.6 节的控制流如图 10.37 所示。项目符号（●）表示三种可能的入口点。只有一个出口，`restore_all`。

![](img/f8d94a0b5fe7abf9dfdff7fa0c4ae5f1_326_0.png)

**图 10.37** 从中断处理退出的路径

# 11 异常处理器

上一节检查了 CPU 可能产生的各种异常的第一级处理器。本节将检查 Linux 内核为这些异常中的每一个所提供的二级处理器。

异常处理器的通用模式是：查询硬件以尽可能多地获取有关异常原因的信息。它这样做是为了（如果可能的话）从导致异常的任何故障中恢复。最后，它会向产生异常发生时正在运行的进程发送一个信号，并传回从硬件处获取的信息。这使得用户进程如果注册了适当的信号处理程序，就有了自行进行处理的选择。

这些异常中有 12 个的二级处理非常简陋，以至于对它们使用了几乎相同的代码。这些代码是由许多参数化宏生成的。本节将首先查看这 12 个“简单”异常的处理器。本节的其余部分将处理其他 8 个异常。

## 11.1 生成通用异常处理器

如前所述，许多异常所需的二级处理非常相似，因此开发者采取了捷径，使用宏来生成这些处理器。本节将检查它们是如何生成的以及它们的作用。

### 11.1.1 生成处理器

单独的二级异常处理器是通过使用多个宏生成的。图 11.1 来自 `arch/i386/kernel/traps.c` 显示了涉及的 12 个处理器。这里需要记住的第一点是，这些并不是宏定义；这些每一行都会被预处理器展开为完整的宏代码，因此如果你检查预处理器输出的代码，你会发现每一个处理器都对应一个 C 函数。

```
338 DO_VM86_ERROR_INFO(0, SIGFPE, "divide error", divide_error,
    FPE_INTTDIV, regs->eip)
339 DO_VM86_ERROR(3, SIGTRAP, "int3", int3)
340 DO_VM86_ERROR(4, SIGSEGV, "overflow", overflow)
341 DO_VM86_ERROR(5, SIGSEGV, "bounds", bounds)
342 DO_ERROR_INFO(6, SIGILL, "invalid operand",
ILL_ILLLOPON, regs->eip)
343 DO_VM86_ERROR(7, SIGSEGV, "device not available",
device_not_available)
344 DO_ERROR(8, SIGSEGV, "double fault",
double_fault)
345 DO_ERROR(9, SIGFFPE, "coprocessor segment overrunning",
coprocessor_segment_overrun)
346 DO_ERROR(10, SIGSEGV, "invalid TSS", invalid_TSS)
347 DO_ERROR(11, SIGBUS, "segment not present",
segment_not_present)
348 DO_ERROR(12, SIGBUS, "stack segment", stack_segment)
349 DO_ERROR_INFO(17, SIGBUS, "alignment check",
alignment_check, BUS_ADRALN, cr2(2))
```

**图 11.1** 生成中断处理器的宏

正如稍后提到的，每个宏生成的代码本质上是向当前进程发送一个信号。传递给宏的参数决定了将发送的信号。

- 第一个参数是异常编号。它最终会进入 `thread` 中的 `trap_no` 字段。
- 第二个参数是要发送给当前进程的信号。
- 第三个参数是错误消息。如果内核必须终止进程，该消息将输出到控制台。
- 第四个参数是赋给生成的函数的特定名称部分。全名将始终是 `do_name()` 形式。

在第 338、342 和 349 行有两个额外参数。在这些情况下，处理器使用扩展信号机制向信号处理程序传回额外信息。这两个参数提供了这些额外信息，这些信息被复制到传递给信号处理器的 `siginfo_t` 结构中。关于信号的相关背景，请见第 17 节。
