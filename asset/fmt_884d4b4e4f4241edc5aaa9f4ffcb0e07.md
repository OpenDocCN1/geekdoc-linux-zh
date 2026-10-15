
24 这找到了我们当前运行的 CPU 的 ID。`smp_processor_id()` 宏在在 7.2.1.4 节中描述过。

25 `local_irq_count()` 和 `local_bh_count()` 都在第 16.5.1.2 节中描述过。每当进入硬件或软件中断处理程序时，它们从特定 CPU 计数器的返回值就会增加。如果这两个计数器之一或两者不为 0，则返回 TRUE。如果两者都为 0，则返回 FALSE。

27 这是 `forego` 宏的精简版本。它只检查硬件中断。

31 如果本地 CPU 上没有正在进行的硬件中断，该宏为 TRUE；否则为 FALSE，因此实际上不会获取任何锁。

32 该宏的单处理器版本什么都不做。

34–35 这些宏封装了硬件中断的处理。它们仅仅是增加或减少指定 CPU 上正在进行的硬件中断嵌套层次。

37 `barrier()` 宏保证其他 CPU 的写入已刷新到内存并对此 CPU 可见。

### 16.5.3.2 多处理器情况的函数

在多处理器系统中，上子节讨论的宏实现如图 16.4 所示，来自 `<asm-i386/hardirq.h>`。

```c
static inline int irqs_running(void)
{
    int i;

    for (i = 0; i<smp_num_cpus; i++)
        if (local_irq_count(i))
            return 1;
    return 0;
}
```

```c
static void release_irock(int cpu)
{
    if (global_irq_holder== (unsigned char) cpu) {
        global_irq_holder = NO_PROC_ID;
        clear_bit(0,&global_irq_lock);
}
}
```

```c
static inline void irq_enter(int cpu, int irq)
{
    ++local_irq_count(cpu);

    while(test_bit(0,&global_irq_lock)) {
        cpu_relax();
    }
}
```

```c
static inline void irq_exit(int cpu, int irq)
{
    --local_irq_count(cpu);
}
```

```c
static int hardirq_trylock(int cpu)
{
    return !local_irq_count(cpu) && !test_bit(0,&global_irq_lock);
}
```

图 16.4 中断相关宏的多处理器版本

51–53 我们遍历每个 CPU，如果其中任何一个有一个中断处理程序，则返回 TRUE。
51 `smp_num_cpus` 变量在 7.2.1.1 节定义。
52 `local_irq_count()` 宏来自 16.5.1.2 节。
54 否则，我们返回 0。

60–62 如果当前 CPU 拥有 `global_irq_lock`，则归还它；否则什么都不做。
61 没有 CPU 拥有锁。
62 使用第 16.5.1.2 节的函数来清除锁位。
68 这是单处理器部分，使用第 16.5.1.2 节的宏。
70–71 如果其他 CPU 持有全局锁，则循环直到锁释放。
75–78 如果此 CPU 上没有正在处理的中断且全局锁空闲；我们返回 TRUE；否则返回 FALSE。

# 信号机制

前面的章节处理了对操作系统的中断。现在我们在接下来的章节中将考虑信号机制。这是中断的另一种形式。这次是用户进程被操作系统或另一个进程中断。

Unix 中的信号机制允许一个进程通知另一个进程发生了特定事件，并且有一组系统定义的信号，每个信号对应一个要调用的用户定义函数。这些信号通过整数标识，定义为以 `SIG` 开头的符号常量，并带有特定事件的助记；例如，`SIGCHLD` 是子进程死亡时发送给父进程的信号。

内核实现信号涉及的数据结构数量异常。这些以及操作它们的函数是本章的主题。有了这些背景，第 18 节将检查信号如何由源进程发送并传递给目标进程。信号在内核模式下传递给进程；但处理程序必须在用户模式下运行。实现此点的机制在第 19 节中描述。

## 17.1 实现信号的数据结构

在第一节中将检查内核实现信号涉及的基础数据结构，以便所有人可以使用。这些数据结构大部分（包括信号列表本身）都是特定于架构。

### 17.1.1 基础定义

信号集经常用位图表示。i386 架构上实现信号的若干基础定义见图 17.1，来自 `<asm-i386/signal.h>`。

```c
#define _NSIG 64
#define _NSIG_BPW 32
#define _NSIG_WORDS (_NSIG / _NSIG_BPW)
```

```c
typedef struct {
unsigned long sig[_NSIG];
} sigset_t;
```

**图 17.1** 基础定义

- i386 架构中有 64 个可能的信号。
- 这是基本处理器字中的位数[每个字的位数 (BPW)]。
- 这是表示所有可能信号的位图中的字 (2)。

19–21 代表信号的基础位图 (`sigset_t`) 实现为 `unsigned long` 数组。在 i386 上，它有两个元素。

### 17.1.2 信号定义

i386 上使用的标准信号定义如图 17.2 所示，来自 `<asm-i386/signal.h>`。为了理解原理不需要理解每个信号的用途，但对每个信号给出了简短描述。

```c
#define SIGHUP 1
#define SIGINT 2
#define SIGQUIT 3
#define SIGILL 4
#define SIGTRAP 5
#define SIGABRT 6
#define SIGIOT 6
#define SIGBUS 7
#define SIGFPE 8
#define SIGKILL 9
#define SIGUSR1 10
#define SIGSEGV 11
#define SIGUSR2 12
#define SIGPIPE 13
#define SIGALRM 14
#define SIGTERM 15
#define SIGKILLFL 16
#define SIGCHLD 17
#define SIGCONT 18
#define SIGSTOP 19
#define SIGTSTP 20
#define SIGTTIN 21
#define SIGTTO 22
```
