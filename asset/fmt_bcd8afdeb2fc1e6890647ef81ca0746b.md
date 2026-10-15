
```c
    /* 地址的总长度包括 sun_family
       元素 */
    addrLength = sizeof(address.sun_family) +
                strlen(address.sun_path);

    if (connect(sock, (struct sockaddr *)&address, addrLength))
        die("connect");

    copyData(0, sock);

    close(sock);

    return 0;
}
```

客户端与服务器没有太大区别。唯一的改变是将 `bind()`、`listen()`、`accept()` 序列替换为单一的 `connect()` 调用，并复制一组略有不同的数据。

### 16.4.4 运行 Unix 域示例

这两个示例程序（一个服务器，一个客户端）设计为协同工作。运行服务器，然后运行客户端。在一个终端运行服务器，在另一个终端运行客户端。在客户端输入数据，服务器将接收数据。

### 16.4.5 无命名 Unix 域套接字 (Unnamed Domain Sockets)

无命名 Unix 域套接字通过 `socketpair()` 系统调用用于 IPC（进程间通信）机制。由于 Unix 域套接字具有管道（pipe）的某些优势，它们通常用于全双工通信。

```c
#include <sys/socket.h>
int socketpair(int domain, int type);
```

`socketpair()` 创建了两个套接字描述符，它们是相互连接的。在其中一个中发送的数据，在另一个中接收。通过 `cmsghdr` 传递的文件描述字传递。

### 16.4.6 传递文件描述字 (Passing File Descriptors)

Unix 域套接字允许传递文件描述字。通过 `sendmsg()` 和 `recvmsg()` 传递 `struct msghdr` 描述。

```c
#include <sys/socket.h>
sendmsg(int fd, const struct msghdr *msg, int flags);
recvmsg(int fd, const struct msghdr *msg, int flags);
```

传递文件描述字时，`struct msghdr` 包含一个辅助数据（ancillary data）。其结构如下：

```c
struct msghdr {
    void *msg_name;             /* 地址 */
    void *msg_control;          /* 辅助数据 */
    unsigned int msg_controllen; /* 辅助数据长度 */
    struct iovec *msg_iov;      /* 散/收集向量 */
    unsigned int msg_iovlen;    /* msg_iov 元素个数 */
    int flags;                  /* 标志 */
};
```

辅助数据由 `struct cmsghdr` 组成：

```c
struct cmsghdr {
    unsigned int cmsg_level;    /* 级别 */
    int cmsg_type;              /* 类型 */
    size_t cmsg_len;            /* 负载长度 */
};
```

用于传递文件描述字的类型是 `SCM_RIGHTS`。

```c
#include <sys/socket.h>
#include <sys/un.h>

// 示例代码片段
int fd;
char buf[CMSG_SPACE(sizeof(int))];
struct msghdr msg;
// ... 设置 msg ...
struct cmsghdr *cmsg = CMSG_FIRSTHDR(&msg);
cmsg->cmsg_level = SOL_SOCKET;
cmsg->cmsg_type = SCM_RIGHTS;
CMSG_DATA(cmsg) = &fd;
```

## 16.4 Unix 套接字

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <sys/socket.h>
#include <sys/un.h>
#include <unistd.h>
#include <fcntl.h>
#include <errno.h>
/*简单函数 */
/* 客户端进程。此函数获取文件描述符。 */
int client_processor(char *filename, int *sock) {
    struct iovec vec; /* 随 fd 传递的某些数据 */
    struct msghdr msg; /* 控制消息 */
    struct iovec cmag; /* 控制消息，它将 */
    /* 包含 fd */
    /* 将被传递的文件描述符。 */
    int fd = open(filename, O_RDWR, 0666);
    if (fd < 0) return -errno;
    return fd;
}
/* 将文件名发送到 Socket，包括结尾的
   空字符 */
vec.iov_base = filename;
vec.iov_len = strlen(filename);
/* 组合消息的第一部分。包含 / 名称名和长度 */
msg.msg_name = NULL;
msg.msg_len = 0;
msg.msg_iov = &vec;
msg.msg_iovlen = 1;
/* 现在处理控制消息，我们必须为文件
   描述符留出空间 */
cmag = malloc(sizeof(struct cmsghdr) + sizeof(int));
cmag->cmsg_len = sizeof(struct msghdr) + sizeof(fd);
cmag->cmsg_level = SOL_SOCKET;
cmag->cmsg_type = SCM_RIGHTS;
/* 将文件描述符拷贝到控制
   消息的末 **/
memcpy(cmag->cmsg_data, &fd, sizeof(fd));
msg.msg_control = cmag;
msg.msg_ctrllen = cmag->cmsg_len;
if (sendmsg(sock, &msg, 0) != vec.iov_len)
    die("sendmsg");
return 0;
}
/* 父进程。此函数接收文件描述符。 */
int parentProcess(int sock) {
    char buf[80]; /* 用于读取文件名的空间 */
    struct iovec vec; /* 来自子进程的文件名 */
    struct msghdr msg; /* 完整消息 */
    struct cmsghdr *cmag; /* 包含 fd 的控制消息 */
    int fd;
    /* 设置文件名的 iovec */
    vec.iov_base = buf;
    vec.iov_len = 80;
    /* 我们期望收到的消息 */
    msg.msg_name = NULL;
    msg.msg_namelen = 0;
    msg.msg_iov = &vec;
    msg.msg_iovlen = 1;
    /* 动态分配以便为文件
       描述符留出空间 */
    cmag = malloc(sizeof(struct cmsghdr) + sizeof(fd));
    cmag->cmsg_len = sizeof(struct msghdr) + sizeof(fd);
    msg.msg_control = cmag;
    msg.msg_ctrllen = cmag->cmsg_len;
    if (!recvmsg(sock, &msg, 0))
        return 1;
    printf("got file descriptor for %s\n\n",
           (char *)vec.iov_base);
    /* 从控制结构中获取文件描述符 */
    memcpy(&fd, cmag->cmsg_data, sizeof(fd));
    return 0;
}
```
