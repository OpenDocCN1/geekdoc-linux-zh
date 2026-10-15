
`child_make(int i, int listenfd, int addrdlen)`

```
{
    int sockfd[2];
    pid_t pid;
    void child_main(int, int, int);
    socketpair(AF_LOCAL, SOCK_STREAM, 0, sockfd);
    if ((pid = fork()) > 0) {
        close(sockfd[1]);
        ctpr[i]->child_pid = pid;
        ctpr[i]->pipefd = sockfd[0];
        ctpr[i]->child_status = 0; /* 父进程 */
        return (pid);
    }
    dup2(sockfd[1], STDERR_FILENO); /* 子进程到父进程的流管道 */
    close(sockfd[0]);
    close(sockfd[1]);
    close(listenfd); /* 子进程不需要打开这个 */
    child_main(i, listenfd, addrdlen); /* 永返回 */
}
```

**图 30.21** 预叉服务器的 `child_make` 函数描述符。

**图 30.22** 父、子进程都关闭一端后的流管道。

所有子进程创建完成后，我们得到了如图 30.23 所示的布局。我们在每个子进程中关闭监听 `socket`，因为只有父进程可以执行 `accept`。我们展示了父进程必须处理监听 `socket` 以及所有的流 `socket`。正如你可能猜到的那样，父进程使用 `select` 来多路复用所有这些描述符。

图 30.24 显示了 `main` 函数。与该函数的之前的版本相比，由于分配了描述符集，并在集合中开启了对应于监听 `socket` 以及通往每个子进程流管道的位。同时，还计算了最大描述符值。我们为 `Child` 结构体数组分配了内存。主循环由调用 `select` 驱动。

## 30.9 节 TCP 预叉服务器，描述符传递 839

![](img/1cc56227d30f6730abd74fbc5905c5ff_862_0.png)

图 30.23 所有子进程创建后的流管道。

```c
#include <unistd.h>
#include "child.h"
static int nchildren;
int
main(int argc, char **argv) {
    int listenfd;
    listenfd = Tcp_listen(NULL, navail, nsel, maxfd, confnd, rc);
    void (*sig_int)(int sig);
    pid_t child = child_make(int, int, int);
    size_t n;
    fd_set rset, masterset;
    socklen_t addrlen = clilen;
    struct sockaddr *cliaddr = &sockaddr;
    if (argc == 3)
        listenfd = Tcp_listen(NULL, argv[1], &addrlen);
    else if (argc == 4)
        listenfd = Tcp_listen(argv[1], argv[2], &addrlen);
    else
        err_quit("usage: %s <host> <port> <children>", argv[0]);
    FD_ZERO(masterset);
    FD_SET(listenfd, &masterset);
    maxfd = listenfd;
    cliaddr = malloc(addrlen);
    nchildren = atoi(argv[3]);
    navail = nchildren;
    ctpr = calloc(nchildren, sizeof(Child));
    /* 预叉所有进程 */
    for (i = 0; i < nchildren; i++) {
        child_make(i, listenfd, addrdlen); /* 父进程 */
        FD_SET(ctpr[i]->pipefd, &masterset);
        maxfd = max(maxfd, ctpr[i]->pipefd);
    }
    Signal(SIGINT, sig_int);
    for (;;) {
        rset = masterset;
        /* 如果没有可用子进程，关闭监听 socket */
        if (navail <= 0)
            FD_CLR(listenfd, &rset);
        /* 检查新连接 */
        if (nsel = select(maxfd + 1, &rset, NULL, NULL, NULL) > 0) {
            addrlen = clilen;
            if (FD_ISSET(listenfd, &rset)) {
                conffd = accept(listenfd, cliaddr, &addrlen);
                /* 寻找可用子进程 */
                for (i = 0; i < nchildren; i++) {
                    if (ctpr[i]->child_status == 0) {
                        ctpr[i]->child_status = -1; /* 标记为忙碌 */
                        ctpr[i]->child_count++;
                        navail--;
                        /* 将描述符传递给子进程 */
                        write(ctpr[i]->pipefd, &conffd, sizeof(conffd));
                        break;
                    }
                }
            }
        }
        /* 检查新就绪的子进程 */
        for (i = 0; i < nchildren; i++) {
            if (FD_ISSET(ctpr[i]->pipefd, &rset)) {
                if ((n = read(ctpr[i]->pipefd, &conffd, sizeof(conffd))) == 0)
                    err_quit("child %d terminated unexpectedly", i);
                ctpr[i]->child_status = 0; /* 标记为可用 */
                navail++;
            }
        }
    }
}
```

图 30.24 使用描述符传递的 `main` 函数。

## 30.10 TCP 并发服务器，每个客户端一个线程

```c
server/child05.c
23 void
24 child_main(int i, int listenfd, int addrlen)
25 {
26     char  c;
27     int connfd;
28     ssize_t n;
29     void  web_child(int);
30     printf("%ld starting...\n", (long) getpid());
31     for ( ; ; ) {
32         if (n = Read_fd(STDERR_FILENO, &c, 1, &connfd)) == 0
33             err_quit("read_fd returned 0");
34         if (connfd < 0)
35             err_quit("no descriptor from read_fd");
36         web_child(connfd);    /* 处理请求 */
37     Close(connfd);
```
