
```c
#include "unp.h"

static void recvfrom_alarm(int);

void
dg_clibc(FILE *fp, int sockfd, const SA *pservaddr, socklen_t servlen)
{
    int n;
    const int on = 1;
    char sendline[MAXLINE], recvline[MAXLINE + 1];
    fd_set rset;
    sigset_t sigset_alarm, sigset_empty;
    socklen_t len;
    struct sockaddr *preply_addr;

    preply_addr = Malloc(servlen);
    setsockopt(sockfd, SOL_SOCKET, SO_BROADCAST, &on, sizeof(on));

    FD_ZERO(&rset);
    sigemptyset(&sigset_empty);
    sigemptyset(&sigset_alarm);
    sigaddset(&sigset_alarm, SIGALRM);

    Signal(SIGALRM, recvfrom_alarm);

    while (gets(sendline, MAXLINE, fp) != NULL) {
        sendto(sockfd, sendline, strlen(sendline), 0, passervaddr, servlen);

        sigprocmask(SIG_BLOCK, &sigset_alarm, NULL);
        alarm(5);
        for (;;) {
            FD_SET(sockfd, &rset);
            n = pselect(sockfd + 1, &rset, NULL, NULL, &sigset_empty);
            if (n < 0) {
                if (errno == EINTR)
                    break;
                else
                    err_sys("pselect error");
            } else if (n != 1) {
                err_sys("pselect error: returned %d", n);
            }

            len = servlen;
            n = recvfrom(sockfd, recvline, MAXLINE, 0, preply_addr, &len);
            recvline[n] = 0; /* null terminator */
            printf("%*s: %s\n", len, Sock_ntop(preply_addr, len), recvline);
        }
        free(preply_addr);
    }
}
```

```c
static void
recvfrom_alarm(int sign)
{
    /* just interrupt the recvfrom() */
    return;
}
```

22-33 阻塞 `SIGALRM`，调用 `pselect`。`pselect` 的最后一个参数是指向 `sigset_empty` 变量的指针，这是一个没有阻塞任何信号的信号集，即所有信号都是取消阻塞的。`pselect` 会在当前信号掩码（已阻塞了 `SIGALRM`）、特定的描述符以及必要的信号掩码（设置为空集）时进行阻塞。返回时，预设的信号掩码将重置为调用 `pselect` 时的值。调用 `pselect`、设置信号掩码、测试描述符和重置信号掩码对于调用进程是原子操作。

34-38 如果我们的 socket 是可读的，我们调用 `recvfrom`，尽管知道它不会（阻塞）。

如第 6.9 节所述，`pselect` 是 POSIX 规范中的新特性；图 1.16 中的所有系统、freeBSD 和 Linux 都支持该函数。然而，图 20.8 显示了一个简单但不正确的实现。我们展示这个错误的实现是为了说明涉及的三个步骤：将信号掩码设置为调用者指定的值并保存当前掩码、测试描述符以及重置信号掩码。

## 图 20.8 `pselect` 的简单、不正确的实现。

`lib/pselect.c`

```c
#include    "unp.h"

int
pselect(int nfds, fd_set rset, fd_set wset, fd_set xset,
            const struct timespec *ts, sigset_t *sigmask)
{
            int        n;
            struct timeval tv;
            sigset_t sigmask;
    if (ts != NULL) { tv.tv_sec = ts->tv_sec;
        tv.tv_usec = ts->tv_usec;
    }
        tv.tv_usec = ts->tv_nsec / 1000; /* nanosec -> microsec */
    sigprocmask(SIG_SETMASK, &sigmask); /* caller's mask */
    n = select(nfds, rset, wset, xset, (ts == NULL) ? NULL : &tv);
    sigprocmask(SIG_SETMASK, sigmask);
    return (n);
}
```

## 使用 `setjmp` 和 `longjmp`

解决我们问题的另一种正确方法不是使用信号处理函数来中断调用，而是让信号处理函数使用 `longjmp` 跳出函数。这是因为我们使用了 `setjmp`。图 20.9 展示了这种技术。

### 图 20.9 使用 `setjmp` 和 `longjmp`

`bcast/dgclibcast.c`

```c
#include "unp.h"
#include <jmp.h>

static void recvfrom_alarm(int);
sigjmp_buf jmp;

void
dg_clibc(FILE *fp, int sockfd, const SA *pservaddr, socklen_t servlen)
{
    int n;
    const int on = 1;
    char sendline[MAXLINE], recvline[MAXLINE + 1];
    fd_set rset;
    sigset_t sigset_alarm, sigset_empty;
    socklen_t len;
    struct sockaddr *preply_addr;

    preply_addr = Malloc(servlen);
    setsockopt(sockfd, SOL_SOCKET, SO_BROADCAST, &on, sizeof(on));

    FD_ZERO(&rset);
    sigemptyset(&sigset_empty);
    sigemptyset(&sigset_alarm);
    sigaddset(&sigset_alarm, SIGALRM);

    Signal(SIGALRM, recvfrom_alarm);

    while (gets(sendline, MAXLINE, fp) != NULL) {
        sendto(sockfd, sendline, strlen(sendline), 0, passervaddr, servlen);

        sigprocmask(SIG_BLOCK, &sigset_alarm, NULL);
        alarm(5);
        for (;;) {
            FD_SET(sockfd, &rset);
            n = pselect(sockfd + 1, &rset, NULL, NULL, &sigset_empty);
            if (n < 0) {
                if (errno == EINTR)
                    break;
                else
                    err_sys("pselect error");
            } else if (n != 1) {
                err_sys("pselect error: returned %d", n);
            }

            len = servlen;
```
