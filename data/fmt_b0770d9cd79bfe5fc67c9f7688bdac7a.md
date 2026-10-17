
```c
if ((n = Read(fileno(fp), buf, MAXLINE)) == 0) {
    stdineof = 1;
    shutdown(sockfd, SHUT_WR); /* 发送 FIN */
    FD_CLR(fileno(fp), &rset);
    continue;
}
write(sockfd, buf, n);
}
}
```

（注：OCR 代码存在严重的行号和语法错误如 `Select`、`stdineof(...)`，已修正为上方标准的 C 结构）

图 6.13 使用 `select` 并正确处理 EOF 的 `str_cli` 函数。

`stdineof` 是一个初始化为 0 的新标志。只要该标志为 0，每次循环主循环，我们都对输入的可读性进行 `select`。

当我们在套字上遇到 EOF 时，我们已经遇到了标准输入上的 EOF，此时函数正常终止并返回。但如果我们还没有在标准输入上遇到 EOF，说明服务器进程提前终止了。我们现在调用 `read` 和 `write` 对缓冲区而非行进行操作，并让 `select` 按预期为我们工作。

当我们在标准输入上遇到 EOF 时，我们的新标志 `stdineof` 被设置，我们调用调用第二个参数为 `SHUT_WR` 的 `shutdown` 来发送 FIN。在这里，我们也改变了在行内部对缓冲区进行的操作，改用 `read` 和 `write`。

我们还没有完成 `str_cli` 函数。我们将在第 16.2 节开发一个使用非阻塞 I/O 的版本并在第 26.3 节通过使用线程的版本。

## 6.8 TCP 回显服务器（再次回顾）

我们可以回顾第 5.2 节和 5.3 节中的 TCP 回显服务器，并将服务器重写为单进程，通过 `select` 处理任意数量的客户端，为每个客户端产生一个子进程。在显示代码之前，让我们先看看数据结构。图 6.14 显示了服务器的状态。

| client[] | rset | fd0 | fd1 | fd2 | fd3 | fd4 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| [0] | 4 | 0 | 0 | 0 | 1 | 1 |
| [1] | 5 | | | | | |
| [2] | -1 | | | | | |
| ... | | | | | | |
| [FD_SETSIZE-1] | -1 | | | | | |

该服务器能够处理的客户端数量的唯一限制是 `FD_SETSIZE` 值与内核允许该进程的最大描述符数量之间的最小值（我们在 6.3 节末讨论过）。

当客户端到达时，我们将连接的套字描述符记录在 `client` 数组的第一个可用项（即第一个值为 -1 的项）。我们必须将连接的套字添加到读取描述集中。变量 `maxi` 是 `client` 数组中当前使用的最高索引，变量 `maxfd`（加 1）是 `select` 第一个参数的当前值。

图 6.21 显示了该版本服务器的前半部分。

## 178 I/O 多路复用：select 和 poll 函数 第6 章

```c
1 #include "unp.h"
2 int
3 main(int argc, char **argv)
4 {
    int i, maxfd, listenfd, connfd, sockfd;
    int nready, client[FD_SETSIZE];
    ssize_t n;
    fd_set rset, allset;
    char buf[MAXLINE];
    socklen_t clilen;
    struct sockaddr_in cliaddr, servaddr;
    listenfd = socket(AF_INET, SOCK_STREAM, 0);
    bzero(&servaddr, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    servaddr.sin_port = htons(SERV_PORT);
    bind(listenfd, &servaddr, sizeof(servaddr));
    listen(listenfd, LISTENQ);
    maxfd = listenfd; /* 初始化 */
    max = -1; /* index 进入 client[] 数组 */
    for (i = 0; i < FD_SETSIZE; i++)
        client[i] = -1; /* -1 表示可用条目 */
    FD_ZERO(&allset); // tcpserver/tcpselect01.c
    FD_SET(listenfd, &allset);
```

### 创建监听 socket 并为 select 初始化

创建监听 socket 的步骤与之前看到的相同：`socket`、`bind` 和 `listen`。我们假设最初被 `select` 的唯一描述符是监听 socket，并据此初始化数据结构。

函数的后半部分如图 6.22 所示。

## 6.8 节 TCP 回显服务器（回顾）

```c
25   for ( ; ) {
26       rset = allset;               /* 结构赋值 =//
27       nready = Select(maxfd, 1, rset, NULL, NULL, NULL);
28       if (FD_ISSET(listenfd, &rset)) {   /* 新客户端连接 *//
29           clen = sizeof(cliaddr);
30           confd = accept(listenfd, (SA *) &cliaddr, &clen);
       for (i = 0; i < FD_SETSIZE; i++)
           if (client[i] < 0) {   /* 保存描述符 * *//
               client[i] = confd; 
               break;
           }
37       if (i == FD_SETSIZE)
           err_quit("too many clients");
       FD_SET(confd, &allset);   /* 将新描述符添加到集合 *//
           if (confd > maxfd)
               maxfd = confd;   /* 为了 select *//
       if (i > maxfd)
           i++;   /* client[i] 数组中的最大索引 *//
           if (--nready <= 0)   /* 没有更多可读描述符 *//
               continue;
           }
       for (i = 0; i <= maxfd; i++) {   /* 检查所有客户端是否有数据 * *//
           if ((sockfd = client[i]) < 0) {
               continue;
           }
           if (FD_ISSET(sockfd, &allset)) == 0) {
               if (n = Read(sockfd, buf, MAXLINE)) {
                   /* 客户端关闭连接 * *//
                   Close(sockfd);
                   FD_CLR(sockfd, &allset);
                   client[i] = -1;
               } else
                   Wn(sockfd, buf, n);
           }
           if (--nready <= 0)
               break;   /* 没有更多可读描述符 *//
       }
   }
```
