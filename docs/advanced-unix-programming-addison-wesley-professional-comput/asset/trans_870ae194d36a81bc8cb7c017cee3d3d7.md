
```c
int main(void)
{
    struct sigaction act;
    time_t start, stop;

    memset(&act, 0, sizeof(act));
    act.sa_handler = handler;
    act.sa_flags = SA_RESTART;
    ec_negl( sigaction(SIGINT, &act, NULL) )
    printf("Type Ctrl-c in the next 10 secs.\n");
    ec_negl( start = time(NULL) )
    sleep(20);
    ec_negl( stop = time(NULL) )
    printf("Sleep for %ld secs\n", (long)(stop - start));
    if (gotsig > 0)
        printf("Got signal number %ld\n", (long)gotsig);
    else
        printf("Did not get signal\n");
    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

这是我得到的输出结果；在看到第一行之后我输入了 Ctrl-c：

```text
Type Ctrl-c in the next 10 secs.
Sleep for 4 secs
Got signal number 2
```

### 9.1.8 最小防御性信号处理

即使你决定避免使用信号处理程序，通常你仍然需要至少最低限度的信号处理，以防止你的应用程序被用户意外终止。此外，如果存在导致程序非正常终止的 bug（例如引用了无效内存，即“段错误”），仅仅让程序非正常终止也是不专业的。更好的做法是捕获该信号，记录问题，并告知用户，而不是简单地显示“程序中止 – 段错误”或 shell 决定显示的任何内容。

因此，大多数应用程序至少应该做到以下几点：

- 在程序开始时尽快阻塞所有信号，如下所示：

```c
sigset_t set;

ec_negl( sigfillset(&set) )
ec_negl( sigprocmask(SIG_SETMASK, &set, NULL) )

(如果你有多个线程，请使用 `pthread_sigmask`。)
```

- 设置你不希望捕获的所有键盘生成信号为忽略状态，例如 `SIGINT`。
- 捕获 `SIGTERM`，并安排在其到达时进行清理和终止，因为这是系统管理员关闭进程的标准方式。
- 捕获所有由错误生成的信号，并安排在收到其中一个信号时显示和/或记录错误并终止。
- 忽略 `SIGPIPE`，以便在写入空管道时 `write` 返回错误。这比接收信号更方便。
- 通过调用 `sigemptyset` 和 `sigprocmask`（或 `pthread_sigmask`）解除对所有信号的阻塞。

这是一个你可以在应用程序开始时调用的函数，用于最小化地处理信号：

```c
static bool handle_signals(void)
{
    sigset_t set;
    struct sigaction act;

    ec_negl( sigfillset(&set) )
    ec_negl( sigprocmask(SIG_SETMASK, &set, NULL) )
    memset(&act, 0, sizeof(act));
    ec_negl( sigfillset(&act.sa_mask) )
    act.sa_handler = SIG_IGN;
    ec_negl( sigaction(SIGHUP, &act, NULL) )
    ec_negl( sigaction(SIGINT, &act, NULL) )
    ec_negl( sigaction(SIGQUIT, &act, NULL) )
    ec_negl( sigaction(SIGPIPE, &act, NULL) )
    act.sa_handler = handler;
    ec_negl( sigaction(SIGTERM, &act, NULL) )
    ec_negl( sigaction(SIGBUS, &act, NULL) )
    ec_negl( sigaction(SIGFPE, &act, NULL) )
    ec_negl( sigaction(SIGILL, &act, NULL) )
    ec_negl( sigaction(SIGSEGV, &act, NULL) )
    ec_negl( sigaction(SIGSYS, &act, NULL) )
    ec_negl( sigaction(SIGXCPU, &act, NULL) )
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

这里的想法是用适合你应用程序的代码替换 `clean_up` 的内部实现。我自己编写了 `strlen` 的版本，因为听起来可能很荒唐，标准的 `strlen` 并不在异步信号安全函数列表中。出于同样的原因，我在处理程序中使用了 `write` 而不是 `fprintf`。还要注意使用了 `_exit` 而不是 `exit`——如 5.7 节所述，带下划线的版本会跳过调用 `atexit` 和刷新标准 C I/O 缓冲区，这是执行异步信号安全正常退出的唯一方式。

### 9.1.9 合成生成信号

正如我在 9.1.3 节中所述，每个信号都有一个自然的原因，也可以通过调用 `kill`、`killpg`、`pthread_kill`、`abort`、`raise` 或 `sigqueue`（9.5.4 节）显式生成：

![](img/41b4c8f6d6a5c349eee321a301703d97_635_0.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_635_1.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_635_2.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_635_3.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_636_0.png)

命名不当的 `kill` 系统调用可以向一个或多个进程发送任意信号，而不仅仅是 `SIGKILL`，前提是具有发送信号的权限。如果由超级用户运行，或者发送进程的 real 或 effective user ID 与接收进程的 real 或 saved set-user-ID 匹配，则具有权限。信号传递给哪些进程取决于 `pid` 参数：

- `> 0` 进程 ID 为 `pid` 的进程
- `0` 其进程组 ID 与发送进程的进程组 ID 相同的进程组
- `< -1` 其进程组 ID 与 `pid` 的绝对值相同的进程组
- `-1` 发送者具有权限的所有进程，除了实现定义的一组系统进程外

如果 `sig_num` 为 0，`kill` 仅测试其 `pid` 参数的有效性。这是一种判断进程或进程组是否存活的方法。如果发送进程没有权限发送信号，调用将失败，但 `errno` 值将指示进程或进程组是否存活：如果 `pid` 不存在，则为 `ESRCH`；如果存在但发送者无权限，则为 `EPERM`。

`killpg` 是一个完全不必要的系统调用，它只为进程组 ID 为 `pgrp` 的进程组生成信号，因此它与以下调用等效：

```c
kill(-pgrp, sig_num);
```

`pthread_kill` 类似于 `kill`，但它只向线程 `thread_id` 发送信号，该线程必须与发送线程位于同一进程中。它没有 `kill` 对进程拥有的广播功能。使用 `pthread_kill` 时要小心——记住，终止、停止或继续的信号始终会影响整个进程。因此，`pthread_kill` 仅对捕获的信号按你期望的方式工作。如果你执行

```c
pthread_kill(tid, SIGKILL);
```

进程将被终止，而不仅仅是线程 `tid`。（你使用 `pthread_cancel` 来终止单个线程。）

`abort` 几乎等同于参数为 `SIGABRT` 的 `kill`，但如果该信号被捕获且信号处理程序不返回（例如，调用 `siglongjmp` 或 `_exit`），进程无论如何都会被终止，就好像 `SIGABRT` 具有默认行为一样；`abort` 永不返回。例如，如果通过 `sigaction` 将 `SIGABRT` 设置为 `SIG_IGN`，`abort` 会终止进程，但

```c
kill(getpid(), SIGABRT)
```

没有效果。

`raise` 实际上是一个标准 C 函数。它向执行它的线程发送信号。也就是说，它与以下调用相同：

```c
pthread_kill(pthread_self(), signum);
```

然而，即使不支持 POSIX 线程选项，`raise` 始终存在，在这种情况下它与以下调用相同：

```c
kill(getpid(), signum);
```

### 9.1.10 fork、pthread_create 和 exec 对信号的影响

`fork`、`pthread_create` 或 `exec` 为新进程、线程或程序设置了线程的三个属性：

1. **信号动作：** 在 `fork` 之后，子进程继承所有信号动作。在 `exec` 之后，设置为 `SIG_DFL` 的信号保持该状态；设置为 `SIG_IGN` 的信号保持该状态，除了 `SIGCHLD`，它可能被设置为 `SIG_IGN` 或 `SIG_DFL`，具体由实现决定；被捕获的信号被设置为 `SIG_DFL`。由于所有动作都是进程范围的，`pthread_create` 没有影响。

2. **信号掩码：** 在 `fork` 之后从 fork 线程继承；在 `exec` 之后保持与执行线程相同；在 `pthread_create` 之后从创建线程复制到新线程。

3. **待处理信号：** 在 `fork` 之后被清除；在 `exec` 之后与执行线程相同；在 `pthread_create` 之后被清除。

记住这九条规则（三个属性乘以三个系统调用）的简单方法是这样：倾向于复制或继承属性而不改变，因此只需记住三个例外，其中前两个完全合乎逻辑：

