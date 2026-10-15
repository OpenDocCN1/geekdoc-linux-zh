
我们已经在图 13.9 中见过此结构，当它配合 `IP_RECVSTDADDR` 套接字选项用于返回数据报的目的 IP 地址时。`msg_control` 指向的辅助数据相对于 `cmsghdr` 结构必须对齐。我们在图 14.11 中展示了这种方法。图 13.12 显示了缓冲区中两个辅助数据对象的示例。

`msg_control` 指向第一个辅助数据对象，辅助数据的总长度由 `msg_control` 指定。每个对象之前都有一个描述对象的 `cmsghdr` 结构。在 `cmsghdr_type` 成员与实际数据之间可能存在填充，在数据末尾、下一个辅助数据对象之前也可能存在填充。稍后描述的五个 `CMSG_xxx` 宏考虑了这种可能的填充。

并非所有实现都支持在缓冲区中使用多个辅助数据对象。

# 364 高级 I/O 函数 第13 章

图 13.13 显示了 `cmsghdr` 结构在使用 Unix 域套接描述符（第 14.7 节）或凭据传递（第 14.8 节）时的格式。

| cmsghdr () | cmsghdr () |
|---|---|
| cmsg_len | 16 | 112 |
| cmsg_level | SOL_SOCKET | SOL_SOCKET |
| cmsg_type | SCM_RIGHTS | SCM_CREDS |
| descriptor | | |

图 13.13 用于 Unix 域套接字的 cmsghdr 结构。

在图中，我们假设 `cmsghdr` 结构的三个成员每个占用 4 字节，且 `cmsghdr` 结构与实际数据之间没有填充。当传递描述符时，`cms_data` 数组的内容是实际的描述符值。图中我们只显示了传递了一个描述符，但通常可以传递多个（在这种情况下，`cmsg_len` 的值将为 12 加上描述符数量的倍，假设每个描述符占用 4 字节）。

由于 `recvmsg` 返回的辅助数据可以包含任意数量的辅助数据对象，并对应用程序隐藏可能的填充，通过包含 `<sys/socket.h>` 头文件定义了以下五个宏来简化辅助数据的处理。

```
#include <sys/socket.h>  /* 在许多实现中用于 ALIGN 宏 */

#include <sys/param.h>

struct cmsghdr *CMSG_FIRSTHDR(struct cmsghdr *cmsghdrptr);

        返回指向第一个 cmsghdr 结构的指针，如果不存在辅助数据则返回 NULL

struct cmsghdr *CMSG_NXTHDR(struct cmsghdr *cmsghdrptr, struct cmsghdr *cmsghdrptr);

        返回指向下一个 cmsghdr 结构的指针，如果没有更多辅助数据对象则返回 NULL

unsigned char *CMSG_DATA(struct cmsghdr *cmsghdrptr);

        返回指向与 cmsghdr 关联的数据的第一个字节的指针

unsigned int CMSG_LEN(unsigned int length);

        给定数据量，返回存储在 cmsg_len 中的值

unsigned int CMSG_SPACE(unsigned int length);

        给定数据量，返回辅助数据对象的总大小
```

## 第 13.7 节

### 队列了多少数据？ 365

Posix 定义了前三个宏，[Stevens and Thomas 1997] 定义了后两个。

这些宏将用于下方的伪代码中：

```
struct msghdr      msg;

struct msghdr     *cmmsgptr;

/* 填充 msg 结构 */

/* 调用 recvmsg(&msg); */

for (cmmsgptr = MSG_FIRSTHDR(&msg); cmmsgptr != NULL; cmmsgptr = MSG_NXTHDR(cmmsgptr)) {

if (cmmsgptr->cmsg_level == ...) {

    char *ptr;

    ptr = MSG_DATA(cmmsgptr);

    /* 处理 ptr 指向的数据 */

}
```

`CMSG_FIRSTHDR` 返回指向第一个辅助数据对象的指针，如果 `msghdr` 结构中没有辅助数据，则返回空指针（`msg_control` 为空指针，或 `cms_len` 小于 `cmsghdr` 结构的大小）。`CMSG_NXTHDR` 在控制缓冲区中没有另一个辅助数据对象时返回空指针。

许多 `CMSG_FIRSTHDR` 的实现从不查看 `msg_control` 并返回 `cmsg_control` 的值。在图 20.2 中，我们在调用此宏之前测试了 `msg_control` 的值。

`MSG_LEN` 和 `MSG_SPACE` 的区别在于，前者没有考虑辅助数据对象数据部分之后的任何填充，因此是存储在 `cms_len` 中的值；而后者考虑了末尾的填充，因此是在为辅助数据对象动态分配空间时使用的值。

## 队列了多少数据？

有时我们想查看套接字上队列了多少数据等待读取，而不实际读取这些数据。有三种技术可用：

1. 如果目标是在当没有数据可准备好读取时时不在内核中阻塞，则可以使用非阻塞 I/O。我们在第 15 节中描述了这一点。
2. 如果我们想检查数据但将其将其留在接收队列中供进程的其他部分读取，可以使用 `MSG_PEEK` 标志（图 13.6）。如果我们想这样做，但不确定是否有数据准备好读取，可以将此标志与非阻塞套接字结合，或将此标志与 `MSG_DONTWAIT` 标志结合。
   注意，对于流，在连续调用 `recv` 之间接收队列上的数据量可能会发生。例如，假设我们对 TCP 套接字调用 `recv`，指定缓冲区长度为 100 并带有 `MSG_PEEK` 标志，返回值为 100。如果我们再次调用 `recv`，可能会返回超过 100 的值（假设我们指定了大于 100 的缓冲区长度），在两次调用之间 TCP 可能接收更多数据。
3. 某些实现使用 `ioctl` 的 `FIONREAD`。`ioctl` 的第三个参数是一个指向整数的指针，其中返回的值是套接字接收队列上的字节数（第 553 页）。还需要注意，Berkeley 派生实现为 UDP 套接字返回的 `count` 包含了每个数据报所需的发送者 IP 地址和端口的套接字结构空间（IPv4 为 16 字节，IPv6 为 24 字节）。

## 13.8 套接字与标准 I/O

在之前的所有示例中，我们都使用了所说的 Unix I/O，即 `read` 和 `write` 函数及其变体（`recv`, `send` 等）。这些函数处理描述符，通常在内核中实现为系统调用。

另一种执行 I/O 的方法是标准 I/O 库。由 ANSI 标准指定，旨在移植到支持 ANSI 的非 Unix 系统。标准 I/O 库处理了在使用 Unix I/O 函数时我们必须担心的细节，它会自动对输入输出流进行缓冲。遗憾的是，它对流缓冲的处理可能会带来一组我们必须担心的新问题。APUE 的第 5 章详细介绍了标准 I/O 库 [Plauer 1992] 并讨论了完整的实现。

> 流与标准 I/O 库链接，就好像“我们打开一个输入流”或“我们刷新输出流”一样。不要将此与 System V 子系统混淆，我们在第 3 节中讨论了它们。

标准 I/O 库可以与套接字一起使用，但有几点需要考虑：

- 可以通过 `fdopen` 从描述符创建标准 I/O 结构。同样，给定一个 I/O 流，可以通过 `fileno` 获取对应的描述符。我们第一次遇到 `fileno` 是在图 6.9 中，当我们需要对标准 I/O 流调用 `select` 时。`select` 只作用于描述符，所以我们必须获取描述符。
- TCP 和 UDP 套接字是全双工的。标准 I/O 流也可以全双工：如果我们以描述符 r 打开流，意味着可读写。在这样的流上，输出函数之后调用输入函数之前必须调用 `fflush`、`fseek`、`fsetpos` 或 `rewind`。同样，输入函数之后调用输出函数之前必须调用 `fseek`、`fsetpos` 或 `rewind`。
- 处理这种读读写问题的简单方法是为给定的端口打开两个 I/O 流：一个用于读取，一个用于写入。

### 示例：使用 I/O 的 str_echo 函数

现在我们用标准 I/O 替换 `readline` 和 `write` 来实现 TCP echo 服务器（图 5.3）。图 13.14 是我们使用标准/O 的 `str_echo` 函数版本（该版本有一个我们稍后描述的问题）。

```
#include "unp.h"

void

str_echo(int sockfd) {

    char line[MAXLINE];

    FILE *fpin, *fpout;

    fpin = fdopen(sockfd, "r");

    fpout = fdopen(sockfd, "w");
```
