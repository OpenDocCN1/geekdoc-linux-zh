
图 19-5：`audit_log_start` 的代码流图。

基本上，`audit_log_start` 的工作是设置缓冲区并将其返回给调用者。`backlog`（即存储审计记录的队列）的最大长度由全局变量 `backlog` 给出。如果超过此限制，则将丢弃消息。

修正后的 `audit_log_start` 逻辑描述：
`audit_log_start` 的工作是设置缓冲区并将其返回给调用者。`backlog`（即存储审计记录的队列）的最大长度由全局变量 `backlog` 给出。如果超过此限制，则将丢弃消息。

### 写入消息

`audit_log_format` 用于向审计缓冲区写入消息。该函数的原型如下：

```c
kernel/audit.c
void audit_log_format(struct audit_buffer *ab, const char *fmt, ...)
```

正如原型所示，`audit_log_format` 类似于 `printk` 的变体。填充 `fmt` 中的字符串并将生成的字符串写入审计缓冲区。

### 关闭审计日志

在必要的日志消息写入审计缓冲区后，需要调用 `audit_log_end` 以确保审计日志发送到用户态守护进程。该函数的代码流图见图 19-6。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_1142_0.png)

在执行另一个速率检查后（如果提交消息过于频繁），与审计缓冲区关联的套字字放入队列供 `kaudit` 处理。

```c
kernel/audit.c
void audit_log_end(struct audit_buffer *ab)
{
    struct nlmsghdr *nlh = (struct nlmsghdr *)ab->data;
    nlh->msg_ien = skb->len - NLMS_SPACE(0);
    skb_queue_tail(&audit_skb_queue, ab->skb);
    ab->skb = NULL;
    wake_up_interruptible(&kaudit_wait);
}
```

注意，内核提供了便利函数 `audit_log`，它可以作为上述三个任务（启动审计日志、写入消息和结束日志）的缩写。它的原型为：

```c
audit.h
struct audit_buffer *audit_log_start(struct audit_context *ctx,
    gfp_t gfp_mask, int type,
    const char *fmt, ...);
```

## 19.3.5 系统调用审计

到目前，系统调用审计所需的数据结构和机制已经描述，因此本节继续描述实现。系统调用审计与基础机制不同，因为它依赖在前节中引入的任务结构扩展——审计上下文。

### 审计上下文分配

首先，你需要考虑在什么情况下分配上下文。由于这是一项开销较大的操作，只在显式启用系统调用审计时才会执行。

如果是这种情况，`copy_process`（即源自 `fork` 系统调用）是调用 `audit_alloc` 来分配新的 `struct audit_context` 实例的地方。图 19-7 显示了 `audit_context` 的代码流图。

![](img/a80e0e530e25bf9e2df2fc130fff42a2_1143_0.png)

图 19-7：`audit_context` 的代码流图。

首先，`audit_filter_task` 决定当前任务是否需要激活系统调用审计。如果完全禁用了系统审计，甚至不会立即调用 `audit_alloc`。该函数分配类型为 `AUDIT_FILTER_TASK` 的注册过滤器。如果判定结果为 `AUDIT_DISABLED`，`audit_alloc` 可以直接返回，而不分配 `audit_context` 实例，因为不需要系统调用（审计代码的其他部分可以轻松检查这一点——在这种情况下 `task_struct` 中的 `audit_context` 元素保持为空指针）。

如果需要系统调用审计，`audit_alloc_context` 会分配一个新的 `audit_context` 实例。运行时会将该实例的状态设置为由过滤器操作给定的状态。

最后，内核按照如下方式保留运行任务的 UID（这对于创建审计轨迹是必要的，因为 UID 在 fork 过程中需要被保留）：

```c
kernel/auditsc.c
int audit_alloc(struct task_struct *tsk)
{
    /* Preserve login uid * */
    context->loginuid = -1;
    if (current->audit_context)
        context->loginuid = current->audit_context->loginuid;
    tsk->audit_context = context;
    set_tk_thread_flag(tsk, T_TIF_SYSCALL_AUDIT);
    return 0;
}
```

此外，在属于进程的 `task_struct` 中设置了 `T_TIF_SYSCALL_AUDIT` 标志。这对于底层中断处理代码在中断进入或其他处理结束时调用审计函数是必要的——出于性能考虑，这一步将被跳过。

注意，由于 `audit_alloc` 源自 `fork` 系统调用，关于是否启用系统调用审计的决策会在进程创建自己的副本时都做出。这确保了系统中的每个任务都执行了检查。

## 第 19 章：审计

### 系统调用事件

当进入系统调用和系统调用结束时，审计子系统会参与其中——在两种情况下都会调用 `audit_syscall_exit`。为了实现这一点，需要底层特定于架构的中断处理代码的支持。这种支持集成在 `do_syscall_trace` 中，每当发生中断或处理完成时，底层中断处理代码都会调用它。对于 IA-32 架构，实现方式如下：

```c
arch/x86/kernel/ptrace_32.c
__attribute__ (regparm(3))
int do_syscall_trace(struct pt_regs *regs, int entryexit)
{
    if (unlikely(current->audit_context) && entryexit)
        audit_syscall_entry(current, AUDIT_ARCH_I386, regs->orig_eax,
        regs->dbx, regs->ecx, regs->edx, regs->esi);
    if (unlikely(current->audit_context))
        audit_syscall_exit(current, AUDITSC_RESULT(regs->eax),
        regs->eax);
}
```
