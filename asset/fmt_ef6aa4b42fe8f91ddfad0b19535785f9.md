
如果 `flag` 为 0，关闭读部分；如果 `flag` 为 1，关闭写部分；如果 `flag` 为 2，则关闭读写写部分。当 `shutdown` 与 `socketpair` 调用（在 UNIX 域中创建两个连接的套接字）结合使用时，可以精确模拟 `pipe` 系统调用。

## 12.11 网络数据库与地址映射

例如，示例程序涉及带有 UNIX 域地址的套接字。对于 Internet，套接字地址（图 12.5）更为复杂，需要主机的数字 IP 地址以及特定服务器的端口号。`DNS`（参见第 9.6 节）、一组数据库文件（通常保存在 `/etc` 下）以及一组库函数共同帮助在应用程序程序中构建所需的 Internet 套接字地址。

### 网络数据库

- `/etc/resol.conf` —— 这是 DNS 解析器的配置文件（参见第 9.6 节）。它识别本地域并列出该域的若干个服务器。如 `gethostbyname` 等地址映射库函数依赖 DNS 解析器，解析器查询列出的名称服务器获取网络地址信息。

- `/etc/named.boot` —— 这是 DNS 名称服务器文件，包含初始数据文件所在的信息。只有运行名称服务器（`named`）的主机需要此文件。通常，数据文件提供根名称服务器的位置、邮件交换信息以及由名称服务器控制的低级区域的资源记录。

- `/etc/services` —— 此文件包含有关已知 Internet 服务的信息。每个服务由单行表示，具有以下由空格分隔的字段：

  `official-service-name port-number/protocol-name alias ...`

  例如：`smtp 25/tcp mail` 代表在端口 25 处使用 Internet TCP 协议的 sendmail 服务器。官方网络服务具有由 InterNIC 分配的标准端口号。这些端口号在 1-1023 范围内，只有具有 root 权限的进程才能访问。编写实验性网络程序时，普通用户通常被限制在 1024 到 5000 之间的端口。

- `/etc/protocols` —— 此文件包含有关已知 Internet 协议的信息。每个协议由单行表示，用空格分隔以下字段：

```
official-protocol-name protocol-member alias... 
```

例如，以下是 Internet 协议：

| ip | IP | # Internet 协议，伪协议号 |

| :--- | :--- | :--- |

| icmp | 1 | ICMP | # Internet 控制消息协议 |

| igmp | 2 | IGMP | # Internet 组组播协议 |

| tcp | 6 | TCP | # 传输控制协议 |

| udp | 17 | UDP | # 用户数据报协议 |

### 网络库函数

网络库提供了一组标准函数来访问网络映射。这些函数在 DNS 的帮助下，返回包含 IP 地址、端口号等的结构体。使用这些函数的任何必须包含 `<netdb.h>`。例如，要获取主机的 IP 地址，使用：

```c
struct hostent {
    char *h_name;        /* 名称 */
    char **h_aliases;    /* 别名 */
    int h_type;          /* 类型 */
    int h_length;        /* 长度 */
    struct in_addr *h_addr; /* 地址 */
    int h_addr_len;      /* 地址数量 */
};
```

在实验 Internet 套接字（sockets）时，使用不与现有网络服务冲突的空端口是非常重要的。`/etc/services` 文件列出了 UNIX 系统已知的所有服务。通常情况下，端口 1–1023 是预留的。其他如 X Window System 等常用服务使用了定义良好的端口。对于实验性代码，使用 3000 到 4000 之间的端口号通常是安全的。

现在让我们关注客户端侧端。`inetclient.c` 进程可以连接到任何主机上的简单服务器。它首先获取从命令行发送的主机结构体（A 行），然后逐字节通过已经正确初始化的对端套接字地址，复制地址 `h_addr_list[0]`（B 行）。建立连接后（C 行），发送消息 `Hello Internet`（D 行）并显示来自服务器的回显（echo）内容。

```c
****** inetclient.c *****/
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/socket.h> /* Internet domain header */
#include <netinet/in.h>
#include <netdb.h>
```

```c
#define SERVER_PORT 3900
struct sockaddr_in peer = {AF_INET, htons(SERVER_PORT)};
```

```c
int main(int argc, char *argv[])
{ 
    int soc;
    char buf[256];
    struct hostent *hp;
    if (argc != 2)
    { 
        fprintf(stderr, "Usage: %s hostname\n", argv[0]);
        exit(1);
    }
    /* fill in peer address */
    hp = gethostbyname(argv[1]); /* (A) */
    if (hp == NULL)
    { 
        fprintf(stderr, "%s: %s unknown host\n", argv[0], argv[1]);
        exit(1);
    }
    bcopy(peer->sin_addr.s_addr, hp->h_addr[0], hp->h_length);
    /* create socket */
    soc = socket(AF_INET, SOCK_STREAM, 0);
    /* request connection to server */
    if (connect(soc, &peer, sizeof(peer)) == -1)/* (C) */
    { 
        perror("client:connect"); 
        close(soc);
        exit(1);
    }
```

第 12 章 进程间网络通信

在不同的主机上编译并运行这两个程序，以便在本地网络上进行测试。

## 12.12 远程登录服务

### 远程登录客户端

为了说明此处介绍述的网络材料，让我们看看实际网络服务中套接字的使用。以下代码显示了客户端程序（rlogin）的片段。该程序接收命令行指定的主名，并在目标主机上的登录服务器建立虚拟电路。网络库例程 `getservname` 获取 login/tcp 服务器的端口号（第1行）。`gethostname` 获取远程主机的 IP 地址（第2行）。获取的信息随后被存入 `peer` 结构体中（第3-4行），以形成服务器套接字的完整地址。客户端创建一个 Internet 域套接字 `s`（第5行），然后连接到由地址 `peer` 指定的服务器套接字（第6行）。一旦建立连接，两端服务器进程与客户端进程之间的双向通信通道便已建立。随后远程主机与本地用户之间转发消息的主要任务就可以进行。

```c
**** rlogin code segments *****/
int main(int argc, char *argv[])
{ 
    struct sockaddr_in peer;
    struct servent *sp;
    struct hostent *hp;
    ...
    sp = getservname("login", "tcp");      /* (1) */
    if (sp == NULL)
        fprintf(stderr, "rlogin: tcp/login: unknown service\n");
        exit(1);
    hp = gethostname(argv[1]);      /* (2) */
    if (hp == NULL)
        fprintf(stderr, "rlogin:%s:unknown host\n", argv[1]);
        exit(1);
```

远程登录服务 417

```c
}
    bzero((char *)peer, sizeof(peer));      /* (3) */
    bcopy(hp->h_addr_list[0],
        (char*)&peer.sin_addr, hp->h_length);
    peer.sin_family = hp->h_type;
    peer.sin_port = sp->s_port;           /* (4) */
    s = socket(AF_INET, SOCK_STREAM, 0);   /* (5) */
    if (s < 0) {
        perror("login: socket"); exit(1);
    }

    if (connect(s, (char *)peer, sizeof(peer)) < 0)/* (6) */
        perror("login: connect"); exit(1);
}
/* now perform login service */
```

例程 `bzero(char *s, int n)` 将字符串 `s` 的 `n` 个字节置零。例程 `bcopy(char *x, char *y, int n)` 将字符串 `x` 复制到字符串 `y`。为了完成这张图，我们现在来看服务器侧。

### 远程登录服务器

为了提供网络服务，服务器必须能够响应任何潜在客户端的请求。这可以通过在后台运行的守护进程持续监控标准端口的请求来实现。一旦接收到请求，就可以调用一个单独的进程提供服务，而服务器守护进程保持准备处理额外的请求。以下代码片段涉及远程登录服务器。初始化 Internet 地址结构（A 行）后，程序获取 login/tcp 服务（B 行）并将端口存入登录套接字（C 行）。完成的地址绑定到流套接字（D 行）。`listen` 调用（E 行）使 `s` 准备好后续的 `accept`（F 行）。然后服务器进入无限循环：为了处理登录请求，它建立套接字连接（H 行）并派生每个客户端登录服务器（I 行）。服务器继续监控其他请求且永退出。

```c
**** login server *****/
#include <sys/types.h>
#include <sys/stat.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <netdb.h>
#include <errno.h>

struct sockaddr_in login = { AF_INET };    /* (A) */

int main(int argc, char *argv[])
{ 
    struct servent *sp;
    struct sockaddr_in peer;
    int s;
    ...
    sp = getservbyname("login", "tcp");    /* (B) */
    if (sp == NULL)
        fprintf(stderr, "%s: login/tcp: unknown service\n", argv[0]);
        exit(1);
```

```c
#ifndef DEBUG
/* code to disassociate from terminal */
#endif
```

```c
    login.sin_port = sp->s_port;    /* (C) */
```

```c
...
    s = socket(AF_INET, SOCK_STREAM, 0);    /* (D) */
    if (s < 0)
        perror("socket"); exit(1);
    ...
```

```c
    if (bind(s, &login, sizeof(login)) < 0)    /* (E) */
    { 
        perror("bind"); exit(1);
    }
    ...
```

```c
    listen(s, 3);    /* (F) */
    for (;;);    /* (G) */
    { 
        int ns, len=sizeof(peer);
        ...
    }
```

```c
    ns = accept(s, &peer, &len);    /* (H) */
    if (s < 0)
    { 
        if (errno == EINTR) continue;
        perror("accept");
        continue;
    }
```

```c
    if (vfork() == 0)    /* (I) */
        close(s);
        /* exec per-client rlogin server */
    }
    close(ns);
```

上述材料仅仅说明了套接字的使用。实际的 rlogin 服务器更为复杂。

### 实际 rlogin 服务

在实践中，Internet 多服务守护进程（inetd）监控 login/tcp 端口并调用每个进程的服务器（例如 rlogin），将其传递给客户端套接字的 IP 地址（host）和端口号（port），以处理每个远程登录请求。rlogin 服务器经常通过检查端口和主机来验证登录请求：

- 1. 如果端口不在 0–1023 范围内（特权端口），连接将被终止。
- 2. 如果主机未列在服务器机器上的 `/etc/hosts` 数据库中，连接将被终止。

随后，rlogin 分配一个伪终端（pty），将 pty 的从机（或计算机）侧连接到登录进程，并将自己连接到控制（或用户）侧。

图 12.8 远程登录概览

（图 12.8）。登录进程是 `login -r` 的实例。服务器进程会在注销或其对端套接字关闭时终止。

## 12.13 守护进程

在 UNIX 上，许多隐藏进程在后台静默运行完成各种任务，如魔法一般。这些被称为守护进程，它们与其他进程并发运行。例如：

- `cron` 守护进程（通常为 `/etc/cron`）根据 `crontab` 命令指定的日期和时间执行命令（见 5.10 节）。
- 打印守护进程（通常为 `/usr/lib/lpd`）处理由 `lpr` 提交的打印请求（见 5.2 节）。
- `nfsfd` 和 `bind` 守护进程支持网络文件系统（见 8.8 节）。
- `named`（通常为 `/etc/named`）是 Internet DNS 服务器（见 9.6 节）。
- `sendmail` 守护进程（通常为 `/usr/lib/sendmail -bd`）发送和接收 Internet 邮件（见第 4 章）。
- Internet 服务守护进程（通常为 `/etc/inetd`）监控不同的标准网络服务端口并启动相应的每个客户端的服务器（例如 `rlogind`）。

许多其他网络服务器未在此处列为守护进程。但也有一些服务器，如 X Window System 服务器，并不被认为是守护进程。

`inetd` 等待下一个传入的连接（流套接字）或数据（数据套接字），采取采取的操作：

- 当检测到连接请求时，它会调用一个根据套接字端口号确定的客户端服务器，并将连接的套接字传递给子进程进行标准 I/O。
- 当检测到传入的数据（数据套接字）时，它会调用一个根据套接字端口号确定的客户端服务器，并将数据套接字传递给子进程进行标准 I/O。

随后 `inetd` 回到监控状态，忽略任何仍在被服务的数据套接字上的活动。

### 编写守护进程

如 `cron`、`inetd` 和 `sendmail -bd` 等守护进程程序具有以下四个重要特征：

1. 守护进程永不退出。
2. 守护进程没有控制终端。
3. 守护进程不对控制终端进行 I/O 操作。
4. 系统守护进程通常在系统启动时启动，由 `init` 进程（进程 1）控制，并在由于某些原因崩溃后可以重启。

为了将进程从其控制终端分离，可以使用系统调用 `setid()`。该调用会创建一个新的会话和一个新的进程组。它将调用进程设置为会话首进程和进程组组。此时尚未分配控制终端。调用进程是新进程组中的唯一进程，也是新会话中的唯一进程。

因此，守护进程通常执行图 12.9 所示的序列，以便从控制终端和父进程分离。一旦变成孤儿，守护进程将由 `init` 进程接管。

图 12.9 从控制终端分离

```c
setid();
if (fork() == 0)
    perform_duty(); /* 无限循环 */
exit(0); /* 子进程孤儿 */
```

## 12.14 输入/输出多复用

`inetd` 和 X Window 系统服务器等程序需要监控或多复用多个 I/O 描述符的能力。即使第一章描述的 `talk` 命令也多复用了来自不同终端的 I/O。`select` 系统提供了一种通用的同步多复用方案。

```c
#include <sys/time.h>
int select(int nfds, int* readfds, int* writefds, int* exceptfds,
       struct timeval *timeout)
```
