
每个进程还可能拥有一个与其关联的 `struct sigcount`，由 `proc` 结构中的字段 `p_p_sigcountp` 指向。`sigcount` 结构用于跟踪进程有多少个未决信号——即已发送但尚未接收的信号。此结构仅用于通过 `sigqueue()` 系统调用发送的信号，该系统调用允许发送方在信号中附带数据。`kill()` 系统调用不使用 `sigcount` 结构。系统中存在一个这些结构的池，保留在空闲列表中。当进程发送信号时，从池中取出一个 `struct sigcount` 并附加到该进程。当最后一个信号被接收时，该结构被返回到池中。之所以它是一个独立的结构而不是仅仅在 `proc` 结构中的一个计数器，是因为进程可能发送了一个信号，然后在信号被接收之前退出。这为我们提供了已发送信号的持久记录。清单 14.3 是 `sigcount` 结构。

### 清单 14.3 sigcount 结构

```c
typedef struct sigcount {
    unsigned int    sc_count:16; /* sigs queued sent by this process and pending at a receiver */
    sc_owner_state_t sc_owner_state:1;
    unsigned int    sc_unused:7;
    unsigned int    sc_cookie:8; /* DS ID token */
    struct sigcount *sc_next;   /* for freelist management */
} sigcount_t;
```

除了 `sigcount` 结构之外，使用 `sigqueue()` 发送的信号还需要一个地方来存储随信号发送的数据。出于与 `sigcount` 相同的原因，这些信息必须位于 `proc` 结构之外——它必须在进程终止后仍然存在。保存此数据的结构是 `struct __ksi`，或称为 `ksi_t`。更有趣的字段包括指向与该数据关联的 `sigcount` 结构的指针、信号编号、信号的原因（用户生成、定时器生成、I/O 完成等）、可以与信号关联的 `errno`，以及两个数据字段。第一个字段 `si_value` 由 `sigqueue()` 系统调用使用。当用户使用 `sigqueue()` 发送信号时，他或她可以指定一个随信号发送的值。第二个数据字段是一个名为 `__data` 的大型联合，根据信号编号包含各种信息。一些示例是 `SIGSEGV` 或 `SIGBUS` 的故障地址，或者子进程为 `SIGCLD` 返回的状态。以下是 `ksi_t` 中内容的部分列表：

```c
typedef struct __ksi {
    struct sigcount *si_countp; /* sender’s pending signal count */
    int             si_signo;   /* signal number */
    signal_t        si_value;
    int             si_code;    /* cause of signal */
    int             si_errno;   /* associated errno */
    union {
        ...
    } __data;
} ksi_t;
```

每个 `kthread` 结构也包含一些与信号相关的数据。如下所示：

```c
struct kthread {
    ...
    char            kt_cursig;   /* number of current pending signal,
                                       if any */
    ksigget_t kt_sig; /* signals pending to this thread */
    ksigget_t kt_ksi_aval; /* signals with signifo available */
    ksi_t *kt_ksiactive; /* list of pending queued signals*/
    ksigget_t kt_sigmask; /* current signal mask */
    int kt_proc_sig; /* signo of sig directed at proc */
    ...
}
```

最后，我们有 `ksigwait` 结构。每个明确等待信号的线程——通过 `pause()`、`sgsigpause()`、`sigwait()` 或 `sgsigsuspend()` 系统调用——都将拥有其中一个结构。`ksigwait` 结构由 `proc` 结构指向，反过来它们又指向等待信号的线程。

### 信号预期

*信号预期*（*Signal anticipation*）是指应用程序可以为处理信号所做的规划。从应用程序的角度来看，规划信号的首选方法是使用 *sigaction()* 系统调用。还有其他可用的系统调用，但它们的功能基本上相同。*Sigaction()* 是 POSIX 标准，应在新开发中使用。

*Sigaction()* 期望三个参数：信号编号、一个包含用于该信号的新值的 `struct sigaction`，以及一个可以返回旧值的 `struct sigaction`。文件 `/usr/include/sys/signal.h` 包含信号编号的符号定义、*sigaction* 结构的定义以及各种其他与信号相关的声明。*sigaction* 结构包含指向处理例程的指针、一个指示在处理此信号期间应屏蔽哪些信号的掩码，以及一组用于修改信号处理行为的标志。我们很快就会看到这些是如何使用的。

如果用户为第二个参数指定了一个非 NULL 值，表示他或她想更改信号的现有值，*sigaction()* 首先会进行几项合理性检查，以确保通过 *sigaction* 结构传入的值是有效的。首先，我们检查用户是否试图更改 `SIGKILL`、`SIGSTOP` 或 `SIGCANCEL` 的操作。这些信号不能被捕获。任何试图将处理程序更改为 `SIG_DFL`（默认处理程序）以外的值的尝试都会导致 *sigaction()* 返回 `EINVAL`。接下来，我们验证标志，确保标志字段中没有设置不支持的位。如果设置了 `signal.h` 中定义的位之外的任何位，*sigaction()* 将再次返回 `EINVAL`。最后，如果用户试图更改 `SIGFALLFAULT` 信号的行为，他或她必须在标志字段中设置 `_SA_SIGFAALLFAULT` 标志。`SIGFALLFAULT` 由图形库使用，通常不应由用户应用程序更改。这个标志是一种表示“是的，我真的想更改 SIGFALLFAULT”的方式。

一旦通过了合理性检查，*sigaction()* 做的下一件事是调用 `setsgvec_setup()`。这个例程负责分配所需的内存，并获取确保操作是原子的且不会被中断所需的任何锁。

具体来说，如果设置了 `SA_SIGINFO` 标志，内核必须分配内存以存储传递给信号处理器的信号信息。这首先完成，因为在获取任何锁之前执行，因为它需要使用 `MALLOC` 内存，而当内存不可用时，`MALLOC` 可能会睡眠。接下来，如果被修改的信号是 `SIGCLD`，我们获取三个锁：`MTPROC_REAP_LOCK`、系统范围的 `sched_siglock` 自旋锁以及当前进程的 `exit_lock` 自旋锁。这是因为 `SIGCLD` 的更改会修改子进程退出时采取的行为。`MTPROC_REAP_LOCK` 确保进程当前未被回收；`sched_lock` 确保调度器无法修改它；`exit_lock` 确保进程当前并未试图退出。最后，我们获取控制进程结构的自旋锁：`p->p_lock`。完成所有这些后，我们就回到 `sigaction()`。

实际上设置和获取信号处理器值的操作相当简单。如果用户为 `sigaction` 的第三个参数传递了一个非 NULL 指针，表明他/她希望获取当前值，我们只需从进程结构（及其相关的 `Process_Shared_Fields` 结构）中提取处理器和标志值，并将其传回给用户。然后 `sigaction` 调用 `sigsetget` 设置新值，这同样相当简单。处理器被复制到 `p->p_shared->p_signal[sig+1]`。掩码被复制到 `p->p_shared->p_sighandmask [sig+1]`。然后我们遍历标志值，并将每个标志复制到其正确的位置——对于大多数标志来说，这是 `p->p_shared` 中的一个位。
