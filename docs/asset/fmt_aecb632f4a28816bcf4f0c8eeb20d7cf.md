
107: `write(STDOUT_FILENO, buf, n);`

108:

109:

110: `// ...`

111: `}`

```
*(注：由于提供的原文代码块在第 70-111 行存在严重的行号错乱和内容重复，上述翻译主要基于逻辑结构进行了对齐，并保持了代码块的完整性。)*
```

# 16.5 使用 TCP/IP 网络

Socket 的主要用途是允许运行在不同机器上的应用程序进行通信。TCP/IP 协议 [Stevens, 1994] 是互联网上使用的协议。Linux 提供了一套清晰、健壮的 TCP/IP 实现，使其作为 TCP/IP 服务端和客户端。

目前的 TCP/IP 版本是 4 (`IPv4`)。互联网的快速增长显示了该版本的某些缺点，在写作期间，已经开始开发 TCP/IP 版本 6 (`IPv6`)。该版本经过仔细设计，允许从 `IPv4` 缓慢迁移，大多数 Internet 主机预计将逐渐转换到 `IPv6`。

`IPv4` 的 socket 接口与提出的 `IPv6` 接口略有不同。我们将仅介绍 `IPv4` socket；如果你需要开发 `IPv6` 应用程序，请记住本章的剩余内容可能并不完全适用，尽管概念是相同的。

## 16.5.1 字节序

TCP/IP 网络通常是异构的；包含了各种机器和架构。架构之间最常见的差异之一是存储数字的方式。

计算机数字由字节序列组成。例如，C 整数通常是 4 个字节。在内存中存储这 4 个字节有多种方法。大端序架构将最高字节存储在最低地址，其他字节按从最高位到最低位的顺序排列。小端序机器以完全相反的存储多字节值。

## 16.5.2 IPv4 体系

`IPv4` 连接是一个四元组，即 (`本地主机`, `本地端口`, `远程主机`, `远程端口`)。在建立连接之前，必须确定连接的每个部分。本地主机和远程主机都是 IP 地址。IP 地址是 32 位（4 字节）数字，在整个网络中是唯一的。通常，它们以 `aaa.bbb.ccc.ddd` 的形式写入，地址中的每个元素都是机器地址中某一个字节的十进制表示。地址中最左侧的数字对应于地址中的最高有效字节。这种 IP 地址格式被称为点分十进制表示。

由于机器需要运行多个并发的 TCP/IP 应用，因此 IP 号并无法为单台机器上的连接提供唯一标识。端口号是 16 位数字，用于唯一标识单个主机上连接的某个端点。IP 地址和端口号的组合标识了单个 TCP/IP 网络任意位置的连接端点（互联网就是一个单一 TCP/IP 网络）。两个连接端点构成一个 TCP 连接，因此两个 IP 地址/端口对可以唯一标识网络上的一个 TCP/IP 连接。

尽管端口号范围从 0 到 65,535，但 Linux 将其分为两类。保留端口编号从 0 到 1,024，仅允许以 root 身份运行的进程使用。这使得客户端程序信任运行在服务器上的程序不是由用户启动的木马。¹¹

## 16.5.3 IP Socket 地址

IP 地址存储在 `struct sockaddr_in` 结构体，其定义如下：

```c
#include <sys/socket.h>
#include <netinet/in.h>
struct sockaddr_in {
  short int            sin_family;    /* AF_INET */
  unsigned short int   sin_port;      /* 端口号 */
  struct in_addr       sin_addr;      /* IP 地址 */
};
```

> 10. 然而，它仍然可能是超级用户启动的木马。

## 16.5 使用 TCP/IP 的网络机器

第一个元素必须是 `AF_INET`，表示这是一个 IP 地址。下一个元素是网络字节序的端口号。最后一个元素是该 TCP 地址对应的机器 IP 号。存储在 `sin_addr` 中的 IP 号应被视为不透明类型，而不直接访问。

如果 `sin_port` 或 `sin_addr` 被填充为 0 字节（通常通过 `memset()` 实现），则表示“不关心”状态。服务器进程通常不关心本地连接使用何种 IP 地址，例如，它们愿意接受到机器拥有的任何地址的连接。然而，如果应用程序希望仅在单个接口上监听连接，它将指定该地址。

## 16.5.4 操作 IP 地址

应用程序通常需要在点分十进制表示法和 `struct in_addr` 的二进制表示之间转换 IP 地址。`inet_ntoa()` 获取一个二进制 IP 地址并返回一个指向包含点分十进制形式字符串的指针¹¹

```c
#include <netinet/in.h>
#include <arpa/inet.h>
char * inet_ntoa(struct in_addr address);
```

生成的字符串存储在内存的静态区域，并在下次调用 `inet_ntoa()` 时被销。

最初，`inet_addr()` 提供了反向操作，将点分十进制字符串转换为二进制 IP 地址。该函数有两个问题，因为它返回的是一个 `long` 类型。由于没有返回其他标准函数期望的结构体，迫使程序员进行丑陋的强制转换。此外，如果 `long` 是 32 位，程序将无法区分 -1（表示错误，例如地址格式不正确）和 255.255.255.255 的二进制表示。为了遗留应用程序，这里是 `inet_addr()` 的样子：

> 11. `ntoa` 是 network-to-ascii（网络转 ASCII）的助记忆。

## 第 16 章使用 Socket 网络

```c
#include <netinet/in.h>
#include <arpa/inet.h>
unsigned long inet_addr(const char * ddaddress);
```

该函数获取传入的字符串（应包含点分十进制 IP 地址）并将其转换为二进制 IP 地址。

新程序不应使用 `inet_addr()` 的块接口，而应该应该使用 `inet_aton()`。

```c
#include <netinet/in.h>
#include <arpa/inet.h>
int inet_aton(const char * ddaddress, struct in_addr * address);
```

此函数期望一个包含点分十进制 IP 地址的字符串，并在 `address` 指向的 `struct in_addr` 中填充该地址的二进制表示。与大多数库函数不同，`inet_aton()` 在发生错误时返回 0，转换成功时返回非 0。

## 16.5.5 使用主机名

尽管 32 位数字是计算机识别彼此非常合理的标识方法，但人们往往对处理数字字符串感到感。。为了允许人类使用字母名称而不是数字名称，TCP/IP 协议族包含一个用于转换主机和 IP 地址的分布式数据库。该数据库被称为域名系统（DNS），许多书籍对其进行了深入介绍 [Stevens, 1994][Albitz, 1996]。

DNS 提供了许多功能，但我们感兴趣的是它将主机名转换为 IP 地址的能力。尽管这看起来像是一对一的映射，但实际上是多对多的。

## 16.5 使用 TCP/IP 的网络机器

```c
#include <netinet/in.h>      /* 用于地址结构 *
#include <arpa/inet.h>       /* 用于 inet_ntoa() *
#include <stdio.h>
int main(int argc, char ** argv) {
    struct hostent *answer;
    struct in_addr address, **addrptr;
    char **next;
    if (argc != 2) {
        fprintf(stderr, "only a single argument is supported\n");
        return 1;
    }
    /* 如果参数看起来像一个 IP，则假设它是一个 IP * */
    if (inet_aton(argv[1], &address)) {
        answer = gethostbyaddr((char *) &address, sizeof(address),
            AF_INET);
    } else
        answer = gethostbyname(argv[1]);
    /* 主机名查找失败 :- * */
    if (!answer) {
        perror("error looking up host");
        return 1;
    }
    // ... (剩余逻辑)
    return 0;
}
```

这是该程序运行时的对应的输出：

```
$lookup ftp.netscape.com
Canonical hostname: ftp25.netscape.com
Aliases: ftp.netscape.com anonftp10.netscape.com
Addresses: 207.200.74.21
```

### 16.5.7 查找端口号

Internet 标准的一部分是由互联网数字分配机构（IANA）维护的一组已知端口号。常见的 Internet 协议（如 ftp、telnet 和 http）每个都分配了一个端口号。大多数服务器在分配的端口号上提供这些服务，这使得它们易于找到。某些服务器运行在备用端口号上，通常是为了允许单台机器提供多个服务。

Linux 系统包含 `/etc/services` 文件，该文件将协议映射到端口号。访问此文件的最常用方法是通过 `getservbyname()` 函数，该函数返回特定服务的信息。

```c
#include <netdb.h>
struct servent * getservbyname(const char * name, const char * protocol);
```

第一个参数 `name` 是应用程序需要信息的服务的名称。`protocol` 参数指定了将使用的协议。服务数据库包含了关于其他协议（特别是 UDP）的信息；指定协议允许该函数忽略其他协议的信息。协议通常是字符串 `"tcp"`，但也可以使用其他协议名称（如 `"udp"`）。

> 12. 有关 IANA 的信息请参阅 http://www.iana.org。

`getservbyname()` 返回一个指向结构体的指针，该结构体包含查询服务的信息。这些信息可能会被下一次调用 `getservbyname()` 覆盖，因此应用程序应该保存任何重要信息。以下是 `getservbyname()` 返回的信息：

```c
#include <netdb.h>
struct servent {
    char * s_name;      /* 服务名称 */
    char ** s_aliases;  /* 服务别名 */
    int s_port;         /* 端口号 */
    char * s_proto;     /* 使用的协议 */
}
```

每个服务可能关联有多个名称，但只有一个数字。`s_name` 列出服务的标准名称，`s_port` 包含该服务的已知端口号（网络字节序），`s_proto` 是服务的协议（如 `"tcp"`）。`s_aliases` 元素是一个指向服务别名的指针数组，并用 NULL 指针标记列表的结束。

如果函数失败，它将返回 NULL 并设置 `h_errno`。

这是一个示例程序，用于查找命令行中指定的 TCP 服务，并显示服务的标准名称、端口号以及所有的别名：

```c
#include <netdb.h>
#include <netinet/in.h>
#include <stdio.h>
/* 显示命令行中指定的服务的 TCP 端口号和任何别名 */
/* services.c - 查找服务的端口号 */
int main(int argc, char ** argv) {
    struct servent *service;
    char **ptr;
    if (argc != 2) {
        fprintf(stderr, "only a single argument is supported\n");
        return 1;
    }
    /* 在 /etc/services 中查找该服务，如果失败则给出错误信息 */
    service = getservbyname(argv[1], "tcp");
    if (!service) {
        perror("getservbyname failed");
        return 1;
    }
    printf("service: %s\n", service->s_name);
    printf("tcp port: %d\n", ntohs(service->s_port));
    /* 显示任何别名 */
    if (service->s_aliases) {
        printf("aliases:\n");
        for (ptr = service->s_aliases; ptr; ptr++)
            printf("%s\n", *ptr);
    }
    return 0;
}
```

以下是运行该程序的示例；注意它可以通过标准名称或别名来查找服务。

```
$ ./services http
service: http
tcp port: 80
$ ./services ftp
service: ftp
tcp port: 21
```

### 16.5.8 监听 TCP 连接

监听 TCP 连接与监听 Unix 域套连接几乎相同。唯一的区别在于协议。以下是监听 TCP 连接的示例：

```c
/* tcpserver.c - 用于 TCP 的服务器 */
#include <arpa/inet.h>
#include <netinet/in.h>
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <unistd.h>
int main(void) {
    struct sockaddr_in address;
    int sock, conn;
    size_t addrLen;
    if ((sock = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
        die("socket");
    }
    /* 允许短时间内重复运行该服务器 */
    i = 1;
    setsockopt(sock, SOL_SOCKET, SO_REUSEADDR, &i, sizeof(i));
    address.sin_family = AF_INET;
    address.sin_port = htons(1234);
    address.sin_addr.s_addr = INADDR_ANY;
    if (bind(sock, (struct sockaddr *)&address, sizeof(address)) < 0)
        die("bind");
    if (listen(sock, 5))
        die("listen");
    while ((conn = accept(sock, (struct sockaddr *)&address, &addrLen)) >= 0) {
        printf("getting data\n");
        // 获取数据逻辑
        printf("done\n");
        close(conn);
    }
    if (conn < 0)
        die("accept");
    close(sock);
    return 0;
}
void die(const char *msg) {
    perror(msg);
    exit(1);
}
```

绑定到套接字的 IP 地址指定了一个端口，而不是 IP 地址。这让内核自由使用它喜欢的本地 IP 地址。另一个需要解释的地方是这段代码序列：

```c
i = 1;
setsockopt(sock, SOL_SOCKET, SO_REUSEADDR, &i, sizeof(i));
```

Linux 的 TCP 实现与大多数 Unix 系统一样，限制了（本地主机，本地端口）组合可以重新使用的时间。设置此选项允许服务器在短时间内运行。这与 Unix 域服务器在调用 `bind()` 之前移除现有 socket 文件的原因相似。

`setsopt()` 允许你设置许多套接字和协议特定的选项。

> 13. 对于 TCP 端口，该组合在两分钟内不能再次使用。

```c
#include <sys/socket.h>
getsockopt(int sock, int level, int option, const void *valptr, int vallength);
```
