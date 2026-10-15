
```c
1 #include "unp.h"
2 static void recvfrom_int(int signo);
3 static int count;
4 void
5 dg_echo(int sockfd, SA *pcliaddr, socklen_t clilen)
6 {
7  int n;
8  socklen_t len;
9  char msg[MAXLINE];
10 Signal(SIGINT, recvfrom_int);
11 n = 240 * 1024;
12 Setsockopt(sockfd, SOL_SOCKET, SOL_RCVBUF, &n, sizeof(n));
13 for ( ; ; ) {
14  len = clilen;
15  Recvfrom(sockfd, msg, MAXLINE, pcliaddr, &len);
16  count++;
17 }
18 }
19 static void
20 recvfrom_int(int signo)
21 {
22  printf("received %d datagrams\n", count);
23  exit(0);
24 }
```

> 图 8.22 增加套字接收队列大小的 `dg_echo` 函数。

8.23 显示了一个简单的 UDP 程序，它连接到指定的 IP 地址，然后调用 `getsname` 打印本地 IP 地址和端口。

如果我们在多网口主机 `bdsi` 上运行该程序，将得到以下输出：

```
bdsi udcg1 206.62.226.41
local address 206.62.226.35:1331

bdsi udcg1 206.62.226.65
local address 206.62.226.66:1332

bdsi udcg1 127.0.0.1
local address 127.0.0.1:1335
```

我们从图 1.16 中看到，当我们运行运行两次程序时，命令行参数是不同以太网上的 IP 地址。内核会将本地 IP 地址分配给该以太网接口的主地址。也就是说，`.42` 主机位于顶部以太网上，因此传出接口地址具有 `.35` 地址。`.65` 主机位于下方以太网上，因此传出接口具有 `.66` 地址。在 UDP 套字上调用 `connect` 不会向该主机发送任何内容；它完全是一个本地操作，用于保存对端的 IP 地址和端口。我们还看到，在未绑定的 UDP 套字上调用 `connect` 也会为套字分配一个临时端口。

# TCP 和 UDP 回显服务器 select

```c
1 #include "unp.h"
2 int
3 main(int argc, char **argv)
4 {
5     int sockfd;
6     socklen_t len;
7     struct sockaddr_addr cliaddr, servaddr;
8
9     if (argc != 2)
10        err_quit("usage: %s <IPAddress>");
11    sockfd = socket(AF_INET, SOCK_DGRAM, 0);
12 bzero(&servaddr, sizeof(servaddr));
13 servaddr.sin_family = AF_INET;
14 servaddr.sin_port = htons(SERV_PORT);
15 Inet_pton(AF_INET, argv[1], &servaddr.sin_addr);
16
17 Connect(sockfd, &servaddr, sizeof(servaddr));
18
19 len = sizeof(cliaddr);
20 Getsockname(sockfd, (struct sockaddr *)&cliaddr, &len);
21 printf("local address %s\n", inet_ntop(..., &cliaddr.sin_addr));
22 exit(0);
```

图 2.23 UDP 程序使用 `connect` 来确定输出接口。

遗憾的是，这在所有实现中都不起作用，特别是源自 SVR4 的内核。例如，这在 HP-UX、Solaris 2.5 和 UnixWare 上无效，但在 AIX、Digital Unix、Linux 和 Solaris 26 上有效。

# 8.15 TCP 和 UDP 回显服务器 select

我们将第 5 章的并发 TCP 回显服务器与本章的迭代 UDP 回显服务器合并为一个单一服务器，该服务器使用 `select` 来多路复用 TCP 和 UDP 套字。图 8.24 是该服务器的前半。

## 创建监听套字

创建一个绑定到服务器已知端口的监听套字。我们设置了 `SO_REUSEADDR` 套字选项，以防在该端口已存在我们的连接。

## 创建 UDP 套字

同样创建一个 UDP 套字并绑定到相同端口。尽管 TCP 和 UDP 套字使用了相同的端口，但在调用 `bind` 之前不需要设置 `SO_REUSEADDR` 套字选项，因为 TCP 端口与 UDP 端口是相互独立的。

图 8.25 显示了服务器的后半。

![](img/aeda3be9ee318bedd42850d461da0f28_243_0.png)

## 基础 UDP 套字

```c
#include "unp.h"

int
main(int argc, char **argv) {

    int listenfd, connfd, updfd, nready, maxfdpl;
    char msg[MAXLINE];
    pid_t child_pid;
    fd_set rset;
    size_t n;
    socklen_t len = 10;
    const int on = 1;
    struct sockaddr_in cliaddr, servaddr;
    void sig_child(int);

    /* 创建监听套字 */
    listenfd = socket(AF_INET, SOCK_STREAM, 0);

    bzero(&servaddr, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.addr = htonl(INADDR_ANY);
    servaddr.sin_port = htons(SERV_PORT);

    setsockopt(listenfd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));
    bind(listenfd, (struct sockaddr *)&servaddr, sizeof(servaddr));
    listen(listenfd, LISTEN_QUEUE);
```

图 8.4 使用 `select` 处理 TCP 和 UDP 的回显服务器前半。

## 为 SIGCHLD 建立信号处理器

为 `SIGCHLD` 建立信号处理器，连接将由子进程处理。我们在图 5.11 中展示了这个处理器。

## 为 select 准备

初始化 `select` 的描述符集并计算我们要等待的两个描述符的最大值。

### 调用 select

调用 `select` 等待监听套字或 UDP 套字的可读性。我们的 `sig_child` 处理器可能会 `EINTR` 中断我们的 `select` 调用。

# 8.16 总结

## 处理新连接

当监听套字可读时，接受新连接，创建一个子进程并在子进程中调用 `str_echo`。这与第 5 章使用的步骤相同。

## 处理数据报到达

如果 UDP 套字可读，则一个数据报已到达。我们使用 `recvfrom` 读取它并使用 `sendto` 发送到客户端。将我们的回显服务器转换为 UDP 是简单的，但缺少 TCP 提供的许多功能：检测丢包和重传。

```c
    Signal(SIGCHLD, sig_child); /* 调用 waitpid() */

    FD_ZERO(&rset);

    maxfd = max(listenfd, updfd) + 1;

    for ( ; ; ) {

        FD_SET(listenfd, &rset);

        FD_SET(updfd, &rset);

        if ((ready = select(maxfd, &rset, NULL, NULL)) < 0) {

            if (errno == EINTR) /* 回到 for() */

                continue;

        } else {

            err_sys("select error");

            if (FD_ISSET(listenfd, &rset)) {

                len = sizeof(cliaddr);
```
