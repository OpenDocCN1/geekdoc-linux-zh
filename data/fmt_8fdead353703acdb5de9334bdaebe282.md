
```c
1062 int do_sigaltstack(const stack_t*uss, stack_t*uoss, unsigned long sp)
1064 {
1065 stack_t oss;
1066 error;
1067
1068 if (uss) {
1069 oss.ss_sp = (void*)current->sas_ss_sp;
1070 oss.ss_size = current->sas_ss_size;
1071 oss.ss_flags = sas_ss_flags(sp);
1072 }
1074 if (uss) {
1075 void* sp;
1076 size_t ss_size;
1077 int ss_flags;
1078
1079 error = -EFAULT;
1080 if (verify_area(VERIFY_READ, uss, sizeof(*uss))
1081 || __get_user(ss_sp, &uss->ss_sp)
1082 || __get_user(ss_flags, &uss->ss_flags)
1083 || __get_user(ss_size, &uss->ss_size))
1084 goto out;
1085
1086 error = -EPERM;
1087 if (on_sig_stack(sp))
1088 goto out;
1089 error = -EINVAL;
1090 if (ss_flags != SS_DISABLE)
    && ss_flags != SS_ONSTACK && ss_flags != 0)
1100 goto out;
1102 if (ss_flags == SS_DISABLE) {
1103 ss_size = 0;
1104 ss_sp = NULL;
1105 } else {
1106 error = -ENOMEM;
1107 if (ss_size < MINSIGTSKSZ)
1108 goto out;
1109 }
1111 current->sas_ss_sp = (unsigned long) ss_sp;
1112 current->sas_ss_size = ss_size;
1115 if (uoss) {
1116 error = -EFAULT;
1117 if (copy_to_user(uoss, &oss, sizeof(oss)))
1118 goto out;
1119 }
1121 error = 0;
```

图 17.34 切换到信号处理 `sigaltack` 结构，指定一个区域

- 1063 第一个参数，如果不为空，是指向用户空间中 `sigaltack` 的指针，在执行指定信号的处理器时作为栈。
- 第二个参数，如果不为空，指向 `sigaltack` 结构，其中返回调用之前任何备用栈的信息。
- 第三个是保存在内核栈上的 SP。
- 1068-1072 如果调用者通过传递值指针指定了要返回的状态信息，执行此代码代码。前两个值直接从进程的 `task_struct` 复制。它们保存在局部临时 `struct sigaltack` 中，因为在复制到用户空间之前可能会被覆盖。
- 1069 如果为空，这是指向之前设置的备用栈的指针。
- 1070 如果不为0，这是之前设置的备用栈的大小。
- 1071 该函数在第 17.6.3 节中描述。它返回关于之前设置的任何备用栈的状态信息。如果没有设置，将是 `SS_DISABLE`；如果进程在备用栈上执行，将是 `SS_ONSTACK`；如果设置了备用栈但当前未使用，它将为 0。
- 1074–1113 如果调用者提供了新备用栈的有效 `struct sigstack` 指针，执行此代码块。这是函数的内核。
- 1079–1084 如果从用户空间读取出现问题，我们返回 `EFAULT`。
- 1080 检查是否可以从用户空间的 `struct sigstack` 读取。函数是内存管理器的一部分；成功时返回 0。
- 1081–1083 将新 `struct sigstack` 的三个字段从用户空间复制到局部内核变量。`__get_user()` 函数是内存管理器的一部分；成功时返回 0。
- 1084 如果这四个函数中任何一个返回失败，条件为真，跳转跳转到第 1122 行，函数返回 `EFAULT`。
- 1086–1088 如果进程已经在备用栈上工作，我们返回 `EPERM`。该函数在第 17.6.3 节中描述。此测试可能从用户空间复制信息之前进行。
- 1090 这为下一段代码设置了默认返回值 `EINVAL`，该段是检查 `ss_flags` 字段的有效性。
- 1099–1100 此条件过滤掉用户 `ss_flags` 的这些值。这些是唯一的有效值；任何其他值如果返回 `EINVAL`。
- 1102–1104 如果设置了 `SS_DISABLE`（即这是一个取消请求栈的请求），则我们清空两个局部字段，无论用户提供了什么值。
- 1105–1109 由于第 1099–1100 行的过滤，此时 `ss_flags` 必须是 `SS_ONSTACK` 或 0。代码说为了向后兼容，不尝试区分 0 和 `SS_ONSTACK`。
- 1111–1112 在进程的 `task_struct` 中设置备用栈的基地址和长度的新值。注意由于 `task_struct` 的声明方式，`ss_sp` 必须强制转换为 `unsigned long`。
- 1115–1119 如果调用者提供了有效的 `sigaltack` 指针，则执行此代码块。第 1068–1072 行的临时副本被复制到用户空间。
- 1116–1118 如果我们无法将信息复制到用户空间，返回 `EFAULT`。`copy_to_user()` 函数是内存管理器的一部分，在此不再进一步考虑。
- 1121 这是成功值。

### 17.6.3

内核提供了两个函数，用于检查是否设置了备用信号栈。这些函数在图 17.35 中所示，来自 `<linux/sched.h>`。

```
678 static inline int on_sig_stack(unsigned long)
679 {
680     return (sp - current->sas_ss_sp < current->sas_ss_size);
681 }
682
683 static inline int sas_ss_flags(unsigned long)
684 {
685     return (current->sas_ss_size == 0) ? SS_DISABLE
686             : on_sig_stack(sp) ? SS_ONSTACK : 0);
687 }
```

图 17.35 检查备用信号栈

678 参数是栈指针的保存值。该函数检查在中断发生时栈指针的值是否位于备用栈区域内。

680 从当前栈指针中减去备用栈的基地址得到备用栈的偏移量，如果该值小于声明的备用栈大小，则进程正在此备用栈上操作，函数返回 TRUE；否则，它在主栈上工作。

683 参数是栈指针的保存值。这部分是在检查备用栈的状态。

685–686 如果备用栈声明的大小为 0，则表示未设置，我们返回 `SS_DISABLE`。如果已设置，则如果进程正在备用栈上操作，我们返回 `SS_ONSTACK`；否则返回 0。

## 信号的发送与递送

信号的处理清晰地分为两个部分。首先是信号的发送（posting）。这包含了发送端涉及的所有检查和处理。其最终结果是目标进程中的某些数据结构被修改，指示该信号处于“挂起”（pending）。在此阶段不采取任何操作。其次是信号的递送（delivery）。这在目标进程感知到挂起的信号并采取相应行动时发生。信号机制的这两个方面在本章中都得到了考虑。

## 18.1 发送信号

有很多函数以各种方式参与信号发送。首先是基础函数 `send_sig_info()`，我们将首先考虑它。它会调用许多辅助函数，随后将对这些函数进行描述。最后，还有专门用于发送信号的函数，面向特定的进程组或使用其他接口。这些函数最终都会调用 `send_sig_info()`。

### 18.1.1 带有额外信息的信号发送

生成信号的基本函数如图 18.1 所示，来自 `kernel/signal.c`。

```
503 int
504     send_sig_info(int sig, struct siginfo *info, struct task_struct *t)
505     {
506         unsigned long flags;
507         int ret;

513
514         ret = -EINVAL;
```
