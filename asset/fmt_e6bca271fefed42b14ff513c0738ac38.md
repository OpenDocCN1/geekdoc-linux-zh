
```c
#include <unistd.h>
int
main(int argc, char **argv)
{
    int sockfd, n;
    char recline[MAXLINE + 1];
    struct sockaddr_in servaddr;
    if (argc != 2)
        err_quit("usage: a.out <IPAddress>");
    if ((sockfd = socket(AF_INET, SOCK_STREAM, 0)) < 0)
        err_sys("socket error");
    memset(&servaddr, 0, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    if (inet_pton(AF_INET, argv[1], &servaddr.sin_addr) <= 0)
        err_quit("inet_pton error for %s", argv[1]);
    if (connect(sockfd, (struct sockaddr *)&servaddr, sizeof(servaddr)) < 0)
        err_sys("connect error");
    while ((n = read(sockfd, recline, MAXLINE)) > 0) {
        recline[n] = 0; /* null terminate */
        if (fputs(recline, stdout) == EOF)
            err_sys("fputs error");
    }
    if (n < 0)
        err_sys("read error");
    exit(0);
}
```

这是我们在文中所有源代码中将采用的格式。每个非空行都有行号。左侧的文本描述了代码部分的注释以及结束行号，如短例所示。有时段落之前会有一个简短的、具有描述性的**粗体**标题，提供对所展示代码的总结陈述。

代码片段开头和结尾的水平线指定了源代码文件：在本例中，它是 `intro` 目录下的 `datetympcoli.c` 文件。由于文中所有示例的源代码都是免费提供的（见前言），这可以帮助你找到相应的源文件。在阅读过程中编译、特别是修改这些程序，是学习网络编程概念的极佳方法。

在全文中，我们将使用缩进和像这样的括号状注释来描述实现细节和历史点。

如果我们将程序编译为默认的 `.out` 文件并执行它，将得到以下结果：

```
solaris % a.out 206.168.112.96
Mon May 26 20:58:40 2003
```

每当我们显示交互式输入输出时，我们将用**粗体**显示你的输入，并像这样显示计算机输出。注释在右侧用*斜体*标记。我们始终会将系统名称作为 shell 提示符的一部分（本例中为 solaris），以显示是在哪个系统上运行命令。图 1.6 显示了运行书中大多数示例的系统。主机名通常也描述操作系统（OS）。

这个 27 行程序中有许多细节需要考虑。我们在这里简要提到它们，以防这是你第一次接触网络程序，并在文后部分对这些主题提供更多信息。

我们包含了自己的头文件 `unp.h`，我们将在 D.1 节中展示。该头文件包含了大多数网络程序所需的许多系统头文件，并定义了我们使用的各种常量（例如 `MAXLINE`）。

1 这是 `main` 函数定义以及命令行参数。我们在文中使用了美国标准协会（ANSI）C 编译器（也称为 ISO 编译器）编写了代码。

10-11 `socket` 函数创建一个 Internet (`AF_INET`) 流 (`SOCK_STREAM`) 套接字，这是 TCP 套接字的形象名称。该函数返回一个小的整数描述符，我们可以用它在后续所有的函数调用中标识套接字（例如随后的 `connect` 和 `read` 调用）。

该语句包含对 `socket` 函数的调用，将返回值赋值给名为 `sock` 的变量，然后测试该赋值结果是否小于 0。虽然我们可以将其拆分为两个 C 语句：

```
sockfd = socket(AF_INET, SOCK_STREAM, 0);
if (sockfd < 0)
```

但将这两行结合起来是一种常见的惯用法。根据 C 语言的优先级规则（小于运算符的优先级高于赋值运算符），函数调用和赋值外的括号是必须的。作为编码风格，作者始终在两个开启符号之间放置空格，作为视觉指示，表示比较的左侧也是一个赋值。（这种风格拷贝自 Minix 源代码 [Tanenbaum-1987]）。我们在程序稍后的 `while` 语句中使用了相同的风格。

我们将遇到很多“socket（套接字）”术语。首先，我们使用的 API 是 sockets API。在前面的段落中，我们提到了作为 sockets API 一部分的名为 `socket` 的函数。在前面的段落中，我们还提到了 TCP 套接字，它与 TCP 端点同义词。

如果 `socket` 调用失败，我们通过调用自己的 `err_sys` 函数来终止程序；它会打印我们的错误信息以及所发生系统错误的描述（例如，“Protocol not supported”就是来自 `socket` 的一个错误），并终止进程。该函数以及我们在文中其他几个以 `err-` 开头的函数，我们将在 D.3 节中描述。

我们通过服务器的 IP 地址和端口号来填充 Internet 套接字地址（一个名为 `servaddr()` 的 `sockaddr_in` 结构）。我们使用 `bzero` 将整个结构设置为 0，将地址族设置为 `AF_INET`，将端口号设置为 13（这是任何托管此服务的 TCP/IP 主机上白天服务器已知端口，如图 2.18 所示），并将 IP 地址设置为命令行参数指定的值（`argv[1]`）。该结构体中的 IP 地址和端口号字段必须符合特定格式：我们使用库 `htons("host to network")` 来转换二进制端口号，并调用库函数 `inet_pton("presentation to numeric")` 将 ASCII 格式的命令行参数（例如我们运行时时的 192.168.62.236）转换为正确的格式。

`bzero` 不是 ANSI 函数。它源自伯利网络代码。尽管如此，我们在全文中使用了它，而不是 ANSI 的 `memset` 函数，因为 `bzero`（只有两个参数）比 `memset`（有三个参数）更容易记忆。每个支持 sockets API 的厂商都提供了 `bzero`，如果没有，我们在我们的 `unp.h` 中提供了它的宏定义。

事实上，TCP 的顺序涉及到第一次打印中 `memset` 的第二个和第三个字节的交换。C 语言编译器无法捕获此错误，因为两个参数的类型相同。（实际上，第二个参数类型是相同的）。

## 读取并显示服务器回复

我们读取服务器的回复并使用标准 I/O 函数显示结果。在使用 TCP 时必须小心，因为它是一种没有边界的字节流协议。

退出程序。Unix 在程序终止时总是关闭所有打开的描述符，因此我们的 TCP 套接字现在关闭了。

正如我们所提到的，本书将对我们刚才描述的所有点进行更详细的介绍。

我们在图 1.5 中的程序依赖于 IPv4 协议。我们分配并初始化 `sockaddr_in` 结构，将该结构的族设置为 `AF_INET`，并将 `socket` 的第一个参数指定为 `AF_INET`。

要修改程序以便在 IPv6 下运行，我们必须更改代码。图 1.6 显示了一个可以在 IPv6 下运行的版本，更改部分用蓝色标出。
