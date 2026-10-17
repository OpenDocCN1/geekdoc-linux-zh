
```c
11     listenfd = Tcp_listen(argv[1], argv[2], NULL);

12 else

13     err_quit("tcprec3 {host} <port>");

14 confnd = Accept(listenfd, NULL, NULL);

15 FD_ZERO(rset);

16 FD_ZERO(xset);

17 for ( ; ) {

18     FD_SET(confnd, &rset);

19     if (justreadob == 0)
        FD_SET(confnd, &xset);

20     Select(confnd + 1, &rset, &xset, NULL);

21     if (n = Recv(confnd, buff, sizeof(buff) - 1, MSG_OOB)
        buff[n] = 0; /* null terminate */
        printf("read %d OOB byte: %s\n", n, buff);
        justreadob = 1;

22     FD_CLR(confnd, xset);
23 }
24 }
25 if (FD_ISSET(confnd, rset)) {
26     if (n = Read(confnd, buff, sizeof(buff) - 1) == 0) {
27         printf("received EOP\n");
28         exit(0);
29     }

30     buff[n] = 0; /* null terminate */
31     printf("read %d bytes: %s\n", n, buff);
32     justreadob = 0;
33 }
34 )
```

```c
#include <sys/socket.h>
int socketmark(int sockfd);
```

返回 1 如果是带外标记, 0 如果不是标记, -1 如果发生错误

# 带外数据 (Out-of-Band Data)

```c
#include "unp.h"
int
sockmark(int fd)
{
    int flag;
    if (ioctl(fd, SIOCATMARK, &flag) < 0)
        return (-1);
    return (flag != 0 ? 1 : 0);
}
```

图 21.7 使用 `ioctl` 实现的 `sockmark` 函数。

无论接收进程是以内联方式接收带外数据（`SO_OOBINLINE` 套接选项）还是带外方式接收（`MSG_OOB` 标志），带外标记都会生效。一个常见用途是让接收者在标记传递之前特殊处理所有数据。

### 示例

现在我们通过一个简单的示例来说明带外标记两个特性。

- 1. 带外标记始终指向普通数据最后一个字节之后的一个字节。这意味着，如果带外数据是内联接收的，且下一个读取的字节是带有 `MSG_OOB` 标志发送的字节，则 `sockatmark` 返回真。或者，如果没有启用 `SO_OOBINLINE` 套接选项，且下一个数据字节是带外数据之后发送的第一个字节，则 `sockatmark` 返回真。
- 2. 读取操作始终在带外标记处停止（见 *TCP2* 第 519–520 页）。也就是说，如果接收缓冲区中有 100 个字节，但距离带外标记只有 5 个字节，而进程执行了请求 100 字节的读取操作，则只返回到标记之前的5 个字节。这种在标记处的强制停止允许进程调用 `sockatmark` 来确定缓冲区指针是否位于标记处。

图 21.8 是我们的发送程序。它发送了 3 字节普通数据、1 字节带外数据，随后是另一个字节的普通数据。每个输出操作之间没有暂停。

图 21.9 是接收程序。该程序没有使用 `SIGUR` 信号或 `select`。相反，它调用 `sockatmark` 来确定何时遇到带外字节。

# 第 21.3 节

```c
1 #include "ump.h"
2 int
3 main(int argc, char **argv)
4 {
5     int sockfd;
6     if (argc == 3)
7         err_quit("usage: tcpsend4 <host> <port>");
8     sockfd = Tcp_connect(argv[1], argv[2]);
9     Write(sockfd, "123", 3);
10 printf("wrote 3 bytes of normal data\n");
11 Send(sockfd, "*", 1, MSG_OOB);
12 printf("wrote 1 byte of OOB data\n");

13 Write(sockfd, "5", 1);
14 printf("wrote 1 byte of normal data\n");
15 exit(0);
}
```

图 21.8 发送程序。

```c
1 #include "ump.h"
2 int
3 main(int argc, char **argv)
4 {
5     int listenfd, confnd, n, on = 1;
6     char buff[100];

7     if (argc == 2)
8         listenfd = Tcp_listen(argv[1], NULL);
9    else if (argc == 3)
10        listenfd = Tcp_listen(argv[1], argv[2], NULL);
11    else
12        err_quit("usage: tcrecv04 <host> <port>");

13    confnd = Accept(listenfd, NULL, NULL);
14    setsockopt(confnd, SOL_SOCKET, SO_OOBINLINE, &on, sizeof(on));

15    for (sockmark(confnd)) {
16        printf("at OOB mark\n");

17        if ((n = Read(confnd, buff, sizeof(buff) - 1)) == 0) {
18            printf("received EOP\n");
19            exit(0);
20        }
21        buff[n] = 0; /* /null terminator * */
22        printf("read %d bytes: %s\n", n, buff);
23    }
```

图 21.9 调用 `sockmark` 的接收程序。

# 设置 SO_OOBINLINE 套接选项

我们希望内联接收带外数据，因此必须设置 `SO_OOBINLINE` 套接选项。但如果我们等到 `accept` 返回后再在连接套接字上设置选项，三次握手已经完成，带外数据可能已经到达。因此，我们必须在监听套接字上设置此选项，因为所有的套接选项都会从监听套接字传递到连接套接字（第 7.4 节）。

### 连接后睡眠

接收者在接受连接后睡眠，以便让发送的所有数据被接收。这允许我们证明，即使接收缓冲区中还有额外数据，读取也会在带外标记处停止。

# 读取所有数据

程序在循环中调用 `read` 并打印接收的数据。在调用 `read` 之前，`sockmark` 检查缓冲区指针是否在带外标记处。当我们运行此程序时，会有如下输出：

```
at OOB mark
received EOP
```
