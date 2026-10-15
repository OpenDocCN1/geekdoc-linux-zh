
```c
child_main(listenfd, addrlen); /* 永远不返回 * */
}
```

图 27.22 `child_make` 函数在预分派服务器中描述符的传递。

![](img/aeda3be9ee318bedd42850d461da0f28_747_0.png)

图 27.23 父子进程都关闭一个后的相同管道。

在创建所有子进程后，布局如图 27.24 所示。我们在每个子进程中关闭监听套接字，因为只有父进程会调用 `accept`。我们展示了父进程必须持有监听套接字以及所有的套接字。正如你可能猜到的，父进程使用 `select` 对所有这些描述符进行多路复用。

图 27.25 显示了主函数。与该函数的之前的版本相比，变化在于分配了描述符集合，并在集合开启了每个子进程流管道对应的位。同时也计算了最大描述符值。我们为 `Child` 结构体数组分配了内存。主循环由 `select` 调用驱动。

![](img/aeda3be9ee318bedd42850d461da0f28_748_0.png)

```c
1 #include "unp.h"
2 #include "child.h"
3 static int nchildren;
4 int
5 main(int argc, char **argv) {
7     int listenfd, i, navail, maxfd, nsel, confd, rc;
     void (*sig_int)(int, int, sig_t*);
     pid_t child_make(int, int, int);
    size_t n;
    fd_set set, masterset;
    socklen_t addrlen, clien;
    struct sockaddr *cliaddr;
15    if (argc == 3)
        listenfd = Tcp_listen(NULL, argv[1], &addrlen);
    else if (argc == 4)
        listenfd = Tcp_listen(argv[1], argv[2], &addrlen);
    else
        exit(EXIT_FAILURE, "usage: servov05 <host> <port> <children>");
22    FD_ZERO(masterset);
    FD_SET(listenfd, &masterset);
    maxfd = listenfd;
    cliaddr = malloc(&addrlen);
27    nchildren = atoi(argv[argc-1]);
    navail = nchildren;
    cptr = malloc(nchildren, sizeof(Child));
```

```c
/* 优先所有子进程 */
for (i = 0; i < children; i++) {
    child_make(i, listenfd, addrdn); /* 父进程返回 * */
    FD_SET(cptr[i].child_pipefd, &masterset);
    maxfd = max(maxfd, cptr[i].child_pipefd);
}
Signal(SIGINT, sig_int);
nrset = masterset;
if (avail < 0) {
    FD_CLO(listenfd, &rset); /* 如果没有可用子进程则关闭 */
    nsel = Select(nsel + 1, &rset, NULL, NULL);
}
/* 检查新连接 */
if (FD_ISSET(listenfd, &rset)) {
    cliden = addrdn;
    confd = Accept(listenfd, cliaddr, &cliden);
    for (i = 0; i < children; i++) {
        if (cptr[i].child_status == 0)
            break; /* 变为可用 */
    }
}
if (i == children) {
    err_quit("没有可用子进程");
    cptr[i].child_status = 1; /* 标记子进程为忙 */
    cptr[i].child_count++;
    nsel--;
}
n = read(cptr[i].child_pipefd, "*", 1, confd);
Close(confd);
if (-nsel <= 0) {
    /* 逻辑继续 ... */
}
/* 查找任何子进程 */
for (i = 0; i < children; i++) {
    if (FD_ISSET(cptr[i].child_pipefd, &rset)) {
        if (n = read(cptr[i].child_pipefd, &c, 1, &confd) == 0)
            err_quit("read_fd 返回了 0");
        cptr[i].child_status = 0;
        nsel++;
    }
}
if (-nsel <= 0) {
    /* 逻辑继续 ... */
}
```

```c
#include "unthread.h"
int
main(int argc
```

图 27.27 TCP 多线程服务器的 `main` 函数。

我们从图 27.1 中注意到，这个简单的线程版本在 Solaris 和 Digital Unix 上的速度甚至比最快的预取（prefetched）版本还要快。这种一个线程一个客户端的版本也比每个客户端一个线程的版本（第 1 行）快许多倍。

在第 23.5 节中，有三种替代方法可以将非线程安全的函数转换为线程安全的函数。我们的 `web_child` 函数调用了我们的 `readline`，而图 3.17 所示的版本不是线程安全的。第 23.5 节中的替代方案 2 和 3 已经针对图 27.27 中的示例进行了测试。从替代方案 3 到替代方案 2 的加速小于百分之一，这可能是因为 `read()` 仅用于从客户端读取 5 个字符的计数。因此，为了简单起见，在本章的线程服务器示例中使用了图 3.16 中效率较低的版本。

## 27.11 TCP 预线程服务器，每线程 accept

我们在本章前面发现，预分叉（prefork）子进程池为每个客户端创建一个子进程速度更快。在支持线程的系统中，可以预期在服务器启动时创建一个线程池来获得类似的加速，而不是为每个客户端创建一个新线程。该服务器的基本设计是让每个线程都调用 `accept`。为了执行 `accept`，我们将使用一个互斥锁（类似于第 27.8 节），允许一次只有一个线程调用 `accept`。我们没有理由使用文件锁来保护对 `accept` 的调用：因为我们知道在单个进程的多个线程可以使用互斥锁。

图 27.28 显示了 `pthread07.h` 头文件，它定义了一个 `Thread` 结构体，维护了关于每个线程的一些信息。

```c
1 typedef struct {
    pthread_t thread_tid;      /* 线程 ID */
    long thread_count;        /* 处理的连接数 */
} Thread;    pthread_t *tptr;               /* Thread 结构体数组；通过 calloc 分配 * */
6 int
    listenfd, threads;
7 socklen_t addrlen;
8 pthread_mutex_t mlock;
```

图 27.28 `pthread07.h` 头文件。

我们还声明了一些全局变量，例如监听套字和一个所有线程都需要共享的互斥变量。

图 27.29 显示了 `main` 函数。

```c
1 #include "pthread.h"
2 #include "pthread07.h"
3 pthread_mutex_t mlock = PTHREAD_MUTEX_INITIALIZER;
4 int
5 main(int argc, char **argv)
6 {
7     int i;
8     void
9         sig_int(int), thread_make(int);
10    if (argc == 3)
11        listenfd = Tcp_listen(NULL, argv[1], &addrlen);
12    else if (argc == 4)
```
