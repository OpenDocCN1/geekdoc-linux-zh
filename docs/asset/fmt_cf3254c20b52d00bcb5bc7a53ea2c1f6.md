
`sigwaitinfo()` 的一个示例见列表 22-6。该程序首先阻塞所有信号，延迟其可选命令行参数中指定的秒数。这允许信号在 `sigwaitinfo()` 之前发送到程序。程序随后循环使用 `sigwaitinfo()` 接受传入的信号，直到接收到 `SIGINT` 或 `SIGTERM`。

下面的 shell 日志演示了该程序的使用，我们在后台运行该程序，指定它在调用 `sigwaitinfo()` 之前延迟 60 秒，然后发送了两个信号：

```bash
$ /t_sigwaitinfo 6 &
./t_sigwaitinfo: PID is 383
./t_sigwaitinfo: signals blocked
./t_sigwaitinfo: about to delay 60 seconds
[1] 383
$ /t_sigqueue 383 43
./t_sigwaitinfo: PID is 383, UID is 100
$ /t_sigqueue 383 42
./t_sigwaitinfo: PID is 383, UID is 100
```

最终，程序完成了它的睡眠间隔，`sigwaitinfo()` 接受了队列信号。（因为 `sigwaitinfo()` 是从后台输出，我们看到了程序的下一行。）我们看到信号首先被递送，并且 `siginfo_t` 结构允许我们获取发送进程的 ID：

```
got signal: 42
si_sign=42, si_code=-1 (SI_QUEUE), si_value=200
pid=383, uid=100
got signal: 43
si_sign=43, si_code=-1 (SI_QUEUE), si_value=100
pid=383, uid=100
```

我们继续使用 `kill` 命令向进程发送信号。这次，我们看到 `si_code` 字段被设置为 `SI_USER`（而不是 `SI_QUEUE`）：

```
Press Enter to see next promptDisplay of shell
$ echo 374
$ kill -USR1 383
Shell sends SIGUSR1 using kill(
got signal: 10
si_sign=10, si_code=0 (SI_USER), si_value=100
pid=374, uid=100
Press Enter to see next prompt
$ kill -TERM
Terminate program with SIGTERM
Press Enter to see notification of background job
[1]+ Done ./t_sigwaitinfo 60
```

在接收到的 `SIGUSR1` 信号输出中，我们看到 `si_value` 字段值为 100。这是通过 `sigwaitinfo()` 发送的先前信号所初始化的值。我们早早注意到 `si_value` 字段包含了通过 `sigwaitinfo()` 发送的信号的有效信息。

# Listing 列表 22-6: 使用 `sigwaitinfo()` 同步等待信号

```c
#define GNU_SOURCE
#include <string.h>
#include <signal.h>
#include <time.h>
#include <sys/types.h>

int main(int argc, char *argv[])
{
    int sig;
    siginfo_t si;
    sigset_t allSigs;

    if (argc > 1 && strcmp(argv[1], "--help") == 0)
        usage("s: PID [delay-secs]", argv[0]);

    printf("%s: PID is %d\n", argv[0], (long)getpid());

    /* Block all signals (except SIGKILL 和 SIGSTOP) */
    sigfillset(&allSigs, NULL);
    if (sigprocmask(SIG_SETMASK, &allSigs, NULL) == -1)
        perror("%s: signals blocked\n", argv[0]);

    if (argc > 1) {
        /* Delay so that signals can be sent to us */
        printf("%s: to delay by %d seconds\n", argv[0], atoi(argv[1]));
        sleep(strtol(argv[1], NULL, 10));
    }
    printf("%s: finished\n", argv[0]);
```

```c
    for (int i=0; ; i++) {
        /* Fetch signals until SIGINT (^C) 或 SIGTERM */
        sig = sigwaitinfo(&allSigs, &si);
        if (sig == -1)
            perror("sigwaitinfo");

        if (sig == SIGINT || sig == SIGTERM)
            exit(EXIT_SUCCESS);
    }

    printf("got signal: %d (%s)\n", sig, strsignal(sig));
    printf("si_signo=%d, si_code=%d (%s), si_value=%d\n",
        si.si_signo, si.si_code, 
        (si.si_code == SI_USER) ? "SI_USER" : 
           (si.si_code == SI_QUEUE) ? "SI_QUEUE" : "other",
        si.si_value);
    printf("si_pid=%ld, si_uid=%ld\n",
      (long)si.si_pid, (long)si.si_uid);
}
```

`signals/t_sigwaitinfo.c`

`sigtimedwait()` 系统调用是 `sigwaitinfo()` 的变体。唯一的区别是 `sigtimedwait` 允许我们指定等待时间限制。

```c
#define POSIX_C_SOURCE 199909
#include <signal.h>
```

```c
int sigtimedwait(const sigset_t *set, siginfo_t *info,
                                     struct timespec *timeout);
```

成功时返回信号号，出错或超时（`EAGAIN`）时返回 -1。

`timeout` 参数指定 `sigtimedwait()` 等待信号的最大时间。它指向一个以下类型的结构：

```c
struct timespec {
    time_t t_sec;      /* 秒 ('time_t' 是一个整数类型） */
    long t_nsec;      /* 纳秒 */
};
```

`timespec` 结构的字段被填充以指定 `sigtimedwait()` 应等待的最大秒数和纳秒数。将结构的两个字段都设置为 0 会导致立即超时——即检查指定的信号集中是否有任何处于挂起状态的信号。如果调用在没有递送信号的情况下超时，`sigtimedwait()` 将以错误 `EAGAIN` 失败。

如果 `timeout` 参数指定为 `NULL`，`sigtimedwait()` 完全等同于 `sigwaitinfo()`。SysV 未规定 `NULL timeout` 的含义，某些实现将其解释为立即返回的轮询请求。

`mask` 参数是一个信号集，指定了我们可以通过 `signalfd` 文件描述符读取的信号。与 `waitinfo()` 类似，我们通常应该在 `sigprocmask()` 中阻塞所有信号，这样这些信号在我们有机会读取它们之前就不会按照它们的默认位置被递送。

如果 `fd` 被指定为 -1，`signalfd()` 会创建一个新的文件描述符，用于读取 `mask` 中的信号；否则，它将修改与 `fd` 关联的掩码，而 `fd` 必须是由之前调用 `signalfd()` 创建的文件描述符。

在初始实现中，`flags` 参数被留以后使用，并且必须指定为 0。然而，自 Linux 2.6.27 起，支持了两个标志：

- `SFD_CLOEXEC`：设置“执行时关闭”（`FD_CLOEXEC`）标志，这在某些情况下非常有用，类似于第 4.3.1 节描述的 `open()` 的 `O_CLOEXEC` 标志。
