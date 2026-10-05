

## 102 TCP/IP 与 Linux 协议实现

```c
23 gettimeofday(&then,(struct timezone *0);
24 if (select(selret,NULL, NULL, NULL, timeout) < 0) {
25     check(selret, "select");
26 gettimeofday(&now,(struct timezone *0);
27     printf("Delay %ld microseconds\n",now.tv_sec - then.tv_sec)*1000000 +
28             now.tv_use - then.tv_use);
29     exit(0);
30 }
```

除了 select() ，许多系统还实现了 poll() 调用。

**图 4.6** poll().

```c
1 #include <sys/poll.h>
2 int poll(struct pollfd *ufds, unsigned int nfds, int timeout);
```

poll() 是 select 的一种变体。它指定了一个类型如下所示的 `nfds` 结构体数组。

**图 4.7** pollfd.

```c
1 struct pollfd {
2     int fd;          /* 文件描述符 */
3     short events;    /* 请求事件 */
4     short revents;    /* 返回事件 */
5 };
```

timeout 以毫秒为单位，而不是像 select() 中那样复杂的结构。

### 4.4.2 非阻塞 I/O

在某些情况下，我们并不感兴趣等待输出是否已经完成，而是希望启动它。在其他情况下，程序员可能希望在数据已就绪时立即读取尽可能多的数据，如果还没有数据则不等待。为了这个目的，提供了非阻塞 I/O，它通过设置与文件描述符相关的进程数据中的标志位来触发。

图 4.8 NBIO: pix/nbio.c。

```c
setnb()
{
    int on = 1;
    int iret;

    if ((iret=ioctl(0, FNBIO, (char *) &on) < 0)
        check(iret, "ioctl FNBIO error");
}
```

最后，我们可能希望执行一组任务，但被新数据的到达的中断——这可以在用户空间通过使用信号来实现。对于 I/O，其设置如下。

### 4.4.3 异步 I/O

图 4.9 展示了异步输入。在这里，应用程序在注册了特定事件的回调函数后，继续其当前的工作。

![](img/06c11ba8be5c1c24aa633e12618e2ebd_158_0.png)

图 4.9 异步接收。

## TCP/IP 与 Linux 协议实现

使用此方法的应用程序示例如图 4.10 所示。

# 图 4.10 SIGIO: pix/asynch.c。

```c
#include    <signal.h>
#include    <fcntl.h>

#define BUFFERSIZE 4096
int     sigflag; /* 必须是全局变量！ */
int sigio_handler()
{
    sigflag = 1;      /* 只设置标志并返回 */
}

int main()
{
    int     n, fret;
    char    buff[BUFFERSIZE];

    signal(SIGIO, sigio_handler);
    fret=fcntl(0, F_SETOWN, getpid());
    check(fret, "F_SETOWN error");

    fret=fcntl(0, F_SETFL, FASYNC);
    check(fret, "F_SETFL FASYNC error");

/* 这将异步变成了一个在 sigpause ... 中阻塞的循环 ... */
    for (;;) {
        sigblock(sigmask(SIGIO));
        while (sigflag == 0)
            pause(0);      /* 等待信号 */

        /*
        * 如果 sigflag != 0，我们就在这里。此外，我们知道
        * SIGIO 信号当前处于阻塞状态。
        */
        if ((n = read(0, buff, BUFFERSIZE)) > 0) {
            if (write(1, buff, n) != n)
                check(-1, "write error");
        } else if (n < 0)
            check(fret, "read error");
        } else if (n == 0)
            exit(0);      /* EOF */

        sigflag = 0;      /* 关闭我们的标志 */
        sigsetmask(0);    /* 并重新启用信号 */
    }
}
```

## 替代编程模型

Java 等其他语言内置了并发机制，如线程。对于事件处理程序，使用这些机制进行编程可能非常优雅。

### 4.4.4 系统包含头文件

在前面的示例中有几个头文件对于所有 socket 编程都是通用的，并提供了用于 socket 系统层的类型定义。这些文件位于源码树的 `/usr/include/netinet` 中。

图 4.11 IP 地址结构：linux/include/in.h。

```c
/* 描述互联网 (IP) socket 地址的结构体 */
#define SOCK_SIZE__ 16    /* sizeof(struct sockaddr) */
struct sockaddr_in {
    sa_family_t      sin_family;    /* 地址族 */
    unsigned short   sin_port;      /* 端口号 */
    struct in_addr    sin_addr;      /* IP地址 */
    /* 填充到 struct sockaddr 的大小 */
    unsigned char     __pad[SOCK_SIZE__ - sizeof(short int) - 
                      sizeof(unsigned short int) - sizeof(struct sockaddr)];
};
#define sin_zero         __pad          /* 用于 BSD UNIX 编译 -FVK */
```

其 IPv6 版本如下（出乎意料，更加复杂）。

图 4.12 IPv6 地址结构视图：linux/include/in6.h。

```c
struct sockaddr_in6 {
    union {
        u8_t            __u8    u6_addr[16];
        u16_t           __u16   u6_addr[8];
        u32_t           __u32   u6_addr[4];
    } in6_u;
    #define s6_addr         
    #define s6_addr16      in6_u
    #define s6_addr32      in6_u
    u8_t            sin6_family;    /* 地址族 */
    u16_t           sin6_port;      /* 端口号 */
    struct in6_addr sin6_addr;      /* IP地址 */
    /* 填充到 struct sockaddr_6 的大小 */
    unsigned char     __pad[40 - sizeof(short int) - 
                      sizeof(unsigned short int) - sizeof(struct in6_addr)];
};
#define sin6_zero         __pad          /* 用于 BSD UNIX 编译 -FVK */
```

