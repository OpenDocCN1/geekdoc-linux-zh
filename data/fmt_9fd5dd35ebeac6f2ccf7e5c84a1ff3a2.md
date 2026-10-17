
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

### 11.1.2 生成处理器

有四个不同的生成宏显示在图 11.1，我们将轮流考虑它们。

#### 11.1.2.1 发送信号

最简单的生成宏位于图 11.2，来自 `arch/i386/kernel/traps.c`。它具有四个参数：异常的编号、发送给处理器的信号、输出到处理器的错误消息以及函数名称。该宏的作用是生成一个名为 `do_name` 的 C 函数，它和所有处理器一样接收一个 `struct pt_regs` 指针和一个错误代码。

```
304 #define DO_ERROR
```

**图 11.2** 发送信号的包装器

当 `do_trap()` 返回时，它跳转回第一级处理器，位于第 291 行（见第 10.5 节）。如图 11.1 所示，该宏用于异常 8、9、10、11 和 12。

#### 11.1.2.2 发送额外信息

稍微复杂的生成宏版本位于图 11.3，来自 `arch/i386/kernel/traps.c`。它包含了设置 `siginfo_t` 结构字段并将该结构传递给 `do_trap()`。

```
310 #define DO_ERROR_INFO
```

**图 11.3** 发送额外信息的包装器

#### 11.1.2.3 在 86 模式发生的异常

在 86 模式发生的异常生成宏位于图 11.4，来自 `arch/i386/kernel/traps.c`。

```
321 #define DO_VM86_ERROR
```

**图 11.4** 在 86 模式发生的包装器

### 11.1.3 通用处理器函数

上一节描述的四个宏中的每一个都生成一个存根，通过调用通用处理器 `do_trap()` 实现；见图 11.5，来自 `arch/i386/kernel/traps.c`。

```
269 static void inline do_trap(int trapnr, int signr, char *str,
270     int vm86 struct pt_regs *regs, long error_code,
271     siginfo_t *info)
272 {
273     if (vm86 && regs->eflags & VM_MASK)
274         goto vm86_trap;
275     if (!((regs->xcs & 3))
276         goto kernel_trap;
277 
278     trap_signal:{
279         struct task_struct *tsk = current;
280         tsk->thread.error_code = error_code;
281         tsk->thread.trap_no = trapnr;
282         if (info)
283             force_sig_info(signr, info, tsk);
284         else
285             force_sig(signr, tsk);
286             return;
287 }
```

# 生成通用异常处理程序

```c
kernel_trap: {
    unsigned long fixup=search_exception_table (regs->eip);
    if (fixup)
        regs->eip = fixup;
    else
        die(str, regs, error_code);
    return;
}

vm86_trap: {
    int ret=handle_vm86_trap((struct kernel_vm86
        *regs),error_code, tapnr);
    if (ret) goto trap_signal;
    return;
}
```

图 1.5 通用异常处理程序

通用函数的缺点是它们通常需要大量的参数，这一个也不例外。它传递了：

- 正在处理的异常编号；
- 要发送给中断进程的信号编号；
- 一个错误消息字符串的指针；
- 一个指示该特定异常是否可以在 vm86 模式下发生的标志（1）或否（0）；
- 指向栈上保存的寄存器值的指针；
- 错误代码；
- 一个 `siginfo_t` 结构体的指针；如果为 NULL，它包含了处理信号的扩展信息。

如果 `vm86` 参数为 1 且发生了中断，则会在第 297 行执行 vm86 异常的特殊代码。

在内核模式选择器中，低两个位始终为 0。这用于测试在发生中断时，计算处理器（CPU）是否运行在内核模式。如果是，则会在第 288 行执行内核的特殊代码。

这是函数的体，即默认的异常处理程序。

这获取当前进程的 `task_struct` 指针。

这些根据传递给此函数的参数，填充线程结构中的错误代码和异常编号字段。

281–284 这些代码将 `signr` 参数指定的信号发送给当前进程。这使用了 `force_sig_info()`（第 18.2.1 节）或 `force_sig()`（第 18.2.7 节），取决于是否通过 `info` 参数提供了额外信息。

285 无论信号如何递送，我们都会返回二级异常处理程序，即调用 `do_trap()`。

288–295 如果在发生异常时 CPU 运行在内核模式，则执行此代码块。在这种情况下，不会发送信号。因为在内核模式下，用户级进程对此一无所知，无法期望它进行处理。

289 这检查在内核代码在此处发生异常的预定义修复代码（fixup）。由于此表由内存管理器维护，我们在这里不再进一步考虑它。

290–291 如果存在此类修复代码，则打印 `str` 参数传递的行和消息、栈保存的寄存器值以及错误代码。有关 `die()` 函数，请参见第 11.10.4 节。

292–293 否则，进程将被杀死，并打印 `str` 参数传递的消息、栈保存的寄存器值以及错误代码。有关 `die()` 函数，请参见第 11.10.4 节。

294 只有在可以修复问题时才会到达此行。它返回二级处理程序，从而返回一级处理程序，但保存在栈上的是修改过的 EIP 值。

297–301 如果中断是可以在 vm86 模式下发生的，且在发生中断时 CPU 运行在 vm86 模式，则执行此代码块。

298 此特殊处理程序在第 24.5 节中描述。
