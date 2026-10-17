
结果取决于客户端和服务器主机。如果客户端和服务器在同一主机上，`counter` 通常为 1，这意味着尽管服务器写入了 26 次，数据也是通过一次读取返回的。但客户端和服务器的某种组合可能会产生两个包，而另一种组合可能会产生 26 个包。（我们在第 7.9 节对 Nagel 算法的讨论解释了这一点。）此示例的目的是重申不同的 TCP 对数据的处理方式不同，我们的应用程序准备准备读取字节流直到遇到数据流结束。

## 第 2 章

### 2.1
访问 `http://www.iana.org/numbers.htm` 并找到名为“IP Version Number”的注册。版本 0 是保留的，版本 1–3 未分配，版本 5 是 Internet Stream Protocol。

### 2.2
所有 RFC 都可以通过电子邮件、匿名 FTP 或 Web 免费获取。起点是 `http://www.ietf.org`。目录 `ftp://ftp.rfc-editor.org/in-notes` 是 RFC 的一个位置。首先获取 RFC 索引，通常是 `filer-index.txt`，其 HTML 版本也位于 `http://www.rfc-editor.org/rfc-index.html`。如果我们用编辑器搜索 RFC 索引（参见上一个示例中的解答），查找术语“Stream”，我们发现 RFC 1819 定义了 Internet Stream Protocol 版本。每当查找可能被 RFC 覆盖的信息时，应搜索 RFC 索引。

### 2.3
使用 IPv4，这会生成一个 56 字节的数据报文（20 字节的 IPv4 头和 20 字节的 TCP 头），这是 IPv4 的最小重组缓冲区大小。

### 2.4
在此示例中，服务器执行主动关闭，而不是客户端。

### 2.5
令牌环上的主机无法发送超过 1,460 字节的数据包，因为它收到的 MSS 是 1460。以太网上的主机可以发送高达 4,096 字节的数据包，但它不会超过输出接口（以太网）的 MTU 以避免分片。TCP 不能超过另一端公布的 MSS，但它可以发送少于此量。

### 2.6
“Protocol Numbers”节的“Protocol Numbers”节（`http://www.iana.org/numbers.htm`）显示 26。

### 2.7
“Protocol Numbers”节的“Protocol Numbers”节（`http://www.iana.org/numbers.htm`）显示 26。

## 第 3 章

### 3.1
启动在服务器主机上的服务器进程创建一个监听 `socket` 并等待新连接请求的到达。

### 3.2
问题是 `fgets` 标志着它返回的数据结束（带有空字节）。

## 第 4 章

### 4.1
客户端将数据发送到服务器。

### 4.2
客户端将数据发送到服务器。

```c
len = sizeof(cliaddr);

accept(sockfd, (struct sockaddr *)&cliaddr, &len);

printf("local address: %s\n", inet_ntop(AF_INET, &((struct sockaddr_in *)&cliaddr)->sin_addr, buf, INET_ADDRSTRLEN));
```

## 第 5 章

### 5.6
图 E.1 显示了该程序。在 Solaris 下运行此程序会产生以下结果：

```
solaris % tsigpipe 192.168.1.10

SIGPIPE received

write error: Broken pipe
```

初始的二秒钟等待是为了让时间服务器发送回复并结束连接。我们的第一次 `write` 向服务器发送了一个数据段，服务器响应了 RST（因为时间服务器已经完全关闭了它的套字）。注意，我们的 TCP 允许我们向一个接收了 FIN 的套字写入。第二次 `sleep` 让服务器的 RST 被接收，我们的第二次 `write` 产生了 SIGPIPE。由于我们的信号处理函数返回了，`write` 返回 EPIPE 错误。

### 5.7
假设服务器主机支持弱端点系统模型（我们在第 8.8 节中描述过），一切都能正常工作。也就是说，服务器将接受从最左侧数据链路到达的 IP 数据报（在这种情况下它包含一个 TCP 段），即使目的 IP 地址是最右侧数据链路的地址。我们可以通过在我们的主机 `linux`（图 1.6）上运行服务器，并在我们的主机 `solaris` 上启动客户端来测试，为客户端指定服务器的另一个 IP 地址（20.168.11.96）。连接建立后，如果我们在服务器上运行 `netstat`，我们看到本地 IP 地址是客户端 SYN 报文的目的 IP 地址，而不是 SYN 到达时所在数据链路的 IP 地址（正如我们在第 4.4 节中提到的）。

## 图 E.1 生成 SIGPIPE。

```
tcpcliser/tsigpipe.c
1 #include
2     "unp.h"
2 void
3 sig_pipe(int signno)
4 (
5     printf("SIGPIPE received\n");
6     return;
7 )
8 int
9 main(int argc, char **argv)
10 {
11     int sockfd;
12     struct sockaddr_in servaddr;
13     if (argc != 2)
14         err_quit("usage: tcpcli <Address>");
15     sockfd = Socket(AF_INET, SOCK_STREAM, 0);
16     bzero(&servaddr, sizeof(servaddr));
17 servaddr.sin_family = AF_INET;
18 servaddr.sin_port = htons(13); /* 时间服务器 */
19 Inet_pton(AF_INET, argv[1], &servaddr.addr);
20 Signal(SIGPIPE, sig_pipe);
21 Connect(sockfd, (SA *) &servaddr, sizeof(servaddr));
22 sleep(2);
23 Write(sockfd, "hello", 5);
24 sleep(2);
25 Write(sockfd, "world", 5);
26 exit(0);
27 )
```
