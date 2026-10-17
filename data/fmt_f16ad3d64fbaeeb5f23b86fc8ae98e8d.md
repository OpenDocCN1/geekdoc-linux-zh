
```c
15     pid = fork();    /* 创建一个新的子进程 */
16 
17 if (pid == -1) {
18     fprintf(stderr,"%s: Failed to fork()\n", strerror(errno));
19     exit(13);
20 }
21 else if (pid == 0) {
22     printf("PID %ld: Child started, parent is %ld.\n",
23             (long)getpid(),    /* 当前子 PID */
24             (long)getppid());    /* 父 PID */
25     return 0;                /* 子进程直接退出 * */
26: }
27: /*
28: * 父进程 :
29: */
30:
31: (long)getpid(), /* 当前父 PID * */
32: (long)pid); /* 进程 PID */
33: sleep(1); /* 等待一秒 */
34:
35: /*
36:
37: * 到此时，我们的子进程应该已经终止
38: */
39: system("ps -1"); /* 列出僵尸 * */
40:
41: return 0;
42: }
```

列表 19.2 中的程序与之前的列表不同之处在于子进程通过第 24 行的返回语句立即退出。只有父进程会执行第 28–42 行。

父进程在第 34 行通过调用 `sleep(3)` 等待一秒。这为子进程的启动和终止留了充足的时间。由于父进程从未调用 `wait(2)`，第 39 行的 `system(3)` 调用导致 `ps(1)` 命令列出僵尸进程。

以下是在 FreeBSD 下编译和运行的示例：

```bash
$ make zombie
cc -D_Wall zombie.c
cc -o zombie zombie.o
$zombie
PID 1367: Started child PID 1368.
PID 1368: Child started, parent is 1367.
UID PID PPID CPU NI VSZ RSS STAT TIME COMMAND
1001 1231 1 0 10 596 344 S p 0:00:07 -sh
1001 1233 3 0 10 600 348 wait Ss 0:00:24 -sh (sh)
1001 1367 2 0 10 824 404 S+ 0:00:01 ./zombie
1001 1368 1367 0 0 Z+ 0:00:00 (zombie)
1001 1369 1 0 10 496 332 S+ 0:00:00 ps -1
1001 1370 1 28 0 380 244 R+ 0:00:00 ps -
```

输出显示 `./zombie` 为进程 ID 1367。进程 1368 是由第 14 行的 `fork()` 创建的子进程。`ps(1)` 命令提供的输出（进程 1369 和 1370）显示子进程 1368 是僵尸（zombie）。

## wait(2) 函数

`wait(2)` 函数挂起调用进程，直到子进程终止或接收到信号。函数原型如下：

```c
#include <sys/types.h>
#include <sys/wait.h>
pid_t wait(int *status);
```

参数 `status` 必须是一个指向 `int` 的指针，`wait(2)` 将接收子进程的终止状态。返回值是与终止状态匹配的进程 ID。否则，返回 `(pid_t)-1` 错误位于变量 `errno`（当接收到信号时）。

列表 19.3 中的程序是之前示例的修改版本。在这个示例中，`sleep(3)` 被 `wait(2)` 系统调用取代。

## 列表 19.3 调用 wait(2) 无僵尸进程的示例

```c
1: /* wait.c */
2: #include <stdio.h>
3: #include <unistd.h>
4: #include <string.h>
5: #include <errno.h>
6: #include <sys/types.h>
7: #include <sys/wait.h>
8:
9: int
10: main(int argc, char **argv) {
11:     pid_t pid;                      /* 子进程的 PID */
12:     pid_t wpid;                     /* 来自 wait(2) 的 PID */
13:     int status;                      /* 来自 wait(2) 的状态 */
14:     pid = fork();                    /* 创建一个新的子进程 */
15:     if (pid == (pid_t)-1) {
16:         fprintf(stderr,"%s: Failed to fork()\n", strerror(errno));
17:         exit(13);
18:     } else if (pid == 0) {
19:         printf("PID %ld: Child started, parent is %ld.\n",
20:                 (long)getpid(),    /* 当前 PID */
21:                 (long)getppid());    /* 父 PID */
22:         return 0;                /* 子进程直接退出 * */
23:     }
24:     /* 父进程 : */
25:     printf("PID %ld: Started child PID %ld.\n",
26:                 (long)getpid(),
27:                 (long)wpid);
28:
29:     /* 等待子进程退出并获取其终止状态 */
30:     wpid = wait(&status);
31:     if (wpid == (pid_t)-1) {
32:         perror("Wait");
33:     }
34:     /* 列出进程 */
35:     system("ps -1");
36:     return 0;
37: }
```

变量 `wpid` 和 `status` 定义在第 14 行和 15 行。它们用于第 42–44 行的 `wait(2)` 调用。`wait(2)` 调用导致父进程挂起执行，直到子进程终止。当执行 `ps(1)` 命令时，将没有终止进程的痕迹。

在 FreeBSD 下编译和运行提供以下结果：

```bash
$ make wait
cc -Wall wait.c
cc -o wait wait.o
$ ./wait
PID 1463: Started child PID 1464.
PID 1464: Child started, parent is 1463.
UID PID PPID CPU PRI NI VSZ RSS WCHAN STAT TT COMMAND
1001 1231 1 0 10 596 344 wait p 0:00:07 -sh (sh)
1001 1233 3 0 10 600 348 wait Ss 0:00:24 -sh
1001 1463 2 0 10 824 404 S+ 0:00:01 ./wait
1001 1464 1463 0 0 Z+ 0:00:00 (zombie)
1001 1465 1 0 10 496 332 S+ 0:00:00 sh -c ps -1
```

在此会话中，输出显示 `./wait` 为进程 ID 1463。进程 1464 是由第 14 行的 `fork()` 创建的子进程。`ps(1)` 命令提供的输出显示子进程 1464 是僵尸。这种情况是因为父进程通过调用 `wait(2)` 获取了子进程的终止状态。系统调用 `wait(2)` 导致内核释放进程表条目，因此不再有僵尸进程。

## 解释退出状态

`wait(2)` 返回的状态包含的比程序退出码更多的信息。它记录了程序是正常退出、中止、被杀死（接收信号）还是停止。预计程序员使用宏来测试这些状态差异，因为这是使用此类状态信息的唯一可能方法。列表 19.1 标识了程序员可以使用宏。

| 表 19.1 状态宏表 |
| :--- | :--- |
| `WIFEXITED(status)` | 如果状态表示进程正常退出，则该宏返回真。可以使用宏 `WEXITSTATUS(status)` 获取进程的退出码，它返回一个 8 位退出码。 |
| `WIFSIGNALED(status)` | 如果状态表示进程接收到了未捕获的信号并导致其终止，则该宏返回真。可以使用 `WTERMSIG(status)` 从状态中提取导致终止的信号号。可以使用宏 `WCOREDUMP(status)`，它指示是否创建了转储文件。 |
| `WIFSTOPPED(status)` | 如果状态表示进程当前已停止，则该宏返回真。可以使用 `WOPSIG(status)` 从状态中提取导致进程停止的信号号。 |

# 其他 wait 系统调用

`wait(2)` 家族中的其他成员提供了额外的功能。这些额外的成员在下述概要所示：

```c
#include <sys/types.h>
#include <sys/wait.h>
pid_t waitpid(pid_t wpid, int *status, int options);
#include <sys/time.h>
#include <sys/resource.h>
pid_t wait3(int *status, int options, struct rusage *rusage);
pid_t wait4(pid_t wpid, int *status, int options, struct rusage *rusage);
```

`wait(2)` 函数是 `wait(2)` 的 POSIX 扩展，在没有数据可报告时，它可以在不返回数据的情况下返回。这与 `wait(2)` 系统调用对比，后者始终阻塞调用进程的执行，直到有信息可报告为止。`waitpid(2)` 系统调用也可以等待特定的子进程 ID。当父进程有多个悬待处理的子进程时，这有时非常有用。

## 注意

所有现代 UNIX 平台都支持 `wait(2)` 和 `waitpid(2)` 函数。然而，Solaris 8 不支持 BSD 函数 `wait3(2)` 和 `wait4(2)`。

`wait3(2)` 系统调用受 IBM AIX 4.3、SGI IRIX 6.5、HPUX 11 和 UnixWare 7 支持。

Linux 和 BSD 支持 `wait(2)`、`waitpid(2)`、`wait3(2)` 和 `wait4(2)` 函数。

`wait3(2)` 和 `wait4(2)` 系统调用允许在状态之外返回子进程的资源利用情况。`wait3(2)` 允许像 `waitpid(2)` 调用一样指定选项。`wait4(2)` 系统调用是家族中最灵活的，因为它除了其他调用支持的功能外，还包含了等待特定子进程的能力。

`options` 参数支持以下位掩宏：

| | |
|---|---|
| `WNOHANG` | 如果无报告内容则立即返回 |
| `WUNTRACED` | 报告收到 `SIGTTIN`、`SIGITTOU`、`SIGTSTP` 或 `SIGSTOP` 信号的子进程 |

`WNOHANG` 选项用于 `waitpid(2)`、`wait3(2)` 或 `wait4(2)`，当执行不能挂起时。这允许父进程在不放弃控制权的情况下查询子进程的状态。`WUNTRACED` 选项用于 shell 作业控制，超出了本文范围。

`waitpid(2)` 和 `wait4(2)` 调用允许调用者在参数 `wpid` 中指定特定的子进程 ID。将 `wpid` 指定为 `-1` 会导致这些系统等待子进程，就像 `wait(2)` 和 `wait3(2)` 调用所做的。

`wait(2)` 家族中的所有系统调用在调用成功时都会返回返回信息的进程 ID。当报告错误时，返回值 `(pid_t)-1`，错误代码为 `errno`。当选项参数包含 `WNOHANG` 位时，返回值 `(pid_t)0` 表示没有可用信息。

如果执行 `wait(2)` 家族调用且没有可报告的悬待子进程，则可能发生错误代码 `ECHILD`。例如，如果当前进程没有启动任何子进程，就会发生这种情况。这与 `(pid_t)0` 返回值（用于 `WNOHANG` 选项）不同，后者表示至少有一个子进程正在执行。

## 注意

`ECHILD`—无子进程。当调用父进程没有子进程时，`wait(2)`、`waitpid(2)`、`wait3(2)` 或 `wait4(2)` 返回此值。

当参数 `wpid` 不代表调用进程的子进程时，会报告 `ECHILD`。

资源利用结构根据 UNIX 平台而异。FreeBSD 的定义如下述概要所示：

```c
struct rusage {
    struct timeval ru_utime; /* 用户使用时间 */
    struct timeval ru_stime; /* 系统使用时间 */
    long ru_maxrss; /* 最大驻内存大小 */
    long ru_ixrss; /* 整数共享内存大小 */
    long ru_idlim;
    long ru_isrss;
    long ru_minflt;
    long ru_majflt;
    long ru_nrss;
    long ru_inblock; /* 块输入操作 */
    long ru_oblock; /* 块输出操作 */
    long ru_msgsnd; /* 发送的消息 */
    long ru_msgrcv; /* 接收的消息 */
    long ru_nsignals; /* 接收的信号 */
    long ru_nvcswitch; /* 自愿上下文切换 * */
    long ru_nivcsw; /* 非自愿上下文切换 * */
}; /* FreeBSD 3.4 release */
```

在支持 `wait3(2)` 或 `wait4(2)` 的 UNIX 平台上使用的常用资源是 `ru_utime` 和 `ru_stime`。它们分别代表用户和系统 CPU 时间。该结构中的其他成员可能是平台特有的。

# 执行新程序

虽然 `fork(2)` 系统调用的是当前进程的克隆，但程序员仍然需要一种方法启动新的可执行程序。`exec(2)` 函数族填补了这一需求。

当执行新程序时，会执行以下通用步骤：

1. 内核调用当前进程的克隆，但程序员仍然需要一种方法启动新的可执行程序。`exec(2)` 函数族填补了这一需求。
2. 内核打开可执行文件进行读取（如果失败，执行被挂起）。
3. 从可执行文件加载新程序（可执行位已设置）。
4. 内核重置某些标志位（例如栈指针被重置）。
5. 新程序开始执行。

`exec(2)` 调用的整体效果是用新程序替换当前执行的进程。当 `execve()` 调用成功时，它不会返回控制权。

有许多函数可以启动新程序，但首先描述的是 `execve()` 函数：

```c
#include <unistd.h>
int execve(const char *pathname, char *const argv[], char *const envp[]);
```

该函数接受三个参数：

- 程序的路径
- 传递给 `main()` 的 `argv[]` 数组
- 环境变量 `envp[]` 数组

当函数成功时，不返回。如果调用失败，返回值为 `-1`，`errno` 将包含错误代码。

```c
/* exec.c */
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <errno.h>
#include <sys/types.h>
#include <sys/wait.h>

/*
 * 如果系统上的 ps(1) 命令不在 /bin/ps，
 * 则请修改下方定义的 PS_PATH 路径。
 */
#define PS_PATH "/bin/ps"   /* PS(1) */

extern char *environ;               /* 我们的环境变量 */

/*
 * EXEC(2) PS(1) 命令：
 */
static void
exec_ps_cmd(void) {
    static char *argv[] = { "ps", "-l", NULL };
    /*
     * 执行 ps 命令: ps f
     */
    execve(PS_PATH, argv, environ);
    /*
     * 如果程序执行到这里，说明 execve(2)
     * 调用失败了！
     */
    fprintf(stderr, "%s: execve(2)\n", strerror(errno));
}

/*
 * 主程序：
 */
int
main(int argc, char **argv) {
    /* 子进程的进程 ID */
    pid_t pid;
    /* 来自 wait() 的进程 ID */
    pid_t wpid;
    /* 来自 wait() 的退出状态 */
    int status;
    /*
     * 创建一个新的子进程：
     */
    pid = fork();
}
```
