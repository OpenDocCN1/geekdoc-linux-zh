
**图 19.1 调用信号处理器**

- 538–539 代码传递了信号号、指向指定该信号处理器的 `k_sigaction` 指针、指向包含该信号信息的 `siginfo_t` 指针、指向进程阻塞位图的指针以及指向 `pt_regs` 指针（包含栈上保存的寄存器值）。
- 542–545 只有当 `pt_regs` 中的 `orig_eax` 存在有效的系统调用号时，才会执行此代码。这意味着进程在系统调用过程中被信号中断了。
- 544 当进程调用阻塞的系统服务时，它会被放入 `TASK_INTERTIBLE` 或 `TASK_UNINTERTIBLE` 状态。如果向 `TASK_INTERTIBLE` 状态的进程发送信号，它会被唤醒并移动到运行队列，即使系统服务尚未完成。在这种情况下，当系统服务再次运行时，尽管尚未完成但已被信号识别，它会在栈上的 `EAX` 副本中放入一个错误值。

# 处理信号

545–547 如果内部代码为 `RESTARTNOHAND`，返回值将更改为 `EINTR`。系统将不会重启。

549–553 如果是 `ERESTARTSYS`，系统调用是否重启取决于 `struct k_sigaction` 结构中 `SA_RESTART` 标志的值。如果该位被设置，我们保持返回值为 `ERESTARTSYS` 并跳转到下一个 `case`。系统调用将在稍后重启。注意 `break` 语句位于 `if` 块内部。否则，我们将返回值改为 `EINTR` 并跳出 `switch` 语句；系统调用将不会重启。

555–557 系统调用将要重启，我们将 `orig_ax` 中的系统调用号恢复到 `EAX`，并将保存的指令指针回退两个字节。为了调用系统服务，在用户模式下执行的最后一条指令必须是 `INT 0x80`，或者机器码中的 `EC CD 80`。这使得 `EIP` 寄存器指向 `0x80` 之后的下一条指令，而这就是保存在内核栈上的 `EIP` 值。将此值减 2 意味着它现在指向 `0xD` 指令。当控制权返回用户模式时，在处理完所有待处理信号后，这些来自（内核）栈的值将恢复到硬件寄存器中，因此在返回用户模式后执行的下一条指令将是 `0x80` 或 `INT 0x80`，且 `EAX` 中包含系统调用，以重复对系统服务的请求。

562–566 为用户的信号处理程序设置栈帧。如果设置了 `SA_SIGINFO` 标志，则用户愿意使用 `siginfo_t` 结构中可能关于此信号的任何额外信息。虽然在每情况下调用了不同的函数来设置栈，但它们都安排了处理器在用户模式下运行并返回内核。这可能是信号处理中最复杂的部分。记住，在此阶段进程运行在内核模式下。信号处理器是一个用户定义的函数，必须在用户模式下运行，进程必须切换到用户模式、运行处理器，然后切换回内核模式。这就像是系统调用在执行时切换到内核模式的镜像。目前没有一种优雅的方法来实现这一点。当信号处理器结束时，它必须返回到内核以及定义它的用户程序。这意味着要修改用户模式栈上的返回地址，特别是 `setup_frame()` 函数（见第 19.3.1 节）正是负责此的，它在用户栈上设置了一个栈帧。`setup_frame()` 函数构建了一个更为复杂的栈帧，用于处理 `struct siginfo_t` 中的额外信息（见第 19.3.2 节）。

567–568 如果用户在注册信号时设置了 `SA_ONESH` 标志，我们将处理器更改为未来该信号发生时的默认值 `SIG_DFL`。

570–570 `SA_NODEFER` 标志意味着在运行此信号的处理器时，如果它被屏蔽，则不应阻塞额外的信号，因此只有当该位被清零且有一些额外的信号需要阻塞时，我们才会进入代码块。当前进程的阻塞位图在 `sigmask_lock` 自旋锁的保护下进行操作。

572 `sa_mask` 是一个位域，指定了在处理某个信号时应该阻塞的任何额外信号。第 17.2.2 节描述的 `sigsets()` 宏在 `blocked` 字段和 `sa_mask` 字段之间进行位或运算并将结果放入其中。实际上，这意味着 `sa_mask` 中设置的任何位在 `blocked` 中设置，无论它们之前是否被设置过。

正在处理的信号对应的位会在 `blocked` 中设置。该函数已在第 17.2.1.1 节中描述。信号在处理期间始终是被阻塞的。

此函数已在第 18.3.2 节中描述。阻塞位图刚刚被修改，因此需要重新评估进程的信号状态。

## 19.2 信号处理的栈帧

正如第 17 章所述，信号处理器必须在用户模式下运行，并在终止时返回内核模式。这种不规则的控制传递通过预先在用户模式栈上设置特殊值来实现。该栈帧的结构是本节的主题。这种结构实际上是如何构建的将在 19.3 和 19.4 节中描述。

### 19.2.1 栈帧的结构

在用户栈上构建的帧结构如图 19.2 所示，源自 `arch/i386/kernel/signal.c`。它既可以在普通用户模式栈上构建，也可以在备用栈上构建，如第 17.6 节所述。

```c
166 struct sigframe
167 {
168     char *precode;
169     int sig;
170     struct sigcontext sc;
171     struct _fpstate fpstate;
172     unsigned long extramask[_NSIG_WORDS-1];
173     charretcode[8];
174 };
176 struct rt_sigframe
177 {
178     char *precode;
179     int sig;
180     struct siginfo *pinfo;
181     void *puc;
182     struct sigcontext sc;
183     struct siginfo *pinfo;
184     struct ucontext uc;
185     char retcode[8];
186     struct _fpstate fpstate;
187 };
```

图 19.2 栈帧的结构（注：提供的结构体定义文本是碎片化的，上述内容反映了标准的 Linux 内核结构）。

166–174 这是旧式帧。
168–179 这是新式帧。

### 用于信号处理的栈帧

```c
struct ucontext {
    unsigned long uc_flags;
    struct ucontext *uc_link;
    stack_t uc_stack;
    struct sigcontext uc_mcontext;
    sigset_t uc_sigmask;
};
```

**图 19.4** 信号处理程序的扩展上下文信息

- 5 此字段目前未使用。它由创建扩展栈帧的函数 `setup_rt_frame()` 设置为 0（见第 19.3.2 节）。
- 6 此字段目前也未使用。它由 `setup_rt_frame()` 设置为 0 (NULL）（见第 19.3.2 节）。
- 7 `sig_t` 在第 17.6.1 节中定义。它包含了关于正在使用的栈的信息，作为其指针、标志和大小。
- 8 这是旧式的 `sigcontext` 结构（见第 19.2.2 节）。
- 9 此字段包含当前进程的阻塞位图。它是一个完整的 `sigset_t`（第 17.1.1 节），而不仅仅是一个 `unsigned long`。

### 19.2.4 浮点状态

如果进程使用了浮点单元（FPU），则 FPU 寄存器的状态也会提供给信号处理程序。用于这些的结构如图 19.5 所示，来自 `<asm-i386/sigcontext.h>`。

```c
struct_fpreg {
    unsigned short signific[4];
    unsigned short exponent;
};

struct_fpxreg {
    unsigned short signific[4];
    unsigned short exponent;
    unsigned short padding[3];
};

struct_xmmreg {
    unsigned long element[4];
};

struct_fpstate {
    unsigned long cw;
    unsigned long sw;
    unsigned long tag;
    unsigned long ipoff;
    unsigned long cssel;
    unsigned long dataoff;
    unsigned long datasel;
    struct_fpreg _st[8];
    unsigned short status;
    unsigned short magic;
    unsigned long _fxsr_env[6];
    unsigned long mxcsr;
```
