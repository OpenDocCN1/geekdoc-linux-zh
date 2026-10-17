
```
$ /a.out
normal termination, exit status = 7
abnormal termination, signal number = 6 (core file generated)
abnormal termination, signal number = 8 (core file generated)
```

遗憾的是，没有通用的方法可以将信号值映射到 `WTERMSG` 的描述性名称。（方法见第 10.21 节）。我们必须查看 `<signal.h>` 头文件来验证 `SIGABRT` 的值为 6，`SIGFPE` 的值为 8。

### 图 8.5. 退出状态描述

```c
#include "apue.h"
#include <sys/wait.h>

void
pr_exit(int status)
{
    if (WIFEXITED(status))
        printf("normal termination, exit status = %d\n",
               WEXITSTATUS(status));
    else if (WIFSIGNALED(status))
        printf("abnormal termination, signal number = %d\n",
               WTERMSIG(status));
#ifdef WCOREDUMP
        printf(WCOREDUMP(status) ? " (core file generated)" : "");
#else
        printf("");
#endif
    else if (WSTOPPED(status))
        printf("child stopped, signal number = %d\n",
               WSTOPSIG(status));
}
```

### 图 8.6. 演示不同的退出状态

```c
#include "apue.h"
#include <sys/wait.h>

int
main(void) {
    pid_t pid;
    int status;

    if (pid = fork()) < 0
        err_sys("fork error");
    else if (pid == 0) /* child */
        exit(7);

    if (wait(&status) == pid) /* wait for child */
        err_sys("wait error");
    pr_exit(status); /* and print its status */

    if (pid = fork()) < 0
        err_sys("fork error");
    else if (pid == 0) /* child */
        abort(); /* generates SIGABRT */

    if (wait(&status) == pid) /* wait for child */
        err_sys("wait error");
    pr_exit(status); /* and print its status */

    if (pid = fork()) < 0
        err_sys("fork error");
    else if (pid == 0) /* child */
        status /= 0; /* divide by 0 generates SIGFPE */

    if (wait(&status) == pid) /* wait for child */
        err_sys("wait error");
    pr_exit(status); /* and print its status */

    exit(0);
}
```

如所述，我们有多个子进程，`wait` 在子进程终止时返回。如果我们想等待某个特定的进程终止（假设我们知道想要等待的进程 ID）该怎么办？在旧版本的 UNIX 系统中，我们必须调用 `wait` 并将返回的进程 ID 与有效值进行比较。如果终止的进程不是我们想要的，我们必须保存进程 ID 和终止状态，并再次调用 `wait`。我们需要继续这样做，直到所需的进程终止为止。下次当我们想要等待某个特定进程时，我们将遍历已终止进程的列表，查看我们是否已经等待过它，如果没有，则再次调用 `wait`。针对特定进程的函数是什么？这种功能（以及更多）由 POSIX.1 `waitpid` 函数提供。

`waitpid` 参数的解释取决于它的值：

```
pid == 1    等待子 pid。在这方面，waitpid 等于 wait。
pid > 0     等待进程 ID 等于 pid 的子进程。
pid == 0    等待进程 ID 等于调用进程 ID 的任何子进程。（我们将在第 9.4 节讨论进程组）
pid < 1     等待进程 ID 等于 qid 绝对值的任何子进程。
```

`waitpid` 函数返回已终止的子进程的进程 ID，并将子进程的状态信息存储在 `stat` 指向的内存位置。唯一的真实错误是调用进程没有子进程。

### 图 8.7. waitpid 的选项

| 常量 | 描述 |
| :--- | :--- |
| `WCONTINUED` | 如果实现支持作业控制，则返回任何停止子进程的状态。 |
| `WNOHANG` | 如果子进程没有立即可用，`waitpid` 不阻塞；返回 0。 |
| `WTRACED` | 如果实现支持作业控制，则返回任何停止子进程的状态。 |

### 示例

回顾第 8.5 节关于僵尸进程的讨论。如果我们想写一个进程，它产生一个子进程但我们不希望子进程在我们终止之前变成僵尸，方法是调用两次。图 8.8 中的程序就是这样做。

我们在第二个子进程中调用 `sleep` 以确保子进程在父进程之前终止。`fork` 之后，父进程或子都可以都可以执行；我们不知道哪个先执行。如果我们没有让第二个子进程睡眠，它在父进程之前执行，它打印的进程 ID 将不是 1。

执行图 8.8 中的程序得到：

```
$ /a.out
second child, parent pid = 1
```

注意 shell 在原始进程终止时会打印提示符，这发生在第二个子进程打印其父 ID 之前。

### 图 8.8. 通过调用两次避免僵尸进程

```c
#include "apue.h"
#include <sys/wait.h>

int main(void)
{
    pid_t pid;

    if (pid = fork()) < 0) {
        err_sys("fork error"); /* first child */
    } else if (pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid > 0) {
        exit(0); /* parent from second fork == first child */
        /* 我们是第二个子进程；一旦我们的父进程调用上面的
           * exit，我们的父进程就会变成 init。
           * 在这里我们继续执行，知道如果不
           * 执行，init 将重复我们的状态。
           */
        sleep(2);
        printf("second child, parent pid = %d\n", getppid());
        exit(0);
    }

    if (waitpid(pid, NULL, 0) != 1) /* wait for first child */
        err_sys("waitpid error");

    /* 我们是父进程（原始进程）；我们继续执行，
       * 我们不是第二个子进程的父进程。
    */
    exit(0);
}
```

## 8.7. waitid 函数

单 Unix 规范（Single UNIX Specification）的 XSI 包含一个额外的函数用于获取进程的退出状态。`waitid` 与 `waitpid` ，但提供了更大的灵活性。

```c
#include <sys/wait.h>

int waitid(id_t itype, id_t pid, siginfo_t *infop, int options);
```

返回值：成功返回 0，错误返回 1

与 `wait` 不同，`waitid` 允许进程指定要等待的子进程。它不是将此信息与进程 ID 或进程组 ID 结合在单个参数中，而是使用了独立的参数。`id` 参数根据 `itype` 的值进行解释。支持的类型总结在图 8.9 中。

### 图 8.9 waitid 的 itype 常量

| 常量 | 说明 |
| --- | --- |
| `P_PID` | 等待特定进程：`id` 包含要等待的子进程 `PID`。 |
| `P_PGID` | 等待特定进程组中的任何子进程：`id` 包含要等待的子进程的进程组 `PGID`。 |
| `P_ALL` | 等待任何子进程：`id` 被忽略。 |

`options` 参数是图 8.10 所示标志的按位或操作的结果。这些标志指示了调用者感兴趣的状态变化。

### 图 8.10 waitid 的 options 常量

| 常量 | 说明 |
| --- | --- |
| `WCONTINUED` | 等待一个之前停止并已继续，且状态尚未报告的进程。 |
| `WEXITED` | 等待已退出的进程。 |
| `WNOWHANG` | 如果没有可用的退出状态，则立即返回而不是阻塞。 |
| `WNOWAIT` | 不要销毁子进程退出状态。可以通过后续调用 `wait`、`waitid`、`waitpid` 获取子进程退出状态。 |
| `WSTOPPED` | 等待一个已停止且状态尚未报告的进程。 |

`infop` 参数是一个指向 `siginfo` 结构的指针。该结构包含了关于导致子进程状态变化的生成信号的详细信息。`siginfo` 结构将在第 10.14 节中进行进一步讨论。

在本书涵盖的四个平台中，Solaris 将支持 `wait`。

## 8.8. wait3 和 wait4 函数

大多数 UNIX 系统实现都提供了额外的 `wait3` 和 `wait4` 函数。从历史上看，这两个变体源自 UNIX 系统的 BSD 分支。这两个函数提供的 `wait`、`waitid` 和 `waitpid` 函数未提供的特性是一个额外的参数，它允许内核返回已终止进程及其所有子进程所使用的资源摘要。

```c
#include <sys/types.h>
#include <sys/time.h>
#include <sys/resource.h>

pid_t wait3(int *statoc, int *ataloc, struct rusage *usage);

pid_t wait4(pid_t pid, int *statoc, int options, struct rusage *usage);
```

两者均：成功返回进程 ID，错误返回 0 或 1 或 -1。

资源信息包括：CPU 时间量、使用的内存量、页故障次数、接收到的信号数量等。更多细节请参阅 `getrusage(2)` 手册页。（此资源信息与我们在第 7.11 节中描述的资源限制不同）图 8.11 详细列出了 `wait` 函数支持的各种参数。

### 图 8.11 各种系统支持的 wait 参数

| 函数 | pid | options | usage | POSIX.1 | Free BSD 5.2.1 | Linux 2.4.22 | Mac OSX 10.3 | Solaris 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `wait` | | | | | | | | |
| `waitid` | | | XSI | | | | | |
| `waitpid` | | | | | | | | |
| `wait3` | | | | | | | | |

| 函数 | pid | options | rusage | POSIX.1 | Free BSD 5.2.1 | Linux 2.4.22 | Mac OSX 10.3 | Solaris 9 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| `wait4` | . | . | . | . | . | . | . | . |

`wait3` 函数被包含在单 Unix 规范的早期版本中。在第 2 版中，`wait3` 被移动到了遗留类别：在第 3 版中，`wait3` 从规范中移除。

## 8.9. 竞态条件

就我们而言，竞态条件发生在多个进程尝试对共享数据进行操作，且最终结果取决于它们运行的顺序。`fork` 函数是竞态条件的活跃滋生地，如果在 `fork` 之后的任何逻辑显式或隐式地取决于 `fork` 之后父进程还是子进程先运行，我们就无法预测结果。

结果取决于系统的调度。即使我们知道哪个进程先运行，`fork` 之后发生什么也取决于调度。如果子进程先运行，它可能在父进程有机会之前更新一个文件。这类问题可能很难调试，因为它们在大多数时候运行正常。为了避免竞态条件，需要某种形式的信号。

这种轮询方式的问题在于它浪费 CPU。为了避免竞态条件，需要某种形式的信号。我们将在第 15 节和第 17 节讨论其中一些。也可以使用各种形式的进程间通信（IPC）。

让我们来看使用这五个例程的示例。

### 示例

我们将标准输出设置为无缓冲，因此每个字符输出都会产生一次写操作。此示例的目标是允许内核尽可能在两个进程之间切换，以演示竞态条件。（如果我们不这样做，可能永远看不到后续的类型输出。没有看到错误输出并不意味着竞态条件不存在；它意味着我们在这个特定的系统上看不到它。）实际输出显示了结果是如何变化的：

```
$ .out
output from child
tput from parent
$ .out
output from child
tput from parent
$ .out
output from child
output from parent
```

练习 8.3 继续此示例。

### 图 8.12. 竞态条件的程序

```c
#include "apue.h"

static void charatatime(char *);

int
main(void)
{
    pid_t pid;

    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {
        charatatime("output from child");
    } else {
        charatatime("output from parent");
    }
    exit(0);
}

static void
charatatime(char *str)
{
    char *ptr;
    int c;

    setbuf(stdout, NULL);  /* 设置为无缓冲 */
    for (ptr = str; (c = *ptr++) != 0; ) {
        putc(c, stdout);
    }
}
```

### 图 8.13. 对图 8.12 的修改以避免竞态条件

```c
#include "apue.h"

static void charatatime(char *);

int
main(void)
{
    pid_t pid;

    wait_wait();
    if ((pid = fork()) < 0) {
        err_sys("fork error");
    } else if (pid == 0) {
        wait_parent();  /* 父进程先执行 */
        charatatime("output from child");
    } else {
        charatatime("output from parent");
        wait_child(0);
    }
}

static void
charatatime(char *str)
{
    char *ptr;
    int c;
    setbuf(stdout, NULL);    /* 设置为无缓冲 */
    for (ptr = str; (c = *ptr++) != 0; ) {
        putc(c, stdout);
    }
}
```

![img/902515e97eef28cac8083866e00a6f4c_349_0.png](img/902515e97eef28cac8083866e00a6f4c_349_0.png)

## 10.8. exec 函数

我们在第 8.3 节中提到过使用 `fork` 创建一个新进程（子进程），然后通过调用其中一个 `exec` 函数来执行另一个程序。当进程调用 `exec` 函数时，该进程将完全被新程序替换，新程序开始执行 `main`。在 `exec` 时，进程 ID（PID）不会改变，因为没有创建新进程；`exec` 用磁盘上的新程序替换当前的文本、数据段和栈。

有不同的 `exec` 函数，但我们将简单地统称为“`exec` 函数”，指的是使用任何一种尺寸函数。这些函数完善了 UNIX 系统的进程控制。通过 `fork`，我们可以创建新进程；通过 `exec`，我们可以启动新程序。`exit` 和 `wait` 处理终止和等待终止。这些是我们需要的进程控制原语。我们将在随后的章节中使用这些原语来构建额外的函数，例如 `popen` 系统调用。
