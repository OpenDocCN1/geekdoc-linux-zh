
但我们希望父进程先执行，然后通知子进程何时继续。我们第一次尝试同步它们的方法是父进程向子进程发送一个 SIGUSR1 信号，子进程捕获该信号并设置一个变量：

```c
static volatile sig_atomic_t got_sig;
static void handler(int signum)
{
    if (signum == SIGUSR1)
        got_sig = 1;
}

void try2(void)
{
    pid_t pid;

    got_sig = 0;
    ec_neg1(pid = fork());
    if (pid == 0) {
        struct sigaction act;

        memset(&act, 0, sizeof(act));
        act.sa_handler = handler;
        ec_neg1(sigaction(SIGUSR1, &act, NULL));
        while (got_sig == 0)
            if (pause() == -1 && errno != EINTR)
                EC_FAIL
        printf("child\n");
        exit(EXIT_SUCCESS);
    }
    printf("parent\n");
    ec_neg1(kill(pid, SIGUSR1));
    return;

    EC_CLEANUP_BGN
    EC_FLUSH("try2")
    EC_CLEANUP_END
}
```

处理程序是安全的——它只是设置一个允许类型的变量。子进程在循环中测试该变量，暂停以等待信号的到来。（`pause`，我们将在 9.2.1 节中详细讨论，会阻塞直到信号到达。）现在的执行顺序是我们所期望的：

- 父进程
- 子进程

但存在两个问题：

- 如果 *SIGUSR1* 在子进程有机会安装处理程序之前就被投递给子进程，它将终止子进程。一个潜在的解决方案是在 *fork* 之前安装处理程序，这样子进程将继承它，但这仅在父子进程中有效。我们希望能找到一种适用于需要同步的任意进程的解决方案。
- 如果 *SIGUSR1* 在 *while* 语句中的测试和调用 *pause* 之间被投递，*pause* 将永远等待，因为本应唤醒它的信号在它进入睡眠之前就已经到达了。

我们可以尝试通过阻塞 *SIGUSR1* 信号直到我们准备好接收它来修复问题：

```c
void try3(void)
{
    sigset_t set;
    pid_t pid;

    got_sig = 0;
    ec_neg1( sigemptyset(&set) )
    ec_neg1( sigaddset(&set, SIGUSR1) )
    ec_neg1( sigprocmask(SIG_SETMASK, &set, NULL) )
    ec_neg1( pid = fork() )
    if (pid == 0) {
        struct sigaction act;
        sigset_t suspendset;

        memset(&act, 0, sizeof(act));
        act.sa_handler = handler;
        ec_neg1( sigaction(SIGUSR1, &act, NULL) )
        ec_neg1( sigfillset(&suspendset) )
        ec_neg1( sigdelset(&suspendset, SIGUSR1) )
        ec_neg1( sigprocmask(SIG_SETMASK, &suspendset, NULL) )
        while (got_sig == 0)
            if (pause() == -1 && errno != EINTR)
                EC_FAIL
        printf("child\n");
        exit(EXIT_SUCCESS);
    }
    printf("parent\n");
    ec_neg1( kill(pid, SIGUSR1) )
    return;

    EC_CLEANUP_BGN
        EC_FLUSH("try3")
    EC_CLEANUP_END
}
```

这彻底解决了问题 #1。由于信号被阻塞，SIGUSR1 无法在处理程序安装前到达。但问题 #2 依然存在，我们无能为力。尽管时间窗口很小，信号仍然可能在测试和暂停之间到达。

我们需要一种方法，在暂停开始之前保持信号处于阻塞状态。或者换一种说法，我们希望解除阻塞和暂停是原子的。这正是 `sigsuspend` 所做的：

**sigsuspend**——更改信号掩码并等待信号

```c
#include <signal.h>
int sigsuspend(
   const sigset_t *sigmask      /* 临时信号掩码 */
); /* 出错时返回 -1，始终如此（设置 errno） */
```

`sigsuspend` 暂时用 `sigmask` 替换线程的信号掩码，然后等待直到一个未被阻塞的信号被投递，其动作为终止或被捕获。如果是终止，进程（而不仅仅是线程，请记住）将被终止，且 `sigsuspend` 不会返回。如果是被捕获且信号处理程序返回，之前的信号掩码将被恢复，并且 `sigsuspend` 会带错误返回。通常，错误仅为 EINTR；也就是说，返回 -1 且 errno 为 EINTR 对于被中断的系统调用来说是正常的（与 `pause` 相同，如上述示例所示）。

在几乎所有情况下，传递给 `sigsuspend` 的掩码的效果是解除在调用前被阻塞的一个或多个信号的阻塞，尽管这实际上并不是要求。只是做其他事情没有太大意义。

好的，完美。我们现在可以通过简单地将 `pause` 替换为 `sigsuspend` 来永久解决我们的同步问题。我们不再需要 while 循环，因为解除信号阻塞和暂停现在是原子的。

```c
void try4(void)
{
   sigset_t set;
   pid_t pid;

   ec_neg1( sigemptyset(&set) )
   ec_neg1( sigaddset(&set, SIGUSR1) )
   ec_neg1( sigprocmask(SIG_SETMASK, &set, NULL) )
   ec_neg1( pid = fork() )
   if (pid == 0) {
      struct sigaction act;
      sigset_t suspendset;

      memset(&act, 0, sizeof(act));
      act.sa_handler = handler;
      ec_neg1( sigaction(SIGUSR1, &act, NULL) )
      ec_neg1( sigfillset(&suspendset) )
      ec_neg1( sigdelset(&suspendset, SIGUSR1) )
      if (sigsuspend(&suspendset) == -1 && errno != EINTR)
          EC_FAIL
      printf("child\n");
      exit(EXIT_SUCCESS);
   }
   printf("parent\n");
   ec_neg1( kill(pid, SIGUSR1) )
   return;

   EC_CLEANUP_BGN
   EC_FLUSH("try4")
   EC_CLEANUP_END
}
```

我们仍然可以使用相同的处理函数，它设置 *got_sig* 变量；但是，我们不再需要该变量，空的处理程序也能正常工作：

```c
static void handler(int signum)
{
}
```

此外，将 *sigsuspend* 的返回值与 −1 进行比较的测试其实并不需要，因为它始终返回 −1。但这样做很奇怪，会让那些不记得或不了解 *sigsuspend* 所有细节的读者感到困惑。

注意，我们在 *fork* 之前阻塞 SIGUSR1，以便子进程继承信号掩码。在需要同步的两个进程互不相关的情况下，调用 *sigsuspend* 的进程只需自行进行阻塞。实际上，这只是我们在 9.1.8 节中提到的通用建议的一个特例，即每个应用程序开始时都阻塞所有信号。

请注意，与 *sigwait* 不同，你几乎总是将 *sigsuspend* 与信号处理程序一起使用，但通常处理程序不做任何事。它的存在只是为了让投递的信号中断 *sigsuspend*。

*sigsuspend* 和 *sigwait* 之间的另一个重大区别是，使用 *sigwait* 时，你正在等待的信号保持阻塞状态。事实上，它从未被投递——相反，*sigwait* 接受它；将其从待处理信号集合中移除并返回它。因此，使用 `sigwait` 时不存在解除信号阻塞与等待信号投递之间的竞争条件，`sigsuspend` 消除了这种竞争条件，因为你永远不会解除信号的阻塞。我们的同步代码变得更加简单：

```c
void try5(void)
{
    sigset_t set;
    pid_t pid;

    ec_neg1( sigemptyset(&set) )
    ec_neg1( sigaddset(&set, SIGUSR1) )
    ec_neg1( sigprocmask(SIG_SETMASK, &set, NULL) )
    ec_neg1( pid = fork() )
    if (pid == 0) {
        int signum;

        ec_rv( sigwait(&set, &signum) )
        printf("child\n");
        exit(EXIT_SUCCESS);
    }

    printf("parent\n");
    ec_neg1( kill(pid, SIGUSR1) )
    return;

    EC_CLEANUP_BGN
        EC_FLUSH("try5")
    EC_CLEANUP_END
}
```

我们应该提到，父进程和子进程的同步也可以通过管道完成，完全跳过信号的复杂性：

```c
void try6(void)
{
    int pfd[2];
    pid_t pid;

    ec_neg1( pipe(pfd) )
    ec_neg1( pid = fork() )
    if (pid == 0) {
        char c;

        ec_neg1( close(pfd[1]) )
        ec_neg1( read(pfd[0], &c, 1) )
        ec_neg1( close(pfd[0]) )
        printf("child\n");
        exit(EXIT_SUCCESS);
    }
    printf("parent\n");
    ec_neg1( close(pfd[0]) )
    ec_neg1( close(pfd[1]) )
    return;

    EC_CLEANUP_BGN
        EC_FLUSH("try6")
    EC_CLEANUP_END
}
```

这里，子进程在 `read` 中阻塞，直到父进程关闭管道的写端，导致子进程获得零返回。

## 9.3 杂项信号系统调用

你可以通过 `sigpending` 得知是否有信号处于挂起状态，它返回一组挂起的信号：

**sigpending**——检查挂起信号

```c
#include <signal.h>

int sigpending(
        sigset_t *set        /* 返回的挂起信号集合 */
); /* 成功时返回 0，出错时返回 -1（设置 errno） */
```

你可以使用 `sigismember`（见 9.1.5 节）对返回的集合进行测试，以确定哪些信号是挂起的。当然，除非信号被阻塞，否则在测试时它可能已不再处于挂起状态。

回想 9.1.6 节，SA_ONSTACK 标志安排信号的处理程序在备用栈上执行。你使用 `sigaltstack` 来管理该栈：

**sigaltstack**——设置和获取备用栈上下文

```c
#include <signal.h>

int sigaltstack(
        const stack_t *stack,      /* 新栈 */
                stack_t *ostack    /* 旧栈 */
); /* 成功时返回 0，出错时返回 -1（设置 errno） */
```

关于此系统调用的详细信息，请参阅你的系统文档或 SUS（单一 UNIX 规范）。

