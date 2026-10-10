
`char *dst`              /* 字符串（输出） */

`socklen_t dst_len`       /* `dst` 缓冲区的长度 */

);

/* 出错时返回字符串或 `NULL`（设置 `errno`） */

```

`inet_pton`—将 IPv4 或 IPv6 字符串地址转换为二进制

```c

#include <arpa/inet.h>

int inet_pton(

      int domain,              /* `AF_INET` 或 `AF_INET6` */

      const char *src,         /* 字符串（输入） */

      void *dst                /* 二进制地址的缓冲区（输出） */

);

/* 成功时返回 1，字符串无效时返回 0，出错时返回 -1（设置 `errno`） */

```

调用 `inet_ntop` 时，`src` 指向二进制地址，对于 IPv4 是 32 位数字，对于 IPv6 是 16 字节数组。结果放置在 `dst` 指向的缓冲区中。有两个宏可用于确定 `dst` 的大小：IPv4 使用 `INET_ADDRSTRLEN`，IPv6 使用 `INET6_ADDRSTRLEN`。

对于 `inet_pton`，输入是点分或冒号表示法的字符串，二进制输出写入 `dst` 指向的位置，该位置必须足够大，因为没有长度参数。IPv4 地址需要 32 位，IPv6 需要 128 位（16 字节）。

这里有一个示例：

```c

static void cvt(void)

{

    char ipv6[16], ipv6str[INET6_ADDRSTRLEN], ipv4str[INET_ADDRSTRLEN];

    uint32_t ipv4;

    int r;

    ec_negl( r = inet_pton(AF_INET, "66.218.71.94", &ipv4) )

    if (r == 0)

        printf("Can't convert\n");

    else {

        ec_null( inet_ntop(AF_INET, &ipv4, ipv4str, sizeof(ipv4str)) )

        printf("%s\n", ipv4str);

    }

    ec_negl( r = inet_pton(AF_INET6,

        "FEDC:BA98:7654:3210:FEDC:BA98:7654:3210", &ipv6) )

    if (r == 0)

        printf("Can't convert\n");

    else {

        ec_null( inet_ntop(AF_INET6, &ipv6, ipv6str, sizeof(ipv6str)) )

        printf("%s\n", ipv6str);

    }

    return;

    EC_CLEANUP_BGN

        EC_FLUSH("cvt")

    EC_CLEANUP_END

}

```

调用该函数的输出：

```
66.218.71.94
fedc:ba98:7654:3210:fedc:ba98:7654:3210
```

## 8.10 高性能考量

我在 8.4.4 节中展示了一个 Web 服务器的示例，使用了 8.1.3 节中的多客户端方法。现在想象一下，我们的 Web 服务器正试图同时处理 1000 个客户端。或者 10,000 个。它能正常工作吗？

让我们列举一下我们简单示例中所谓的“C10K”（“10,000 个客户端”）问题可能有哪些：

- `select` 必须查看多达 10,001 个文件描述符。这可能超出了 `fd_set` 的容纳能力。即使它能容纳这个数量，`select` 处理所有描述符也会花费很长时间。
- 进程可以打开的文件描述符数量是有限制的，通常远小于 10,001。
- 为了提供良好的响应，我们希望启用多个进程或多个线程来处理所有工作，但对这些资源也有限制。

- 将数据从文件复制到套接字（进出进程内存）的过程非常耗时。对于 10,000 个客户端来说，这将是一个致命的问题。
- 服务器可能使用的许多其他内部表和资源开始耗尽空间，或运行速度大幅下降，或两者兼而有之。

因此，如你所见，这些问题变得相当严重。这就是为什么真正的 Web 服务器（或任何其他大容量服务器）是一个极其复杂的软件组件的原因之一。

如果你试图处理 10,000 个客户端，甚至只是 500 个，有一篇题为“C10K 问题”的精彩文章解释了该问题并综述了大多数可能的解决方案 [Keg2003]。

### 练习

- **8.1.** 修改 8.1.3 节中的多客户端示例，使其在计算机之间工作（`AF_INET`）。在一台计算机上运行服务器，在至少另一台计算机上运行客户端。

- **8.2.** 基于 [RFC1288] 中的信息，实现 `finger` 命令的简单版本，除了 `user@host` 参数外没有其他选项。使用连接套接字（`SOCK_STREAM`）。对于下一个练习，你可能需要一个选项来设置端口号。

- **8.3.** 同样基于 [RFC1288]，实现一个简单的 `finger` 服务器，但使用未占用的较高编号端口（例如 3079）代替标准端口 79。使用连接套接字。使用上一个练习中编写的 `finger` 命令测试你的服务器。如果你有一台可以玩的机器，请安装你的服务器在端口 79 上，并使用在另一台机器上运行的标准 `finger` 命令进行测试。

- **8.4.** 与练习 8.2 相同，但使用无连接套接字。

- **8.5.** 与练习 8.3 相同，但使用无连接套接字。

- **8.6.** 设计并尝试实现一个基于 RFC 2549 的简单通信示例，你可以在 [RFC] 中找到它。你可以将自己限制在协和式和第一类服务质量级别。

- **8.7.** 使用 Qt 等 GUI 工具包实现一个图形 Web 浏览器。警告：这真的很难！你可能希望将其作为一个学期长的团体项目来完成。提示：从处理嵌套表格的方法开始你的设计。如果你正确地处理了那部分，其他一切都是相对容易的。

- **8.8.** 实现 SMI，使用无连接套接字，而不是像我们在 8.5 节中做的那样使用连接套接字。运行一些像 7.15 节中的那样计时测试。

- **8.9.** 实现一个 Web 爬虫，它从某个 URL 开始，然后扫描在那里找到的内容以发现额外的 URL（例如，通过查找以 "href" 开头的字符串）。它将发现的 URL 添加到列表中，然后扫描它们，发现更多的 URL。当它找到了指定数量的 URL 或被中断时，它会停止。（显然，当它遇到错误时需要继续。）应该有一种方式显示结果——至少包括所有发现的 URL，以及它们是否被成功扫描（HTTP 状态码为 200）或没有，如果没有，原因是什么。你*必须*实现机器人排除协议（有关详细信息，请参见 www.robotstxt.org），以便你不爬取你被要求远离的页面。提供一个“唯一主机”选项，该选项仅爬取每个主机（URL 直到第一个斜杠的部分）一次，使用为该主机尝试的第一个 URL（例如，www.basepath.com/index.htm）。使用该选项，尝试找到一个起始 URL，使其产生最多成功扫描的唯一主机。（我以为从 www.yahoo.com 开始是个好主意，但我恰好只得到一个命中，因为那里的所有链接都是相对于 www.yahoo.com 的。）当你运行你的爬虫时，通过确保你不独占网络资源来善待他人。

- **8.10.** 扩展你在练习 5.14 中编写的程序，包括附录 A 中在本章解释的进程属性。

## 9 信号和计时器

### 9.1 信号基础

信号是事件已发生的通知，例如用户输入中断（通常是 Ctrl-c）、浮点异常或闹钟响起。通常，信号是异步地传递到进程或线程的，并且无论进程或线程正在做什么都会被打断。信号可能会立即终止进程，或者，按照预先安排，被指定捕获它的函数可能会执行。

#### 9.1.1 信号简介

为了展示程序如何处理信号，这里有一个简单的程序示例，该程序每三秒显示一个数字，但当发生中断信号时，它显示一条消息并终止：

```c

static void fcn(int signum)

{

    (void)write(STDOUT_FILENO, "Got signal\n", 11);

    _exit(EXIT_FAILURE);

}

int main(void)

{

    int i;

    struct sigaction act;

    memset(&act, 0, sizeof(act));

    act.sa_handler = fcn;

    ec_negl( sigaction(SIGINT, &act, NULL) );

    for ( i = 1; ; i++ ) {

        sleep(3);

        printf("%d\n", i);

    }

    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN:

    exit(EXIT_FAILURE);

EC_CLEANUP_END:

}

```

对 `sigaction` 的调用为 `SIGINT` 信号安装了一个信号处理函数。当我运行这个程序时，我在出现“2”之后输入了 Ctrl-c。这导致程序正在做的任何事（可能在睡眠，或在 `printf` 内部，或只是循环）被打断，并且立即调用函数 `fcn`。它显示一条消息并通过调用 `_exit` 终止程序。（有关为什么我没有使用 `exit` 的原因，参见 9.1.7 节。）

屏幕上的输出是：

```
1
2
Got signal
```

如果我没有安装信号处理程序，输入 Ctrl-c 会立即终止进程。从技术上讲，原因是 `SIGINT` 信号的默认动作是终止进程。

我也可以调用 `sigaction` 来安排忽略 `SIGINT` 信号：

```c

int main(void)

{

    int i;

    struct sigaction act;

    memset(&act, 0, sizeof(act));

    act.sa_handler = SIG_IGN;

    ec_negl( sigaction(SIGINT, &act, NULL) );

    for ( i = 1; ; i++ ) {

        sleep(3);

        printf("%d\n", i);

    }

    exit(EXIT_SUCCESS);

EC_CLEANUP_BGN:

    exit(EXIT_FAILURE);

EC_CLEANUP_END:

}
