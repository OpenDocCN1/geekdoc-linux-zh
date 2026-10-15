
我们阻塞 `SIGALRM` 并调用 `pselect`。`pselect` 的最后一个参数指向 `sigset_empty` 变量的指针，这是一个没有阻塞信号的信号集，即所有信号都是解阻塞的。`pselect` 会保存当前的信号掩码（该掩码阻塞了 `SIGALRM`），测试描述符，并在必要时使用信号掩码为空集进行阻塞。在返回之前，进程的信号掩码将重置为调用 `pselect` 时的值。`pselect` 的关键在于设置信号掩码、测试描述符以及重置信号掩码。

如果我们的套接字是读的，我们调用 `recvfrom`，知道它不会阻塞。正如第 6.9 节提到的，`recvfrom` 现在在 POSIX 规范中；所有 FreeBSD 和 Linux 系统都支持该函数。尽管如此，图 20.8 显示了一个简单但不错误的实现。我们认为这种实现错误是因为三个步骤：将信号掩码设置为调用者指定的值并保存当前掩码、测试描述符以及重置信号掩码。

```c
#include "unp.h"
int pselect(int nfds, fd_set *rset, fd_set *wset, fd_set *xset,
       const timespec *ts, sigset_t *sigmask)
{
    int n;
    struct timeval tv;
    sigset_t savemask;

    if (ts != NULL) {
        tv.tv_sec = ts->tv_sec;
        tv.tv_usec = ts->tv_nsec / 1000; /* nansec -> microsec */
    }
    sigprocmask(SIG_SETMASK, sigmask, &savemask); /* caller's mask */
    n = select(nfds, rset, wset, (ts == NULL) ? NULL : &tv);
    sigprocmask(SIG_SETMASK, &savemask, NULL); /* restore mask */
    return (n);
}
```

图 20.8 `pselect` 的简单但不错误的实现。

## 使用 sigsetjmp 和 siglongjmp

解决此问题的另一种方法不是利用信号处理器中断阻塞系统调用的能力，而是从信号处理器中调用 `siglongjmp`。这被称为非局部跳转（nonlocal goto），因为我们从一个函数跳回另一个函数。图 20.9 展示了这种技术。

```c
#include <unp.h>
#include <setjmp.h>

static void recvfrom_alarm(int);
static void
dg_cli(FILE *fp, int sockfd, const struct *pservaddr, socklen_t servlen)
{
    int n;
    const int on = 1;
    char sendline[MAXLINE], recvline[MAXLINE + 1];
    socklen_t len;
    struct sockaddr *prely_addr;

    prely_addr = malloc(servlen);
    setsockopt(sockfd, SOL_SOCKET, SO_BROADCAST, &on, sizeof(on));
    signal(SIGALRM, recvfrom_alarm);
    while (fgets(sendline, MAXLINE, fp) != NULL) {
        send(sockfd, sendline, strlen(sendline), 0, pservaddr, servlen);
        alarm(5);
        for ( ; ) {
            if (sigsetjmp(jmpbuf, 1) != 0)
                break;
            len = servlen;
            n = recvfrom(sockfd, recvline, MAXLINE, 0, prely_addr, &len);
            recvline[n] = 0; /* null terminate */
            printf("from %s: %s", sock_ntop(prely_addr, len), recvline);
        }
    }
    free(prely_addr);
}
static void
recvfrom_alarm(int sign)
{
    siglongjmp(jmpbuf, 1);
}
```

图 20.9 信号处理器中使用 `sigsetjmp` 和 `siglongjmp`。

### 分配跳转缓冲区

我们分配了一个供函数和信号处理器使用的跳转缓冲区。

### 调用 sigsetjmp

当我们从 `dg_cli` 函数直接调用 `sigsetjmp` 时，它建立了跳转缓冲区并返回 0。我们继续调用 `recvfrom`。

### 处理 SIGALRM 和 siglongjmp

当信号被递送时，我们调用 `siglongjmp`。这导致 `dg_cli` 函数中的 `sigsetjmp` 返回第二个参数（1），这必须是一个非零值。这将导致 `dg_cli` 中的 `for` 循环终止。

这种方式使用 `setjmp` 和 `siglongjmp` 保证了我们不会因为不时的信号递送而在 `recvfrom` 中永久阻塞。然而，这引入了另一个潜在问题：如果信号在 `printf` 输出过程中递送，我们将有效地跳出 `printf` 并返回到带有不一致数据结构的 `sigjmp`。为了防止这一点，我们应该将图 2.6 中的信号阻塞和解阻塞与非局部跳转结合。这使得解决方案变得复杂，因为信号阻塞必须发生在任何可能因信号中断而产生不良行为的周围。

### 从信号处理器到函数使用 IPC

没有其他方法可以解决我们的问题。信号处理器不再仅仅返回并希望中断阻塞的 `recvfrom`，而是让处理器使用 IPC 通知我们的 `dg_cli` 函数定时器已到期。这与我们之前提出的信号处理器在定时器到期时设置全局 `had_alarm` 类似，但该变量被用作 IPC 的（函数和信号处理器之间的共享内存）。然而，该解决方案的问题在于我们测试该变量的函数，如果信号同时递送，会导致计时问题。

我们在图 2.10 中使用的是进程内部的一条管道，信号处理器在定时器到期时向管道写入一个字节，我们的 `dg_cli` 函数读取该字节以知道何时终止 `for` 循环。这种解决方案之所以非常棒，是因为对管道可读性的测试是使用 `select` 完成的。

### 创建管道

我们创建一个普通的 Unix 管道并返回两个描述符。`pipefd[0]` 是读端，`pipefd[1]` 是写端。

我们也可以使用 `pair` 获取全双工管道。在某些系统（如 SVR4）上，普通的 Unix 管道总是全双工的，我们可以在任何一端进行读写。

### 对套接字和管道端进行 select

我们对 `sockfd` 和 `pipefd[0]`（管道读端）进行 `select`。当 `SIGALRM` 被递送时，我们的信号处理器向管道写入一个字节，使读端变为可用。我们的信号处理器也返回，中断 `select`。因此，如果 `select` 返回 `EINTR`，那么管道读端也将变为可用，从而导致 `for` 循环终止。

### 读取管道

当管道端变为可用时，我们读取信号处理器写入的字节并忽略它。但这告诉我们定时器已到期，因此我们跳出无限 `for` 循环。

# 广播

# 第 20 章
