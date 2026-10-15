
# 检查监听的 Unix 域套接字

32-34 首先测试监听的 Unix 域套接字，如果就绪则调用 `readable_listen`。变量 `nready`（`select` 返回为可读的描述符数量）是一个全局变量。

我们的每个 `readable_XXX` 函数都会递减这个变量，并将其新值作为函数的返回值。当该值达到 0 时，所有可读描述符都已处理完毕，并再次调用 `select`。

## 检查原始 ICMP socket

35-42 测试原始 `ICMP4` socket，然后测试原始 `ICMPv6` socket。

## 检查 Unix 域套接字

43-49 我们检查任何连接的 Unix 域套接字是否是可读的。这些套接字中的任何一个可读性都意味着客户端发送了描述符，或者客户端已终止。

图 28.36 显示了当守护进程的监听套接字可读时的 `readable_listen` 函数。这表示有一个新的客户端连接。

### 图 28.36 处理新的客户端连接。

`icmpd/readable_listen.c`

```
1 #include "icmpd.h"

2 int

3 readable_listen(void)

4 {

5 int i, connfd;

6 socklen_t clilen;

7 clilen = sizeof(cliaddr);

8 connfd = Accept(cliaddr, (SA *) &cliaddr, &clilen);

9 /* 找到第一个空 client [] 结构 */

10 for (i = 0; i < FD_SETSIZE; i++)

11 if (client (i).connfd < 0)

12 client (i).connfd = connfd; /* 保存描述符 */

13 break;

14 }

15 if (i == FD_SETSIZE)

16 close(connfd); /* 无法处理新客户端， */

17 return (--nready); /* 关闭新连接 */

18 }

19 printf("new connection, i = %d, connfd = %d\n", i, connfd);

20 FD_SET(connfd, &maxfd); /* 将新描述符添加到集合 */

21 if (connfd > maxfd)

22 maxfd = connfd; /* 为了 select () */

23 if (i > maxi)

24 maxi = i; /* client [] 数组中的索引 */

25 return (--nready);

26 )
```

7-25 连接被接受并使用了 `client` 数组中的第一个项。该函数的代码来自图 28.22。如果在 `client` 数组中没有找到项，我们简单的关闭新连接：当连接的套接字可读时，调用 `readable_conn` 函数（图 28.37）。它的参数是该客户端在 `client` 数组中的索引。

## 读取客户端数据和可能的描述符

13-18 我们调用图 28.15 中的 `read_fd` 函数来读取数据和可能的描述符，返回值为 0 表示客户端通过终止关闭了其连接。

### 图 28.37 从客户端读取数据和可能的描述符。

`icmpd/readable_conn.c`

```
1 #include "icmpd.h"

2 int

3 readable_conn(int i)

4 {

5 int unixfd, recvfd;

6 char c;

7 size_t n;

8 socklen_t len;

9 struct sockaddr_storage ss;

10 unixfd = client [i].conndfd;

11 recvfd = -1;

12 if ((n = read_fd(unixfd, &c, 1, &recvfd)) == 0) {

13 err_msg("client %d terminated, recvfd = %d", i, recvfd);

14 goto clientdone; /* 可能已终止 */

15 }

16 /* 来自客户端的数据；应该是描述符 */

17 if (recvfd < 0) {

18 err_msg("read_fd did not return descriptor");

19 goto clienterr;

20 }
```

设计决定是在应用程序和守护进程之间使用 Unix 域套接字还是 Unix 域数据套接字。应用程序的 UDP 套接字可以通过任何一种 Unix 域套接字传递。我们使用流套接字是为了检测客户端何时终止。当客户端终止时，它所有的描述符会自动关闭，这告诉守护进程从客户端数组中移除它。如果我们使用数据套接字，将不知道客户端何时终止。如果客户端没有关闭连接，我们期望一个描述符。`readable_conn` 函数的后半部分在图 28.38。

## 绑定到 UDP 套接字的端口号

21-25 `getsname` 让守护进程可以获取绑定到套接字的端口号。我们不知道为套接字地址结构分配的大小，因此使用 `sockaddr_storage` 结构，它足够大并对齐对对对齐。

26-33 套接字族与端口号一起存储在 `client` 结构中。如果端口号为 0，我们调用 `sock_bind_wild` 函数将通配地址和临时端口绑定到套接字，如之前提到的，这在某些服务器实现上不可行。

### 28.38 获取客户端绑定到其 UDP 套接字的端口号。

`icmpd/readable_conn.c`

```
21 len = sizeof(ss);
22 if (getsname (recvfd, (SA *) &ss, &len) < 0) {
23 err_msg("getsname error");
24 goto clienterr;
25 }

26 client[i].family = ss.ss_family;
27 if ((client[i].port = sock_get_port ((SA *) &ss, len)) == 0) {
28     client[i].port = sock_bind_wild (recvfd, client[i].family);
29     if (client[i].port <= 0) {
30         err_msg("error binding ephemeral port");
31         goto clienterr;
32     }
33 }

34 Write (unixfd, "1", 1); /* 通知客户端 OK */
35 Close (recvfd); /* 客户端 UDP 套接字处理完毕 */
36 return (--nready);

37 clienterr:
38 Write (unixfd, "0", 1); /* 通知客户端发生错误 */
39 clientdone:
40 Close (unixfd);
41 if (recvfd >= 0) {
42     Close (recvfd);
43     FD_CLR (unixfd, &allset);
44     client[i].conffd = -1;
45 } return (--nready);
46 }
```

## 向 select 指示客户端

34 向客户端返回一个由字符“1”组成的字节。

## 关闭客户端的 UDP 套接字

35 我们已经处理完客户端的 UDP 套接字并将其关闭。这个描述符是由客户端传递给我们的，因此是一个副本；因此，UDP 套接字在客户端端仍然开启。

## 处理错误和客户端终止

37-45 如果发生错误，则向客户端写回字节“0”。当客户端终止时，Unix 域连接的末端被关闭，描述符从 `select` 的描述符集中移除。`client` 结构中的 `conf` 成员被设置为 -1。`readable_v4` 函数在 `ICMP4` socket 可读时调用。我们在图 28.39 中显示了前半部分。

### 28.39 处理接收到的 ICMP4 数据包，前半部分。

`icmpd/readable_v4.c`
