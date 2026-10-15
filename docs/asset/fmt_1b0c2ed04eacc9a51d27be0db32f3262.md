
```c
dg_cli(FILE *fp, int sockfd, SA *pservaddr, socklen_t servlen)
{
    int n;
    char sendline[MAXLINE], recvline[MAXLINE + 1];
    Signal(SIGALRM, sig_alarm);
    while (fgets(sendline, MAXLINE, fp) != NULL) {
        if (recvfrom(sockfd, recvline, MAXLINE, 0, pservaddr, servlen) < 0) {
            alarm(5);
            if (errno == EINTR)
                fprintf(stderr, "socket timeout\n");
        } else {
            alarm(0); /* 空终止 */
            fputs(recvline, stdout);
        }
    }
}

static void
sig_alarm(int signo)
{
    return;
}
```

## 处理 SIGALRM

信号处理程序返回，假设此返回将中断悬挂的 `connect`，导致 `connect` 返回错误 `EINTR`。回想一下我们的信号函数（图 5.6），当捕获的信号为 `SIGALRM` 时，该函数不会设置 `SA_RESTART` 标志。关于这个示例的一点是，我们始终可以使用这种技术缩短 `connect` 的超时时间，但无法扩展内核现有的超时时间。也就是说，在派自 Berkeley 的内核上，`connect` 的超时通常为 75 秒。如果我们为函数指定一个较小的值（例如 10），但如果我们指定一个较大的值，`connect` 仍然会在 75 秒后超时。

关于这个示例的另一点是，我们利用系统调用（`connect`）的可中断性返回到内核定时器。当我们执行系统调用并处理 `EINTR` 错误时，这是可以的。在第 26.6 节中，我们遇到了一个执行系统调用的库函数，当返回 `EINTR` 时，库函数会恢复系统调用。在这种情况下，我们仍然可以使用 `SIGALRM`，但我们在图 26.10 中看到，我们还必须使用 `sigsetjmp` 和 `siglongjmp` 来绕过库对 `EINTR` 的忽略。

## 使用 SIGALRM 实现超时的 recvfrom

图 13.2 是对图 8.8 中 `dg_cli` 函数的重写，但如果未在 5 秒内收到回复，则调用 `alarm` 来中断 `recvfrom`。

## 处理 recvfrom 的超时

为 `SIGALRM` 建立一个信号处理程序，然后在每次调用 `recvfrom` 之前设置 5 秒超时的闹钟。如果 `recvfrom` 被我们的信号处理程序中断，我们

*注：用户提供的文本有很多重复。我将提供最逻辑的清理版本。*

## 第13.3节

```c
#include <unp.h>
/* advio/dgclitimeo2.c */
void dgcli(FILE *fp, int sockfd, const struct sockaddr_in *pservaddr, socklen_t servlen)
{
    int n;
    char sendline[MAXLINE], recvline[MAXLINE + 1];
    struct timeval tv;
    tv.tv_sec = 5;
    tv.tv_usec = 0;
    setsockopt(sockfd, SOCK_SOCKET, SO_RCVTIMEO, &tv, sizeof(tv));
    while (fgets(sendline, sizeof(sendline), fp) != NULL) { // 修复逻辑错误
        if ((n = recvfrom(sockfd, recvline, MAXLINE, 0, pservaddr, NULL)) < 0) {
            if (errno == EULDBLOCK) {
                fprintf(stderr, "socket timeout\n");
                continue;
            } else {
                err_sys("recvfrom error");
            }
        }
        recvline[n] = '\0'; /* 空字符终止 */
        fputs(recvline, stdout);
    }
}
```

`recv` 和 `send` 的第一个参数与 `read` 和 `write` 的第一个参数相同。`flags` 参数可以是 0，也可以通过图 13.6 显示的一个或多个常量进行逻辑或（OR）形成。

| flags | 描述 | recv | send |
|---|---|---|---|
| `MSG_DONTROUTE` | 跳过路由表查找 | * | |
| `MSG_DONTWAIT` | 仅此操作为非阻塞 | | * |
| `MSG_OOB` | 接收或带外数据 | | |
| `MSG_PEEK` | 探测即将进入的消息 | | |
| `MSG_WAITALL` | 等待所有数据 | * | |

图 13.6 I/O 函数的标志。

图 13.5 `dg_cli` 函数，用于接收和发送 `SO_RCVTIMEO` 套接字选项以设置超时。

此标志告诉内核目标位于本地连接的网络上，不要执行路由表查找。我们已通过 `MSG_DONTROUTE` 套接字选项提供了关于此功能的额外信息（第 7.5 节）。可以使用 `MSG_DONTROUTE` 标志启用单个操作的功能，也可以通过套接字选项启用给定套接字的所有输出操作。

## 高级 I/O 函数

此标志指定单个 I/O 操作为非阻塞，而无需打开套接字的非阻塞标志、执行 I/O 操作后再关闭非阻塞标志。我们将在第 15 章中描述非阻塞 I/O，以及如何对套接字上的所有 I/O 操作开启和关闭非阻塞标志。

此标志是 Net/3 引入的新特性，可能在所有系统上都不受支持。

对于 `send`，此标志指定正在发送带外数据。正如我们在第 21 章中描述的，TCP 仅应发送 1 字节的带外数据。对于 `recv`，此标志指定读取带外数据而非普通数据。

此标志允许查看可读数据，而系统不会在 `recv` 或 `recvmsg` 返回后丢弃这些数据。我们将在第 13.7 节中详细讨论这一点。

此标志随 4.3BSD Reno 引入。它告诉内核在读取请求字节数之前不要从 `read` 操作返回。如果系统支持此标志，我们可以省略 `read` 函数（图 3.14）并将其替换为宏：

```c
#define readn(fd, ptr, n) recv(fd, ptr, n, MSG_WAITALL)
```
