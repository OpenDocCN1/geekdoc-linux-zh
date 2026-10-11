
## 原型

```c
#include <netinet/in.h>
unsigned short int ntohs(unsigned short int network_short);
unsigned long int ntohl(unsigned long int network_long);
```

## 返回值

转换后的值（16 位或 32 位）。

## 参数

| 参数 | 描述 |
| :------- | :------- |
| `network_short` | 要转换的 16 位值 |
| `network_long` | 要转换的 32 位值 |

## 可能的错误

（无）

## 示例

```c
struct sockaddr_in addr;
int client, addr_len=sizeof(addr);
client = accept(sockfd, &addr, &addr_len);
if ( client > 0 )
        printf("Connected %\ix%d\n", ntohl(addr.s_in_addr),
            ntohs(addr.s_in_port));
```

# inet_addr()

这是一个已弃用的工具，用于将数字、点分地址转换为网络字节序的二进制形式。如果失败，返回值（-1 或 255.255.255.255）仍然是一个合法的地址。`inet_aton()` 工具具有更好的错误处理机制。

## 原型

```c
#include <netinet/in.h>
unsigned long int inet_addr(const char *ip_address);
```

## 返回值

| 返回值 | 描述 |
| :------- | :------- |
| 非零 | 如果一切正常，值为转换后的 IP 地址。 |
| `INADDR_NONE`(-1) | 参数无效。（这是该调用的缺陷——没有负值，而 255.255.255.255 是通用广播地址。） |

## 参数

| 参数 | 描述 |
| :------- | :------- |
| `ip_address` | 人类可读的点分表示形式（例如，128.187.34.2） |

## 可能的错误

（不设置 errno）

## 示例

```c
if ( (addr.sin_addr.s_addr = inet_addr("128.187.34.2")) == -1 )
    perror("Couldn't convert address");
```

# inet_aton()

将人类可读的点分表示 IP 地址转换为二进制、网络字节序形式。此调用取代了 `inet_addr()`。

## 原型

```c
#include <netinet/in.h>
int inet_aton(const char* ip_addr, struct in_addr *addr);
```

## 返回值

如果一切正常，则返回非零值。如果发生错误，该调用返回零。

## 参数

- `ip_addr` IP 地址的 ASCII 字符串（例如，187.34.2.1）。
- `addr` 目标地址。通常，你会填充 `sockaddr_in` 结构中的 `sin_addr` 字段。

## 可能的错误

（不设置 errno）

## 示例

```c
struct sockaddr_in addr;
if ( inet_aton("187.43.32.1", &addr.sin_addr) == 0 )
    perror("inet_aton() failed");
```

# inet_ntoa()

此调用将网络字节序的二进制转换为人类可读的形式。注意，此调用使用静态内存区域；后续调用会覆盖较旧的结果。

## 原型

```c
#include <netinet/in.h>
const char* inet_ntoa(struct in_addr *addr);
```

## 返回值

地址在返回的字符串中。

## 参数

- `addr` 二进制地址（通常是 `sockaddr_in` 结构中的地址字段）

## 可能的错误

（不设置 errno）

## 示例

```c
clientfd = accept(serverfd, &addr, &addr_size);
if ( clientfd > 0 )
    printf("Connected %s:\n\n", inet_ntoa(addr.sin_addr));
```

# inet_pton()

将人类可读的 IPv4 或 IPv6 地址从点/冒号表示法转换为二进制、网络字节序形式。

## 原型

```c
#include <netinet/in.h>
int inet_pton(int domain, const char* prsnt, void *addr);
```

## 返回值

如果一切正常，则返回非零值。如果发生错误，该调用返回零。

## 参数

- **domain**：网络类型（AF_INET 或 AF_INET6）。
- **prsnt**：IP 地址的 ASCII 字符串（例如，187.34.2.1 或 FFFF::8090:A03:3245）。
- **addr**：目标地址。通常，你会填充 `sockaddr_in` 结构中的 `sin_addr` 字段或 `sockaddr_in6` 结构中的 `sin6_addr` 字段。

## 可能的错误

（不设置 errno）

## 示例

```c
struct sockaddr_in addr;
if ( inet_pton(AF_INET6, "187.43.32.1", &addr.sin6_addr) == 0 )
    perror("inet_pton() failed");
```

# inet_ntop()

此调用将网络字节序的二进制转换为人类可读的形式。与 `inet_ntoa` 不同，你需要提供给它一个临时字符串缓冲区。此函数支持 `AF_INET` 和 `AF_INET6`。

## 原型

```c
#include <arpa/inet.h>
char* inet_ntop(int domain, struct in_addr *addr, char* str, int len);
```

### 返回值

该调用返回参数 *str*。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| *domain* | 网络类型（*AF_INET* 或 *AF_INET6*） |
| *addr* | 二进制地址（通常是 *struct sockaddr_in* 中的地址字段） |
| *str* | 字符串缓冲区 |
| *len* | *str* 中可用的字节数 |

### 可能的错误

（不设置 *errno*）

### 示例

```c
char str[100];
clientfd = accept(serverfd, &addr, &addr_size);
if ( clientfd > 0 )
  printf("Connected %s:%d\n",
         inet_ntop(AF_INET, &addr.sin_addr, str, sizeof(str)),
         ntohs(addr.sin_port));
```

# 网络寻址工具

与数据和寻址工具一样，API 提供了访问命名服务的接口。这些服务包括域名服务（DNS）、协议等。本节描述了用于转换人类可读名称的调用。

## getpeername()

此例程获取连接的对端在 *sockfd* 通道另一端的绑定地址或名称。该调用将结果放置在 *buf* 中。*buf_len* 是 *buf* 中可用的字节数。如果太小，信息将被截断。这与使用 *accept*() 调用获得的信息相同。

### 原型

```c
#include <sys/socket.h>
int getpeername(int sockfd, struct sockaddr *addr,
                socklen_t *addr_len);
```

### 返回值

如果一切正常，则返回零。如果发生错误，可以在 *errno* 中找到原因。

## 参数

- **sockfd** 已连接的套接字通道。
- **addr** 持有地址结构的缓冲区。
- **addr_len** `addr` 中可用的字节数。这是通过引用传递的（该调用会修改此字段）。

## 可能的错误

- **EBADF** 参数 `sockfd` 不是有效的描述符。
- **ENOTSOCK** 参数 `sockfd` 是一个文件，而不是套接字。
- **ENOTCONN** 套接字未连接。
- **ENOBUFS** 系统中没有足够的资源来执行该操作。
- **EFAULT** `addr` 参数指向的内存不在进程地址空间的有效部分。

## 示例

```c
struct sockaddr_in addr;
int add_len = sizeof(addr);
if ( getpeername(client, &addr, &addr_len) != 0 )
    perror("getpeername() failed");
printf("%s:%d\n", inet_ntoa(addr.sin_addr),
       ntohs(addr.sin_port));
```

# gethostname()

获取本地主机的名称。该调用将结果放置在 `name` 参数中，最多为 `len` 字节。

## 原型

```c
#include <unistd.h>
int gethostname(char *name, size_t len);
```

## 返回值

如果一切正常，则返回零。如果发生错误，可以在 `errno` 中找到原因。

## 参数

- **name** 用于接受本地主机名称的缓冲区
- **len** `name` 中可用的字节数

## 可能的错误

- **EINVAL** `len` 为负值，或者对于 Linux/i386 上的 `gethostname()`，`len` 小于实际大小。
- **EFAULT** `name` 是无效地址。

## 示例

```c
char name[50];
if ( gethostname(name, sizeof(name)) != 0 )
    perror("gethostname() failed");
printf("My host is: %s\n", name);
```

# gethostbyname()

搜索并将主机名转换为 IP 地址。名称可以是主机名或地址。如果是地址，该调用不会进行搜索；相反，它会在 hostent 结构的 `h_name` 和 `h_addr_list[0]` 字段中返回该地址。

如果主机名以句号结尾，该调用将名称视为不带缩写的绝对名称。否则，该调用将搜索本地子网名称。如果在环境中定义了 HOSTALIASES，该调用将搜索 HOSTALIASES 指向的文件。

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

**name**
要搜索的主机名或 IP 地址

## 可能的错误

| 错误 | 描述 |
| :--- | :--- |
| `ENOTFOUND` | 指定的主机未知。 |
| `NO_ADDRESS, NO_DATA` | 请求的名称有效，但没有 IP 地址。 |
| `NO_RECOVERY` | 发生了不可恢复的名称服务器错误。 |
| `EAGAIN` | 权威名称服务器上发生临时错误。请稍后重试。 |

