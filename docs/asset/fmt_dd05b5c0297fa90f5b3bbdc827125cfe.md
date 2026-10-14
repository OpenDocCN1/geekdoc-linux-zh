
（注：代码块继续在下一页）

**图 18.32 从信号队列中移除项**

- 179 参数是信号号、指向排到该进程的信号列表头部的指针，以及指向一个将拷贝特定信号信息的 `struct siginfo` 结构体的指针。
- 181 只有当与此信号对应的位被设置时，才会执行函数体（即队列上存在该信号的实例）。这是一个健全检查；如果为假，说明出了问题，它会在第 224 行返回失败。有关 `sigismember()` 宏见第 17.2.1.2 节。
- 184 获取队列中第一项的间接指针。
- 185–189 遍历队列直到找到相应的项或到达末尾的 `NULL` 指针。
- 186–187 如果此项与提供的信号匹配，则停止。
- 188 否则，移动指针并尝试下一项。
- 194–200 这是当搜索了整个队列但未找到对应项的情况。这可能发生在信号入队时内存管理器耗尽了空间。`list->signal` 字段会被设置以记录信号的存在，但没有记录进一步的信息。
- 194 清除位图中表示该信号队列项的位。该函数见第 17.2.1 节。
- 195–199 在调用者期望接收该信号信息的 `siginfo` 字段中放入默认值。
- 195 这是搜索信号时唯一具有有效信息的行。
- 200 返回成功。该信号已发布，即使无法提供相关信息。由于没有队列项，因此跳过了内存释放代码。
- 202–224 如果找到了 `struct sigqueue`，则执行此代码。它负责取消链接并释放。
- 203–204 如果是列表中的最后一项，我们将尾指针指向其前驱。
- 207 将信息从 `struct sigqueue` 拷贝到调用者提供的 `siginfo_t`。该函数已在 18.1 节描述。
- 208 释放队列项。该函数是内存管理器的一部分，在此不考虑。
- 209 原子地减少全局队列信号计数（见第 17.2.6 节）。
- 212–218 只有当出队的项表示实时信号时，才会执行此代码块。
- 213–17 继续在队列中寻找相同信号的第二个实例。
- 214–215 如果此项匹配提供的信号，则停止。存在第二个信号实例，因此不清除该信号的位。`goto` 跳过了第 220 行的操作。
- 216 移动指针并尝试下一项。
- 220 如果不是实时信号，或未找到实时信号的第二个实例，清除位图中表示该信号队列项的位（见第 17.2.1）。
- 221 如果存在第二个实时信号实例，我们在掩码中保留该位。每个信号只有一个位。
- 222 这是成功值。
- 224 返回错误，根据位图（在 181 行测试），队列上没有对应此信号的项。

# 执行信号

当发现为特定信号注册了自定义处理器时，内核必须安排其运行。此类处理器在用户态运行，因此必须临时切换到用户态运行处理器，完成后回到内核。本章分为三个部分：首先，考虑主函数 `handle_signal()`。然后查看操作用户态栈的函数，以确保返回用户态后运行主程序。最后，检查在处理器完成后安排控制返回内核的函数。

## 19.1 处理信号

`arch/i86/kernel/signal.c` 中的图 19.1 显示了调用信号处理器的代码。它只在注册了自定义处理器时被调用；在 `SIG_IGN` 或 `SIG_DFL` 情况下永远不会调用。

```c
537 static void

538     handle_signal(unsigned long sig, struct k_sigaction*ka,
539     siginfo_t*info, sigset_t*oldset, struct pt_regs*regs)
540     {
541         if (regs->orig_eax >= 0) {
542             switch (regs->eax) {
543                 case -ERSTARTNOHAND:
544                     regs->eax = -EINTR;
545                     break;

547                 case -ERESTARTSYS:
```

```c
if (!(ka->sa.sa_flags&SA_RESTART)) {
    regs->eax = -EINTR;
    break;
    }

    /* fallthrough */
    case -ERESTARTNOINTR:
        regs->eax = regs->orig_eax;
        regs->eip = 2;
}
```

```c
if (ka->sa.sa_flags&SA_SIGINFO)
    setup_rt_frame(sig, ka, info, oldset, regs);
else
    setup_frame(sig, ka, oldset, regs);

if (ka->sa.sa_flags&SA_ONESHOT)
    ka->sa.sa_handler = SIG_DFL;

if (!(ka->sa.sa_flags&SA_NODEFER)) {
    spin_lock_irq(&current->sigask_lock);
    sigorssets(&current->blocked,current->blocked,&ka->sa.sa_mask);
    sigaddset(current->blocked,sig);
    recalc_sigpending(current);
    spin_unlock_irq(&current->sigask_lock);
}
```
