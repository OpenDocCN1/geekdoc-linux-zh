
```c
if ((h = gethostbyname("www.yahoo.com")) == NULL) {
    if (h_errno == HOST_NOT_FOUND)
        printf("host not found\n");
    else
        printf("h_errno = %d\n", h_errno);
} else
    display_hostent(h);
}
```

我们调用该函数得到的输出如下：

```text
name: www.yahoo.akadns.net; type: 2; len: 4
www.yahoo.com
66.218.71.95
66.218.70.49
66.218.71.88
66.218.71.81
66.218.71.86
66.218.71.92
66.218.71.94
66.218.71.89
66.218.70.48
66.218.71.93
66.218.70.50
66.218.71.87
66.218.71.84
```

你可以将此输出与 8.2.6 节中显示的输出进行比较，在那一节中，我们通过调用 `getaddrinfo` 做了几乎相同的事情。

`gethostbyname` 的反向操作是 `gethostbyaddr`，它使用主机数据库（可能是 `DNS`）将 `IP` 地址转换为名称：

```text
gethostbyaddr—按地址查找主机
#include <netdb.h>

struct hostent *gethostbyaddr(
        const void *addr,           /* IP 地址 */
        size_t len,                /* 地址长度 */
        int family);                /* 协议族（在 SUS 中称为“类型”） */

/* 返回指向 hostent 的指针，出错时返回 NULL（设置 h_errno） */
```

下面是一个示例程序（`inet_addr` 在 8.2.3 节中介绍）：

```c
static void gethostbyaddr_ex(void)
{
    struct hostent *h;
    in_addr_t a;
    ec_neg1(a = inet_addr("66.218.71.94"));
    if ((h = gethostbyaddr(&a, sizeof(a), AF_INET)) == NULL) {
        if (h_errno == HOST_NOT_FOUND)
            printf("address not found\n");
        else
            printf("h_errno = %d\n", h_errno);
    } else
        display_hostent(h);

    return;

    EC_CLEANUP_BGN
    EC_FLUSH("gethostbyaddr_ex")
    EC_CLEANUP_END
}
```

输出如下：

```text
name: wl5.www.scd.yahoo.com; type: 2; len: 4
66.218.71.94
```

发生的情况是，当我们获取 `www.yahoo.com` 的 `IP` 地址时，`66.218.71.94` 在列表中，但当我们询问该 `IP` 的名称时，得到的是 `wl5.www.scd.yahoo.com`。这就是 `DNS` 的工作方式——显然 `Yahoo` 使用了很多服务器，当然，它必须如此。

`gethostbyaddr` 和 `gethostbyname` 一样过时。现代函数是 `getaddrinfo`（见 8.2.6 节）的对应函数，称为 `getnameinfo`：

```text
getnameinfo—获取名称信息
#include <sys/socket.h>
#include <netdb.h>

int getnameinfo(
     const struct sockaddr *sa,    /* 套接字地址 */
     socklen_t sa_len,            /* 套接字地址长度 */
     char *nodename,              /* 节点名称 */
     socklen_t nodelen,           /* 节点名称缓冲区长度 */
     char *servname,             /* 服务名称 */
     socklen_t servlen,          /* 服务名称缓冲区长度 */
     unsigned flags             /* 标志 */
);

/* 成功返回 0，出错返回错误码 */
```

`getnameinfo` 接受完整的套接字地址，而不仅仅是裸 `IP` 地址，因为它潜在地与许多不同的协议族配合工作。最重要的是，它支持 `IPv6` 地址，而 `gethostbyname` 不支持。答案返回到两个缓冲区中：长度为 `nodelen` 的 `nodename` 用于节点（或主机）名称，长度为 `servlen` 的 `servname` 用于服务名称。如果缓冲区指针为 `NULL` 或其长度为 0，你就不会获取到该信息。

与 `getaddrinfo` 类似，`getnameinfo` 返回的错误号不是 `errno` 代码，而是特殊的“`EAI`”代码，如果你愿意，可以对它们使用函数 `gai_strerror`（见 8.2.6 节）。或者，使用我们专门为这两个函数提供的 `ec_ai` 宏。

你可以按位或（`OR`）组合的各种标志控制 `getnameinfo` 的返回值：

| 标志 | 描述 |
| :--- | :--- |
| `NI_NOFQDN` | 对于本地主机，仅返回节点名称部分，而不是完全限定域名。 |
| `NI_NUMERICHOST` | 返回地址的数字形式（`IPv4` 为点分表示法，`IPv6` 为冒号表示法），而不是名称。 |
| `NI_NAMERQD` | 如果找不到主机名称，则返回错误。通常在这种情况下返回数字形式。 |
| `NI_NUMERICSERV` | 返回端口号（作为字符串），而不是服务名称。 |
| `NI_DGRAM` | 查找 `SOCK_DGRAM` (`UDP`) 服务。通常它查找 `SOCK_STREAM` (`TCP`) 服务。 |

下面是一个示例：

```c
static void getnameinfo_ex(void)
{
    struct sockaddr_in sa;
    char nodename[200], servname[200];
    sa.sin_family = AF_INET;
    sa.sin_port = htons(80);
    sa.sin_addr.s_addr = inet_addr("216.109.125.70");
    ec_ai(getnameinfo((struct sockaddr *)&sa, sizeof(sa), nodename,
        sizeof(nodename), servname, sizeof(servname), 0));
    printf("node: %s; service: %s\n", nodename, servname);
    return;

    EC_CLEANUP_BGN
    EC_FLUSH("getnameinfo_ex")
    EC_CLEANUP_END
}
```

输出如下：

```text
node: w17.www.dcn.yahoo.com; service: http
```

另一个需要讨论的面向主机的函数是：

```text
gethostid—获取本地主机的标识符
#include <unistd.h>

long gethostid(void);
/* 返回标识符（无错误返回） */
```

`gethostid` 看起来可能返回本地机器的 `IP`，但它并不一定这样做。它只需要返回一个唯一标识符，而即使这样做是否有效，可能也取决于是否在启动时设置了这样的标识符。我在此处记录它，只是为了避免你误以为它是有用的函数。

还有另一个函数，它与网络没有直接关联，但提供了识别系统的信息：

### `uname`—获取当前系统信息

```text
#include <sys/utsname.h>

int uname(
  struct utsname *info  /* 返回的信息 */
); /* 成功返回非负值，出错返回 -1（设置 errno） */
```

### `struct utsname`—`uname` 的结构体

```text
struct utsname {
  char sysname[];   /* 操作系统名称 */
  char nodename[];  /* 网络中的节点名称 */
  char release[];   /* 发行版编号（字符串形式） */
  char version[];   /* 版本号（字符串形式） */
  char machine[];   /* 硬件类型或计算机型号 */
};
```

不幸的是，`utsname` 结构体的任何成员都没有标准化，因此你不能用它们来控制应用程序的处理逻辑。例如，测试 `machine` 成员以查看是否运行在 `Intel` `CPU` 上会很方便；然而，运行在该 `CPU` 上的每个系统都会按其想要的方式格式化字符串，而且“`Intel`”或“`x86`”这个词甚至可能根本不存在。你可以做的是将这些字符串用于显示目的——也许用于标记性能测试输出。而且，自然，`uname` 系统调用是 `uname` 命令的核心，我们的版本（没有选项）如下：

```c
int main(void)
{
    struct utsname info;
    ec_neg1(uname(&info));
    printf("sysname = %s\n", info.sysname);
    printf("nodename = %s\n", info.nodename);
    printf("release = %s\n", info.release);
    printf("version = %s\n", info.version);
    printf("machine = %s\n", info.machine);
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

下面是我们在四个测试系统上运行此程序得到的输出$^9$；看看你能否发现其中的规律：

```text
sysname = SunOS
nodename = sol
release = 5.8
version = Generic_108529-13
machine = i86pc
```

```text
sysname = Darwin
nodename = Marc-Rockhinds-Computer.local.
release = 6.6
version = Darwin Kernel Version 6.6: Thu May  1 21:48:54 PDT 2003;
    root:xnu/xnu-344_34.obj-1/RELEASE_PPC
machine = Power Macintosh
```

```text
sysname = FreeBSD
nodename = bsd.MSHOME
release = 4.6-RELEASE
version = FreeBSD 4.6-RELEASE #0: Tue Jun
machine = i386
```

```text
sysname = Linux
nodename = suse2
release = 2.4.18-4GB
version = #1 Wed Mar 27 13:57:05 UTC 2002
machine = i686
```

## 8.8.2 网络函数

此类别中的函数用于获取本地机器可能连接到的网络信息。首先是三个类似主机函数（例如 `gethostent`）的函数，用于扫描网络：

### `setnetent`—开始扫描网络数据库

```c
#include <netdb.h>

void setnetent(
    int stayopen; /* 是否保持连接打开？ */
);
```

### `getnetent`—获取网络数据库条目

```c
#include <netdb.h>

struct netent *getnetent(void);
/* 返回指向 netent 的指针，或在结束时返回 NULL（未定义 errno） */
```

### `endnetent`—结束扫描网络数据库

```c
#include <netdb.h>

void endnetent(void);
```

### `struct netent`—用于网络数据库函数的结构体

```c
struct netent {
   char *n_name;        /* 正式网络名称 */
   char *n_aliases;     /* 替代网络名称数组 */
   int n_addrtype;      /* 地址族（而非类型） */
   uint32_t n_net;      /* 网络号 */
};
```

这是一个示例：

```c
static void netdb(void)
{
    struct netent *n;
    setnetent(true);
    while ((n = getnetent()) != NULL)
        display_netent(n);
    endnetent();
}

static void display_netent(struct netent *n)
{
    int i;
    printf("name: %s; type: %d; number: %lu\n", n->n_name, n->n_addrtype,
           (unsigned long)n->n_net);
    for (i = 0; n->n_aliases[i] != NULL; i++)
        printf("\t%s\n", n->n_aliases[i]);
}
```

输出如下：

```text
name: loopback; type: 2; number: 127
name: arpanet; type: 2; number: 10
arpa
```

几乎所有（如果不是全部的话）机器都有一个用于测试的回环网络。这台机器（运行 `Solaris` 系统）还拥有一个连接到它称之为“`arpanet`”（为了纪念其历史）的互联网网络的连接。请记住，显示的“`type`”实际上是地址族；事实证明，宏 `AF_INET` 定义为 2。

与主机数据库类似，也有用于通过网络号或名称查找条目的函数：

`getnetbyname`—按名称查找网络

```c
#include <netdb.h>

struct netent *getnetbyname(
          const char *name       /* 网络名称（需匹配 n_name 成员） */
);

/* 返回指向 netent 的指针，若未找到则返回 NULL（未定义 errno） */
```

`getnetbyaddr`—按网络号查找网络

```c
#include <netdb.h>

struct netent *getnetbyaddr(
        uint32_t net,           /* 网络号（需匹配 n_net 成员） */
        int type                /* 地址族（需匹配 n_addrtype 成员） */
);

/* 返回指向 netent 的指针，若未找到则返回 NULL（未定义 errno） */
```

### 8.8.3 协议函数

按照同样的模式，扫描协议数据库的函数如下：

`setprotoent`—开始扫描协议数据库

```c
#include <netdb.h>

void setprotoent(
       int stayopen          /* 是否保持连接打开？ */
);
```

`getprotoent`—获取协议数据库条目

```c
#include <netdb.h>

struct protoent *getprotoent(void);
/* 返回指向 protoent 的指针，或在结束时返回 NULL（未定义 errno） */
```

`endprotoent`—结束扫描协议数据库

```c
#include <netdb.h>

void endprotoent(void);
```

`struct protoent`—用于协议数据库函数的结构体

```c
struct protoent {
    char  *p_name;         /* 正式协议名称 */
    char **p_aliases;      /* 替代协议名称数组 */
    int   p_proto;         /* 协议号 */
};
```

在某些系统上，调用 `setsockopt` 或 `getsockopt` 时可以使用协议号作为协议级别，但这是非标准的。

如果你一直阅读到这里，示例代码应该显而易见：

```c
