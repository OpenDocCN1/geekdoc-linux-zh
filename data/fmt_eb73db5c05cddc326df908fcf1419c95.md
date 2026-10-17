
| 4 | 7 | 4 | 6 | 7 | 5 | 7 |

| 5 | 8 | 5 | 7 | 8 | 6 | 9 |

| 6 | 10 | 6 | 9 | 8 | 7 | 10 |

| 7 | 11 | 7 | 10 | 8 | 8 | 12 |

| 8 | 13 | 8 | 12 | 8 | 9 | 13 |

| 9 | 14 | 9 | 13 | 8 | 10 | 15 |

| 10 | 16 | 10 | 15 | 8 | 11 | 16 |

| 11 | 17 | 11 | 16 | 8 | 12 | 18 |

| 12 | 18 | 12 | 18 | 8 | 13 | 19 |

| 13 | 20 | 13 | 18 | 8 | 14 | 21 |

| 14 | 22 | 14 | 19 | 8 | 15 | 22 |

图 4.10 对于 `backlog` 值提供的实际队列连接数。

AIX、BSD/OS 和 SunOS 4 采用了传统的 Berkeley 算法，尽管后者不允许 `backlog` 超过 5。HP-UX 和 Solaris 2.6 增加了一点修正系数

### 4.6 accept 函数

关于待处理队列（`backlog`）。Digital Unix、Linux 和 UnixWare 对 `backlog` 的解释是字面的，而 Solaris 2.5.1 则在 `backlog` 的基础上加1。

Linux 允许 `backlog` 为 0 时有无限数量的连接，这表明是一个错误。

用于测量这些值的程序在练习 14.5 的解答中给出。

正如我们所说的，历史上，`backlog` 指定了两个队列之和的最大值。在 1996 年，互联网上出现了一种新的攻击手段，称为 SYN 洪水攻击（CERT 1996）。黑客编写一个程序以特定的速度向受害者发送 SYN 信号，填满一个或多个 TCP 连接的未完成连接队列。正如 (Cheswick and Bellavin 1994) 前言中所述，我们用“黑客”一词来指代攻击者。此外，每个 SYN 的服务器 IP 地址都是被伪造的（这被称为欺骗），这使得服务器无法获黑客的真实 IP 地址。SYN/ACK 无处可去。通过填满连接队列，合法的 SYN 无法进入队列，文中讨论了处理此类攻击的各种方法（Internet 1997）。但此笔记中最有趣的是重新审视 `backlog` 的真正含义。如果 `backlog` 指定了给定 `socket` 已完成连接的最大数量，那么内核必须停止服务器接受新的连接请求。如果对这些连接设置限制（无论出于什么），这种将是不可接受的，因为服务器需要对 SYN 洪水攻击提供保护（例如 Web 服务器）。内核处理大量的未完成连接，无论这些连接是合法的还是来自黑客。根据这种解释，我们可以在图 4.9 中看到完成连接队列累积的情况（最多 15 个），其中传统的值是不够的。`accept` 被 TCP 服务器调用，从完成连接队列的头部返回下一个完成连接。如果完成连接队列为空，进程将进入睡眠（假设是阻塞的）。

```c
#include <sys/socket.h>
int accept(int sock, struct sockaddr *addr, socklen_t *addrlen);
```

返回：子进程返回非负描述符，错误返回 -1

`addr` 和 `addrlen` 参数用于返回对端的协议地址。`addrlen` 是一个值参数（第 3.3 节）；在调用之前，我们将由 `addr` 指向的 `socket` 结构的大小设置为整数，返回时，该整数包含了内核存储在 `socket` 结构中的实际字节数。

如果 `accept` 成功，其返回值是由内核自动创建的新描述符。这个新描述符指向与客户端的 TCP 连接。在讨论 `accept` 时，我们调用第一个参数是 `socket` 创建的监听 `socket`，然后作为 `bind` 和 `listen` 的第一个参数，并调用 `accept` 的返回值。区分这两个 `socket` 是重要的。服务器通常只创建一个监听 `socket`。内核为每个被接受的客户端连接创建一个连接 `socket`（即 TCP 三次握手完成）。当服务器完成任务时，连接 `socket` 被关闭。

此函数返回三个值：一个新 `socket` 描述符或错误、客户端的协议地址（通过 `cliaddr` 指针）以及该地址的大小（通过 `addr` 指针）。如果我们不需要返回客户端的协议地址，可以将 `cliaddr` 和 `addr` 设置为空。

图 1.9 显示了这些点。连接 `socket` 每次循环都会关闭，但监听 `socket` 在服务器的生命期间保持打开。我们看到 `accept` 的第二和第三参数为空，因为我们不需要客户端的身份。

## 示例：返回值参数

现在我们将展示如何通过修改图 1.9 的代码来处理 `accept` 的返回值参数，以打印客户端的 IP 地址和端口。我们在图 4.11 中展示。

### 声明

- 7-8 我们定义两个变量：`len`，这是一个返回值变量；以及 `cliaddr`，它将包含客户端的协议地址。

### Accept 连接和客户端地址

- 19-23 我们初始化 `len` 为 `socket` 结构的大小，并传递 `cliaddr` 结构和 `accept` 的第二、第三参数。我们调用 `inet_ntop`（第 3.7 节）将 `socket` 结构中的 32 位 IP 地址转换为点分化的 ASCII 字符串，并调用 `ntohs`（第 3.4 节）将 16 位端口号从网络字节序转换为字节序。

使用 `sock` 而不是 `inet_ntop` 会使服务器更具协议无关性，但这已经依赖 IPv4。我们在图 1.9 中展示该服务器的协议无关版本。

如果我们运行服务器并在同一台主机上连接客户端，连续连接两次服务器，客户端将得到如下输出：

```
solaris # inet_ntop 127.0.0.1
Wed Jan 17 15:42:35 1996
solaris # inet_ntop 206.62.226.33
Wed Jan 17 15:42:53 1996
```

我们首先指定服务器的 IP 地址 (`127.0.0.1`)，然后是自己的 IP 地址 (`206.62.226.33`)。这是对应的输出：

```c
#include <sys/socket.h>
#include <stdio.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <unistd.h>
#include <time.h>

int main(int argc, char **argv) {
    int listenfd, connfd;
    socklen_t len;
    struct sockaddr_in servaddr, cliaddr;
    char buff[MAXLINE];
    time_t ticks;

    listenfd = socket(AF_INET, SOCK_STREAM, 0);
    memset(&servaddr, 0, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_addr.s_addr = htonl(INADDR_ANY);
    servaddr.sin_port = htons(13);

    if (bind(listenfd, (struct sockaddr *)&servaddr, sizeof(servaddr)) < 0) {
        perror("bind");
    }
    listen(listenfd, 5);

    for (;;) {
        len = sizeof(cliaddr);
        connfd = accept(listenfd, (struct sockaddr *)&cliaddr, &len);
        if (connfd < 0) {
            perror("accept");
            continue;
        }
        printf("connection from %s, %d\n", inet_ntop(AF_INET, &cliaddr.sin_addr, buff, sizeof(buff)), ntohs(cliaddr.sin_port));
        ticks = time(NULL);
        printf("%s", ctime(&ticks));
        close(connfd);
    }
}
```

### 4.7 fork 和 exec 函数

在下一节描述编写并发服务器之前，我们必须描述 `fork` 函数。该函数是 Unix 中创建新进程的唯一方法。

```c
#include <unistd.h>
pid_t fork(void);
```

返回：子进程返回 0，返回子进程 PID，错误返回 -1
