
```c
1 #include "unp.h"
2 int
3 main(int argc, char **argv)
4 {
5     int i, sockfd[5];
6     struct sockaddr_in servaddr;
7 
8     if (argc != 2)
9         err_quit("usage: tcpcli <IPAddress>\n", 1);
10
11     for (i = 0; i < 5; i++) {
12         sockfd[i] = Socket(AF_INET, SOCK_STREAM, 0);
13
14         bzero(servaddr, sizeof(servaddr));
15         servaddr.sin_family = AF_INET;
16         servaddr.sin_port = htons(SERV_PORT);
17         inet_pton(AF_INET, argv[1], &servaddr.sin_addr);
18
19         Connect(sockfd[i], (struct sockaddr *) &servaddr, sizeof(servaddr));
20     }
21
22     str_cli(sockfd[0]); // 执行所有操作 */
23
24     exit(0);
25 }
```

当进程终止时，所有打开的描述符都会由内核自动关闭（我们不关闭，只是退出），并且五个连接会同时终止。这导致五个 FIN 终止（每个连接一个），反过来导致五个服务器子进程同时终止。这导致五个 `SIGCHLD` 信号大约在同一时间传递给父进程，我们在图 5.10 中显示。

正是相同信号的多次传递导致了我们将看到的问题。我们首先在后台运行服务器，然后运行我们的新客户端。我们的服务器是图 5.2，修改为调用 `signal` 以建立图 5.7 作为 `SIGCHLD` 的信号处理程序。

### 5.11 在 accept 之前的中止

还有另一种类似于前一节中中断示例的连接调用，可能会导致 `accept` 返回非致命错误，在这种情况下，我们应该再次调用 `accept`。图 5.13 所示的数据包序列在繁忙的（通常是繁忙的服务器）上出现过。

本节的目的是演示可能会遇到的三种场景：

- `1.` 我们必须捕获派生 `SIGCHLD` 的子进程。
- `2.` 我们必须处理被中断的系统调用。
- `3.` 信号处理程序必须使用 `waitpid` 正确编写以防止任何僵尸。

我们服务器的最终版本（图 5.12）结合 `SIGCHLD` 处理了所有场景。

完成的连接已从队列中移除。

我们将在第 16.6 节回到这些已终止的连接，并查看它们在正常阻塞模式下与 `select` 和监听套接字结合时会产生什么问题。

[ Team LiB ]

## 5.12 服务器进程的终止

我们现在启动客户端/服务器并杀死服务器子进程。这模拟了服务器进程的崩溃，以便我们可以看到客户端发生了什么。（我们必须仔细区分即将描述的服务器进程崩溃与我们将在第 5.14 节中描述的服务器主机崩溃。）以下发生了以下步骤：

- `1.` 我们启动服务器和客户端，并输入一行以验证一切正常。服务器子进程正常回显该行。
- `2.` 我们找到服务器子进程的进程 ID 并 `kill` 掉它。作为终止的一部分，子进程中所有打开的描述符都会关闭。这导致向客户端发送一个 FIN，客户端 TCP 用 ACK 响应。这是 TCP 连接终止的前半部分。
- `3.` `SIGLD` 信号发送到服务器父进程并被正确处理（图 5.12）。
- `4.` 客户端端什么都没有发生。客户端 TCP 接收到服务器 TCP 的 FIN 并响应 ACK，但问题是客户端进程阻塞在 `fgets` 调用中，等待从终端读取行输入。
- `5.` 在此时运行 `netstat` 显示套接字的状态。

```
linux % netstat -a | grep 9877
tcp       0 0 *:9877             localhost:43604      LISTEN
tcp       0 0 localhost:9877     localhost:43604      FIN_WAIT2
tcp       1 0 localhost:43604     localhost:9877       CLOSE_WAIT
```

从图 2.4 可以看到，TCP 连接终止序列的半部分已经完成。

- `6.` 我们仍然可以向客户端输入一行内容。以下是从步骤 1 开始在客户端处发生的情况：

```
linux % tcpcli01 127.0.0.1      start client
hello                             我们输入的第一行
hello                             在这里被正确回显，此时我们杀杀了服务器
                                   主机上的子进程
another line                      然后我们又向客户端输入了第二行
str_cli: server terminated
prematurely
```

当我们使用 "another line" 时，`str_cli` 调用和客户端 TCP 向服务器发送数据。TCP 允许这样做，因为 FIN 只表示服务器进程已关闭其连接的端点，将不再发送任何数据。FIN 并没有告诉客户端服务器进程已经终止（在本情况下，它确实终止了）。我们将在第 6.6 节讨论 TCP 的半关闭时再次涵盖这一点。

当服务器 TCP 接收到来自客户端的数据时，它会响应 RST，因为持有该套接字的进程已经终止。我们可以通过 `tcpdump` 观察数据包来验证 RST 是否已发送。

- `7.` 客户端进程看不到 RST，因为它在写入之后立即调用了 `readline`，而由于在步骤 2 中接收到了 FIN，`readline` 立即返回了 0 (EOF)。我们的客户端此时并不预期会接收到 EOF（图 5.5），因此它带有错误消息“terminated prematurely”退出。
- `8.` 当客户端终止时（通过调用图 5.5 中的 `err_quit`），它所有打开的描述符都会被关闭。

我们描述的内容还取决于示例的定时。客户端对 `readline` 的调用可能在客户端接收到 RST 之前发生，正如我们在示例所示的那样。之后，如果 `readline` 在接收到 RST 之前发生，结果是 FIN 中出现了意外之外的 EOF。但如果 RST 先到达，结果是 `readline` 返回 `ECONNRESET`。

此示例中的问题是，当 FIN 到达套接字时，客户端阻塞在 `gets` 调用中。客户端实际上在处理来自两个源（套接字和用户输入）的内容，而不是像目前 `str_cli` 代码阻塞在一个源。它应该对任何一个源进行阻塞。事实上，这正是 `select` 和 `poll` 函数的作用之一。当我们在第 6.4 节重新编写 `str_cli` 函数时，一旦 `kill` 服务器子进程，客户端就会被通知接收到了 FIN。

[ Team LiB ]

## 5.13 SIGPIPE 信号

如果客户端忽略 `readline` 的错误并向服务器写入更多数据会发生什么？可能会发生，例如客户端在读取任何内容之前需要向服务器进行两次写入，而第一次写入触发 RST。规则是：当进程向已接收 RST 的套接字写入数据时，会发送 `SIGPIPE` 信号。该信号的默认动作是终止进程，因此进程必须捕获该信号并从信号处理函数返回，或者忽略该信号，此时写入操作将返回 `EPIPE`。

Usenet 上的一个常见问题 (FAQ) 是如何在第一次写入时获取此信号而不是第二次。这是可能的。根据我们上面的讨论，第一次写入触发 RST，第二次写入触发信号。向已接收 FIN 的套接字写入是好的，但向已接收 RST 的套接字写入是错误的。为了看到发生了什么，我们如图 5.14 所示修改了客户端，使其调用两次 `write`。

```
tcpclient/str_cli.c

#include "unp.h"

void str_cli(FILE *fp, int sockfd)
{
    char sendline [MAXLINE], recvline [MAXLINE];

    while (fgets(sendline, MAXLINE, fp) != NULL) {
        write(sockfd, sendline, 1);
        sleep(1);
        write(sockfd, sendline + 1, strlen(sendline) - 1);

        if (read(sockfd, recvline, MAXLINE) == 0)
            err_quit("str_cli: server terminated");

        fputs(recvline, stdout);
}
```
