
是可以有效的。这是因为 Rlogin 客户端只接受主机名（调用 `gethostname`），不接受点分十进制字符串。POSIX 规范允许但不要求这种行为，因此可移植应用程序不能依赖它。

`gethostbyname` 与我们描述的其他套接字函数不同，它在发生错误时不会设置 `errno`。相反，它会将全局整数 `h_errno` 设置为包含 `<netdb.h>` 后定义的以下常量之一：

- `HOST_NOT_FOUND`
- `TRY_AGAIN`
- `NO_RECOVERY`
- `NO_DATA`（等同于 `NO_ADDRESS`）

`NO_DATA` 错误意味着指定的名称有效，但它没有 A 记录。这种错误的例子是只有 MX 记录的主机名。大多数现代解析器解析 `hstrerror` 函数，该函数接受 `h_errno` 值作为唯一参数，并返回指向错误描述的 `const char *` 指针。我们在下一个示例中展示该函数返回的一些字符串示例。

## 示例

图 11.3 显示了一个简单的程序，它对任意数量的命令行参数调用 `gethostbyname` 并打印返回的所有信息。

# 第 11.3 节 gethostbyname 函数

```c
#include names/hostent.c
int
main(int argc, char **argv) {
    char *ptr, **pptr;
    char str[INET_ADDRSTRLEN];
    struct host *hptr;

    while (-argc > 0) {
        ptr = ++argv;
        if ((hptr = gethostbyname(ptr)) == NULL) {
            fprintf(err_msg("gethostbyname error for host: %s: %s\n", ptr, hstrerror(errno));
            continue;
        }
        printf("official hostname: %s\n", hptr->h_name);
        for (pptr = hptr->h_aliases; *pptr != NULL; pptr++)
            printf("alias: %s\n", pptr);
    }

    switch (hptr->h_addrtype) {
        case AF_INET:
            for (pptr = hptr->h_addr_list; *pptr != NULL; pptr++)
                printf("address: %s\n", pptr, inet_ntop(str, sizeof(str)));
            break;
        default:
            err_ret("unknown address type");
            break;
    }
    exit(0);
}
names/hostent.c
```

`gethostbyname` 为每个命令行参数被调用一次。

官方主机名之后跟着一个别名列表。

`ptr` 指向指向各个地址的指针数组。对于每个地址，我们调用 `inet_ntop` 并打印返回的字符串。

我们首先使用主机名 `aix` 运行程序，它仅有一个 IPv4 地址。

```
freebsd % host aix
official hostname: aix.unbook.com
address: 192.168.42.2
```

注意，官方主机名是 FDN（完全限定域名）。同样请注意，尽管此主机有一个 IPv6 地址，但返回的是 IPv4 地址。

接下来是一个具有多个 IPv4 地址的 Web 服务器。

```
freebsd % host cnn.com
official hostname: cnn.com
address: 64.236.16.20
address: 64.236.16.52
address: 64.236.16.84
address: 64.236.16.116
address: 64.236.24.4
address: 64.236.24.12
address: 64.236.24.20
address: 64.236.24.28
```

接下来是一个我们在 11.2 节中作为 CNAME 记录展示过的名称。

```
freebsd % host www
official hostname: linux.unbook.com
alias: www.unbook.com
address: 206.168.112.219
```

如所期的，主机名与我们的命令行参数不同。

为了查看 `gethostbyname` 函数返回的错误字符串，我们首先指定一个不存在的主机名，然后指定一个没有 MX 记录的名称。

```
freebsd % host nosuchname.invalid
gethostbyname for host: nosuchname.invalid: Unknown host
```

```
freebsd % host uunet.uu.net
gethostbyname for host: uunet.uu.net: No address associated with name
```

# 11.4 gethostbyaddr 函数

`gethostbyaddr` 函数接收一个二进制 IPv4 地址，并尝试查找与该地址对应的主机名。这是 `gethostbyname` 的反操作。

```c
#include <netdb.h>
struct hostent *gethostbyaddr(const char *addr, sock_t len, int family);
返回：如果 OK 则返回非空指针，出错时返回 NULL 并设置 h_errno
```

该函数返回一个指向 `hostent` 结构的指针，与我们在使用 `gethostbyname` 时描述的相同。该结构中感兴趣的字段通常是 `h_name`，即规范主机名。

`addr` 参数不是 `char*`，而是一个指向 `in_addr` 结构的指针，其中包含 IPv4 地址。`len` 是该结构的大小：IPv4 地址为 4。`family` 参数是 `AF_INET`。

从 DNS 的角度来看，`gethostbyaddr` 向域名服务器查询 `in-addr.arpa` 域中的 PTR 记录。

# 11.5 getservbyname 和 getservbyport 函数

服务像主机一样，通常也通过名称识别。如果我们在代码中通过名称而非端口号引用服务，且从名称到端口号的映射位于文件中（通常是 `/etc/services`），那么当端口号发生变化时，我们需要修改 `/etc/services` 文件中的一行，而不需要重新编译应用程序。下一个函数 `getservbyname` 根据名称查找服务。

分配给服务的端口号规范列表由 IANA 维护，位于 http://www.iana.org/assignments/port-numbers（第 2.9 节）。给定的 `/etc/services` 文件可能包含 IANA 分配的一个集。

```c
#include <netdb.h>
struct servent *getservbyname(const char *servname, const char *protname);
返回：如果 OK 则返回非空指针，出错返回 NULL
```

该函数返回一个指向以下结构的指针：

```c
struct servant {
    char *name;        /* 官方服务名 */
    char *aliases;      /* 别名列表 */
    int port;           /* 端口号，网络字节序 */
    char *proto;       /* 使用的协议 */
};
```

必须指定服务名。如果指定了协议（`protname` 为非空指针），必须有匹配的协议。某些互联网服务通过 TCP 或 UDP 提供（例如 DNS 和图 2.1 中的所有服务），而另一些仅支持单一协议（例如 FTP 需要 TCP）。如果没有指定 `protname` 且服务支持多种协议，则返回的端口号取决于实现。这通常没有影响，因为支持多种协议的服务经常使用相同的 TCP 和 UDP 端口。`servant` 结构中感兴趣的字段是 `port`。由于返回的端口号是网络字节序的，在将其存入套接地址时必须调用 `htons`。典型的用例如下：
