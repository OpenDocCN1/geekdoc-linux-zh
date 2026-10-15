
# 信号处理与栈空间调整

## 栈数据初始化

```c
put_fs(long)(current_blocked, tmp_esp++);
put_fs(long)(eax, tmp_esp++);
put_fs(long)(ecx, tmp_esp++);
put_fs(long)(flags, tmp_esp++);
put_fs(long)(old_eip, tmp_esp++);
current_blocked = sa->sa_mask;
```

tmp_esp = esp;

内核栈和用户栈的处理以及用户栈空间数据的调整如图 8.27 和 8.28 所示。

## 信号处理流程

信号预处理已完成，接下来将介绍系统调用返回后这些数据的使用方式，包括“信号处理函数执行”和“执行后的进程保护恢复”。

我们已在进程中将信号处理程序 `sig_user` 与进程处理函数绑定。`sig_user()` 函数执行后将执行 `ret` 指令，其本质是恢复存储在栈中的 EIP 值以恢复 EIP 寄存器，使执行跳转到 EIP 指向的地址。此时，栈顶函数地址值 `sa->sa_restorer` 将起作用，执行将跳转到 `sa->sa_restorer` 所代表的位置值。

如前所述，我们还将名为 `restorer` 的函数地址与 `siginfo[32]` 结构绑定。`restorer` 是一个库函数，通过 `signal()` 传递的实际参数。该库函数将在信号处理工作完成后恢复用户进程执行的“指令和数据”，最后跳转到用户程序的“中断位置”执行。

![](img/f661d64b7eb54840fcb4d65765a4e933_481_0.png)

**图 8.27** 调整前内核栈中保护位点数据及其意义。

![](img/f661d64b7eb54840fcb4d65765a4e933_481_1.png)

**图 8.28** 调整后内核栈中保护位点数据及其意义。

## restorer 函数实现

现在信号处理已经完成，`restorer` 函数开始工作。让我们来看看这个函数代码：

```assembly
.glob      sig_restore
.glob      masking_restore

sig_restore:
    add $4, $esp
    popl %eax      // do_signal() 函数之前在用户栈中最终设置的内容仅用于在此处通过 popl 恢复寄存器值
    popl %ecx
    popl %edx
    popfl
    ret

masking_restore:
    add $4, $esp
    call ssetmask
    add $4, $esp
    popl %eax      // do_signal() 函数之前在用户栈中最终设置的内容仅用于在此处通过 popl 恢复寄存器值
    popl %ecx
    popl %edx
    popfl
    ret
```

## do_signal() 函数分析

我们之前介绍了 `do_signal()` 函数调整了栈空间中的值。它在这里将发挥作用。让我们回顾一下下面所示的代码：

```c
// 代码源：kernel/signal.c
void do_signal(long signr, long eax, long ebx, long ecx, long edx,
    long fs, long es, long ds,
    long eip, long cs, long eflags,
    unsigned long * sa->esp, long ss)
{
    put_fs_long((long) sa->sa_restorer, tmp_esp++);
    put_fs_long(signr, tmp_esp++);
    if ((sa->sa_flags & NOMASK))
        put_fs_long((current->task)->blocked, tmp_esp++);
    put_fs_long(eax, tmp_esp++);
    put_fs_long(ecx, tmp_esp++);
    put_fs_long(edx, tmp_esp++);
    // ... 剩余部分
    put_fs_long(flags, tmp_esp++);
    put_fs_long(old_eip, tmp_esp++);
    current_blocked = sa->sa_mask;
}
```

`do_signal()` 函数调整了栈空间中的值。在此处，执行将跳转到 `sa->sa_restorer` 所代表的位置值。本节之前提到过，我们还将名为 `restorer` 的函数地址与 `siginfo[32]` 结构绑定。`restorer` 是一个库函数，它是通过 `signal()` 传递的实际参数。该库函数将在信号处理工作完成后恢复用户进程执行的“指令和数据”，最后跳转到用户程序的“中断位置”执行。

## 用户空间栈处理策略

在用户空间中，“用户栈”将发挥作用。信号处理后，执行将通过之前在用户空间备份的“指令和数据”返回到“中断位置”。这就是信号处理的策略。让我们来看看具体的实现：

```c
// 代码源：kernel/signal.c
void do_signal(long sign, long eax, long ebx, long ecx, long edx,
    long fs, long es, long ds,
    long eip, long cs, long eflags,
    unsigned long eop, unsigned long esp)
{
    if (sa->flags & SA_SIGRESTART)
        sa_handler = NULL;
    *(eip) = sa_handler; // 在“用户栈”中调整栈指针的位置，使其指向处理进程的信号处理过程 sig_user(esp)

    long len = (sa->flags & SA_NMASK); // 调整栈指针移动空间，使栈指针移动栈的内容，以便后续在用户栈中备份数据

    // 以下是写入数据，这些数据将用于用户栈
    put_fs(long)(sa->sa_restorer, tmp_esp++);
    put_fs(long)(sign, tmp_esp++);
    if (!(sa->flags & SA_NMASK))
        put_fs(long)(current_blocked, tmp_esp++);
    put_fs(long)(eax, tmp_esp++);
    put_fs(long)(ecx, tmp_esp++);
    put_fs(long)(flags, tmp_esp++);
    put_fs(long)(old_eip, tmp_esp++);
    current_blocked = sa->sa_mask;
}
```

tmp_esp = esp;

内核栈和用户栈的处理以及用户栈空间数据的调整如图 8.27 和 8.28 所示。
