
-   `_exit` 和 `_Exit` 在所有方面都表现为完全相同的行为，尽管从技术角度来说，`_exit` 源自 UNIX，而 `_Exit` 源自标准 C。从现在起，我将仅提及 `_exit`，你可以默认我关于它所说的一切都同样适用于 `_Exit`。

-   `exit`（不带下划线）也源自标准 C。它执行了 `_exit` 所做的所有操作，还包括一些更高级的清理工作，至少包括调用通过 `atexit` 注册的函数（见第 1.3.4 节）以及刷新标准 I/O 缓冲区，就好像调用了 `fflush` 或 `fclose` 一样。（`_exit` 是否刷新缓冲区是由实现定义的，因此不要依赖于此。）

由于 `exit` 是 `_exit` 的超集，我在这里关于后者所说的一切都同样适用于前者，因此我主要讨论 `_exit`。

通常，在一个未执行 `exec` 的子进程中，你会调用 `_exit` 而不是 `exit`，正如我在上一节的 `execute2` 中展示的那样，因为子进程继承的清理处理通常只应执行一次。但这并非总是正确的，因此你需要检查每种情况以确定何种做法是合适的。在最常见的情况下，当子进程被 `exec` 覆盖时，程序会重新启动，因此无论它在退出时执行什么清理操作都是可以的。父进程的任何缓冲区或 `atexit` 函数早已不复存在。

如果你像我在这本书中所做的那样使用“ec”宏进行错误检查，请记住，错误消息的自动显示和函数回溯是在一个通过 `atexit` 注册的函数中完成的，如果你使用 `_exit` 终止程序，该函数将不会被调用（见第 1.4.2 节）。在上一节的 `execute2` 中，我们在父进程和子进程中都使用了 `EC_FLUSH` 宏来处理这一问题，尽管只有子进程调用 `_exit`。

以下是退出函数的概要。注意，这里涉及两个不同的包含文件：

```
_exit—在不进行清理的情况下终止进程
#include <unistd.h>
    void _exit(            /* 退出状态 */
    int status
    );
    /* 不会返回 */
```

```
_Exit—在不进行清理的情况下终止进程
#include <stdlib.h>

void _Exit(
        int status           /* 退出状态 */
);
/* 不会返回 */
```

```
exit—在清理的情况下终止进程
#include <stdlib.h>

void exit(
        int status           /* 退出状态 */
);
/* 不会返回 */
```

`_exit` 以及其他两个变体会终止发出该调用的进程，其状态代码等于 `status` 的最右侧（最低有效）字节。还有许多其他副作用；主要列在这里，你可以在 [SUS2002] 中找到完整列表。实际上，这些副作用适用于一般的进程终止（崩溃除外）：

-   所有打开的文件描述符都会被关闭。

-   如第 4.3 节所述，如果该进程是控制进程（会话首进程），则该会话将失去其控制终端。此外，会话中的每个进程都会收到一个挂起（`SIGHUP`）信号，如果未捕获或忽略该信号，它们也将终止。

-   父进程将以下一节中解释的方式获知退出状态。

-   子进程不会受到任何直接的影响，除非它们的新父进程变成了一个特殊的系统进程，并且如果它们执行 `getpid`（见第 5.13 节）系统调用，它们将获得该系统进程的进程 ID（通常是 1）。

正在退出的进程的父进程通过其中一个 `wait` 系统调用接收其状态代码，这些调用在下一节中介绍。状态代码是一个从 0 到 255 的数字。按照惯例，0 表示成功终止，非零值表示某种异常终止，具体由正在退出的程序定义。定义了两个标准宏，我在本书的许多示例中已经使用过它们：`EXIT_SUCCESS` 定义为 0，`EXIT_FAILURE` 定义为某个非零值，通常是 1。使用宏而不是像 0 和 1 这样的整数会使程序稍微更具可读性，这就是我们这样做的原因。

一旦进程通过 `exit` 变体或信号终止，它停止执行，但其退出状态报告给父进程之前不会完全消失，除非系统已确定（如下一节所述）其父进程对状态不感兴趣。一个已终止但尚未报告状态的进程被称为 _僵尸_。

## 5.8 `wait`、`waitpid` 和 `waitid` 系统调用

`wait`、`waitpid` 或 `waitid` 等待子进程状态改变（停止、继续或终止），然后检索该进程的状态。前一节解释了进程如何终止；第 4.3 节解释了停止和继续的进程。我将从 `waitpid` 开始，然后介绍其他两个变体。

本节和下一节中描述的某些特性仅存在于符合 X/Open 标准的系统中，且截至撰写时，尚未在 FreeBSD 或 Linux 中实现；它们用标记“[X/Open]”标出。（X/Open 在第 1.2 节和第 1.5.1 节中讨论；虽然截至撰写时 Linux 声称符合 X/Open（当我们使用特性测试宏进行测试时），但它并不具备本节中描述的 X/Open 功能。）

```
waitpid---等待子进程状态改变

#include <sys/wait.h>

pid_t waitpid(
	pid_t pid,      /* 进程或进程组 ID */
	int *statusp,   /* 指向状态或 NULL 的指针 */
	int options,    /* 选项（见下文） */
);
/* 成功时返回进程 ID 或 0，错误时返回 -1（设置 errno） */
```

`pid` 参数可用于以下四种情况之一：

-   `>0`：等待具有该进程 ID 的子进程

-   `-1`：等待任意子进程

-   `0`：等待与调用进程在同一进程组中的任意子进程

-   `<-1`：等待进程组 ID 为 `-pid` 的进程组中的任意子进程

进程组在第 4.3 节中解释过。通常，运行每个管道（pipeline）在各自进程组中的 shell，在等待管道完成时会将 `pid` 设置为该进程组 ID 的负值，以便管道中的任何进程都会导致 `waitpid` 返回。

当 `waitpid` 因为匹配 `pid` 参数的子进程改变状态而返回时，会返回该子进程的进程 ID。在一种情况下会返回零，这种情况将在下文 `WNOHANG` 选项下解释。

只能等待直接子进程——即那些通过 `fork` 创建的子进程。孙子进程（即通过 `fork` 创建的子进程的子进程）不能被等待，即使它们的父进程（直接子进程）已经终止。如前一节所述，孤儿进程由一个特殊的系统进程继承，而不是由祖父进程继承。

通常，进程等待其创建的每个子进程是很重要的——否则，已终止的子进程将作为僵尸留在系统中，直到父进程终止，届时继承它们的系统进程会执行等待并将它们彻底清理掉。由于有些进程很长时间都不终止（有时长达数月），让僵尸存在那么久真的会塞满系统表。如果等待太麻烦，进程可以使用信号来消除僵尸，如下一节所述。

状态改变的子进程，称为可等待的（waitable），最多只能导致一次 `waitpid` 返回。换句话说，一个已被等待的可等待子进程不再可等待。这意味着，如果程序的某一部分获取了状态并发现这不是它期望的进程的状态，那么没有办法将该结果塞回系统中，以便稍后其他 `waitpid` 能获取该进程的状态。（不过，`waitid` 调用可以做到这一点——见下文。）

如果执行 `waitpid` 且存在符合 `pid` 规范的可等待子进程，`waitpid` 会立即返回。如果存在这样的子进程但它尚未改变状态，`waitpid` 会阻塞，直到有一个合适的可等待子进程。如果根本没有匹配 `pid` 的子进程，`waitpid` 返回 -1 并将 `errno` 设置为 `ECHILD`。可能没有子进程，因为 `pid` 仅仅是错误的，或者因为子进程已经被等待过，在这种情况下它不再可等待（但再次，参见 `waitid`）。

如果 `statusp` 非空指针，则其指向的整数会被设置为子进程的状态。这是子进程调用 `_exit` 或 `exit` 的参数（如果它是以此方式终止的）与一个指示其如何终止或停止的码的组合。提供了若干宏来解释该整数值：

- `WIFEXITED(status)`：如果子进程正常终止（通过 `_exit` 或 `exit`），则为真

- `WEXITSTATUS(status)`：如果 `WIFEXITED` 为真，则为 `_exit` 或 `exit` 参数的低 8 位

- `WIFSIGNALED(status)`：如果子进程异常终止（因为收到信号），则为真

- `WTERMSIG(status)`：如果 `WIFSIGNALED` 为真，则为导致终止的信号编号

- `WIFSTOPPED(status)`：如果子进程停止，则为真；仅当设置了 `WUNTRACED` 选项时可能（见下文）

- `WSTOPSIG(status)`：如果 `WIFSTOPPED` 为真，则为导致子进程停止的信号编号

- `WIFCONTINUED(status)`：如果进程被继续执行，则为真；仅当设置了 `WCONTINUED` 选项时可能 [X/Open]

- `WCOREDUMP(status)`：如果生成了内存转储文件（在 UNIX 中称为“核心转储”），则为真；有时用于事后分析（该宏非标准，但通常已实现）

最后一个参数 `options` 是一个或多个通过按位或（OR）运算组合的标记：

- `WCONTINUED`：除了已终止的子进程外，还报告被继续执行的子进程。[X/Open]

- `WNOHANG`：如果状态不可立即获取，则不等待子进程；返回 0 而不是进程 ID。

- `WUNTRACED`：除了已终止的子进程外，还报告已停止的子进程。

以下是 `waitpid` 的一些使用示例：

```
/* 等待子进程 pid 终止并获取其状态。 */
ec_neg!( waitpid(pid, &status, 0) )
/* 等待任意子进程终止，但不获取其状态。 */
ec_neg!( pid = waitpid(-1, NULL, 0) )
/* 报告进程组 pgid 中任何已终止或停止的子进程，
并获取其状态。如果状态不可立即获取，则不等待。 */
ec_neg!( pid = waitpid(-pgid, &status, WNOHANG | WUNTRACED) )
```

下面是一个示例程序，它创建了三个子进程，每个子进程的终止方式不同。对于每种终止情况，都会报告其状态。

```
int main(void)
{
    pid_t pid;

    /* 情况 1：显式调用 _exit */
    if (fork() == 0) { /* 子进程 */
        _exit(123);
    }
    /* 父进程 */
    ec_false(wait_and_display())

    /* 情况 2：由内核终止 */
    if (fork() == 0) { /* 子进程 */
        int a, b = 0;
        a = 1 / b;
        _exit(EXIT_SUCCESS);
    }
    /* 父进程 */
    ec_false(wait_and_display())

    /* 情况 3：外部信号 */
    if ((pid = fork()) == 0) { /* 子进程 */
        sleep(100);
        _exit(EXIT_SUCCESS);
    }
    /* 父进程 */
    ec_neg!( kill(pid, SIGHUP) )
    ec_false(wait_and_display())

    exit(EXIT_SUCCESS);
}

EC_CLEANUP_BGN
exit(EXIT_FAILURE);
EC_CLEANUP_END
}

static bool wait_and_display(void)
{
pid_t wpid;
int status;

c_negl( wpid = waitpid(-1, &status, 0) )
display_status(wpid, status);
return true;

EC_CLEANUP_BGN
return false;
EC_CLEANUP_END
}

void display_status(pid_t pid, int status)
{
if (pid != 0)
printf("Process %ld: ", (long)pid);
if (WIFEXITED(status))
printf("Exit value %d\n", WEXITSTATUS(status));
else {
char *desc;
char *signame = get_macrostr("signal", WTERMSIG(status), &desc);
if (desc[0] == '?')
desc = signame;
if (signame[0] == '?')
printf("Signal #%d", WTERMSIG(status));
else
printf("%s", desc);
if (WCOREDUMP(status))
printf(" - core dumped");
if (WIFSTOPPED(status))
printf(" (stopped)");
#else defined(_XOPEN_UNIX) && !defined(LINUX)
else if (WIFCONTINUED(status))
printf(" (continued)");
#endif
printf("\n");
}
}
```

如前所述，下面这一行

```c
#if defined(_XOPEN_UNIX) && !defined(LINUX)
```

单独针对 Linux 进行测试，因为它错误地声称符合 X/Open 标准。

函数 `get_macrostr` 提供了信号编号的可打印版本（除其他功能外），其工作方式与 1.4.1 节中的 `errsysob` 非常相似。如果你感兴趣，代码可以在网站 [AUP2003] 上找到。

这是该程序的输出：

```
Process 9585: Exit value 123
Process 9586: Erroneous arithmetic operation - core dumped
Process 9587: Hangup
```

如输出所示，在情况 1 中，子进程通过调用 `exit` 并传入退出值 123 来终止自身。在情况 2 中，当子进程尝试除以零时，被 `SIGFPE`（浮点运算错误）信号终止。在情况 3 中，正在休眠的子进程被其父进程发送的 `SIGHUP` 信号终止。（发送信号的 `kill` 系统调用位于 9.1.9 节。）

我们将在本章稍后的 shell 的下一个版本中使用函数 `display_status`。

第二种变体，`wait` 系统调用，是 `pid` 为 -1 且无选项的 `waitpid` 的简写形式：

![](img/41b4c8f6d6a5c349eee321a301703d97_323_0.png)

由于 `pid` 设为 -1 的 `wait` 和 `waitpid` 会等待任意子进程，因此当一个作为更大程序一部分的函数创建了一个它想要等待的子进程时，它们通常是不合适的。它可能会意外地收到完全来自其他子进程的返回结果，而且由于一个子进程只能被等待一次，这将剥夺程序其他部分等待该子进程的能力，从而导致潜在的混乱。最好使用 `waitpid` 等待特定的子进程，或至少等待进程组中的某个成员，因此 `wait` 很少在简单程序之外使用。它绝不应该用于创建子进程库函数中。

但假设一个进程有两个子进程，且无法预测哪个会先终止。如果它只关心等待它们两个都终止，它可以简单地等待其中任意一个，然后在该次 `waitpid` 调用返回时，等待另一个。或者，父进程可以继续执行其自身的工作，并定期使用 `WNOHANG` 选项为每个进程发起 `waitpid` 调用。但是，正如我们所说，除非能保证没有其他子进程，否则它不应该发起通用的 `waitpid` 调用（`pid` 参数为 `-1`）。通常，在大型、复杂的程序中，其部分代码来自不同的开发团队（例如，成像库、数据库接口），就无法保证没有其他子进程。如果能向某种 `wait` 变体传递一个进程 ID 数组，那就再好不过了，但实际上不能。

第三种变体，`waitid`，随着 SUS1 进入 UNIX，因此截至撰写本文时，它尚不存在于 Linux 或 FreeBSD 中。它提供了一项重要的新功能：你可以在保持进程仍可等待的状态下获取其状态，因此查询错误的进程不会造成损害。此外，它比 `waitpid` 或 `wait` 提供更多信息。以下是其概要：

**`waitid`**—等待子进程状态改变 [X/Open]

```c
#include <sys/wait.h>
int waitid(
    idtype_t idtype, /* id 的解释 */
    id_t id,         /* 进程或进程组 ID */
    siginfo_t *infop,/* 返回的信息 */
    int options
);
/* 成功返回 0，出错返回 -1（并设置 errno） */
```

**`siginfo_t`**—用于 `waitid` 的结构体

```c
typedef struct { /* 仅显示与 waitid 相关的成员 */
    int si_code; /* 代码（见下文） */
    pid_t si_pid; /* 子进程 ID */
    uid_t si_uid; /* 子进程的真实用户 ID */
    int si_status; /* 退出值或信号 */
} siginfo_t;
```

`waitid` 的第一个参数 `idtype` 是以下之一：

- `P_PID`：等待进程 ID 为 `id` 的子进程（类似 `pid > 0` 的 `waitpid`）

- `P_PGID`：等待进程组 `id` 中的任何子进程（类似 `pid < -1` 的 `waitpid`）

- `P_ALL`：等待任何子进程（类似 `pid = -1` 的 `waitpid`）；`id` 被忽略

对于 `pid = 0` 的 `waitpid` 没有直接的等价物，但可以使用 **`P_PID`** 且 `id` 等于调用者的进程组 ID 来实现相同的效果。
