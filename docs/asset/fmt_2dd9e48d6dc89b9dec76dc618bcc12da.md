
# 图 8.14 TCP 和 UDP 套接字：可以指定目标地址吗？

Posix.1g 规定，在未连接的 UDP 套接字上未指定目标地址的输出操作应返回 `EOTCONN`，而不是 `EDESTADDRREQ`。

Solaris 2.5 允许对已连接的 UDP 套接字执行指定目标地址的 `sendto`。Posix.1g 规定返回 `EISCONN`。

图 8.15 总结了我们关于已连接 UDP 套接字的三个要点。

![](img/aeda3be9ee318bedd42850d461da0f28_235_0.png)

图 8.15 已连接的 UDP 套接字，指定对其端的 IP 地址和端口号。

应用程序进行连接，并指定对其端的 IP 地址和端口号。

# 第 8 章

## 基础 UDP 套接字

这些更改引入了新的 `connect` 调用，并将 `sendto` 和 `recvfrom` 的调用替换为 `write` 和 `read` 调用。该函数仍然是与无关的，因为它没有检查传递给 `connect` 的套接地址结构。我们的客户端主函数 8.7 保持不变。

如果我们在主机 `badi` 上运行此程序，指定主机 `solaris` 的 IP 地址（该主机未在我们的服务器端口 9877 上运行），我们将得到如下输出：

```text
badi $ udpcli 206.62.22.33
hello, world
read error: Connection refused
```

我们注意到的第一点是，在启动客户端进程时并没有收到错误。错误仅在我们向服务器发送数据报后才发生。正是发送这个数据报触发了来自服务器主机的 ICMP 错误。但当 TCP 客户端连接到一个指定的、未运行服务器进程的服务器主机时，`connect` 会返回错误，因为该调用将发送 TCP 三次握手的第一个数据包，而正是这个包触发了服务器 TCP 的 RST（第 4.3 节）。

图 8.18 显示了 `tcpcdump` 的输出。

```text
badi % tcpdump
badi.118 > solaris.9877: udp 13
1 0.0
2 0.000628 (0.0006) solaris > badi: icmp: solaris udp port 9877 unreachable
```

图 8.18 接收数据报并终止时的 `tcpdump` 输出。

我们从图 8.15 中看到，此 ICMP 错误被内核映射为错误 `ECONREUSED`，这与我们的 `err_sys` 函数输出的信息“Connection refused.”相对应。

遗憾的是，正如我们所示，并不是所有内核都会向连接的 UDP 套接字返回 ICMP 消息。通常，源自 Berkeley 的内核会返回错误，而 System V 内核则不会。例如，如果你在 Solaris 2.4 主机上运行客户端并连接到未运行我们服务器的 ICMP 端口，我们可以使用 `tcpcdump` 验证服务器主机返回了 ICMP 端口不可达（unreachable），但客户端的 `read` 调用永远不会返回。这个 bug 在 Solaris 2.5 中被修复。UnixWare 不返回错误，而 AI、Digital Unix、HP-X 和 Linux 则返回错误。

## 8.13 UDP 缺乏控制

我们现在检查 UDP 缺乏任何流量控制的影响。首先，我们修改 `dg_cli` 函数以发送固定数量的数据报。它不再从 `stdin` 输入返回。图 8.19 显示了新版本。该函数向服务器写入 2000 个 1400 字节的 UDP 数据报。

然后，我们修改服务器以接收数据报并统计接收的数量。该服务器不再向客户端回传数据报。图 8.20 显示了新的 `dg_echo` 函数。当我们用终端中断（SIGINT）终止服务器时，它会打印出：

```c
1 include "unp.h"
2 #define NDQ 2000    /* 要发送的数据报 */
3 #define DGLEN 1400   /* 每个数据报的长度 */
4
5 void
6 dg_cli(FILE *fp, int sockfd, const SA *pservaddr, socklen_t servlen)
7 {
8  int i;
9  char sendline[DGLEN];
9
10 for (i=0; i<NDQ; i++) {
11  send(sockfd, sendline, DGLEN, pservaddr, servlen);
12 }
13 }
```

图 8.19 `dg_cli` 函数，向服务器写入固定数量的数据报。

```c
1 include "unp.h"
2 static void
3 static int count;

4 void
5 dg_echo(int sockfd, SA *pservaddr, socklen_t clilen)
6 {
7  socklen_t len;
8  char msg[MAXLINE];
9
10 Signal(SIGINT);
11 for (;;) {
12  len = clilen;
13  recv(sockfd, msg, MAXLINE, 0, pservaddr, &len);
14  count++;
15 }
16 }
17 static void
18 recvfrom_int(int)
19 {
20  printf("received %d datagrams\n", count);
21 exit(0);
22 }
```

图 8.20 `dg_echo` 函数，接收数据报。

现在我们在主机 `badi` 上运行服务器，在端口 8036 上。我们在另一个主机运行客户端。此外，我们在服务器上运行 `netstat -s`，在此之前和之后统计数据告诉我们丢失了多少数据报。图 8.21 显示了服务器的输出。

```text
bsdi % netstat -s | tail
udp: 300 datagrams received
0 with incomplete header
0 with bad length field
0 with bad checksums
12 dropped to no socket
77725 broadcast/multicast datagrams dropped to no socket
1970 dropped to full socket buffers
593 delivered
70592 output
```

```text
bsdi % udps6
? start our server
we run the client here
received 82 datagrams
type out interrupt after client finished
bsdi % netstat -s | tail
udp: 82294 datagrams received
0 with incomplete header
0 with bad length field
0 with bad checksums
12 dropped to no socket
77725 broadcast/multicast datagrams dropped to no socket
3882 dropped to full socket buffers
675 delivered
70592 output
```

图 8.21 主机输出。

客户端发送了 200 个数据报，但服务器应用程序只收到了其中的 82 个，丢失率为 96%。服务器应用程序或客户端应用程序完全不知道这些数据报丢失了。正如我们所说的，UDP 没有流量控制，它是不可靠的。正如我们所示，UDP 发送端很容易覆盖接收端。

如果我们查看 `netstat`，服务器主机（而非服务器应用程序）接收的数据报总数为 1994（82294 - 80300）。有 6 个数据报从未被接口接收，可能是接口缓冲区满了，或者被发送主机丢弃。“由于套接字缓冲区满而丢弃（dropped to full socket buffers）”表示 UDP 已接收但由于接收套接字队列满而被丢弃的数据报数量。此值为 1912（3882 - 1970），加上应用程序输出的计数器（82），等于 `netstat` 统计的由于套接字缓冲区满而丢弃的数量是系统范围内的。无法确定哪些应用程序（例如 UDP 端口）受到了影响。

> 注意，在此特定主机上，所有接收 UDP 数据报的 97%（77725 + 80300）都是广播或组播数据报，这些数据报因为没有绑定到目标端口的应用程序而被丢弃。我们回到这个。

## 8.14 使用 UDP 确定传出接口

## 基础 UDP 套接字
