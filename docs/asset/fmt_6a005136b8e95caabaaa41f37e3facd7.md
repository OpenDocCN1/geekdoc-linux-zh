
```c
retvalue = getprotobynumber ( number );
```

## 描述

调用 `getprotobynumber` 根据数字获取有关协议的信息。返回的信息包括官方名称。

## 参数

| 参数 | 类型 | 含义 |
| --- | --- | --- |
| number | int | 协议号（本地主机的原生字节序） |

## 返回值

`Getprotobynumber` 成功时返回指向 `proto_ent` 结构指针，失败返回 NULL 指针表示发生了错误。当发生错误时，可以调用 `WSAGLastError()` 获取提供特定错误原因的代码。结构 `proto_ent` 定义如下：

```c
struct proto_ent {
    /* 描述协议的条目 */
    char FAR* p_name;           /* 协议官方名称 */
    char FAR* FAR* p_aliases;   /* 协议的别名列表 */
    short p_proto;             /* 官方协议号 */
};
```

# Getservbyname 库调用

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = getservbyname ( name, proto );
```

## 描述

`Getservbyname` 根据服务名称从网络服务数据库中获取条目。客户端和服务器都调用 `getservbyname` 将服务名称映射到协议端口号。

如果第二个参数不空，`getservbyname` 将同时匹配服务和协议。如果第二个参数为空，`getservbyname` 将忽略该参数并仅匹配名称。

## 参数

| 参数 | 类型 | 含义 |
|---|---|---|
| name | const char FAR* | 指向包含服务名称的字符串指针。 |
| proto | const char FAR* | 指向要使用的协议名称字符串指针（例如 "tcp"）或 NULL 值。 |

## 返回值

`Getservbyname` 成功时返回指向 `servent` 结构指针，失败返回 NULL 指针表示发生了错误。`servent` 结构定义如下：

```c
struct servent {
  char FAR* s_name;      /* 一个服务条目 */
  char FAR* s_aliases;   /* 官方服务名称 */
                       /* 其他别名列表 */
  short    s_port;         /* 此服务使用的端口 */
  char FAR* s_proto;     /* 此服务使用的协议 */
};
```

# Getservbyport 库调用

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = getservbyport ( port, proto );
```

## 描述

`Getservbyport` 根据端口号从网络服务数据库中获取条目。虽然使用频率不高，但 `getservbyport` 可以将协议端口号映射到服务名称。如果第二个参数不空，`getservbyport` 将同时匹配协议端口号和协议。如果第二个参数为空，`getservbyport` 将忽略该参数并仅匹配端口。

## 参数

| 参数 | 类型 | 含义 |
|---|---|---|
| port | int | 网络字节序的协议端口号。 |
| proto | char FAR* | 指向要使用的协议名称字符串指针（例如 "tcp"）或 NULL 值。 |

## 返回值

`Getservbyport` 成功时返回指向 `server` 结构指针，失败返回 NULL 指针表示发生了错误。`server` 结构定义如下：

```c
struct servent {
    char FAR* s_name;      /* 一个服务条目 */
    char FAR* s_name;      /* 官方服务名称 */
    char FAR* s_aliases;   /* 其他别名列表 */
    short s_port;          /* 此服务使用的端口 */
    char FAR* s_proto;      /* 此服务使用的协议 */
};
```

# Getgetsockname 函数

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = getgetsockname ( socket, name, namelen );
```

## 描述

`Getgetsockname` 获取指定 `socket` 的本地地址和协议端口号。

## 参数

| 参数 | 类型 | 含义 |
|---|---|---|
| socket | SOCKET | socket 描述符。 |
| name | struct* | 接收地址信息的结构。 |
| namelen | int* | 缓冲区的大小。 |

## 返回值

`Getgetsockname` 成功时返回 0，失败时返回 `SOCKET_ERROR`。

# Getsockopt 函数

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = getsockopt ( socket, level, opt, optval, optlen );
```

## 描述

`Getsockopt` 允许应用程序获取 `socket` 的选项值。

## 参数

| 参数 | 类型 | 含义 |
|---|---|---|
| socket | SOCKET | socket 描述符。 |
| level | int | 级别。 |
| opt | int | 选项。 |
| optval | char* | 返回的值。 |
| optlen | int* | 缓冲区的大小。 |

示例：

- `SO_BROADCAST`: 允许传输广播？
- `SO_DONTROUTE`: 绕过输出路由？
- `SO_ERROR`: 获取 socket 最后的错误。
- `SO_LINGER`: 如果有数据时留存？
- `SO_OOBLINE`: 接收带外数据？
- `SO_RCVBUF`: 输入缓冲区大小？
- `SO_SNDBUF`: 输出缓冲区大小？

## 返回值

`Getsockopt` 成功时返回 0，失败时返回 `SOCKET_ERROR`。

# htonl 函数

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = htonl ( hostlong );
```

## 描述

`htonl` 将无符号长整数从本地主机字节序转换为网络字节序。

## 参数

| 参数 | 类型 | 含义 |
| --- | --- | --- |
| hostlong | u_long | 需要转换的 32 位整数。 |

## 返回值

`htonl` 返回网络字节序的值。

# htons 函数

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = htons ( hostshort );
```

## 描述

`htons` 将无符号短整数从本地主机字节序转换为网络字节序。

## 参数

| 参数 | 类型 | 含义 |
| --- | --- | --- |
| hostshort | u_short | 需要转换的 16 位整数。 |

## 返回值

`htons` 返回网络字节序的值。

# Inet_addr 函数

## 头文件

```c
#include <winsock.h>
```

## 使用

```c
retvalue = inet_addr ( dotted );
```

## 描述

客户端和服务器都使用 `inet_addr` 函数将点点形式的 IP 地址转换为 socket 函数期望的内部二进制格式。

## 参数

| 参数 | 类型 | 含义 |
|---|---|---|
| dotted | const char FAR* | 包含点表示法 IP 地址的字符串。 |

## 返回值

成功时，`inet_addr` 返回一个包含二进制格式 IP 地址的无符号长整数。否则，`inet_addr` 返回 `INADDR_NONE` 表示参数不包含有效的点点地址（例如某个值大于 255 或者由点分隔的数字超过四个）。

## Inet_ntoa 函数

### 包含文件

```
#include <winsock.h>
```

### 使用

```
retvalue = inet_ntoa ( ipaddr );
```

### 描述

必须向人类显示 IP 地址的应用程序会调用 `inet_ntoa` 将地址从内部二进制格式转换为包含点分十进制格式地址的文本字符串。

### 参数

| Arg | 类型 | 含义 |
|---|---|---|
