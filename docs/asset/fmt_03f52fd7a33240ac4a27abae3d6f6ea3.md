
参数 `socket` 指定的 socket 连接到参数 `address` 指定的服务器 socket，其长度为 `address_len`。该 socket 必须是通过调用 `socket` 获取的有效文件描述符。

## 第 15 章

如果成功，`connect` 返回 0，如果出错则返回 -1。这次可能出现的错误包括：

| 错误码 | 描述 |
| :--- | :--- |
| `EBADF` | 向 socket 传递了无效的描述符。 |
| `EALREADY` | 该 socket 已经在进行连接中。 |
| `ETIMEDOUT` | 发生了连接超时。 |
| `ECONNREFUSED` | 服务器拒绝了请求的连接。 |

如果无法立即建立连接，`connect` 将阻塞一段未指定的时间。一旦这段时间过期，连接将被中止且 `connect` 将失败。然而，如果 `connect` 调用被一个已处理的信号中断，则 `connect` 调用将失败（并将 `errno` 设置为 `EINTR`）；连接不会被中止，而是以异步方式建立。

与 `accept` 类似，`connect` 的阻塞性质可以通过在描述符上设置 `O_NONBLOCK` 标志来改变。在这种情况下，如果无法立即建立连接，`connect` 将失败并将 `errno` 设置为 `EINPROGRESS`，连接将以异步方式建立。

虽然异步连接处理起来比较棘手，但你可以通过对 socket 文件描述符调用 `select` 来识别该 socket 是否已准备好写入。我们将在本章稍后部分介绍 `select`。

## 关闭 Socket

你可以通过调用 `close` 来终止服务器和客户端的 socket 连接，就像处理底层文件描述符一样。你应该始终在两端关闭 socket。对于服务器，你应该在 `read` 返回 0 时这样做，但如果 socket 有重传的数据、属于面向连接类型且设置了 `SOCK_LINGER` 选项，`close` 调用可能会阻塞。你将在本章稍后学习设置 socket。

## Socket 通信

现在我们已经介绍了与 socket 相关的基本系统调用，可以仔细查看示例程序。我们将尝试将它们转换为网络 socket 而不是文件。

文件系统的缺点是，除非用户使用绝对路径，否则它会在服务器的当前目录下创建。为了使其更有用，你需要在服务器和客户端之间约定的全局可访问目录（例如 `/tmp`）中创建它。对于网络 socket，你只需要选择一个未使用的端口号即可。

对于我们的示例，我们将选择端口号 9734。这是一个任意的选择，允许标准服务器（我们不能使用 1024 以下的端口号，因为它们被留给系统使用）。其他端口号及其提供的服务列在文件系统 `/etc/services` 中。当你编写基于 socket 的应用程序时，始终选择一个未在该文件中列出的端口号。

> 请注意，程序 `client2.c` 和 `server2.c` 中存在一个刻意的错误，我们将在 `client3.c` 和 `server3.c` 中修复它。请不要在你的程序中使用 `client2.c` 和 `server2.c` 中的代码。

## Socket

我们将在本地网络上运行客户端和服务器，但网络 socket 不仅在局域网上有用；任何带有互联网连接的机器（甚至是调制解调器拨号）都可以网络 socket 与他人通信。你可以在独立的 UNIX 计算机上使用基于网络的程序，因为 UNIX 计算机通常配置为使用仅包含自身的环回网络。为了说明之目的，我们将使用这个环回网络，它对于调试网络应用程序也很有用，因为它消除了任何外部网络问题。

环回网络由单台计算机组成，通常称为 `localhost`，标准 IP 地址为 `127.0.0.1`。这是本地机器。你会在网络主机文件 `/etc/hosts` 中找到它的地址，其中列有共享网络上其他主机的名称和地址。

计算机通信的每个网络都有与其相关的硬件接口。计算机在每个网络上可能有不同的网络名称，并且肯定会有不同的 IP 地址。例如，Neil 的机器有三个网络接口，因此有三个地址。这些记录在 `/etc/hosts` 中如下：

```
127.0.0.1               # Loopback
192.168.1.1         # Local, private Ethernet
158.15.2.X           tilde.demon.co.uk  # Modem dial-up
```

第一个是简单的环回网络，第二个是通过以太网适配器访问的局域网，第三个是连接到互联网服务提供商的调制解调器链路。你可以编写一个基于网络的程序与通过这些接口之一访问的服务器进行通信，而无需修改。

## 尝试——网络客户端

这是一个修改后的客户端程序 `client2.c`，用于通过环回网络连接到网络 socket。它包含一个关于硬件依赖的细微错误，我们将在本章稍后讨论。

1. 包含必要的头文件并设置变量。

```
#include <sys/types.h>
#include <sys/socket.h>
#include <stdio.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>

int main()
{
    int sockfd;
    int len;
    struct sockaddr_in address;
    int result;
    char ch = 'A';
}
```

2. 为客户端创建 socket。

```
sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

3. 按约定的族类型命名 socket。

```
address.sin_family = AF_INET;
address.sin_addr.s_addr = inet_addr("127.0.0.1");
address.sin_port = htons(9734);
```

其余部分与 `client` 相同。当你运行它时，会失败：

```
$ client2
connect: connection refused
```

## 工作原理

`client` 使用 `sockaddr_in` 结构连接到 `127.0.0.1`。它使用 `inet_addr` 函数将 IP 的表示转换为相应的格式。

## 尝试——网络服务器

这是一个修改后的服务器程序 `server2.c`，通过环回网络接受连接。

1. 包含必要的头文件并设置变量。

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <stdio.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <unistd.h>

int main()
{
    int sockfd;
    int len;
    struct sockaddr_in address;
}
```

2. 为服务器创建 socket。

```
sockfd = socket(AF_INET, SOCK_STREAM, 0);
```

3. 将 socket 绑定到端口。

```
address.sin_family = AF_INET;
address.sin_addr.s_addr = INADDR_ANY;
address.sin_port = htons(9734);
bind(sockfd, (struct sockaddr *)&address, sizeof(address));
```

4. 监听连接。

```
listen(sockfd, 5);
```

5. 接受连接。

```
len = accept(sockfd, (struct sockaddr *)&address, (socklen_t *)&len);
```

服务器有一个错误：它在调用 `accept()` 之前没有初始化 `len`。为了修复这个问题，在调用 `accept()` 之前设置 `len = sizeof(address);`。

## 主机与网络

当我在计算机上运行这些版本的服务器和客户端（一台基于 Intel 的 Linux 机器），我可以使用 `netstat` 命令查看网络连接。

```
$ server2 &
$ client2 &
$ netstat
Active Internet connections
Proto Recv-Q Send-Q Local Address Foreign Address (State)
tcp        0 0 127.0.0.1:9734        127.0.0.1  ESTABLISHED
```

如果你尝试书中其他的示例，请确保终止服务器，因为它们会竞争连接，你会看到混乱的结果。你可以使用以下命令杀死它们：
`killall server1 server2 server3 server4 server5`

## 第 15 章

为了让不同类型的计算机能够对网络上传输的多字节整数的值达成一致，你需要定义一种网络字节序。客户端和服务器程序必须在传输之前将它们的内部表示转换为网络字节序。它们通过使用 `netinet/inet.h` 中定义的函数来实现。

这些函数是：

```
#include <netinet/inet.h>

unsigned long int htonl(unsigned long hostlong);
unsigned short htons(unsigned short hostport);
unsigned long int ntohl(unsigned long netlong);
unsigned short int ntohs(unsigned short netshort);
```

这些函数在原生主机格式和标准网络字节序之间转换 16 位和 32 位整数。它们的名称是转换操作的缩写——例如，“主机到网络” (`htonl`) 和“主机到网络，短型” (`htons`)。对于原生字节序与网络字节序相同的计算机，这些函数表示的是空操作。

为了确保 16 位端口号的字节序齐正确，你的服务器和客户端需要对端口应用这些函数。对 `server3.c` 的修改如下：

```
server_address.sin_addr.s_addr = htonl(INADDR_ANY);
server_address.sin_port = htons(9734);
```

你不需要转换函数调用 `inet_addr("127.0.0.1")`，因为 `inet_addr` 被定义为产生网络字节序的结果。对 `client3.c` 的修改为：

```
address.sin_port = htons(9734);
```

服务器也通过使用 `INADDR_ANY` 被修改为允许来自任何 IP 地址的连接。
现在，当你运行 `server3` 和 `client3` 时，你会看到本地连接所使用的正确端口。

```
$ netstat
Active Internet Connections
Proto Recv-Q Send-Q Local Address Foreign Address (State) User
tcp 1 0 localhost:9734 localhost:1175 TIME_WAIT root
```

记住，如果你使用的计算机具有相同的原生字节序和网络字节序，你将看不到任何区别。但始终使用转换函数仍然非常重要，以便允许与不同架构计算机上的客户端和服务器进行正确操作。

# 网络信息

到目前为止，你的客户端和服务器程序已经将地址和端口号编译到了程序中。对于更通用的服务器和客户端程序，你可以使用网络信息函数来确定要使用的地址和端口。

# 套接字

如果你有权限这样做，可以将你的服务器添加到 `/etc/services` 的已知服务列表中，这会为端口号分配一个名称，客户端可以使用符号化服务而不是数字。

同样，给定计算机的名称，你可以通过调用解析地址的主机数据库函数来确定 IP 地址。你通过查阅网络配置文件（如 `/etc/hosts`）或网络信息服务（如 NIS（网络信息服务，以前称为黄页）和 DNS（域名系统））来来实现。

主机数据库函数在接口头文件 `netdb.h` 中声明。

```
#include <netdb.h>

struct hostent *gethostbyaddr(const void *addr, size_t len, int type);
struct hostent *gethostbyname(const char *name);
```

这些函数返回的结构体必须包含这些成员：

```
struct hostent {
  char *h_name;          /* 主机名称 */
  char **h_aliases;      /* 别名列表（昵称） */
  int h_addrtype;        /* 地址类型 */
  int h_length;          /* 地址的字节长度 */
  char **h_addr_list;    /* 地址列表（网络字节序） */
};
```

如果指定的主机或地址没有数据库条目，信息函数将返回一个空指针。

同样，有关服务和相关端口号的信息可以通过某些服务函数获取。

```
#include <netdb.h>

struct server *getservbyname(const char *name, const char *proto);
struct server *getservbyport(int port, const char *proto);
```

`proto` 参数指定用于连接到服务的协议，对于 `SOCK_STREAM` TCP 连接使用 `"tcp"`，或者对于 `SOCK_DGRAM` UDP 数据报使用 `"udp"`。

`server` 结构体包含这些成员：

```
struct server {
  char *s_name;          /* 服务名称 */
  char **s_aliases;      /* 别名列表（备用名称） */
  int s_port;            /* IP 端口号 */
  char *s_proto;         /* 服务类型，通常为 "tcp" 或 "udp" */
};
```

你可以通过调用 `gethostbyname` 并打印结果获取关于计算机的主机数据库信息。注意，地址列表需要转换为适当的地址类型，并使用 `inet_ntoa` 转换从网络序转换为可打印字符串，其定义如下：

```
#include <arpa/inet.h>

char *inet_ntoa(struct in_addr in)
```

该函数将 Internet 主机地址转换为点分四位格式的字符串。在出错时返回 -1，但 POSIX 没有定义任何错误。你使用的另一个新函数是 `gethostname`。

```
#include <unistd.h>

int gethostname(char *name, int namlength);
```

此函数将当前主机的名称写入由 `name` 给出的字符串。主机名将以空字符终止。参数 `namlength` 表示字符串的长度，如果主机名太长，它将被截断。

## 第 15 章

## 网络信息

此程序 `getname.c` 获取主机的信息。它调用 `gethostname` 来查找主机名，并打印主机名、别名以及它可能拥有的 IP 地址。

1. 使用通常的包含文件和声明。

```c
#include <arpa/inet.h>
#include <stdio.h>
#include <netdb.h>
#include <stdio.h>
#include <unistd.h>

int main(int argc, char *argv[])
{
    char *host;
    char myname[256];
    struct hostent *hostinfo;
    struct **addrs;

    if (argc == 1)
        host = "localhost";
    else
        host = argv[1];
}
```

2. 将主机设置为参数，或者默认为 localhost。

```c
    gethostname(myname, 256);
    host = myname;
}
```

3. 调用 `gethostname`，如果没有找到则报告错误。

```c
    hostinfo = gethostbyname(host);
    if(!hostinfo) {
        fprintf(stderr, "cannot get host: %s\n", host);
        exit(1);
    }
}
```

4. 显示主机名和任何别名。

```c
    printf("results for host %s:\n", hostinfo->h_name);
    for (addrs = hostinfo->h_aliases; *addrs != NULL; addrs++) {
        printf("%s\n", *addrs);
    }
}
```

5. 如果不是 IP 主则警告。

```c
    if(hostinfo->h_addrtype != AF_INET) {
        fprintf(stderr, "not an host!\n");
        exit(1);
    }
}
```

6. 否则显示它使用的 IP 地址。

```c
    for (addrs = hostinfo->h_addr_list; *addrs != NULL; addrs++) {
        printf("* %s\n", inet_ntoa(*(struct in_addr *)addrs));
    }

    exit(0);
}
```
