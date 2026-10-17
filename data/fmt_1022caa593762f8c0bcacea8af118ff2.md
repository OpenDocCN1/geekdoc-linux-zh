
> 回想第 20.2 节：如果主机采用常见的弱端模型，目标 IP 地址可能与接收接口的 IP 地址不同。在所有情况下，我们都可以确定数据包的目标地址。确定接收接口需要 `IP_RCVIF` 或 `IPv6_PKINFO` 套接字选项。

之前我们在第 19.11 节通过 NTP 示例展示了绑定所有地址的示例。

图 20.15 是这种技术的第一部分，UDP 服务器绑定了所有单播地址、所有广播地址以及最后的通配符地址。

### get_ifi_info 获取接口信息

`get_ifi_info` 获取所有接口（包括别名）的 IPv4 地址。程序随后遍历返回的 `if_info` 结构。

### 创建 UDP 套接字并绑定单播地址

创建一个 UDP 套接字并将单播地址绑定到它上。我们也设置了 `SO_REUSEADDR` 套接字选项，因为我们要为所有 IP 地址绑定相同的端口（`SERVER_PORT`）。并不是所有实现都要求设置此选项。例如，后期的实现不需要该选项，允许绑定已绑定的端口：

```c
#include "unif.h"

void mydg_echo(int, struct sockaddr *, socklen_t, struct sockaddr *);

int
main(int argc, char *argv)
{
    int    sockfd;
    const int on = 1;
    pid_t pid;
    struct if_info *ifi, *ifhead;
    struct sockaddr_in *sa, *cliaddr, *waddr;

    for (ifi = get_info(AF_INET, NULL, NULL, &ifhead); ifi != NULL; ifi = ifi->ifi_next) {
        /* 绑定地址 */
        sockfd = socket(AF_INET, SOCK_DGRAM, 0);

        setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));

        sa = (struct sockaddr_in *)ifi->ifi_addr;
        sa->sin_family = AF_INET;
        sa->sin_port = htons(SERVER_PORT);
        bind(sockfd, (struct sockaddr *)sa, sizeof(*sa));

        printf("Forked %d\n", getpid());

        if ((pid = fork()) == 0) { /* 子进程 */
            myddg_echo(sockfd, (struct sockaddr *)cliaddr, sizeof(cliaddr), (struct sockaddr *)sa);
            exit(0);
        } /* 从不执行 */
    }
}
```

图 20.15 绑定所有地址的 UDP 服务器的第一部分。如果 (a) 绑定的新 IP 地址不是通配符，且 (b) 与已绑定到端口的所有 IP 地址都不同。

### fork 用于地址

派 出子进程并为子进程调用 `mydg_echo` 函数。该函数等待此套接字上到达任何数据包，并将其回给发送者。

图 20.16 显示了下一个 `main` 函数，它处理广播地址。

### 绑定广播地址

如果接口支持广播，则连接 UDP 套接字并将广播地址绑定到它上。我们允许绑定因 `EADDRINUSE` 错误失败，因为一个接口在同一子网上有多个地址（别名）。

## 第 20.6 节

### 绑定接口地址 555

```c
if (ifi->ifi_flags & IFF_BROADCAST)
    /* try to bind broadcast address */
    sockfd = socket(AF_INET, SOCK_DGRAM, 0);
    setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));

    sasa = (struct sockaddr_in *)ifi->brdaddr;
    sasa->sin_port = htons(SR_PORT);
    if (bind(sockfd, (SA *)sa, sizeof(*sa)) < 0)
        if (errno == EADDRINUSE)
            printf("ADDRINUSE: %s\n", setsockopt((SA *)sa, sizeof(*sa)));
        close(sockfd);
    else
        err_ays("bind error for %s, %s\n", (SA *)sa, sizeof(*sa));
    printf("bound %s\n", sa, sizeof(*sa));
    if ((pid = fork()) == 0)    { /* child */
        mydg_echo(sockfd, (SA *) &cliaddr, sizeof(cliaddr), (SA *)sa);
        exit(0);
    }
    else                        { /* never executed */
    }
```

图 20.16 绑定所有地址的第二个 UDP 服务器。

### fork 子进程

产生一个子进程，它会调用 `mydg_echo` 函数。

主函数的最后部分如图 20.17 所示。该代码绑定了通配符地址（wild card address），用于处理除已绑定的单播和广播地址以外的任何目标地址。此套接字应该接收到的数据报应该是指向限制广播地址（255.255.255.255）。

### 创建套接字并绑定通配符地址

创建一个套接字，设置 `SO_REUSEADDR` 套接字选项，并绑定通配符 IP 地址。产生一个子进程，该子进程调用 `mydg_echo` 函数。

### 主函数终止

主函数终止，所有产生的子进程继续执行。

所有子进程都会执行的 `mydg_echo` 函数如图 20.18 所示。

### 高级网络

```c
/* bind wildcard address */
sockfd = socket(AF_INET, SOCK_DGRAM, 0);
setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));
```

```c
memset(&wildaddr, 0, sizeof(wildaddr));
wildaddr.sin_family = AF_INET;
wildaddr.sin_addr = htonl(INADDR_ANY);
wildaddr.sin_port = htons(SERV_PORT);
bind(sockfd, (struct sockaddr *)&wildaddr, sizeof(wildaddr));
```

```c
if ((pid = fork()) == 0) { /* child */
  mydg_echo(sockfd, (SA *)cliaddr, sizeof(cliaddr), (SA *)sa);
  exit(0);
}
```

图 20.17 绑定所有地址的 UDP 服务器的最后部分。

```c
void mydg_echo(int sockfd, SA *cliaddr, socklen_t clilen, SA *myaddr) {
  int n;
  char mesg[MAXLINE];
  socklen_t len;
  for ( ; ; ; ) {
    len = clilen;
    n = recvfrom(sockfd, mesg, MAXLINE, 0, cliaddr, &len);
    printf("%d, datagram from %s\n", n, getpid());
    send_sock((struct sockaddr *)myaddr, len);
    printf("* %s\n", sa);
    sendto(sockfd, mesg, n, 0, myaddr, clilen);
  }
}
```

图 20.18 `mydg_echo` 函数。

该函数的第四个参数是绑定到套接字的 IP 地址。该套接字应该只接收指向该 IP 地址的数据报。如果 IP 地址是通配符，则该套接字应该只接收未被绑定到相同端口的其他套接字匹配的数据报。

### 读取数据报并回显

使用 `recvfrom()` 读取数据报，并通过 `sendto` 发回客户端。此函数会打印客户端的 IP 地址以及绑定到套接字的 IP 地址。

## 20.7
