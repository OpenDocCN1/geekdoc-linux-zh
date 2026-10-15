
```c
21 Write(sockfd, "89", 2);
22 printf("write 2 bytes of normal data\n");
23 sleep(1);
```

```c
24 exit(0);
25 )
```

图 21.3 简单的带带外数据发送程序。

发送了九个字节，在每次输出操作之间有 1 秒的睡眠。暂停的目的是让每次 `write` 或 `send` 作为一个单个 TCP 段传输并被另一端接收。我们稍后会讨论关于带外数据的一些计时考虑因素。当我们运行它时，我们看到了预期的输出：

```
solaris % tcpsends01 badi 9999
write 3 bytes of normal data
write 1 byte of OOB data
write 2 bytes of normal data
write 1 byte of OOB data
write 2 bytes of normal data
```

图 21.4 是接收程序。

### 建立信号处理程序和 socket 所有者

建立了 `SIGURG` 的信号处理程序，并用 `fcntl` 设置了已连接 socket 的所有者。

注意，我们没有在 `accept` 返回之前建立信号处理程序。有一种极小的概率，带外数据会在我们的 TCP 完成三次握手之后、`accept` 返回之前到达，这会导致数据遗漏。但如果我们我们在调用 `accept` 之前建立了信号处理程序，并且设置了所有者，这会传递到连接的 socket，如果带外数据在 `accept` 返回之前到达，我们的信号处理程序中 `confid` 将没有值。如果这对于应用程序很重要，如果你将 `confid` 初始化为 -1，请在信号处理程序中检查此此值，如果为真，则设置一个标志让主循环在 `accept` 返回后检查。*Michael W. Stevens, Unix Socket Programming*

进程从 socket 读取，并打印被读取的每个字符串。当发送端终止连接时，接收端随之终止。

### 我们的信号处理程序

我们的信号处理程序调用 `printf`，通过指定 `MSG_OOB` 标志读取带外数据，并打印返回的数据。注意，我们在 `recv()` 调用中请求了最多 100 字节，但正如我们很快将看到的，只有 1 字节作为带外数据返回。

正如前文所述，不建议在信号处理程序中调用不安全的 `printf` 函数。我们这样做是为了观察程序程序发生了什么。

## 带外数据

## 第 21 章

```c
#include "unp.h"

2 int      listenfd, confnd;
3 void   sig_urg(int);
4 int
5 main(int argc, char **argv)
6 {
7      int      n;
8      char   buff[100];
9      if (argc == 2)
10         listenfd = Tcp_listen(NULL, argv[1], NULL);
11     else if (argc == 3)
12         listenfd = Tcp_listen(argv[1], argv[2], NULL);
13     else
14         err_quit("usage: tcprecv01 <host> <port#");
15     confnd = Accept(listenfd, NULL, NULL);
16     Signal(SIGURG, sig_urg);
17     Fcntl(confnd, F_SETOWN);
18     for ()
19         if ((n = Read(confnd, buff, sizeof(buff) - 1)) == 0) {
20             printf("received EOB!\n");
21             exit(0);
22         }
23         buff[n] = 0;      /* null terminate */
24         printf("read %d bytes: %s\n", n, buff);
25     }
26 }
```

> 图 21.4 简单的带带外数据接收程序。

这是我们运行接收程序，以及从图 21.2.. 中运行发送程序时的输出。

```
badi % tcprecv01 9999
read 3 bytes: 123
SIGURG received
read 1 OOB byte: 4
read 2 bytes: 56
```

21.2 节 TCP 带外数据 571

SIGUR received

read 1 OOB byte: 7

read 2 bytes: 89

received EOF

结果如我们预期的那样。发送端每次发送带外数据都会为接收端生成 SIGUR，接收端读取该单个带外字节。

### 使用 select 的简单示例

我们现在重做带外接收器，使用 `select` 代替 `SIGUR` 信号。

图 21.5 是接收程序。

```c
#1 include "unp.h"
2 int
3 main(int argc, char **argv)
4 {
5     int listenfd, confnd, n;
6     char buff[100];
7     fd_set rset, xset;
8 if (argc == 2)
9     listenfd = Tcp_listen(NULL, argv[1], NULL);
10 else if (argc == 3)
11     listenfd = Tcp_listen(argv[1], argv[2], NULL);
12 else
13     err_quit("usage: tcprecv01 <host> <port>");
14 confnd = Accept(listenfd, NULL, NULL);
15 FD_ZERO(rset);
16 FD_ZERO(xset);
17 for ()
18     FD_SET(confnd, &rset);
19     if (justreadob == 0)
20     FD_SET(confnd, &xset);
21 Select(confnd + 1, &rset, &xset, NULL);
22 if (n = Recv(confnd, buff, sizeof(buff) - 1, MSG_OOB)
23     buff[n] = 0; /* null terminate */
24     printf("read %d OOB byte: %s\n", n, buff);
25     justreadob = 1;
26     FD_CLR(confnd, xset);
27 }
28 }
29 if (FD_ISSET(confnd, rset)) {
30     if (n = Read(confnd, buff, sizeof(buff) - 1) == 0) {
31             printf("received EOP\n");
32         exit(0);
33     }
34     
35     buff[n] = 0; /* null terminate */
36     printf("read %d bytes: %s\n", n, buff);
37     justreadob = 0;
38 }
39 )
```

图 21.5 (错误地) 使用 select 来通知带外数据的接收程序。

### 带外数据

问题在于 `select` 指示了普通数据 (`rset`) 或带外数据 (`xset`)。在每种情况下，接收到的数据都会打印。当我们运行程序以及之前的发送程序 (21.3)，遇到以下情况：

```

bs$ tcsetopt 123

read 3 bytes: 1Invalid argument

```

解决方案是在读取普通数据后设置 select 条件。我们声明了一个新变量 `justreadob` 来指示是否读取了带外数据。当我们设置 `justreadob` 标志时必须清除该描述符。程序运行符合预期。

### 2.3 socketmark

该函数是 Posix 的发明。Posix 替换了 `ioctl` 函数。图 21.7 (p. 574) 显示了使用常用 SIOC 的实现。

```c

1 #include "unp.h"

2 int

3 main(int argc, char **argv)

4 (

5     int listenfd, confnd, n, justreadob = 0;

6     char buff[100];

7     fd_set rset, xset;

8     if (argc == 2)

9     listenfd = Tcp_listen(NULL, argv[1], NULL);

10 else if (argc == 3)
