
`extern FILE *scrf;`

```c
/*
 * status - 打印连接状态信息
 *
*/
/*/ARGUSED*/
int status(SOCKET sfd, FILE *tfp, int c)
{
    struct sockaddr_in sin;
    int sinlen;
    printf(tfp, "\unconnected to %s", host);
    sinlen = sizeof(sin);
    if (getsockname(sfd, (struct sockaddr *)&sin, &sinlen) == 0)
        printf(tfp, "*local port %d", ntohs(sin.sin_port));
    sinlen = sizeof(sin);
    if (getpeername(sfd, (struct sockaddr *)&sin, &sinlen) == 0)
        printf(tfp, "*remote port %d", ntohs(sin.sin_port));
    (void) putc('\n', tfp);
if (doecho || sndbinary || recvbinary) {
    printf("options in effect: %s");
    if (doecho)
        printf(tfp, "remote_echo %s");
    if (sndbinary)
        printf(tfp, "send_binary %s");
    if (recvbinary)
        printf(tfp, "receive_binary %s");
    (void) putc('\n', tfp);
}
if (scrfp) {
    printf(tfp, "scripting to file %s*\n", name);
    return 0;
}
}
```

`status` 过程打印如远程主机名、连接情况以及生效选项列表的信息。为了实现这一点，它调用套接字函数 `gethostname` 获取本地协议端口号的信息，并调用 `getpeername` 获取远程协议端口号相对于本地主机的字节序的信息。它使用库函数 `ntohs` 将端口号从网络字节序转换为本地主机的字节序。最后，`status` 检查当前生效的选项。如果启用了远程回显或二进制传输，`status` 将打印这些选项的状态。

## 26.28 总结

我们的示例 TELNET 客户端使用三个有限状态机来解释从服务器或用户键盘到达的字符序列。每个进入的字符都会导致有限状态机的状态转换。当客户端执行转换时，它会调用实现与该转换关联的动作。

本章描述了构成示例客户端的三个有限状态机的动作过程。某些动作是显而易懂的，而另一些则是复杂的。将客户端软件组织为有限状态机的动作过程的主要缺点在于可读性。生成的代码可能难以理解，因为在不引用有限状态机的情况下，无法确定各个过程之间的关系。

## 深入学习

一系列 RFC 涉及 TELNET 选项的细节，并包含了示例代码处理的每个选项的协议标准。Postel 和 Reynolds [RFC 858] 讨论了允许选项（go-ahead），而 Postel 和 Reynolds [RFC 857] 讨论了字符回显。Postel 和 Reynolds [RFC 856] 描述了控制 8 位二进制传输的选项。最后，VanBokkel [RFC 1091] 讨论了终端类型选项以及相关的选项否定协商（subnegrogation）。

## 练习

- 26.1 某些终端类型支持多种仿真模式，使得单个终端可以拥有一组终端类型名称。阅读 RFC 1091。当客户端与服务器协商终端类型时，如何使用终端名称的列表？

# 将服务器从 UNIX 移植到 Windows

## 27.1 引言

本文中的示例代码从编写开始就是为从零开始构建 Windows 环境客户端/服务器软件的程序员提供概念的说明演示。许多程序员面临着更困难的挑战：将为其他操作系统开发的软件移植到 Windows。特别是由于许多客户端/服务器应用程序最初是为 UNIX 操作系统编写的，程序员经常被要求从 UNIX 移植服务器代码。

本章通过描述专业 UNIX 程序员构建构建程序时遵循的惯例和做法来促进移植工作。尽管这里描述的某些设施和技术在 Windows 中没有对应物，但理解为什么要使用它们将有助于程序员理解它们如何影响程序。

## 27.2 在后台运行

UNIX 允许进程在前台或*后台*（background）执行。理解这种差异的简单方法是想象用户正在向命令解释器输入命令。通常情况下，每个命令都在前台执行，这意味着解释器在命令执行时会等待。一旦命令完成，解释器会发出另一个提示并允许用户输入新命令。相比之下，在后台运行的程序不会在命令解释器之前结束。

## 27.5 工作目录

与 DOS 类似，UNIX 使用“目录”（directory）一术来指代文件系统的抽象，某些系统和应用程序称为“文件夹”（folder）。在 UNIX 中，每个执行进程都会被分配一个当前目录。进程可以通过调用 `chdir` 函数随时更改其当前目录。例如，要更改目录到 `/etc/server1`，程序执行执行：

```c
(void) chdir("/etc/server1");
```

当前目录的概念对于文件名最为重要。不以斜杠（`/`）开头的名字被解释为程序当前目录下的文件。因此，如果服务器的当前工作目录是 `/etc/server1`，创建一个名为 `x` 的文件，它将位于磁盘上的 `/etc/server1/x`。翻译到 Windows 环境时，用于 `chdir` 的文件名必须是有效的，且字符串常量中的反斜杠必须双写：

```c
(void) chdir("C:\\server1");
```

## 27.6 文件创建与 Umask

与 Windows 类似，UNIX 中的每个文件都有一个保护模式，规定了所有者和非所有者允许的访问权限。文件上的 UNIX 保护模式以九位的形式存储，每个 UNIX 进程都有一个 `umask`，它指定了系统为该进程创建的文件分配保护模式。`umask` 是一个整数，其低 9 位是有效的。每当创建一个文件时，系统都会通过对 `open` 调用指定的模式与进程 `umask` 的按位取反进行按位与运算，来计算出该文件的模式。例如，假设一个进程的 `umask` 为 `027`（八进制）。为了创建一个模式为 `0777`（所有人均可读、可写、可执行）的文件，系统通过计算 `0750`（`umask` 027 的取反）与 `0777`（请求的模式）的按位与运算，得到正确的文件模式。结果是，文件模式为 `0750`（所有者和文件所在组可读可执行，仅所有者可写，其他人无法访问）。

### 27.6 文件创建与 Umask

服务器经常执行限制文件创建模式的代码。服务器通常如下所示调用 `umask` 函数：

```c
(void) umask(027);
```

Windows 的 `_umask` 函数工作方式与 UNIX 的 `umask` 函数类似。然而，由于 Windows 没有关于组或其他用户的规定，因此只使用两种模式：只读或读写。相应的常量是：`_S_IREAD` 和 `_S_IWRITE`。

## 27.7 进程组

UNIX 有一种进程组抽象，允许一组进程被视为一个单元。通常，每个服务器都独立于其他进程运行，并调用 `setpgrp` 函数指定自己不属于任何进程组：

```c
(void) setpgrp(0, getpid());
```

在将服务器移植到 Windows 时，可以消除该调用。

## 27.8 标准 I/O 描述符

在 UNIX 中，许多库函数执行打开三个文件描述符以供 I/O 使用。这些描述符被称为标准输入、标准输出和标准错误，其值为 0、1 和 2。例如，用于打印错误信息的库函数 `error` 会直接写入标准错误描述符，而不会检查其是否已打开。为了避免问题，服务器即使不显式地将这三个描述符用于 I/O，也会打开它们。代码类似于以下：

```c
fd = open("/dev/null", O_RDWR); /* stdin */
(void) dup(fd);               /* stdout */
```

对 `open` 调用获取控制终端的描述符，对 `ioctl` 调用将进程从终端分离，而对 `close` 调用释放该描述符。

Windows 没有控制终端的概念。因此，Windows 服务器不需要检测自身以避免来自终端的信号。因此，在将 UNIX 服务器移植到 Windows 时，可以消除上述代码。
