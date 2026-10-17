
```c
numBytes = recvfrom(sfd, buf, BUF_SIZE, 0, NULL, NULL);

if (numBytes == -1)
    errExit("recvfrom");

printf("Server received %ld from %s\n", (long)numBytes, svaddr.sun_path);

for (j = 0; j < numBytes; j++)
    buf[j] = toupper((unsigned char) buf[j]);

if (sendto(sfd, buf, numBytes, 0, &claddr, sizeof(struct sockaddr_un)) != (ssize_t)numBytes)
    fatal("sendto");
}
}
```

### 列表 57-7: 简单的 UNIX 域数据报客户端

```c
#include "ud_usecase.h"

main(int argc, char *argv[]) {
    struct sockaddr_un svaddr, claddr;
    int sfd, j;
    ssize_t numBytes;
    size_t mslen;
    char resp[BUF_SIZE];
    if (argc < 2 || strcmp(argv[1], "--help") == 0) {
        usageError("%s...\n", argv[0]);
        return(0);
    }
    /* 创建客户端套接字；绑定到基于 PID 的唯一路径 */
    sfd = socket(AF_UNIX, SOCK_DGRAM, 0);
    if (sfd == -1)
        errIt("socket");
    memset(&claddr, 0, sizeof(struct sockaddr_un));
    claddr.sun_family = AF_UNIX;
    sprintf(claddr.sun_path, sizeof(claddr.sun_path), "/tmp/ud_usecase_%ld", (long)getpid());
    if (bind(sfd, (struct sockaddr *)&claddr, sizeof(struct sockaddr_un)) == -1)
        errIt("bind");
    /* 向服务器发送消息；将响应回到标准输出 */
    for (j = 0; j < argc; j++) {
        mslen = strlen(argv[j]); /* 可能超过 BUF_SIZE */
        if (sendto(sfd, argv[j], mslen, 0, &svaddr, sizeof(struct sockaddr_un)) != (ssize_t)mslen)
            fatal("sendto");
        numBytes = recvfrom(sfd, resp, BUF_SIZE, 0, NULL, NULL);
        if (numBytes == -1)
            errIt("recvfrom");
        printf("Response %d: %s\n", j, (int)numBytes, resp);
    }
    remove(claddr.sun_path); /* 删除客户端套接字路径 */
    exit(EXIT_SUCCESS);
}
```

以下 shell 会话日志演示了服务器和客户端程序的使用：

```
$ ./ud_ucase_sv & 
[1] 2013
$ ./ud_ucase_cl hello world      向服务器发送 2 条消息
Server received 5 bytes from /tmp/ud_ucase_cl.21050
Response: 1 HELLO
Server received 5 bytes from /tmp/ud_ucase_cl.21050
Response: 2 WORLD
$ ./ud_ucase_cl 'long message'      向服务器发送 1 条较长的消息
Server received 10 bytes from /tmp/ud_ucase_cl.21051
Response: 1 LONG MESSA
$ kill %1                               终止服务器
```

客户端程序的第二次调用设计用于展示：当 `recv()` 调用指定的长度（`BUF_SIZE`，在列表 57-5 中定义，值为 10）小于消息大小时时，消息会被静默地截断。我们可以看到这种截断确实发生了，因为服务器打印了一条消息，说它只收了 10 个字节，而客户端发送的消息包含 12 个字节。

### 57.4 UNIX 域套接权限

套接文件的所有权和权限决定了哪些进程可以与该套接进行通信：

- 连接到 UNIX 域流式套接（stream socket），需要对套接文件具有写权限。
- 向 UNIX 域数据报套接（datagram socket）发送数据报，需要对套接文件具有写权限。

此外，套接路径中的每个目录都需要具有执行（搜索）权限。

默认情况下，套接是通过 `bind()` 创建的，并向所有者（用户）、组组和其他用户授予所有权限。要更改此设置，我们可以在调用 `bind()` 之前先调用 `umask()`，以禁用我们不希望授予的权限。

某些系统会忽略套接文件的权限（SUSv3 允许这样做）。因此，我们无法部分地使用文件权限来控制对套接的访问，尽管我们可以部分地利用宿主目录的权限来实现这一目的。

### 57.5 创建已连接的套接对：socketpair()

有时，让单个进程创建一个套接对并将它们连接在一起是有用的。这可以通过两次调用 `connect()`、一次调用 `bind()`，然后调用 `listen()`、`connect()` 和 `accept()`（针对流式套接字），或者调用一次 `connect()`（针对数据报套接字）来实现。`socketpair()` 系统调用提供了这种操作的简便方法。

```c
#include <sys/socket.h>
socketpair(int domain, int type, int protocol, int sockfd[2]);
成功返回 0，错误返回 -1
```

此 `socketpair()` 系统调用只能在 UNIX 域中使用；该域必须被指定为 `AF_UNIX`（此限制适用于大多数实现，并且是逻辑上的，因为套接字对是在单个主机系统中创建的）。套接字类型可以指定为 `SOCK_DGRAM` 或 `SOCK_STREAM`。协议参数必须指定为 0。`sockfd` 数组返回指向两个已连接套接字的文件描述符。

指定类型会创建一个等同于双向管道（也称为流管道）的内容。每个套接字都可以用于读写，且独立的数据通道在两个套接字之间双向流动。在 BSD 派的实现中，`pipe()` 是通过调用 `socketpair()` 实现的。

通常，套接字对的使用方式类似于管道。在执行 `socketpair()` 之后，进程通过 `fork()` 创建子进程。子进程继承父进程的所有描述符，包括指向套接字对的描述符。父进程和子进程可以使用该套接字对进行进程间通信（IPC）。

`socketpair` 与手动创建一对已连接的套接字不同在于，套接字没有绑定到任何地址。这可以帮助我们避免一整类安全漏洞，因为套接字对任何其他进程不可见。

从内核 2.6.27 开始，Linux 为 `type` 参数提供了第二个用途，允许在使用套接字类型时设置两个非标准标志。`SOCK_CLOEXEC` 标志允许内核为两个新文件描述符开启执行时关闭（FD, CLOEXEC）功能。由于某些原因，该标志很有用，就像第 4.3.1 节描述的 `open()` `O_CLOEXEC` 标志一样。`SOCK_NONBLOCK` 标志允许内核在两个底层文件描述上设置 `O_NONBLOCK` 标志，以便未来对套接字的 I/O 操作将是非阻塞的。这节省了为了实现相同结果而额外调用 `fcntl()` 的次数。

### 57.6 Linux 抽象命名空间

所谓的抽象命名空间（abstract namespace）是 Linux 特有的功能，允许我们将 UNIX 域套接字绑定到一个名称，而无需在文件系统中创建它。这提供了几个潜在的优势：

- 我们不需要担心与系统中现有名称可能发生冲突。
- 在完成套接字后，不需要取消（unlink）套接字路径。当套接字关闭时，抽象名称会自动删除。
- 我们不需要为套接字创建文件系统路径。这在 `chroot` 环境中，或者当我们没有文件系统的写访问权限时可能非常有用。

要创建一个抽象绑定，我们将 `sun_path` 字段的第一字节指定为空字节（0）。这会将抽象套接字名称与传统的 UNIX 域套接字路径区分开来，后者由一个或多个非空字节组成的字符串，并以空字节结尾。抽象套接字由 `sun_path` 中剩余的字节（包括任何空字节）定义，长度为抽象结构大小定义的长度。

### 列表 57-8: 创建抽象绑定

```c
struct sockaddr_un addr;
memset(&addr, 0, sizeof(addr));               /* 清空地址 */
addr.sun_family = AF_UNIX;                      /* UNIX 域 */
char *name = "xyz";                             /* 抽象名称为 "xyz" */
strncpy(&addr.sun_path[1], name, strlen(name));
int sockfd = socket(AF_UNIX, SOCK_STREAM, 0);
if (sockfd == -1)
    perror("socket");
if (bind(sockfd, (struct sockaddr *)&addr, sizeof(sun_family) + strlen(name)) == -1)
    perror("bind");
```

使用空字节来区分抽象套接字名称与传统的 UNIX 域套接字路径可能会产生意外后果。假设变量恰好是一个空字符串，并且我们尝试绑定套接字：

```c
strncpy(&addr.sun_path, name, sizeof(sun_path) - 1);
```
