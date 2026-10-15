
`socket` 函数创建一个 Internet (`AF_INET`) 流 (`SOCK_STREAM`) 套接字，这是 TCP 套接字的一种雅称。该函数返回一个较小的整数描述符，我们用它在后续所有的调用中标识套接字的一端（例如对 `connect` 和 `read` 的调用）。

```
socket = socket(AF_INET, SOCK_STREAM, 0);
if (socket < 0)
```

将这两行结合是一种常见的惯用法。函数和赋值周围的参数已经给出；C 语言优先级规定（小于运算符的优先级高于赋值运算符）。作为一种个人风格，作者始终在左括号之前放置一个空格，作为视觉上的指示，表示比较的一侧也是赋值。（作者首次在 Minix 源代码 [Tanbaum 1987] 中看到这种风格，并从那时一直沿用）。我们在有状态程序也使用了这种风格。

我们将遇到“socket”一词的许多不同用法。首先是编程接口，或 API，我们正在调用 sockets API。在前面的（文未完）

### 引言

如果 `socket` 调用失败，我们通过调用自定义的 `err_sys` 函数来终止程序。它打印错误信息以及对系统错误的描述（例如，“Protocol not supported”是 `socket` 的一个可能错误），并终止进程。这个函数以及其他几个以 `err_` 开头的函数在整个测试中被多次调用。我们将在 D.4 节中描述它们。

### 指定服务器的 IP 地址和端口

我们在地址结构（使用 `sockaddr_in` 结构即可）中填入服务器的 IP 地址和端口号。我们使用 `0 bzero` 设置整个结构，将地址族设置为 `AF_INET`，将端口号设置为 13（这是任何支持此项的 TCP/IP 主机上白天服务器的已知端口，如图 2.3 所示），并将 TCP/IP 地址设置为命令行参数 (`argv[1]`) 指定的值。该结构中的 IP 地址和端口号字段必须采用特定格式：我们使用库函数 `htons("host to network work")` 来转换二进制数，并使用库函数 `inet_pton("presentation to number")` 将 ASCII 格式的命令行参数（在我们运行此示例时为 206.0.226.35）转换为正确的格式。

```
bzero 不是 ANSI 函数。它源自伯克利网络代码。然而，我们在全文中使用它，而不是 ANSI 的 memset，因为与 memset（三个参数）相比，bzero（带有一个参数）更容易记忆。几乎每个支持 API 的供应商都提供了 bzero，如果没有，我们会在 unp.h 中提供它的宏定义。
```

事实上，在 TCN3 的第一次打印版中，有 10 处发生了将 `memset` 的第二个和第三个参数进行交换换的情况。C 编译器无法捕获这个错误，因为两个参数的类型相同。（实际上，第二个参数是 int，第三个参数是 size，通常也是 int；但所指定的数值 -13 和 16 对于正确的参数类型来说仍然没问题）。对 `memset` 的调用仍然有效，但没有指定要初始化的字节数为 0。程序仍然可以工作，因为只有 8 字节的 Internet 套接字地址结构被设置为0。尽管如此，这是一个错误，通过使用 `bzero` 可以避免这种错误，如果使用 C 原型，交换 `bzero` 的参数将始终被 C 编译器捕获。

这可能是你第一次遇到 `inet_pton` 函数。它适用于 IP 版本 6（我们在附录 A 中讨论过）。旧的代码使用 `inet_addr` 函数将 ASCII 点分十进制字符串转换为正确的格式，但该函数有许多 `inet_pton` 不具备备的局限性。如果你的系统（尚未）支持此函数，请不要担心；我们在 3.7 节中提供了一个实现方案。

### 与服务器建立连接

`connect` 函数应用于 TCP 套接字，与由该套接字地址结构所指向的服务器建立连接。

### 协议无关性

在 `unp.h` 头文件中定义 `SA` 为 `sockaddr`，这是一种通用的地址结构。每当 `socket` 函数需要地址结构指针时，该指针必须是 `sockaddr` 类型的。这是因为 `socket` 函数遵循 ANSI 标准，而在 1980 年代还没有空指针（void pointers）。

我们读取服务器的响应并使用标准 I/O 显示结果。在使用 TCP 时必须小心，因为它是一种没有边界的字节流协议。服务器的响应通常是一个 26 字节的字符串，其中 r 是 ASCII 回车，n 是 ASCII 换行。在字节流协议中，这 26 字节可以通过许多方式返回：一个包含 26 字节数据的单个分段，或者总计为 26 字节的其他组合。通常会返回一个包含所有 26 字节数据的单个分段，但对于更大的数据量我们无法这样假设。

其他技术可用。例如，`FTP`（文件传输协议）和 `SMTP`（简单邮件传输协议）使用 2 字节的序列（ASCII 回车后跟 ASCII 换行）来标记记录的结束。`RPC`（远程过程调用）和 `DNS`（域名系统）在在使用 TCP 时，会在每个发送的记录前面放置一个包含记录长度的二进制计数。重要的概念是 TCP 本身不提供记录标记：如果应用程序想要界定记录，它必须自己这样做，并且有几种常用方法。

退出程序。Unix 在进程终止时总是会关闭所有打开的描述符，因此我们的 TCP 套接字现在已关闭。

### 终止程序

我们在图 1.5 中的程序依赖于 IP 版本 4 (`IPv4`)。我们分配并初始化了一个 `sockaddr_in` 结构，将该结构的格式设置为 `AF_INET`，并将套接字的第一个地址指定为 `AF_INET`。

如果我们想修改程序以在 IP 版本 6 (`IPv6`) 下运行，必须更改代码。图 1.6 显示了一个在 IPv6 下运行的版本，其中更改部分用粗体字体突出显示。

# 引绪

## 第1章

```c
#include <stdio.h>
#include "unp.h"

int main(int argc, char **argv)
{
    int sock, fd, n;
    char recvline[MAXLINE + 1];
    struct sockaddr_in servaddr;

    if (argc != 2)
    {
        err_quit("usage: a.out <IPAddress>");
        err_sys("socket error");
    }

    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0)
    {
        err_sys("socket error");
    }

    memset(&servaddr, 0, sizeof(servaddr)); /* daytime server */
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(13);
    if (inet_pton(AF_INET, argv[1], &servaddr.sin_addr) <= 0)
    {
        err_quit("invalid address: %s", argv[1]);
    }

    if (connect(sock, (struct sockaddr *)&servaddr, sizeof(servaddr)) < 0)
    {
        err_sys("connect error");
    }

    while ((n = read(sock, recvline, MAXLINE)) > 0)
    {
        recvline[n] = 0; /* null terminate */
        if (fputs(recvline, stdout) == EOF)
            err_sys("fputs error");
    }

    if (n < 0)
    {
        err_sys("read error");
    }

    exit(0);
}
```

图 1.6 针对 IP 版本 6 的图 1。

虽然只改变了五行，但我们现在拥有的是另一个依赖协议的程序，它依赖于 IP 版本 6。最好让程序与协议无关。图 11.7 显示了使用 `getaddrinfo` 函数（由 `tcp_connect` 调用）实现的协议无关的客户端版本。

我们程序的另一个缺陷是，用户必须以点分进制数输入服务器地址（例如 IPv4 版本的 `206.222.35`）。人类处理名称比处理数字更有效（例如 `laptop.kohala.com` 或只需 `laptop`）。在第 9 章和第 11 章中，我们将讨论在主机地址与 IP 地址之间、服务名称与端口之间转换的函数。我们推迟了对这些函数的讨论，直到确切知道填充并检查的套接字结构体中包含什么。这避免了因另一组函数的细节而使网络编程的讨论变得复杂。

### 错误处理：封装函数
