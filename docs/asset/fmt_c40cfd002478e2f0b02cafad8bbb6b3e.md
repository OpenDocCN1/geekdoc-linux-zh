
```c
/* client (fd) */
size = strlen(message1);
if (write(fd, message1, size) != size) {
    perror("client write fd");
    exit(1);
}
if ((n = read(fd, buff, size)) == -1) {
    perror("client read");
    exit(1);
}
else
    if (write(1, buff, n) != n) {
        perror("client write stdout");
        exit(1);
    }
close(fd);

/* Remove FIFO now that we are done using it */
if (unlink(FIFO) == -1) {
    perror("client unlink FIFO");
    exit(1);
}
exit(0);
}
```

```
% more server.c
```

```c
#include "fifo.h"

int main(void)
{
    char buff[SIZE];
    int fd;
    int n, size;

    /* Create two FIFOs and open them for
       reading and writing */
    if ((mkfifo(FIFO, S_IFIFO | PERMS) == -1)
        && (errno != EEXIST)) {
        perror("mkfifo FIFO");
        exit(1);
    }

    if ((fd = open(FIFO, 2)) == -1) {
        perror("open FIFO");
        exit(1);
    }

    /* server (fd) */
    size = strlen(message1);
    if ((n = read(fd, buff, size)) == -1) {
        perror("server read");
        exit(1);
    }
    if (write(1, buff, n) < n) {
        perror("server write stdout");
        exit(1);
    }
    size = strlen(message2);
    if (write(fd, message2, size) != size) {
        perror("server write fd");
        exit(1);
    }
    close(fd);
}
```

### 21
实现图 20.9 中给出的客户端-服务器模型。服务器提供 `ECHO` 服务。通过在系统上打开三个终端窗口运行三个并发客户端来测试该模型。

### 22
你会使用什么系统调用来为流式通信创建 `IPv4` 套接字，并在进程执行 `exec()` 系列的系统调用（或库调用）时关闭该套接字？

### 23
你会使用什么系统调用来为非阻塞流式通信创建 `IPv6` 套接字，并在进程执行 `exec()` 系列的系统调用（或库调用）时关闭该套接字？

### 24
下列符号常量的值是多少：

- a. `PF_INET`
- b. `PF_INET6`
- c. `SOCK_STREAM`
- d. `SOCK_NONBLOCK`
- e. `AF_UNIX`
- f. `PF_UNIX`
- g. `AF_INET`

### 25
你的系统支持多少种通信域？你是如何得出答案的？如果为此目的定义了符号常量，请显示该定义。提示：浏览 `/usr/include/sys/socket.h` 文件。

### 26
编写代码片段以使用 `TCP` 协议在 `IPv4` 下为流式通信风格创建套接字。将套接字标记为“close-on-exec”和“nonblocking”。

### 27
套接字何时处于半关联状态？何时处于完全关联状态？

### 28
`TCP/IP` 协议的什么特性允许在互联网上的主机上同时运行多个不同的服务器，并在互联网上的主机上运行的客户端和服务器程序之间建立多个并发通信会话？

### 29
什么类型的基于套接字的通信要求两个通信进程的套接字完全关联？

### 30
`inet_aton()` 和 `inet_ntoa()` 调用的新版本是什么？为什么你会更喜欢使用新调用而不是旧调用？

### 31
使用 `UNIX` 域套接字设计并实现 `ECHO` 服务的客户端-服务器模型。

### 32
你系统上与 `listen()` 系统调用关联的队列的最大长度是多少？你使用的是什么类型的 `UNIX`？是如何得出答案的？

### 33
登录到运行至少一个 `Internet` 服务器的机器，例如 `SSH`。使用 `netstat` 命令并使用适当的选项来确定服务器的被动套接字关联的队列大小。显示你为此目的使用的命令的输出。

### 34
`shutdown()` 系统调用用于关闭套接字。当你可以使用 `close()` 系统调用关闭描述符时，为什么需要它？

### 35
对于 `PF_INET` 和 `PF_LOCAL` 域下的 `SOCK_STREAM` 和 `SOCK_DGRAM` 类型套接字，`connect()` 系统调用会产生什么类型的网络流量？

### 36
`accept()` 和 `accept4()` 系统调用之间的区别是什么？

### 37
为什么进程必须在循环中从 `SOCK_STREAM` 套接字读取数据？对于 `SOCK_DGRAM` 套接字为什么不需要这样做？

### 38
主动套接字和被动套接字之间的区别是什么？它们是如何创建的？为什么服务器进程等待连接请求的套接字被称为被动套接字？

### 39
为什么主动套接字也被称为临时套接字？

### 40
以下每个系统调用失败的两个原因：

- a. `socket()`
- b. `mkfifo()`
- c. `mkfifoat()`
- d. `bind()`
- e. `listen()`
- f. `connect()`
- g. `accept()`
- h. `select()`
- i. `shutdown()`

### 41
假设 `S` 是一个面向连接的并发服务器。如果它当前正在为 `K` 个客户端提供服务，服务器使用了多少个套接字和从属进程？如果 `S` 是一个无连接的并发服务器，这些数字会是多少？解释你的答案。

### 42
编写 `ECHO` 服务的并发无连接服务器代码，并用多个客户端同时访问它进行测试。

### 43
编写 `ECHO` 服务的并发面向连接服务器代码，并用多个客户端同时访问它进行测试。

### 44
设计、编码并测试第 20.8.4 节中讨论的面向连接的迭代客户端-服务器模型。

### 45
在你的 `UNIX` 系统上运行的所有服务器的被动套接字关联的队列长度是多少？你是如何得出答案的？展示你的工作过程。

### 46
某些网络编程库函数，例如 `inet_ntop()`，有一个 `size`（或 `length`）参数来指定目标地址变量的字节长度。为什么需要它？

### 47
当 `select()` 系统调用失败并返回 `-1` 时，描述符集合会发生什么？

### 48
当 `select()` 系统调用因计时器过期而返回时，它返回什么？

### 49
何时需要并发客户端？给出几个例子并给出 `HTTP` 客户端的代码结构。

### 54
为什么需要并发客户端？编写用于 `ECHO` 服务的并发客户端，使其连接到多个 `ECHO` 服务器并显示每个服务器的响应时间。展示客户端的源代码、其编译过程以及几次示例运行。

### 55
`inetd`，`UNIX` 超级服务器的配置文件中一行的格式是什么？每个字段的含义是什么？

### 56
通过 `UNIX` `inetd` 提供哪些类型的服务？解释你的答案。

### 57
如果一个负载很重的服务通过 `inetd` 提供会发生什么？解释你的答案。在这种情况下系统管理员应该怎么做？

### 58
写下使 `inetd` 通过使用 `SIGHUP` 信号动态重新配置的代码片段。仅显示信号处理代码和实际重新配置的代码结构。

### 59
当 `inetd` 为两个 `TIME` 客户端和 `ECHO`、`TELNET`、`FTP` 服务各一个客户端提供服务时，运行了多少个服务器和客户端进程？在此设置下服务器端使用了多少个套接字？解释你的答案。

### 60
`kill -HUP `cat /var/run/inetd.pid`` 命令可用于使 `inetd` 在 `BSD` 系统上重新初始化并动态重启。在 `Solaris` 系统上此命令的等价命令是什么？

### 61
你系统上 `inetd` 的 `PID` 是什么？写下你为此目的使用的命令。

### 62
什么是并发客户端？为什么需要并发客户端？列出三个原因。此外，列出三个需要使用并发客户端的知名 `Internet` 服务。

## 系统编程 IV

## *实践考虑*

### 目标

- 解释系统调用重启的概念
- 描述线程安全的系统调用
- 讨论编写一个在后台启动并成为守护进程的程序的概念
- 讨论为守护进程设置信号和 `umask`
- 描述允许仅运行一个程序副本的概念
- 讨论在已知位置保存守护进程的身份
- 解释将终端从进程分离的问题
