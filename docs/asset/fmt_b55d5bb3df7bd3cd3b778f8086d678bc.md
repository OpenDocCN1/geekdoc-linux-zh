
```c
struct sockaddr_un {

    uint8_t  sun_len;      /* AF_LOCAL */

    sa_family_t sun_family;

    char        sun_path[104]; /* 空终止路径名 */

}
```

> 图 14.1 Unix 域套接字地址结构：`sockaddr_un`。

早期的 BSD 版本将 `sun_path` 数组的大小定义为 108 字节，而不是图中所示 104 字节。Posix 只要求其大小至少为 100 字节。这些限制的原因可以追溯到 4.2BSD，它要求该结构适用于 128 字节的缓冲区（内核缓冲区）。`sun_path` 数组中的 `SUN_LEN` 宏必须以空字符终止。它接收一个指向 `sockaddr_un` 结构的指针并返回结构的长度，包括路径名中的空字节数。未指定的地址由空字符串作为路径名表示，值为零。这是 IPv4 `INADDR_ANY` 常量的 Unix 域等效值。

Posix 将 Unix 域协议称为“本地”IPC，以消除对 Unix 操作系统的依赖。历史常量 `AF_UNIX_ANY` 变为 `AF_LOCAL`。尽管如此，无论底层操作系统如何，我们仍然使用“Unix domain”这一术语，因为它已成为事实上的名称。此外，即使 Posix 尝试使这些与操作系统无关，套接字结构仍然保留了 `_un` 后缀！

### 示例：绑定 Unix 域套接字

图 14.2 中的程序创建一个 Unix 域套接字，将其绑定到一个路径名，然后调用 `getockname` 并打印该路径名。

```c
#include "unp.h"

int main(int argc, char **argv)

{

    int sockfd;

    sock_len_t len;

    if (argc != 2)

        err_quit("usage: %s bind <pathname>", argv[0]);

    sockfd = socket(AF_LOCAL, SOCK_STREAM, 0);

    unlink(argv[1]); /* 如果失败则忽略 */

    struct sockaddr_un addr1, addr2;

    bzero(&addr1, sizeof(addr1));

    addr1.sun_family = AF_LOCAL;

    strncpy(addr1.sun_path, argv[1], sizeof(addr1.sun_path) - 1);

    bind(sockfd, (struct sockaddr *)&addr1, SUN_LEN(&addr1));

    len = sizeof(addr2);

    getsockname(sockfd, (struct sockaddr *)&addr2, &len);

    printf("bind %s, returned len %d\n", addr2.sun_path, len);

    exit(0);

}
```

图 14.2 将路径名绑定到 Unix 域。

### 首先移除路径名

绑定套接字的是命令行参数。但如果路径名在文件系统中已，`bind` 将失败。因此，我们调用 `unlink` 删除路径名，以防它已经存在。如果不存在，`unlink` 返回一个错误，我们忽略它。

### bind 和 getsockname

我们使用 `strncpy` 拷贝命令行参数，以防止路径名过长导致结构溢出。由于我们将结构初始化为 0，然后减去 `sun_path` 的大小，我们知道路径名是空终止的。调用了 `bind`，我们使用宏 `SUN_LEN` 计算该函数的长度参数。然后我们调用 `getsockname` 获取已绑定的名称并打印它。

如果我们运行此程序，将得到以下结果：BSD/OS

```
bsdi = umask first print our umask value
0022 shells print pathname in octal
bsdi = unlink /tmp/foo.bar
bound name = /tmp/foo.bar, returned len 14
bsdi = ls -l /tmp/foo.bar
s-------rwx------ 1 root group /tmp/foo.bar
```

# Socket 函数

域族必须是 `AF_LOCAL`，且协议必须为 `0`。然而，类型可以是 `SOCK_STREAM` 或 `SOCK_DGRAM`。创建的两个套接字描述符作为 `sock[0]` 和 `sock[1]` 返回。

此函数返回描述符，且每个描述符都彼此连接。源自伯克利的实现方案通过执行与 `socket` 相同的的操作（见《TCP/IP》第 253–254 页）来实现它。

所创建的两个套接字是无名的；这意味着不涉及隐式的 `bind`。类型为 `SOCK_STREAM` 的 `socketpair` 结果被称为流管道（stream pipe）。它类似于普通的 Unix 管道（由 `pipe` 函数创建），但流管道是全双工的；两个描述符都可以进行读写。我们在图 1.7 中展示了创建的流管道示意。

Posix.1 不要求全双工管道。在 Sys4 返回两个全双工描述符，而源自伯克利的内核传统上返回两个半双工描述符（见《TCPV》图 17.31）。

在使用 Unix 域套接字时，`socket` 函数存在若干差异和限制。我们在适用场景下列出了 Posix.1 的要求，并指出目前所有实现都处于这一水平。

- 1. 默认文件访问权限为 `0777`（用户、组和其他用户均可读、写、执行），并由当前的 `umask` 修改。
- 2. 与 Unix 域套接字关联的路径名应该是绝对路径，而不是相对路径。避免后者的原因是其解析依赖于调用者的工作目录。也就是说，如果服务器绑定了相对路径，则客户端必须与服务器处于同一目录（或必须知道该目录），客户端才能成功连接或发送数据。

> Posix.1 规定，向 Unix 域套接字绑定相对路径会产生不可预测的结果。

- 3. 在 `connect` 调用中指定的路径名通常必须绑定到相同类型（流或数据报）的 Unix 域套接字。出现以下情况会发生错误：(a) 路径存在但不是套接字；(b) 路径存在且是套接字但没有关联套接字描述符；(c) 路径存在且是打开的套接字但类型错误（即 Unix 域流套接字无法连接到关联 Unix 域数据报套接字的路径，反之亦然）。
- 4. Unix 域套接字 `connect` 关联的权限测试与对路径进行仅写访问的权限相同。
- 5. Unix 域套接字与 TCP 套接字类似：它们为进程提供一个没有记录边界的字节流接口。
- 6. 如果对 Unix 域流套接字调用 `connect` 时发现监听套接字队列满（见第 4.5 节），将立即返回 `ECONREFUSED`。这与 TCP 不同：当套接字队列满时，TCP 监听器会忽略到达的 SYN 包，而 TCP 连接端会通过多次发送 SYN 包来重试。
- 7. Unix 域数据报套接字与 UDP 套接字类似：它们提供一种保留记录边界的不可靠数据报服务。
- 8. 与 UDP 套接字不同，在未绑定的 Unix 数据报套接字上发送数据报不会将其绑定到路径。（回想一下，在未绑定的 UDP 套接字上发送数据报会导致临时端口绑定到该套接字。）这意味着除非发送者已对其绑定路径，否则数据报将无法发送回复。同样，与 TCP 和 UDP 不同，调用 Unix 域数据报套接字不会将路径绑定到套接字。

# 14.5 Unix 域流客户端-服务器

我们回顾第 5 章中的 TCP 客户端-服务器，并将其改为 Unix 域套接字。图 14.3 显示了服务器，它是图 5.12 的修改版本，使用 Unix 域流协议代替了 TCP。

套接字地址的数据类型为 `sockaddr_un`。

- 10 `socket` 的第一个参数是 `AF_LOCAL`，用于创建 Unix 域套接字。
- 11 `socket` 的第一个参数是 `AF_LOCAL`，用于创建 Unix 域套接字。
- 12 `socket` 的第一个参数是 `AF_LOCAL`，用于创建 Unix 域套接字。
- 13 `socket` 的第一个参数是 `AF_LOCAL`，用于创建 Unix 域套接字。
- 14 `socket` 的第一个参数是 `AF_LOCAL`，用于创建 Unix 域套接字。
- 15 `socket` 的第一个参数是 `AF_LOCAL`，用于创建 Unix 域套接字。

（注：由于原文文本存在大量重复和乱码片段，此处已根据技术文档逻辑进行了重组翻译。）

# 传递描述符

> 图 14.6 是 Unix 域数据报协议回显客户端。它是图 8.7 的修改。

```
1 #include <unp.h> // unixdomain/undgcli01.c
2 int
3 main(int argc, char **argv)
4 (
5 int socketfd;
```
