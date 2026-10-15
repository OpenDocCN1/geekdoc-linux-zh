
```
solaris % datetimecpcpli 127.0.0.1
socket error: Protocol not supported
```

要找到有关此错误的更多信息，我们首先使用 `grep` 在 `<sys/errno.h>` 头文件中搜索字符串 `Protocol not supported`。

```
solaris % grep 'Protocol not supported' /usr/include/sys/errno.h
#define EPROTONOSUPPORT 120 /* Protocol not supported */
```

这是 `socket` 返回的错误。然后我们查看 `man` 手页：

```
aix % man socket
```

大多数 man 手页会在末尾以“Errors.”为形式的标题提供额外的、尽管很短的信息。

### 1.4
我们将第一个声明更改为如下：

```c
int sockfd, n, counter = 0;
```

我们将语句

```c
counter++;
```

作为 `while` 循环的第一条语句添加。最后，在终止之前执行

```c
printf("counter = %d\n", counter);
```

打印的值始终是 1。

### 1.5
我们声明了一个 `int i` 并将代码修改为：

```c
for (i = 0; i < strlen(buff); i++)
    Write(confd, &buff[i], 1);
```

结果取决于客户端和宿主服务器。如果客户端和服务器在同一主机上，计数器为正常值 1，这意味着尽管服务器执行了 26 次写入，数据也是通过单个 `read` 返回的。但某种客户端和服务器的组合可能会产生两个数据包，而另一种组合可能产生 26 个包。（我们在第 7.9 节对 Nagle 算法的讨论解释了其中的原因。）

这个示例的目的是重申 TCP 对数据有不同的处理方式，我们的应用程序必须准备好以流的形式读取数据，直到遇到数据流的结束。

# 第二章

- 2.1 访问 [http://www.iana.org/numbers.htm]( )，并找到名为“IP Version Number”（IP 版本号）的注册表。版本 0 被预留，1–3 未分配，版本 5 是互联网流协议（Internet Stream Protocol）。

- 2.2 所有 RFC 都可以通过电子邮件、匿名 FTP 或 Web 免费获取。起点是 [http://www.ietf.org](http://www.ietf.org)。目录 `ftp://rfc-editor.org/in-notes` 是 RFC 的一个位置。要开始，请获取 RFC 索引，通常是 `rfc-index.txt` 文件，它在 [http://www.rfc-editor.org/rfc-index.html](http://www.rfc-editor.org/rfc-index.html) 的 HTML 版本中可用。如果我们用某种形式搜索 RFC 索引（参见上一个练习），查找术语“Stream”，发现 RFC 1819 定义了互联网流协议版本 2。在查找可能由 IPv4 涵盖的信息时，应该搜索 RFC 索引。

- 2.3 使用 IPv4，这会生成一个 576 字节的 IP 数据报（20 字节的 IPv4 头部和 20 字节的 TCP），这是 IPv4 最小缓冲区大小。

- 2.4 在此示例中，服务器执行了主动关闭，而不是客户端。

- 2.5 令牌环上的主机无法发送数据超过 1,460 字节的数据包，因为收到的 MSS 是 1,460。以太网上的主机可以发送数据多达 4,960 字节的数据包，但它不会超过操作系统操作接口（以太网）的 MTU 以避免分片。TCP 不能超过另一端公布的 MSS，但它可以始终发送少于此的数据。

- 2.6 Assigned Numbers 页面上的“Protocol Numbers”（协议号）部分 ([http://www.iana.org/numbers.htm](http://www.iana.org/numbers.htm)) 显示 OSPF 的值为 89。

- 2.7 选择性确认（selective acknowledgment）仅表示选择性确认消息中所反映的覆盖的数据已接收。只有累积确认（cumulative acknowledgment）表示到累积确认消息中的序列号及其之前的数据已接收。在根据选择性确认从发送缓冲区释放数据时，系统可能只释放被确认的精确数据，而不释放选择性确认之前或之后的数据。

# 第三章

### 3.1
在 C 语言中，函数无法更改按值传递的参数的值。要让函数修改调用者传递的值，需要调用者传递一个指向要修改值的指针。

### 3.2
指针必须根据读取或写入的字节数进行增加，因为 C 语言不允许对 `void` 指针进行增加（因为编译器不知道它所指向的数据类型）。

# 第四章

### 4.1
查看以 `INADDR_` 开头的常量定义，除了 `INADDR_ANY`（全 0 位）和 `INADDR_NONE`（全 1 位）。例如，C 组播地址 `INADDR_MAX_LOCAL_GROUP` 的定义注释为“0xe00000ff with '224.0.0.255'”，这显然是主机字节序。

### 4.2
以下是调用 `connect` 之后添加的行：

```c
len = sizeof(cliaddr);
getsockname(sockfd, (struct sockaddr *)&cliaddr, &len);
printf("local addr: %s\n", inet_ntoa((struct sockaddr_in *)&cliaddr));
```

*注：根据标准 socket API 使用修正了 OCR 错误）*

我们的第一次 `write` 产生了 `SIGPIPE`。由于我们的信号处理程序返回，`write` 返回了错误 `EPIPE`。

### 4.3
当客户端发送时，服务器响应 `RST`。`RST` 终止了连接并防止了服务器端（主动关闭端）通过 `TIME_WAIT` 状态。

### 4.4
当客户端调用 `close` 时，服务器返回 `EINVAL`。

### 4.5
如果没有调用 `bind`，服务器返回错误。

# 第五章

### 5.1
假设服务器支持端系统模型（我们在第 8.8 节中描述），一切运行正常。也就是说，服务器将接受接收在最左侧数据链路上的入站 IP 数据报（在本例中为 TCP 段），尽管其目标 IP 地址是最右侧数据链路的地址。

### 5.2
初始的两秒睡眠是为了让日期服务器发送其回复并关闭其连接端。我们的第一次 `write` 向服务器发送了一个数据段，服务器以 `RST` 响应。注意，我们的 TCP 允许向已接收 `FIN` 的套接字写入数据。第二次睡眠让服务器的 `RST` 被接收，我们的 `write` 产生了 `SIGPIPE`。

# 选习练习解答

# 附录 E 917

```c
#include "unp.h"

void
sig_pipe(int signo)
{
    printf("SIGPIPE received\n");
    return;
}

int
main(int argc, char **argv)
{
    int sockfd;
    struct sockaddr_in servaddr;

    if (argc != 2)
        err_quit("usage <IPAddress>");

    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(13); /* 日时间服务器 */
    inet_pton(AF_INET, argv[1], &servaddr.sin_addr);

    Signal(SIGPIPE, (SA *)Connect(&servaddr, sizeof(servaddr)));

    sleep(2);
    Write(sockfd, "hello", 5);
    sleep(2);
    Write(sockfd, "world", 5);

    exit(0);
}
```

![](img/1cc56227d30f6730abd74fbc5905c5ff_940_0.png)

服务器 (206.168.112.96) 与客户端的连接。之后，我们在服务器上运行 `netstat`，看到本地 IP 地址是客户端 SYN 包中的目标 IP 地址，正如我们在 4.4 节提到的，这是 SYN 到达的数据链路层。

### 5.8
我们的客户端运行在一个小端序 Intel 系统上，值为 1 的 32 位整数的存储方式如图 E.2 所示。

| 00 | 00 | 00 | 01 |

|---|---|---|---|

| 地址: A+3 | A+2 | A+1 | A |

图 E.2 32 位整数 1 在小端序格式下的表示。
