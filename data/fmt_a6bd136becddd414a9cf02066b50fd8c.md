
`inet_ntop(AF_INET, &addr.sin_addr, str, sizeof(str)), ntohs(addr.sin_port));`

## 网络寻址工具

与数据和寻址工具一样，API 提供了访问命名服务的接口。这些服务包括域名服务（DNS）、协议等。本节描述了用于转换人类可读名称的调用。

## `getpeername()`

此例程获取连接的对端在 `sockfd` 通道另一端的绑定地址或名称。该调用将结果放置在 `buf` 中。`buf_len` 是 `buf` 中可用的字节数。如果太小，信息将被截断。这与使用 `accept()` 调用获得的信息相同。

### 原型

```c
#include <sys/socket.h>

int getpeername(int sockfd, struct sockaddr *addr,
                socklen_t *addr_len);
```

### 返回值

如果一切正常，则返回零。如果发生错误，可以在 `errno` 中找到原因。

## 参数

- `sockfd`：已连接的套接字通道。
- `addr`：持有地址结构的缓冲区。
- `addr_len`：`addr` 中可用的字节数。这是通过引用传递的（该调用会修改此字段）。

## 可能的错误

- `EBADF`：参数 `sockfd` 不是有效的描述符。
- `ENOTSOCK`：参数 `sockfd` 是一个文件，而不是套接字。
- `ENOTCONN`：套接字未连接。
- `ENOBUFS`：系统中没有足够的资源来执行该操作。
- `EFAULT`：`addr` 参数指向的内存不在进程地址空间的有效部分。

## 示例

```c
struct sockaddr_in addr;

int add_len = sizeof(addr);

if ( getpeername(client, &addr, &addr_len) != 0 )
    perror("getpeername() failed");

printf("%s:%d\n", inet_ntoa(addr.sin_addr),
       ntohs(addr.sin_port));
```

## `gethostname()`

获取本地主机的名称。该调用将结果放置在 `name` 参数中，最多为 `len` 字节。

## 原型

```c
#include <unistd.h>

int gethostname(char *name, size_t len);
```

## 返回值

如果一切正常，则返回零。如果发生错误，可以在 `errno` 中找到原因。

## 参数

- `name`：用于接受本地主机名称的缓冲区
- `len`：`name` 中可用的字节数

## 可能的错误

- `EINVAL`：`len` 为负值，或者对于 Linux/i386 上的 `gethostname()`，`len` 小于实际大小。
- `EFAULT`：`name` 是无效地址。

## 示例

```c
char name[50];

if ( gethostname(name, sizeof(name)) != 0 )
    perror("gethostname() failed");

printf("My host is: %s\n", name);
```

## `gethostbyname()`

搜索并将主机名转换为 IP 地址。名称可以是主机名或地址。如果是地址，该调用不会进行搜索；相反，它会在 `hostent` 结构的 `h_name` 和 `h_addr_list[0]` 字段中返回该地址。

如果主机名以句号结尾，该调用将名称视为不带缩写的绝对名称。否则，该调用将搜索本地子网名称。如果在环境中定义了 `HOSTALIASES`，该调用将搜索 `HOSTALIASES` 指向的文件。

## 原型

```c
#include <netdb.h>

struct hostent *gethostbyname(const char *name);
```

## 返回值

该调用返回指向 `struct hostent` 的指针；如果失败，返回值为 `NULL`。该结构列出了主机拥有的所有名称和地址。宏 `h_addr` 提供了向后兼容性。

```c
#define h_addr h_addr_list[0]

struct hostent {
    char  *h_name;       /* 主机的正式名称 */
    char **h_aliases;    /* 别名列表 */
    int    h_addrtype;   /* 主机地址类型 */
    int    h_length;     /* 地址长度 */
    char **h_addr_list;  /* 地址列表；第 0 个是主要的 */
};
```

## 参数

`name`：要搜索的主机名或 IP 地址

## 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `ENOTFOUND` | 指定的主机未知。 |
| `NO_ADDRESS, NO_DATA` | 请求的名称有效，但没有 IP 地址。 |
| `NO_RECOVERY` | 发生了不可恢复的名称服务器错误。 |
| `EAGAIN` | 权威名称服务器上发生临时错误。请稍后重试。 |

## 示例

```c
int i;

struct hostent *host;

host = gethostbyname("sunsite.unc.edu");

if (host != NULL)
{
    printf("Official name: %s\n", host->h_name);

    for (i = 0; host->h_aliases[i] != 0; i++)
        printf("  alias[%d]: %s\n", i,
               host->h_aliases[i]);

    printf("Address type=%d\n", host->h_addrtype);

    for (i = 0; i < host->h_length; i++)
        printf("Addr[%d]: %s\n", i,
               inet_ntoa(host->h_addr_list[i]));
}

else
    perror("sunsite.unc.edu");
```

## `getprotobyname()`

此函数读取 `/etc/protocol` 文件以获取与 `pname` 匹配协议。你可以使用此调用将诸如 `HTTP`、`FTP` 和 `Telnet` 等名称转换为它们的默认端口号。

### 原型

```c
#include <netdb.h>

struct protent *getprotobyname(const char *pname);
```

### 返回值

如果成功，该调用返回指向 `protent` 的指针（在本附录后面定义）。否则，返回 `NULL`。

```c
struct protent {
    char        *p_name;        /* 官方协议名称 */
    char        **p_aliases;    /* 别名列表 */
    int         p_proto;        /* 协议号 */
};
```

字段 `p_proto` 是协议号。

### 参数

- `pname`：协议名称。这可以是任何被识别的协议名称或别名。

### 可能的错误

- （未设置 `errno`）

### 示例

```c
#include <netdb.h>

...

int i;

struct protoent *proto = getprotobyname("http");

if (proto != NULL)
{
    printf("Official name: %s\n", proto->p_name);

    printf("Port#: %d\n", proto->p_proto);

    for (i = 0; proto->p_aliases[i] != 0; i++)
        printf("Alias[%d]: %s\n", i+1,
               proto->p_aliases[i]);
}

else
    perror("http");
```

## 套接字控制

在套接字打开期间，你可以配置它以各种方式运行。本节描述了 API 调用。

### `setsockopt( )`

更改套接字 `sd` 的行为。每个选项都有一个值（某些选项是只读或只写的）。你可以通过 `optval` 和 `optlen` 来设置每个选项。有关选项的完整列表，请参阅附录 A。

**原型**

```c
```
