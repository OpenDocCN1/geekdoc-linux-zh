
```c
PANIC( "Can't make socket input-only");
```

## 网络数据转换

在处理网络数据时，你必須考虑数据的字节序、地址转换等。`Socket API` 包括一个相当大的工具列表，可帮助你获取所需信息。本节描述书中使用的工具（以及其他一些工具）。

## `htons()` 或 `htonl()`

将主机字节序的二进制数据转换为网络字节序。在小端处理器上，此调用会交换字节顺序。大端主机什么都不做，只是返回该值。

### 原型

```c
#include <netinet/in.h>

unsigned short int htons(unsigned short int host_short);

unsigned long int htonl(unsigned long int host_long);
```

### 返回值

（无）

### 参数

- `host_short`：16 位主机值
- `host_long`：32 位主机值

### 可能的错误

（无）

### 示例

```c
/ *** Assign #1023 to socket *** /

struct sockaddr_in addr;

addr.sin_port = htons( 1023);

/ *** Assign 128.1.32.10 to the destination address *** /

struct sockaddr_in addr;

addr.sin_addr.s_addr = htonl( 0x0012100A);
```

## `ntohs()` 或 `ntohl()`

将网络字节序转换为主机的字节序。

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

## `inet_addr()`

这是一个已弃用的工具，用于将数字、点分地址转换为网络字节序的二进制形式。如果失败，返回值（`-1` 或 `255.255.255.255`）仍然是一个合法的地址。`inet_aton()` 工具具有更好的错误处理机制。

## 原型

```c
#include <netinet/in.h>

unsigned long int inet_addr(const char *ip_address);
```

## 返回值

| 返回值 | 描述 |
| :------- | :------- |
| 非零 | 如果一切正常，值为转换后的 IP 地址。 |
| `INADDR_NONE`(`-1`) | 参数无效。（这是该调用的缺陷——没有负值，而 `255.255.255.255` 是通用广播地址。） |

## 参数

| 参数 | 描述 |
| :------- | :------- |
| `ip_address` | 人类可读的点分表示形式（例如，`128.187.34.2`） |

## 可能的错误

（不设置 `errno`）

## 示例

```c
if ( (addr.sin_addr.s_addr = inet_addr("128.187.34.2")) == -1 )

    perror("Couldn't convert address");
```

## `inet_aton()`

将人类可读的点分表示 IP 地址转换为二进制、网络字节序形式。此调用取代了 `inet_addr()`。

## 原型

```c
#include <netinet/in.h>

int inet_aton(const char* ip_addr, struct in_addr *addr);
```

## 返回值

如果一切正常，则返回非零值。如果发生错误，该调用返回零。

## 参数

- `ip_addr`：IP 地址的 ASCII 字符串（例如，`187.34.2.1`）。
- `addr`：目标地址。通常，你会填充 `sockaddr_in` 结构中的 `sin_addr` 字段。

## 可能的错误

（不设置 `errno`）

## 示例

```c
struct sockaddr_in addr;

if ( inet_aton("187.43.32.1", &addr.sin_addr) == 0 )

    perror("inet_aton() failed");
```

## `inet_ntoa()`

此调用将网络字节序的二进制转换为人类可读的形式。注意，此调用使用静态内存区域；后续调用会覆盖较旧的结果。

## 原型

```c
#include <netinet/in.h>

const char* inet_ntoa(struct in_addr *addr);
```

## 返回值

地址在返回的字符串中。

## 参数

- `addr`：二进制地址（通常是 `sockaddr_in` 结构中的地址字段）

## 可能的错误

（不设置 `errno`）

## 示例

```c
clientfd = accept(serverfd, &addr, &addr_size);

if ( clientfd > 0 )

    printf("Connected %s:\n\n", inet_ntoa(addr.sin_addr));
```

## `inet_pton()`

将人类可读的 IPv4 或 IPv6 地址从点/冒号表示法转换为二进制、网络字节序形式。

## 原型

```c
#include <netinet/in.h>

int inet_pton(int domain, const char* prsnt, void *addr);
```

## 返回值

如果一切正常，则返回非零值。如果发生错误，该调用返回零。

## 参数

- `domain`：网络类型（`AF_INET` 或 `AF_INET6`）。
- `prsnt`：IP 地址的 ASCII 字符串（例如，`187.34.2.1` 或 `FFFF::8090:A03:3245`）。
- `addr`：目标地址。通常，你会填充 `sockaddr_in` 结构中的 `sin_addr` 字段或 `sockaddr_in6` 结构中的 `sin6_addr` 字段。

## 可能的错误

（不设置 `errno`）

## 示例

```c
struct sockaddr_in addr;

if ( inet_pton(AF_INET6, "187.43.32.1", &addr.sin6_addr) == 0 )

    perror("inet_pton() failed");
```

## `inet_ntop()`

此调用将网络字节序的二进制转换为人类可读的形式。与 `inet_ntoa` 不同，你需要提供给它一个临时字符串缓冲区。此函数支持 `AF_INET` 和 `AF_INET6`。

## 原型

```c
#include <arpa/inet.h>

char* inet_ntop(int domain, struct in_addr *addr, char* str, int len);
```

### 返回值

该调用返回参数 `str`。

### 参数

| 参数 | 描述 |
| :--- | :--- |
| `domain` | 网络类型（`AF_INET` 或 `AF_INET6`） |
| `addr` | 二进制地址（通常是 `struct sockaddr_in` 中的地址字段） |
| `str` | 字符串缓冲区 |
| `len` | `str` 中可用的字节数 |

### 可能的错误

（不设置 `errno`）

### 示例

```c
char str[100];

clientfd = accept(serverfd, &addr, &addr_size);

if ( clientfd > 0 )

  printf("Connected %s:%d\n",
```
