
```c
err_sys("read error");

close(fd);

exit(0);

}
```

`csopen` 函数在创建 s-pipe 后为服务器执行 `fork`（图 17.28）。

## 图 17.28. `csopen` 函数，版本 1

```c
#include "open.h"
#include <sys/uio.h> /* struct iovec */

/*
 * 向连接服务器发送 "name" 和 "oflag"
 * 并返回一个文件描述符来打开文件。
 */

int
csopen(char *name, int oflag)
{
    pid_t    pid;
    int       len;
    char      buf[10];
    struct iov iov[3];
    static int fd[2] = { -1, -1 };

    if (fd[0] < 0) { /* 第一次 fork/ 打开我们的服务器 */
        if (s_pipe(fd) < 0) {
            err_sys("pipe error");
        } else if ((pid = fork()) < 0) {
            err_sys("fork error");
        } else if (pid == 0) { /* 子进程 */
            close(fd[0]);
            if (fd[1] == 1) { /* STDIN_FILENO */
                if (dup2(fd[1], STDIN_FILENO) == -1)
                    err_sys("dup2 error to stdin");
            }
            if (fd[1] == 2) { /* STDOUT_FILENO */
                if (dup2(fd[1], STDOUT_FILENO) == -1)
                    err_sys("dup2 error to stdout");
            }
            if (execl("/open", "open", (char *)0) < 0) {
                err_sys("execl error");
            }
        }
        close(fd[1]); /* 父进程 */
    }

    printf("%d, %d\n", offset, flag); /* offset 到 ascii */
    iov[0].iov_base = CL_OPEN + offset; /* 字符串拼接 */
    iov[0].iov_len = strlen(CL_OPEN) + 1;
    iov[1].iov_base = name;
    iov[1].iov_len = strlen(name);
    iov[2].iov_base = buf;
    iov[2].iov_len = strlen(buf) + 1; /* buf 结尾 +1 */
    len = iov[0].iov_len + iov[1].iov_len + iov[2].iov_len;
    if (write(fd[0], iov[0], 3) != len) {
        err_sys("write error");
    }
    /* write 返回的描述符 */
    return(recv_fd(fd[0]));
}
```

子进程关闭管道的一端，父进程关闭另一端。对于执行的服务器，另一种选择是将 `fd[1]` 的 ASCII 表示作为参数传递给服务器。父进程发送文件名和打开模式。最后，如果服务器返回错误，则调用 `write` 输出错误消息。现在让我们看看开放服务器。首先我们有 `open.h` 头文件（图 17.29），它包含了标准头文件和函数原型。

## 图 17.29. `open.h` 头文件，版本 1

```c
#include "apue.h"
#include <errno.h>

#define CL_OPEN "open" /* 客户端向服务器请求 */

char errmsg[]; /* 给客户端的错误消息 */
int oflag; /* open() ... */
char *pathname; /* 为客户端 open()的文件 */

int cli_args(int, char **);
void request(int, int);
```

`main` 函数（图 17.30）从 s-pipe（标准输入）读取客户端的请求并调用函数。

## 图 17.30. 服务器 `main` 函数，版本 1

```c
#include "opend.h"

char errmsg[MAXLINE];
int oflag;
char *pathname;

int
main(void)
{
    int read;
    char buf[MAXLINE];
    for(;; ) /* 从客户端读取缓冲区，处理请求 */
    {
        if ((read = read(STDIN_FILENO, buf, MAXLINE)) < 0)
            err_sys("read error on stream pipe");
        else if (read == 0)
            break; /* 客户端关闭了管道 */
        request(buf, read, STDOUT_FILENO);
    }
    exit(0);
}
```

`request` 函数（图 17.31）完成所有工作。它调用 `cli_args` 将客户端的请求拆分为标准参数列表，并调用该函数处理参数。如果一切正常，调用 `open` 打开文件，并通过 `send_fd` 跨 s-pipe（标准输出）传输描述符。如果遇到错误，调用 `send_err` 发送错误消息，之前描述了 `strerror` 协议。

## 图 17.31. `request` 函数，版本 1

```c
#include "opend.h"
#include <fcntl.h>

void
request(char *buf, int read, int fd)
{
    int newfd;
    if (buf[read-1] != '\0') {
        sprintf(errmsg, "request not terminated: %s\n", strerror(errno));
        buf[read] = 0;
        send_err(fd, -1, errmsg);
        return;
    }
    if (cli_args(buf, argc, args) < 0) { /* 解析参数并设置选项 */
        send_err(fd, -1, errmsg);
        return;
    }
    if ((newfd = open(pathname, oflag)) < 0) {
        sprintf(errmsg, "can't open %s: %s\n", pathname, strerror(errno));
        send_err(fd, -1, errmsg);
        return;
    }
    if (send(fd, newfd) < 0) { /* 发送描述符 */
        err_sys("send error");
        close(newfd);
    }
}
```

客户端的请求是一个以空字节终止、由空格分隔的参数字符串。`buf_args` 函数将此字符串转换为标准的 `argv` 风格列表并调用用户函数处理参数。我们将在本章稍后的部分使用 `buf_args` 函数。我们使用 ISO 函数 `strtok` 将字符串拆分为各个参数。

## 图 17.32. `buf_args` 函数

```c
#include "apue.h"

#define MAXARGC 50 /* buf 中参数的最大数量 */
#define WHITE " \t" /* 用于划分参数的空白字符 */

/*
 * buf[] 包含空格分隔的参数。我们将其转换为
 * argv 风格的指针数组，并调用用户的函数 (optfunc)
 * 处理数组。如果解析 buf 出现问题，我们返回 -1，
 * 否则返回 optfunc 的返回值。注意用户的 buf[]
 * 会被修改（在每个标记后放置了空字符）。
 */

int
buf_args(char *buf, int *argc, int (*optfunc)(int, char **)) {
    char *ptr;
    char *argv[MAXARGC];
    *argc = 0;
    if (strtok(buf, WHITE) == NULL) { /* 需要一个 argv[] */
        return(-1);
    }
    argv[(*argc)++] = buf;
    while ((ptr = strtok(NULL, WHITE)) != NULL) {
        if ((*argc) >= MAXARGC-1) { /* 为结尾的 NULL 留出一个空间 */
            return(-1);
        }
        argv[(*argc)++] = ptr;
    }
    argv[*argc] = NULL;
    
    /*
     * 由于 argv[1] 指针指向用户的 buf；
     * 用户函数只需拷贝指针，
     * 尽管 argv 数组在返回时会消失。
     */
    return(optfunc(argc, argv));
}
```

由 `buf_args` 调用的服务器是 `cli_args`（图 17.33）。它验证客户端发送的参数数量正确，并将 `pathname` 和 `oflag` 存储在全局变量中。

## 图 17.33. `cli_args` 函数

```c
#include "opend.h"

/*
 * 此函数由 buf_args() 调用，而 buf_args() 又由
 * request() 调用；buf_args() 将客户端的缓冲区拆分为
 * argv 风格的数组，我们现在对其进行处理。
 */

int
cli_args(int argc, char **argv) {
    if (argc != 3 || strcmp(argv[0], CL_OPEN) != 0) {
        sprintf(errmsg, "usage: <pathname> <oflag>\n");
        return(-1);
    }
    pathname = argv[1]; /* 保存用于打开的 pathname 指针 */
    oflag = atoi(argv[2]);
    return(0);
}
```

这完成了由客户端通过 fork-exec 调用的 open 服务器。在 fork 之前创建了一个单向 s-pipe，用于客户端和服务器之间的通信。通过这种安排，我们每个客户端对应一个服务器。

![](img/902515e97eef28cac8083866e00a6f4c_813_0.png)

## 17.6. 一个 Open 服务器，版本 2

在上一节中，客户端类似于 [第 17.5 节]。相反，主文件 main 与 [图 17.27] 相同。我们在 `open.h` 头文件 [图 17.26] 中添加了以下行：

```c
#define CS_OPEN "/home/user/opend/" /* 服务器的已知名称 */
```

`open.c` 文件发生了从 [图 17.28] 所示的变化，因为我们现在使用 `cli_conn` 而不是 fork 和 exec。这在 [图 17.34] 中所示。

## 图 17.34. `csopen` 函数，版本 2

```c
#include "open.h"
#include <sys/uio.h> /* struct iovec */

/*
 * 通过向连接服务器发送“name”和“flag”
 * 并读回文件描述符来打开文件。
 */

int
csopen(char *name, int flag)
{
    int len;
    char buf[10];
    struct iovec iov[3];
    static int csfd = -1;

    if (csfd < 0) { /* 打开到连接服务器的连接 */
        if ((csfd = cli_conn(CS_OPEN)) < 0) {
            err_sys("cli_conn error");
        }
    }

    sprintf(buf, "%s %d", name, flag); /* flag 转换为 ascii */
    iov[0].iov_base = CL_OPEN; /* 字符串拼接 */
    iov[0].iov_len = strlen(CL_OPEN) + 1;
    iov[1].iov_base = name;
    iov[1].iov_len = strlen(name);
    iov[2].iov_base = buf;
    iov[2].iov_len = strlen(buf) + 1; /* 总是发送空字符 */
    len = iov[0].iov_len + iov[1].iov_len + iov[2].iov_len;
    if (writev(csfd, iov, 3) < 0)
        err_sys("write error");
    /* 读回描述符；返回 write 处理的错误 */
    return(recv_fd(csfd));
}
```

来自客户端的协议保持不变。

接下来，我们将查看服务器头文件。`opend.h`（图 17.35）包含了标准头文件以及全局变量和函数类型。

## 图 17.35. `opend.h` 头文件，版本 2

```c
#include "apue.h"
#include <errno.h>

#define CS_OPEN "/home/sar/opend" /* 已知名称 */
#define CL_OPEN "open" /* 客户端对服务器的请求 */

extern int debug; /* 非零交互（非守护进程） */
extern char *errmsg; /* 返回给客户端的错误信息字符串 */
extern int oflag; /* 客户端标记：O_XXX ... */
extern char *pathname; /* 为客户端打开的文件 */

typedef struct { /* 每个连接的客户端一个客户端结构体 */
    int fd; /* fd，如果可用则为 -1 */
    uid_t uid;
} Client;

extern Client *client; /* 指向 malloc 数组的指针 */
extern int client_size; /* client[] 数组中的条目 */

int cli_args(int, char **argv);
int client_add(int fd, uid_t uid);
void client_del(int fd);
void loop(void);
void request(char *cmd, int, uid_t uid);
```

由于此服务器处理所有客户端，它必须维护每个客户端连接的状态。这是通过 `opend.h` 中定义的 `client` 数组来实现的。图 17.36 定义了操作该数组的三个函数。

## 图 17.36. 操作数组的函数

```c
#include "opend.h"

#define NALLOC 10 /* client 数组 */

static void
client_alloc(void) { /* 分配 client 空间 */
    int i;
    if (client == NULL) {
        client = malloc(NALLOC * sizeof(Client));
    } else {
        client = realloc(client, (client_size + NALLOC) * sizeof(Client));
    }
    /* 初始化项 */
    for (i = client_size; i < client_size + NALLOC; i++)
        client[i].fd = -1;
    client_size += NALLOC;
}

/* 当新请求到达时调用 */
int client_add(int fd, uid_t uid) {
    int i;
    if (client == NULL) {
        client_alloc();
    }
again:
    for (i = 0; i < client_size; i++) {
        if (client[i].fd == -1) { /* 找到空闲槽 */
            client[i].fd = fd;
            client[i].uid = uid;
            return(i);
        }
    }
    /* client 数组满了，重新分配 */
    client_alloc();
    goto again;
}

/* 客户端退出时调用 */
void client_del(int fd) {
    int i;
    for (i = 0; i < client_size; i++) {
        if (client[i].fd == fd) {
            client[i].fd = -1;
            return;
        }
    }
}
```
