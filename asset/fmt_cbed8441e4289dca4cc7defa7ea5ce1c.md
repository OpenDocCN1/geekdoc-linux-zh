
图 17.24 `cli_largs` 函数

这完成了由客户端通过 `fork` 和 `exec` 调用的打开服务器。在 `fork` 之前创建了一个单 `fd` 管道，用于客户端和服务器之间的通信。通过这种安排，每个客户端对应一个服务器。

## 一个打开服务器，版本 2

在上节中，我们开发了一个由客户端通过 `fork` 和 `exec` 调用的打开服务器，演示了如何将文件描述符从子进程传递给父进程。在本节中，我们开发一个守护进程服务器。一个服务器处理所有客户端。我们预计这种设计更高效，因为避免了 `fork` 和 `exec`。我们使用服务器之间的 UNIX 域套接字连接，并演示如何在无关进程之间传递文件描述符。我们将使用第 17.3 节引入的三个函数 `serv_listen`、`serv_accept` 和 `cli_conn`。该服务器还演示了如何使用第 17.4 节中的 `select` 和 `poll` 函数让单个服务器处理多个客户端。

此版本的客户端与第 17.5 节的客户端相似。事实上，`main.c` 是完全一样的（图 17.18）。我们在 `open.h` 头文件中添加了以下行（图 17.17）：

```c
#define CS_OPEN "tmp/opend.socket"
```

# 高级 IPC

## 第 17 章

```c
return;
}
log_quit("can't find client entry for fd %d", fd);
}
```

图 17.27 管理客户端数组的函数

当调用 `client_add` 时，它会调用 `client_alloc`，后者又调用 `allocate` 为数组中的十个条目留出空间。当这十个条目都被使用后，稍后对 `client_add` 的调用会导致 `realloc` 分配额外的空间。通过这种动态分配方式，我们没有在编译时将 `Client` 数组的大小限制在一个我们猜测并放入头文件中的值上。如果发生错误，这些函数会调用 `log_functions`（附录 B），因为我们假设服务器是一个守护进程（daemon）。

通常，服务器会作为守护进程运行，但我们希望提供一个选项，允许它在以前台运行，并将诊断消息发送到标准错误（`stderr`）。这应该让服务器更容易测试和调试，特别是当我们没有权限读取通常写入诊断信息的日志文件时。我们将使用命令行选项来控制服务器是在前台运行还是作为后台守护进程运行。

系统上的所有命令遵循相同的约定是非常重要的，因为这使得它们更容易使用。如果某人熟悉一个命令中命令行选项的构建方式，那么在另一个遵循不同约定的命令中，就会产生更多出错的机会。

这个问题有时在处理命令行上的空白符时会发生。某些命令要求选项与其参数之间用空格隔开，而另一些命令则要求参数紧跟在选项之后，中间不留任何空格。如果没有一致的规则可遵循，用户将记住所有命令的语法，或者在调用它们时诉诸“试错”的过程。

《单份 Unix 规范》（Single UNIX Specification）包含了一套约定和指南，以促进命令行语法的一致性。这些包括诸如“将每个命令行选项限制为单个字母数字字符”以及“所有选项之前都应该有一个字符”之类的建议。

幸运的是，存在 `getopt` 函数，可以帮助开发人员以一致的方式处理命令行选项。

```c
#include <unistd.h>
int getopt(int argc, char *const argv[], const char *optopt);
extern int optind, opterr, optopt;
extern char *optarg;
```

返回值：下一个选项字符，或者当所有选项都处理完毕时返回 `-1`。

## 第 17.6 节

`argc argv` 参数是传递给程序 `main` 函数的。`options` 参数是一个包含该命令支持的选项字符的字符串。如果选项字符后面跟着冒号，则该选项带有一个参数。否则，该选项仅存在。例如，一个命令的用法语句如下：

```bash
command [-i] [-u username] [-z] filename
```

我们将 `"iu:z"` 作为选项字符串传递给 `getopt`。`getopt` 函数通常在一个循环中使用，循环在 `getopt` 返回 `-1` 时终止。在循环的每次迭代中，`getopt` 将返回下一个处理处理的选项。然而，解决选项之间的任何冲突取决于应用程序；`getopt` 仅负责解析选项并强制执行标准格式。

当遇到无效选项时，`getopt` 会返回该字符的问号。如果选项的参数缺失，`getopt` 也会返回一个问号，但如果选项字符串中的第一个字符是冒号，`getopt` 则返回一个冒号。特殊模式 `--` 会导致 `getopt` 停止处理选项并返回 `-1`。这允许用户提供以减号开头但不是选项的命令参数。例如，如果你有一个名为 `-bar` 的文件，你无法通过输入以下内容删除它：

```bash
-bar
```

因为 `rm` 会尝试将 `-bar` 解释为选项。删除文件的方法是输入：

```bash
--bar
```

`getopt` 函数支持外部变量。

- `optarg`: 如果选项带有参数，在处理选项时，`getopt` 会设置 `optarg` 指向选项的参数字符串。
- `opterr`: 如果遇到选项错误，`getopt` 默认打印错误消息。要禁用此功能，应用程序可以将 `opterr` 设置为 `0`。
- `optind`: `argv` 数组中下一个要处理字符串的索引。它从 `1` 开始，每由 `getopt` 处理一个参数，它就会加 `1`。
- `optopt`: 如果处理选项期间遇到错误，`getopt` 会设置 `optopt` 指向导致错误的选项字符串。

打开的服务器的 `main` 函数（图 17.28）定义了全局变量，处理了命令行选项并调用了循环函数。如果我们使用 `-d` 选项启动服务器，服务器将以交互模式运行而不是守护进程运行。此选项用于测试服务器。

```c
#include "opend.h"
#include <syslog.h>

int debug, oflag, client_size, log_to_stderr;
char errmsg[MAXLINE];
char *pathname;
Client *client = NULL;
```

```c
int
main(int argc
```

图 17.28 主函数，版本 2

`loop` 函数是服务器的无限循环。我们将展示该函数的两个版本。图 17.29 显示了一个使用 `select` 的版本；图 17.30 显示另一个使用 `poll` 的版本。

```c
#include "opend.h"
#include <sys/select.h>

void loop(void)
{
    int i, n, maxfd, maxi, listenfd, clifd, nread;
    char buf[MAXLINE];
    uid_t uid;
    fd_set rset, allset;

    /* 获取用于监听客户端的 fd */
    FD_ZERO(&rset);
    FD_ZERO(&allset);
    FD_SET(STDIN_FILENO, &rset);

    /* 监听 */
    if ((listenfd = serv_listen()) < 0) {
        err_sys("listen");
    }
    FD_SET(listenfd, &allset);
    maxfd = listenfd;
    maxi = -1;

    for ( ; ) {
        /* rset 每次 select 都会被修改 */
        FD_ZERO(&rset);
        FD_COPY(&allset, &rset);

        if ((n = select(maxfd + 1, &rset, NULL, NULL, NULL)) < 0)
            log_sys("select error");

        if (FD_ISSET(listenfd, &rset)) {
            /* 等待连接 */
            if ((clifd = serv_accept()) < 0) {
                log_sys("accept error");
                continue;
            }

            i = client_add(clifd);
            FD_SET(clifd, &allset);
            if (clifd > maxfd)
                maxfd = clifd;
        }

        for (i = 0; i <= maxfd; i++) {
            if (FD_ISSET(i, &rset)) {
                /* 读取数据 */
                if ((nread = read(i, buf, MAXLINE)) < 0) {
                    log_sys("read error on %d", i);
                } else if (nread == 0) {
                    /* 客户端断开 */
                    log_sys("client closed on %d", i);
                    FD_CLR(i, &allset);
                } else {
                    /* 处理数据 */
                    handle_client(i, buf, nread);
                }
            }
        }
    }
}
```

图 17.29 使用 `select` 的循环

该函数从 `allset` 开始。`select` 返回后可能出现两种情况：

- `listenfd` 可以就绪，意味着有新客户端连接。处理这种情况，我们调用 `serv_accept`（图 17.9）并更新客户端数组和相关的维护信息。
- 现有客户端的连接可以就绪。这意味着客户端已终止或发送了新请求。我们通过 `read` 返回 `0` 来发现客户端终止。如果 `read` 返回大于 `0`，则有新请求需要处理，我们通过 `handle_client` 进行处理。

我们跟踪哪些描述符位于 `allset` 集合中。当新客户端连接到服务器时，相应的位会被设置。当客户端终止时（无论是否自愿），相应的位会被清除，因为所有的描述符（包括与服务器的连接）都会由内核关闭。这与 `select` 机制不同。

使用 `poll` 的循环所示图 17.30。

```c
#include "opend.h"
#include <poll.h>

#define NALLOC 0 /* 分配/重新分配 pollfd 结构体 */

static struct pollfd* grow_pollfd(struct pollfd *pfd, int *maxfd) {
    int i;
    int oldmax = *maxfd;
    int newmax = oldmax + NALLOC;

    if ((pfd = realloc(pfd, newmax * sizeof(struct pollfd))) == NULL)
        err_sys("realloc error");

    for (i = oldmax; i < newmax; i++) {
        pfd[i].fd = -1;
        pfd[i].events = POLLIN;
        pfd[i].revents = 0;
    }

    *maxfd = newmax;
    return(pfd);
}
```

```c
for (i = 0; i < NALLOC; i++) {
    pollfd[i].fd = -1;
    pollfd[i].events = POLLIN;
    pollfd[i].revents = 0;
}
```

```c
/* obtain fd to listen for client requests */
if ((listenfd = serv_listen(CS_OPEN)) < 0)
    log_sys("serv_listen error");

client_add(listenfd, 0); /* we use [0] for listenfd */
pollfd[0].fd = listenfd;
```

```c
for ( ; ) {
    if (poll(pollfd, numfd, -1) < 0)
        log_sys("poll error");
```

```c
    if (POLLIN) {
        /* accept new client request */
        if ((clifd = serv_accept(listenfd, &uid)) < 0)
            log_sys("serv_accept error: %d", clifd);

        client_add(clifd, uid);

        /* possibly increase the size of the pollfd array */
        if (numfd >= maxfd)
            pollfd = grow_pollfd(pollfd, &maxfd);

        pollfd[numfd].fd = clifd;
        pollfd[numfd].events = POLLIN;
        pollfd[numfd].revents = 0;
        numfd++;
        log_sys("new connection: uid %d, fd %d", uid, clifd);
```

```c
for (i = 1; i < numfd; i++) {
    if (pollfd[i].revents & POLLHUP) {
        goto hungup;
    } if (pollfd[i].revents & POLLIN) {
        /* read argument from client */
        if ((n = read(pollfd[i].fd, buf, MAXLINE)) < 0)
            log_sys("read error on fd %d", pollfd[i].fd);
    } else if (n == 0) {
```

```c
hungup:
    /* the client closed the connection */
    log_sys("closed: uid %d, fd %d", client[i].uid, pollfd[i].fd);
    client_del(pollfd[i].fd);
    close(pollfd[i].fd);

    if (i < numfd-1) {
        /* pack the array */
        pollfd[i].fd = pollfd[numfd-1].fd;
        pollfd[i].events = pollfd[numfd-1].events;
        pollfd[i].revents = pollfd[numfd-1].revents;
        i--; /* recheck this entry */
    }
    numfd--;
} else {
    /* process client's request */
    handle_request(buf, nread, pollfd[i].fd, client[i].uid);
}
```

图 17.30 使用 `poll` 的循环函数

为了允许像打开的文件描述符一样多的客户端连接，我们使用与 `client_alloc` 函数中处理客户端数组时相同的策略，为 `pollfd` 结构数组动态分配空间（参见图 17.27）。

我们使用 `pollfd` 数组的第一个条目（索引 `0`）。新客户端连接的到达通过 `listenfd` 描述符上的 `POLLIN` 来指示。当新客户端连接到达时，我们调用 `serv_accept` 来接受该连接。

对于现有的客户端，我们从 `poll` 获得两种不同的事件：客户端终止由 `POLLHUP` 表示，来自现有客户端的新请求由 `POLLIN` 表示。当服务器端连接中仍有数据可供读取时，客户端可以关闭连接。尽管端点被标记为已挂起（hung up），服务器仍然可以读取队列上的所有数据。但通过这种方式，当我们收到客户端的挂起信号时，可以关闭与客户端的连接，从而有效地丢弃任何队列中的数据。没有理由处理剩余的任何请求，因为我们无法回传任何响应。

在该函数的 `select` 版本中，客户端的新请求通过调用 `handle_request` 函数来处理（图 17.31）。该函数与早期的版本（图 17.22）类似。它调用相同的函数 `buf_args`（图 17.23），该函数又调用 `cli_args`（图 17.24），但由于它是从守护进程运行的，因此它记录错误消息而不是打印到标准错误。

```c
#include <opend.h>
#include <fcntl.h>

void
handle_request(char *buf, int nread, int clifd, uid_t uid)
{
    int newfd;

    if (buf[nread-1] != '\0') {
        printf(errmsg, MAXLINE-1,
```
