
# 第16章 使用 Socket 进行网络编程

## 16.4 Unix 域套接字

## 16.4.4 运行示例

之前的两个示例——服务器和客户端设计为协同工作。在一个终端运行服务器，在另一个终端运行客户端。

## 16.4.5 无名套接字

由于 Unix 域套接字相比管道具有某些优势（例如全工），它们经常被使用。为了方便，引入了 `socketpair()`。

```c
#include <sys/socket.h>

socketpair(int domain, int type, int sockfds[2]);
```

## 16.4.6 传递描述符

Unix 域套接字有一种独特的能力：描述符可以通过它们传递。其他任何进程间通信（IPC）机制都不支持这一点。它允许进程打开文件并将描述符传递给（可能无关的进程。访问检查是在打开文件时进行的，因此接收进程获得了与原始进程相同的访问权限。

这有时被称为访问权限。

对于 `bind()` 和 `connect()`，进程必须对路径查找过程中遍历的目录具有执行权限，就像打开普通文件一样。

```c
#include <sys/socket.h>

struct cmsghdr {
    unsigned int cmsg_len;
    int cmsg_level;
    int cmsg_type;
    int cmsg_data[0];
    /* 控制消息的长度 */
    /* SOL_SOCKET */
    /* SCM_RIGHTS */
    /* 文件描述符存放此处 */
};
```

控制消息的大小（包括头部信息）存储在 `cmsg_len` 中。目前定义的控制消息类型只有 `SCM_RIGHTS`，用于传递文件描述符。对于这种消息类型，`cmsg_level` 和 `cmsg_type` 必须分别设置为 `SOL_SOCKET` 和 `SCM_RIGHTS`。最后一个元素 `cmsg_data` 是一个大小为 0 的数组。这是 gcc 的扩展，允许应用程序将数据拷贝到结构体的末尾（请参考下面的程序示例）。

接收文件描述符的方法类似。必须为控制消息留出足够的缓冲区空间，每个到达的 `struct cmsghdr` 之后都紧跟一个新的文件描述符。

为了说明这些嵌套结构的使用，我们编写了一个名为“花版 cat”的示例程序。它接受文件名作为唯一参数，在子进程中打开指定的文件，并通过 Unix 域套接字将生成的文件描述符传递给父进程。然后，父进程将文件描述符拷贝到标准输出。为了演示目的，文件名也同文件描述符一起发送。

```c
/* passfd.c -- 传递文件描述符 */

/* 我们的行为类似于简单的 /bin/cat，只处理一个
参数（文件名）。我们通过
socketpair() 创建了 Unix 域套接字（然后使用 fork()）。子进程打开命令行中
传递名称的文件，将文件描述符
和文件名传回父进程，然后退出。父进程等待
子进程的文件描述符，然后将数据从
文件描述符拷贝到标准输出（stdout），直到没有数据剩余为止。父进程随后
退出。 */
```

```c
#include <alloca.h>
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/uio.h>
#include <sys/un.h>
#include <sys/wait.h>
#include <unistd.h>

#include "sockutil.h"      /* 简单的工具函数 */

/* * 父进程。它发送文件描述符。 */
int childProcess(char *filename, int sock) {
int fd;
struct iovec vector;       /* 随 fd 传递的一些数据 * */
struct msghdr msg;        /* 完整的消息 */
struct cmsghdr *cmsg;      /* 控制消息，它将 * */
                            /* 包含 fd * */

/* 打开将传递文件描述符的文件。 */
if ((fd = open(filename, O_RDONLY)) < 0) {
    perror("open");
    return 1;
}

/* 将文件名通过套接字发送，包括末尾的
'\0' */
    vector.iov_base = filename;
    vector.iov_len = strlen(filename) + 1;

/* 组装消息的第一部分。包含
文件 iovec */
    msg.msg_name = NULL;
    msg.msg_namelen = 0;
    msg.msg_iov = &vector;
    msg.msg_iovlen = 1;

/* 现在处理控制消息。我们必须为
文件描述符分配空间。 */
    cmsg = alloca(sizeof(struct cmsghdr) + sizeof(int));
cmsg->cmsg_len = sizeof(struct cmsghdr) + sizeof(fd);
cmsg->cmsg_level = SOL_SOCKET;
cmsg->cmsg_type = SCM_RIGHTS;

/* 将文件描述符拷贝到控制
消息的末尾 */
  memcpy(cmsg->cmsg_data, &fd, sizeof(fd));

  msg.msg_control = cmsg;
  msg.msg_maxlen = cmsg->cmsg_len;

  if (sendmsg(sock, &msg, 0) != vector.iov_len)
    die("sendmsg");

  return 0;
}

/* 父进程。它接收文件描述符。 */
int parentProcess(int sock) {
  char buf[256]; /* 用于读取文件名的空间 */
  struct iovec vector;
  struct msghdr msg;
  struct cmsghdr *cmsg;      /* 控制消息，它将 * */
                            /* 包含 fd * */
  int fd;

/* 准备接收传递的文件描述符。 */
    msg.msg_name = NULL;
    msg.msg_namelen = 0;
    msg.msg_iov = &vector;
    msg.msg_iovlen = 1;

/* 现在处理控制消息。我们必须为
文件描述符分配空间。 */
    cmsg = alloca(sizeof(struct cmsghdr) + sizeof(int));
    cmsg->cmsg_len = sizeof(struct cmsghdr) + sizeof(fd);
    cmsg->cmsg_level = SOL_SOCKET;
    cmsg->cmsg_type = SCM_RIGHTS;

/* 将文件描述符拷贝到控制
消息的末尾 */
    memcpy(cmsg->cmsg_data, &fd, sizeof(fd));

    msg.msg_control = cmsg;
    msg.msg_maxlen = cmsg->cmsg_len;

    if (recvmsg(sock, &msg, 0) != vector.iov_len)
    die("recvmsg");

/* 将文件描述符拷贝到标准输出 */
    vector.iov_base = filename;
    vector.iov_len = strlen(filename) + 1;

    while ((n = read(fd, buf, sizeof(buf))) > 0)
        write(STDOUT_FILENO, buf, n);
}
```
