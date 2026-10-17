
`50 sockfd = socket(AF_INET, SOCK_DGRAM, 0);`

`51 setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));`

`52`

`53 bind(&wildaddr, sizeof(wildaddr));`

```c
54 wildaddr.sin_family = AF_INET;
55 wildaddr.sin_addr = htonl(INADDR_ANY);
56 wildaddr.sin_port = htonl(SERV_PORT);
57 bind(sockfd, (SA *)&wildaddr, sizeof(wildaddr));
58 printf("%s\n", sock_ntop((SA *)&wildaddr));
```

```c
59 if ( pid == fork() ) { /* 子进程 */
60 mydg_echo(sockfd, SA *pcliaddr, SA *sa);
61     exit(0);    /* 永远执行 */
62 }
64 exit(0);
```

**图 22.17** 绑定所有地址的 UDP 服务器的最后部分。

所有客户端执行的函数 `mydg_echo` 如图 22.18 所示。

```c
66 mydg_echo(int sockfd, SA *pcliaddr, sock_len clilen, SA *myaddr)
67 {
68     int n;
69     char msg[MAXLINE];
70     sock_len len;
71
72     for (len = ; ; ) {
73         len = clilen;
74         n = recvfrom(sockfd, msg, MAXLINE, 0, pcliaddr, &len);
75         printf("%d, datagram from %s", getpid(),
76         sock_ntop(pcliaddr, len));
77         printf("%s\n", sock_ntop(myaddr, len));
78     }
79     sendto(sockfd, msg, n, 0, myaddr, len);
80 }
```

**图 22.18** `mydg_echo` 函数。

## 新参数

该函数的第四个参数是绑定到 `socket` 上的 IP 地址。此 `socket` 应该只接收发送该 IP 地址的数据报。如果该 IP 地址是通配符，则该 `socket` 应该接收未被绑定到相同端口的其他 `socket` 匹配的数据报。

## 读取数据报并回显回复

使用 `recvfrom` 读取数据报，并使用 `sendto` 将送回客户端。

## 高级 UDP Socket

此函数还会打印客户端的 IP 地址和绑定到 `socket` 上的 IP 地址。

现在我们在为 `hm0` 以太网接口建立别名地址后，在 Solaris 主机上运行此程序。该别名地址是 `10.0.0/24` 上的 `200` 号主机。

```bash
solaris % udpserv03
bound 127.0.0.1:9877
bound 10.0.0.200:9877
bound 10.0.0.255:9877
bound 192.168.1.20:9877
bound 192.168.1.255:9877
bound 0.0.0.0:9877
loopback interface
unicast address of hm0:1 interface
broadcast address of hm0:1 interface
unicast address of hm0 interface
broadcast address of hm0 interface
wildcard
```

我们可以使用 `netstat` 检查这些 `socket` 是否都绑定到了指定的 IP 地址和端口：

```bash
solaris % netstat -na | grep 9877
127.0.0.1:9877             Idle
10.0.0.200:9877            Idle
*.9877                      Idle
192.129.100.100:9877      Idle
*.9877                      Idle
*.9877                      Idle
```

我们应该注意，每个 `socket` 对应一个子进程的设计是为了简单起见，也可以采用其他设计。例如，为了减少进程数量，程序可以使用 `select` 亲自处理所有描述符，而不再调用 `fork`。这种设计的问题在于增加了代码复杂性。虽然对所有描述符使用 `select` 简单，但我们必须为每个描述符维护某种到其 IP 地址的映射（可能是一个结构体数组），以便在从 `socket` 读取数据报时能够打印目标 IP 地址。通常，使用单个进程处理一个操作或描述符，比让单个进程复用许多个操作或描述符要简单得多。

## 22.7 并发 UDP 服务器

大多数 UDP 服务器是迭代的：服务器等待客户端请求，读取请求，处理请求，发送回复，然后等待下一个客户端请求。当处理客户端请求耗时较长，就需要某种形式的并发。

“长时间”的定义是：在为当前客户端提供服务时，另一个客户端等待被认为过长的时间。例如，如果两个客户端在 10 毫秒内到达，而服务一个客户端平均需要 5 秒时钟时间，那么第二个客户端将等待大约 10 秒才能回复，而不是如果请求一到达就被处理时只需等待大约 5 秒。

对于 TCP，只需 `fork` 一个新子进程（或线程）即可。在 UDP 中，没有连接，因此服务器无法轻易区分客户端属于哪个 `socket`。但是，我们可以使用客户端的 IP 地址和端口来识别客户端。（注：原文此处存在大量OCR重复段落，已根据翻译原则进行去重处理。）

# 高级 UDP 套接字

用于接收数据报的接口。

```c
struct in6_pktinfo {
    struct in6_addr ip6_addr;      /* 源/目的 IPv6 地址 */
    int ip6_ifindex;               /* 发送/接收接口索引 */
};
```
