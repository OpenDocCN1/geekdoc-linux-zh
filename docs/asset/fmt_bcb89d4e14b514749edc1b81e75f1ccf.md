
```c
    ec_negl( sigaction(SIGXFSZ, &act, NULL) )

    ec_negl( sigemptyset(&set) )

    ec_negl( sigprocmask(SIG_SETMASK, &set, NULL) )

    return true;

EC_CLEANUP_BGN

    return false;

EC_CLEANUP_END

}
```

以下是实际的处理程序及其调用的两个辅助函数：

```c
static void handler(int signum)
{
    int i;
    struct {
        int signum;
        char *msg;
    } sigmsg[] = {
        { SIGTERM, "Termination signal" },
        { SIGBUS, "Access to undefined portion of a memory object" },
        { SIGFPE, "Erroneous arithmetic operation" },
        { SIGILL, "Illegal instruction" },
        { SIGSEGV, "Invalid memory reference" },
        { SIGSYS, "Bad system call" },
        { SIGXCPU, "CPU-time limit exceeded" },
        { SIGXFSZ, "File-size limit exceeded" },
        { 0, NULL }
    };

    clean_up();
    for (i = 0; sigmsg[i].signum > 0; i++)
        if (sigmsg[i].signum == signum) {
            (void)write(STDERR_FILENO, sigmsg[i].msg,
                strlen_safe(sigmsg[i].msg));
            (void)write(STDERR_FILENO, "\n", 1);
            break;
        }

    _exit(EXIT_FAILURE);
}

static void clean_up(void)
{
    /*
     Clean-up code goes here --
     must be async-signal-safe.
     */
}

static size_t strlen_safe(const char *s)
{
    size_t n = 0;
    while (*s++ != '\0')
        n++;
    return n;
}
```

这里的想法是用适合你应用程序的代码替换`clean_up`的内部实现。我自己编写了`strlen`的版本，因为听起来可能很荒唐，标准的`strlen`并不在异步信号安全函数列表中。出于同样的原因，我在处理程序中使用了`write`而不是`fprintf`。还要注意使用了`_exit`而不是`exit`——如5.7节所述，带下划线的版本会跳过调用`atexit`和刷新标准C I/O缓冲区，这是执行异步信号安全正常退出的唯一方式。

### 9.1.9 合成生成信号

正如我在9.1.3节中所述，每个信号都有一个自然的原因，也可以通过调用`kill`、`killpg`、`pthread_kill`、`abort`、`raise`或`sigqueue`（9.5.4节）显式生成：

![](img/41b4c8f6d6a5c349eee321a301703d97_635_0.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_635_1.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_635_2.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_635_3.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_636_0.png)

命名不当的`kill`系统调用可以向一个或多个进程发送任意信号，而不仅仅是`SIGKILL`，前提是具有发送信号的权限。如果由超级用户运行，或者发送进程的real或effective user ID与接收进程的real或saved set-user-ID匹配，则具有权限。信号传递给哪些进程取决于`pid`参数：

- `> 0` 进程ID为`pid`的进程
- `0` 其进程组ID与发送进程的进程组ID相同的进程组
- `< -1` 其进程组ID与`pid`的绝对值相同的进程组
- `-1` 发送者具有权限的所有进程，除了实现定义的一组系统进程外

如果`sig_num`为0，`kill`仅测试其`pid`参数的有效性。这是一种判断进程或进程组是否存活的方法。如果发送进程没有权限发送信号，调用将失败，但`errno`值将指示进程或进程组是否存活：如果`pid`不存在，则为`ESRCH`；如果存在但发送者无权限，则为`EPERM`。

`killpg`是一个完全不必要的系统调用，它只为进程组ID为`pgrp`的进程组生成信号，因此它与以下调用等效：

```c
kill(-pgrp, sig_num);
```

`pthread_kill`类似于`kill`，但它只向线程`thread_id`发送信号，该线程必须与发送线程位于同一进程中。它没有`kill`对进程拥有的广播功能。使用`pthread_kill`时要小心——记住，终止、停止或继续的信号始终会影响整个进程。因此，`pthread_kill`仅对捕获的信号按你期望的方式工作。如果你执行

```c
pthread_kill(tid, SIGKILL);
```

进程将被终止，而不仅仅是线程`tid`。（你使用`pthread_cancel`来终止单个线程。）

`abort`几乎等同于参数为`SIGABRT`的`kill`，但如果该信号被捕获且信号处理程序不返回（例如，调用`siglongjmp`或`_exit`），进程无论如何都会被终止，就好像`SIGABRT`具有默认行为一样；`abort`永不返回。例如，如果通过`sigaction`将`SIGABRT`设置为`SIG_IGN`，`abort`会终止进程，但

```c
kill(getpid(), SIGABRT)
```

没有效果。

`raise`实际上是一个标准C函数。它向执行它的线程发送信号。也就是说，它与以下调用相同：

```c
pthread_kill(pthread_self(), signum);
```

然而，即使不支持POSIX线程选项，`raise`始终存在，在这种情况下它与以下调用相同：

```c
kill(getpid(), signum);
```

### 9.1.10 fork、pthread_create 和 exec 对信号的影响

`fork`、`pthread_create`或`exec`为新进程、线程或程序设置了线程的三个属性：

1. **信号动作：** 在`fork`之后，子进程继承所有信号动作。在`exec`之后，设置为`SIG_DFL`的信号保持该状态；设置为`SIG_IGN`的信号保持该状态，除了`SIGCHLD`，它可能被设置为`SIG_IGN`或`SIG_DFL`，具体由实现决定；被捕获的信号被设置为`SIG_DFL`。由于所有动作都是进程范围的，`pthread_create`没有影响。
2. **信号掩码：** 在`fork`之后从fork线程继承；在`exec`之后保持与执行线程相同；在`pthread_create`之后从创建线程复制到新线程。
3. **待处理信号：** 在`fork`之后被清除；在`exec`之后与执行线程相同；在`pthread_create`之后被清除。

记住这九条规则（三个属性乘以三个系统调用）的简单方法是这样：倾向于复制或继承属性而不改变，因此只需记住三个例外，其中前两个完全合乎逻辑：

- 如果一个已捕获的信号的处理程序消失了（例如在`exec`时），则该信号必须更改为`SIG_DFL`。
- `挂起`的信号是按进程或按线程划分的，因此当有新进程或新线程时，它们会被清除。
- 标准制定者更关心不破坏现有实现，而不是强制可移植性，因此他们在`SIGCHLD`上摇摆不定。

## 9.2 等待信号

本节描述允许进程等待信号传递的系统调用。

### 9.2.1 pause 系统调用

我们遇到过许多在某个活动完成前会阻塞等待事件的系统调用。例如，在读取终端时，`read`通常等待输入一整行。`pause`是纯粹的等待：它什么都不做，也不特别等待任何内容。

> `pause` — 等待信号
> #include <unistd.h>
> int pause(void);
> /* 出错时返回 -1（设置 errno） */

由于已传递的信号会中断大多数阻塞的系统调用，我们可以说`pause`等待的是一个被捕获的信号。如果信号捕获函数返回，`pause`会返回并将`errno`设置为`EINTR`，但由于这是`pause`返回的唯一方式，测试它是没有意义的。

通常，你会使用像`sigwait`这样更复杂的调用，而不是`pause`。

### 9.2.2 sigwait 系统调用

与`pause`不同，`sigwait`让你可以选择等待什么。你不需要信号处理程序，并且当它返回时，你会被告知到达的是哪个信号：

```c
/*
sigwait — 等待信号
*/
#include <signal.h>
int sigwait(
    const sigset_t *set,      /* 要等待的信号 */
    int *signum              /* 被接受的信号 */
);
/* 成功返回 0，错误时返回错误编号 */
```

参数`set`是一个信号集合（参见第9.1.5节），`sigwait`将等待其中的信号。当一个信号变为挂起状态时，其编号通过`signum`参数返回，`sigwait`随之返回。如果在调用`sigwait`时已有一个或多个信号处于挂起状态，则会以未定义的方式选择一个并立即返回。`sigwait`返回的信号的技术术语是“被接受”；它不是“被传递”。

当你使用`sigwait`时，你希望信号保持挂起状态，直到`sigwait`返回它；你不希望信号被传递。因此，你阻塞了`sigwait`将要等待的信号，并保持它们阻塞状态。（信号的生命周期——从产生到挂起到传递——在第9.1.2节中描述过。）

如果有多个线程在`sigwait`中等待发送给进程的同一直信号，只有一个线程会获取该信号，且选择方式是未定义的。如果信号发送给特定线程，只有该线程的`sigwait`（如果有的话）才能返回它。

通常，你使用`sigwait`有两个目的之一：

- 当线程在某个与信号相关的事件发生前无法继续时。例如，一个线程可能在消息到达时向另一个线程发送`SIGUSR1`。不过，通常使用条件变量（第5.17.4节）来实现此目的更好。本节稍后有一个示例。
- 当指定一个线程来处理信号时。也就是说，使用等待线程代替信号处理函数。所有线程都阻塞了将要等待的信号，一个线程执行`sigwait`。但这仅适用于发送给进程的信号——如果信号发送给线程，只有该线程的`sigwait`才能返回它。

对于发送给进程的信号，使用`sigwait`代替信号处理程序要好得多，因为信号处理程序的所有限制都不适用。当`sigwait`返回时，你可以自由调用任何系统调用或函数，或在线程中做其他任何事情。

在第9.1.8节中，我们展示了一个函数`handle_signals`，它安排捕获所有检测到错误的信号（例如`SIGFPE`、`SIGSEGV`），以便在退出前调用清理函数并显示一条友好消息。让我们重新编写此函数，使用线程中的`sigwait`代替信号处理程序：

```c
static bool handle_signals(void) /* 请勿使用 -- 见下文 */
{
  sigset_t *set;
  struct sigaction act;
  pthread_t tid;
  ec_null( set = malloc(sizeof(*set)) )
  ec_negl( sigfillset(set) )
  ec_rv( pthread_sigmask(SIG_SETMASK, set, NULL) )
  memset(&act, 0, sizeof(act));
  act.sa_handler = SIG_IGN;
  ec_negl( sigaction(SIGHUP, &act, NULL) )
  ec_negl( sigaction(SIGINT, &act, NULL) )
  ec_negl( sigaction(SIGQUIT, &act, NULL) )
  ec_negl( sigaction(SIGPIPE, &act, NULL) )
  ec_negl( sigemptyset(set) )
  ec_negl( sigaddset(set, SIGTERM) )
  ec_negl( sigaddset(set, SIGBUS) )
  ec_negl( sigaddset(set, SIGFPE) )
  ec_negl( sigaddset(set, SIGILL) )
  ec_negl( sigaddset(set, SIGSEGV) )
  ec_negl( sigaddset(set, SIGSYS) )
  ec_negl( sigaddset(set, SIGXCPU) )
  ec_negl( sigaddset(set, SIGXFSZ) )
  ec_rv( pthread_sigmask(SIG_SETMASK, set, NULL) )
  ec_rv( pthread_create(&tid, NULL, sig_thread, set) )
  return true;

EC_CLEANUP_BGN
  return false;
EC_CLEANUP_END
}

static void *sig_thread(void *arg)
{
  int signum;
  int i;
  struct {
    int signum;
    char *msg;
  } sigmsg[] = {
    { SIGTERM, "Termination signal" },
    { SIGBUS, "Access to undefined portion of a memory object" },
    { SIGFPE, "Erroneous arithmetic operation" },
    { SIGILL, "Illegal instruction" },
    { SIGSEGV, "Invalid memory reference" },
    { SIGSYS, "Bad system call" },
    { SIGXCPU, "CPU-time limit exceeded" },
    { SIGXFSZ, "File-size limit exceeded" },
    { 0, NULL }
  };

  while (true) {
    ec_rx( sigwait((const sigset_t *)arg, &signum) )
    clean_up();
    for (i = 0; sigmsg[i].signum > 0; i++)
      if (sigmsg[i].signum == signum) {
        fprintf(stderr, "%s\n", sigmsg[i].msg);
        break;
      }

    _exit(EXIT_FAILURE);
  }

  return (void *)true; /* 永远不会到达这里 */

  EC_CLEANUP_BGN
  EC_PUSH("sig_thread")
  return (void *)false;
  EC_CLEANUP_END
}

static void clean_up(void)
{
  /*
  清理代码放在这里 --
  不需要是异步信号安全的。
  */
}
```
