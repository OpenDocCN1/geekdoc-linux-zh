
`err_quit("icmplen (%d) < 8", icmplen);`

图 28.41 处理接收到的 ICMP6 数据报，前半部分。

ICMP6 错误由我们的 `readable_v6` 函数处理，其前半部分如图 28.41 所示。ICMP6 的处理与图 28.12 和 28.24 中的代码类似。

我们 `readable_v6` 函数的后半部分如图 28.42 （第 785 页）。这段代码与图 28.40 类似：它检查 ICMP 错误的类型，检查导致错误的数据报是否为 UDP 数据报，然后构建 `icmpd_err` 结构并将其发送给客户端。

## 28.7节 ICMP 消息守护进程

```c
31  if (icmp6->icmp6_type == ICMP6_DST_UNREACH || //
32      icmp6->icmp6_type == ICMP6_PACKET_TOO_BIG || //
33      icmp6->icmp6_type == ICMP6_TIME_EXCEEDED) {
34          if (icmp6len < 8 + 8) {
35              err_out("icmp6len %d < 8 + 8", icmp6len);
37          hip6 = (struct ip6_hdr *) (buf + 8);
38          hlenlen2 = sizeof(struct ip6_hdr);
39          printf("%s, %d, next %d\n", hlen2);
40          inet_ntop(AF_INET6, &icmp6->src, srcstr, sizeof(srcstr));
41          inet_ntop(AF_INET6, &icmp6->dst, dststr, sizeof(dststr));
43          hip6->next_hdr;
44          if (hip6->next_hdr == IPPROTO_UDP) {
45              udp = (struct udphdr *) (buf + 8);
46              sport = udp->uh_port;
48          /* 查找客户端的 Unix 套接字，发送头部 */
49          for (i = 0; i <= max_i; i++) {
50              if (client[i].confffd >= 0 &&
51                  client[i].family == AF_INET6 &&
52                  client[i].port == sport) {
53                      bzero(dest, sizeof(dest));
54                      dest.sin6_family = AF_INET6;
55                      dest.sin6_len = sizeof(dest);
                  }
              }
          }}
59          memcpy(&dest.sin6_addr, &icmp6->dst, 
60                   sizeof(struct in6_addr));
61          icmp_err.type = icmp6->icmp6_type;
62          icmp_err.code = icmp6->icmp6_code;
63          icmp_err.len = sizeof(struct in6_addr);
64          memcpy(&icmp_err.dest, dest, sizeof(dest));
65
          /* 将类型转换为合理的错误值 */
66          icmp_err.errno = EHOSTUNREACH; /* 默认值 */
67          if (icmp6->icmp6_type == ICMP6_DST_UNREACH &&
68              icmp6->icmp6_code == ICMP6_NOPORT) {
69                  icmp_err.errno = ECONNREFUSED;
70              if (icmp6->icmp6_type == ICMP6_PACKET_TOO_BIG) {
71                      icmp_err.errno = EMSGSIZE;
72              }
73              write(client[i].confffd, &icmp_err, sizeof(icmp_err));
74          }
75      }
76      return errno;
```

图 28.42 处理接收到的 ICMP6 数据报，后半部分。

## 28.8 总结

原始套接字提供以下功能：

- 我们可以读取和写入 ICMP4，这是大多数操作系统都支持的。
- 我们可以读取和写入 ICMP6，这通常用于诊断目的。
- 我们可以读取和写入数据报，内核不会处理这些包。

两种常用的诊断工具 `ping` 和 `traceroute` 使用原始套接字，我们已经开发了它们的 IPv6 版本。

## 练习

- 2.1 如果我们不设置 `SO_BROADCAST` 选项，对于链路层广播的 `ping` 程序会发生什么？
- 2.2 对于图 28.40 所示，通过 Unix 域的 ICMP 错误在 `ping` 程序中会发生什么？
- 2.3 如果我们以广播地址运行 `ping` 程序，会发生什么？
- 2.4 对于多播组 `224.0.0.1`，会发生什么？

## 29 链路层访问

### 29.1 引言

为应用程序提供链路层访问是一项大多数操作系统操作系统提供了强大的功能：

- 允许以应用程序而不是内核的形式运行某些 RARP 守护程序，例如大多数 Unix 版本的 RARP 服务器。
- 结合网络接口进入混杂模式的能力，这允许 `tcpdump` 等程序观察本地线路上的所有包，而不仅仅是目标主机的包。这种能力在交换机网络中用有限，因为交换机只向端口传递流量（单播、多播或广播）。许多你可能认为交换机的设备实际上是，例如双速率 10/100Mbps 集机：一个端口用于 100Mbps 系统，另一个用于 10Mbps 系统。

Unix 下访问链路层的三种常用方法是 BSD 过滤器 `BPF`、S4 链路提供接口 `DLPI` 以及 Linux 的 `SOCK_PACKET` 接口。介绍了这三种方法，然后描述了 `libpcap`，这是一个公开的数据捕获库。该库适用于所有方法，使用该库使得我们的程序独立于具体的链路层访问。我们通过开发一个向域名服务器发送 DNS 查询（我们构建 UDP 数据报并写入原始套接字）并使用 `libpcap` 读取回复以判断域名服务器是否启用了 UDP 校验，来描述该库。

### 29.2 BSD 过滤器 `BPF`

4.4BSD 和许多其他 Berkeley 派实现都支持 BPF，即 BSD 过滤器。BPF 的实现描述在 TCPv2 的第 31 章。BPF 的历史、BPF 伪机器描述以及与 SunOS 4.1.x NIT 包过滤器的比较请参见 [McCanne and Jacobson 1993]。每个链路层驱动程序在发送数据包之前和接收到数据包之后都会调用 BPF，如图 29.1 所示。

图 29.1 使用 BPF 进行数据捕获。

虽然提供一个链路层的接入点来捕获所有包并不困难，但 BPF 的威力在于其过滤能力。每个打开 BPF 设备的应用程序都可以加载自己的过滤器，然后由 BPF 对每个包进行处理。虽然有些过滤器是简单的

```
tcp and port 80 and tcp[13:1] & 0x7 = 0
```
