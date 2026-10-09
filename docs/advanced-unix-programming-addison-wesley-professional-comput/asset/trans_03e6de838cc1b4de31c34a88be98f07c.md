
当类型提供选择时，可以自行决定，但在大多数情况下，使用默认值即可，因此设为零。

接下来，服务器必须使用 `bind` 为套接字命名：

```c
bind—将名称绑定到套接字
#include <sys/socket.h>

int bind(
    int socket_fd,                    /* 套接字文件描述符 */
    const struct sockaddr *sa,         /* 套接字地址 */
    socklen_t sa_len                   /* 地址长度 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

套接字地址拥有一个独立的章节（第 8.2 节）来专门介绍。我们已经看到了一个 `AF_UNIX` 的例子，它仅用于单机内部的通信，就像第 7 章中介绍的 IPC 机制一样。稍后我们将看到如何为其他域（包括 `AF_INET`）设置地址。

请记住，在大多数系统上，对于 `AF_UNIX`，`bind` 会创建一个全新的套接字文件；它无法重用已存在的文件。

服务器还必须调用 `listen` 来配置套接字以接受连接：

```c
listen—标记套接字以接受连接并设置队列上限
#include <sys/socket.h>

int listen(
    int socket_fd,                    /* 套接字文件描述符 */
    int backlog                       /* 最大连接队列长度 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

上一节的示例并未展示这一点，但服务器可以从众多客户端接受连接。此外，由于服务器只能以特定速率处理 `accept`，因此连接请求可能会排队。`listen` 的第二个参数限制了该队列的长度。通常，当队列已满时，客户端尝试连接会导致其 `connect` 返回 -1，并将 `errno` 设置为 `ECONNREFUSED`。在我的示例中，我使用了常量 `SOMAXCONN`，它是系统定义的最大值。

接下来，服务器接受连接：

```c
accept—在套接字上接受新连接并创建新套接字
#include <sys/socket.h>

int accept(
    int socket_fd,            /* 套接字文件描述符 */
    struct sockaddr *sa,      /* 套接字地址或 NULL */
    socklen_t *sa_len         /* 地址长度 */
);
/* 成功时返回文件描述符，出错时返回 -1（设置 errno） */
```

通常，accept 会阻塞，直到收到连接请求（来自另一个进程调用的 connect），然后它会为该连接的 I/O 创建一个新套接字，并返回一个新的文件描述符。该文件描述符可以与普通的 read 和 write 系统调用一起使用，尽管为了更精细地控制 I/O，您也可以使用针对套接字的特定调用——send、sendto、sendmsg、recv、recvfrom 和 recvmsg——我将在第 8.6.2、8.6.3 和 8.9.1 节中讨论这些调用。

如果为套接字文件描述符设置了 O_NONBLOCK 标志（通过 fcntl；参见第 3.8.3 节），accept 不会等待连接，如果队列上没有请求，则立即返回 −1，并将 errno 设置为 EAGAIN 或 EWOULDBLOCK。

套接字文件描述符可以与 select 或 poll 一起使用，而且通常确实如此，我们将在第 8.1.3 节中看到。通常，服务器使用套接字文件描述符和 accept 返回的每个文件描述符来为 select（或 poll 的等价物）设置 fd_set。如果 select 或 poll 表示套接字文件描述符就绪，这意味着服务器应该执行 accept（此时不会阻塞）。如果其他某个文件描述符就绪，这意味着数据已从客户端到达，应该被读取。

如果 sa 参数不为 NULL，它将用于返回已连接套接字的地址。在输入时，必须将 sa_len 设置为 sa 指向的存储大小；在返回时，它会被设置为实际地址的大小。

关于服务器的部分就说到这里。客户端在创建其套接字后，只需调用 connect，并使用与服务器 bind 时相同的套接字地址：

```c
connect—连接套接字
#include <sys/socket.h>

int connect(
    int socket_fd,                /* 套接字文件描述符 */
    const struct sockaddr *sa,    /* 套接字地址 */
    socklen_t sa_len              /* 地址长度 */
);
/* 成功时返回 0，出错时返回 -1（设置 errno） */
```

与 *accept* 类似，*connect* 通常也会阻塞，直到连接请求被接受，但它不返回文件描述符——客户端在套接字文件描述符上进行 I/O。

如果设置了 *O_NONBLOCK* 标志，*connect* 不会阻塞等待连接，而是返回 −1，并将 *errno* 设置为 *EINPROGRESS*。连接请求并未被放弃，而是保留在队列中等待最终被满足。在此期间对 *connect* 的后续调用也会返回 −1，但此时 *errno* 被设置为 *EALREADY*。当连接建立时，可以使用该套接字文件描述符。如果需要，可以使用 *select* 或 *poll* 等待其变为可写状态（而非可读状态）。一个典型的用例是具有某些初始化任务的应用程序。它发起非阻塞的 *connect*，执行初始化，然后发起 *select* 或 *poll* 进行阻塞等待。

### 8.1.3 处理多个客户端

现在让我们扩展第 8.1.1 节中的示例，以便服务器能够处理多个客户端。以下是该示例中服务器端代码的替代版本：

```c
static bool run_server(struct sockaddr_un *sap)
{
  int fd_skt, fd_client, fd_hwm = 0, fd;
  char buf[100];
  fd_set set, read_set;
  ssize_t nread;

  ec_neg1( fd_skt = socket(AF_UNIX, SOCK_STREAM, 0) )
  ec_neg1( bind(fd_skt, (struct sockaddr *)sap, sizeof(*sap)) )
  ec_neg1( listen(fd_skt, SOMAXCONN) )
  if (fd_skt > fd_hwm)
    fd_hwm = fd_skt;
  FD_ZERO(&set);
  FD_SET(fd_skt, &set);
  while ( true ) {
    read_set = set;
    ec_neg1( select(fd_hwm + 1, &read_set, NULL, NULL, NULL) )
    for (fd = 0; fd <= fd_hwm; fd++)
      if (FD_ISSET(fd, &read_set)) {
        if (fd == fd_skt) {
          ec_neg1( fd_client = accept(fd_skt, NULL, 0) )
          FD_SET(fd_client, &set);
          if (fd_client > fd_hwm)
            fd_hwm = fd_client;
        }
        else {
          ec_neg1( nread = read(fd, buf, sizeof(buf)) );
          if (nread == 0) {
            FD_CLR(fd, &set);
            if (fd == fd_hwm)
              fd_hwm--;
            ec_neg1( close(fd) );
          }
          else {
            printf("Server got '%s'\n", buf);
            ec_neg1( write(fd, "Goodbye!", 9) );
          }
        }
      }
  }
  return true;

EC_CLEANUP_BGN
    close(fd_skt);
    return false;
EC_CLEANUP_END
}
```

新代码的大部分都涉及设置和使用 select。我在第 4.2.3 节中讨论过，但这里做一个回顾：

```c
**select**—等待 I/O 就绪

#include <sys/select.h>

int select(
    int nfds,          /* 最高 fd + 1 */
    fd_set *readset,   /* 读集合或 NULL */
    fd_set *writeset,  /* 写集合或 NULL */
    fd_set *errorset,  /* 错误集合或 NULL */
    struct timeval *timeout   /* 超时时间（微秒）或 NULL */
);
/* 返回置位的位数，出错时返回 -1（设置 errno） */
```

函数 run_server 中有两个 fd_set：一个是 set，它保存所有感兴趣的文件描述符：套接字文件描述符，以及由 accept 返回的每个客户端各一个。我们需要 select 应该查看的集合中文件描述符的数量，因此变量 fd_hwm（“高水位标记”）会随着我们从 accept 获得新的文件描述符而保持更新。当我们关闭最高的文件描述符时，我们将其从 set 中移除并递减高水位标记。将其从 set 中移除非常重要；否则，select 会持续报告它已就绪，这意味着并不是有数据可供读取，而仅仅是 read 不会阻塞。

第二个 fd_set，read_set，每次调用 select 时都会从 set 复制，然后由 select 修改以指示哪些文件描述符已就绪。

然后该函数永远循环，直到我们用信号终止它。每次从 select 返回时，它都会遍历返回的集合（被修改的 read_set 变量）以寻找就绪的文件描述符。如果 fd_skt 就绪，它就执行 accept；如果其他任何内容就绪，这意味着客户端已发送了一些数据。我们读取它，显示它，并发送一条简短的消息回去。

客户端的代码与之前的示例相同，只是发送给服务器的消息包含进程 ID：

```c
static bool run_client(struct sockaddr_un *sap)
{
    if (fork() == 0) {
        int fd_skt;
        char buf[100];

        ec_neg1( fd_skt = socket(AF_UNIX, SOCK_STREAM, 0 ) )
        while (connect(fd_skt, (struct sockaddr *)sap, sizeof(*sap)) == -1) {
            if (errno == ENOENT) {
                sleep(1);
                continue;
            }
            else
                EC_FAIL
        }
        snprintf(buf, sizeof(buf), "Hello from %ld!",
                 (long)getpid());
        ec_neg1( write(fd_skt, buf, strlen(buf)) )
        ec_neg1( read(fd_skt, buf, sizeof(buf)) )
        printf("Client got \"%s\"\n", buf);
        ec_neg1( close(fd_skt) )
        exit(EXIT_SUCCESS);
    }

    return true;

EC_CLEANUP_BGN
    /* 只有子进程到达这里 */
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

最后，有一个小的 main 函数，它设置套接字地址，创建四个客户端子进程，并在父进程中运行服务器：

