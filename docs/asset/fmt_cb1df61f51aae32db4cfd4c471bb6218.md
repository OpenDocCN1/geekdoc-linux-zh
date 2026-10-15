
这让我们认为，可以在包含此文件之前使用 `#define FD_SIZE` 设置为较大的值，以增加描述符集的大小。遗憾的是，这通常不起作用。

为了看出问题所在，`TCP2` 的图 16.53 表明内核中声明了三个描述符集，并将内核的 `FD_SIZE` 作为上限。增加描述符集大小唯一方法是增加 `FD_SIZE` 的值然后重新编译内核。如果不重新编译内核，该值是不够的。

某些变体正在改变 `select` 的实现，允许进程将 `FD_SIZE` 定义为更大的默认值。`BSD/OS` 已经更改了内核实现以允许更大的描述符集，并提供了四个新宏来动态分配和操作这些描述符集。从可移植性的角度来看，使用大描述符集是有利的。

## 6.4 str_cli 函数（重温）

我们现在可以重写第 5.5 节中的 `str_cli` 函数，这次使用 `select`，这样一旦服务器进程终止我们就能收到通知。之前的版本的问题是，当套接字发生某些情况时，我们可能会阻塞在 `fgets` 调用上。我们的新版本改为阻塞在 `select` 调用上，等待![](img/aeda3be9ee318bedd42850d461da0f28_166_0.png)标准输入或套接字可读。图 6.8 显示了我们的 `select` 调用处理的各种条件。

![](img/aeda3be9ee318bedd42850d461da0f28_167_0.png)

对套接字处理了三种条件。

- 1. 如果对方 TCP 发送数据，套接字变为可读并返回大于 0 的值（即数据字节数）。
- 2. 如果对方 TCP 发送 FIN（对方进程终止），套接字变为可读并返回 0（文件结束符）。
- 3. 如果对方 TCP 发送 RST（对方主机崩溃并重启），套接字变为可读并返回 -1，且 `errno` 包含特定的错误代码。

图 6.9 显示了此新版本的源代码。

### 调用 select

我们只需要一个描述符集来检查可读性。该集合由 `FD_ZERO` 初始化，我们使用 `FD_SET` 开启两个位：对应于标准 I/O 文件指针 `fp` 的位和对应套接字 `sockfd` 的位。`fileno` 函数将标准 I/O 指针转换为对应的描述符。`select`（以及 `poll`）仅在计算出两个描述符的最大值后才工作。在调用写集指针和异常集指针之后的调用中，它们都是空指针。最后一个参数（时间限制）也是空指针，因为我们希望阻塞直到某些准备就绪。

### 处理可读套接字

如果从 `select` 返回时套接字是可读的，通过 `readline` 读取并由 `fputs` 输出。

## 第6 章

### 6.5 section

```c
#include "unp.h"

void
    str_cli(FILE *fp, int sockfd)
{
    int maxdpl;
    fd_set rset;
    char sendline[MAXLINE], recline[MAXLINE];
    FD_ZERO(&rset);
    for (;)
        FD_SET(fileno(fp), &rset);
        FD_SET(sockfd, &rset);
    maxdpl = max(fileno(fp), sockfd) + 1;
    select(maxdpl, &rset, NULL, NULL);
    if (FD_ISSET(sockfd, &rset)) { /* 套接字可读 */
        if (read(sockfd, recline, MAXLINE) == 0)
            err("str-cli: server terminated prematurely");
        fputs(recline, stdout);
    }
    if (FD_ISSET(fp, &rset)) { /* 输入可读 */
        if (fgets(sendline, MAXLINE, fp) == NULL)
            return;
        write(sockfd, sendline, strlen(sendline));
    }
}
```
