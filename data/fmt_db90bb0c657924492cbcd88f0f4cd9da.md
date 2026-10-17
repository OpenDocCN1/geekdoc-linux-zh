
# write()

从缓冲区向文件描述符 `fd` 写入 `msg_len` 个字节。你也可以使用套接字描述符，但它提供的控制选项不如 `send()` 系统调用多。

## 原型

```c
#include <unistd.h>

int write(int fd, const void *buffer, size_t msg_len);
```

## 返回值

写入的字节数。字节数可能小于 `msg_len`。如果调用未能成功写入所有必需的字节，你可以使用循环进行连续写入。如果为负数，调用会在 `errno` 中存储错误详情。

## 参数

- `fd`
  文件描述符（可以是套接字描述符）
- `buffer`
  要写入的消息
- `msg_len`
  消息的长度

## 可能的错误

| 错误 | 描述 |
| :---- | :---------- |
| `EBADF` | `fd` 不是有效的文件描述符，或者未打开以用于写入。 |
| `EINVAL` | `fd` 附加到一个不适合写入的对象。 |
| `EFAULT` | `buf` 超出了可访问的地址空间。 |
| `EPIPE` | `fd` 连接到一个读取端已关闭的管道或套接字。当发生这种情况时，写入进程将收到 `SIGPIPE` 信号；如果它捕获、阻塞或忽略该错误，则返回 `EPIPE`。 |
| `EAGAIN` | 已使用 `O_NONBLOCK` 选择了非阻塞 I/O，且与 `fd` 连接的管道或套接字中没有空间立即写入数据。 |
| `EINTR` | 在写入任何数据之前，调用被信号中断。 |
| `ENOSPC` | 包含 `fd` 所指文件的设备没有空间容纳数据。 |
| `EIO` | 在修改 `inode` 时发生了底层 I/O 错误。 |

## 示例

```c
/* ** Write a message (TCP, UDP or Raw) ** */

int sockfd;

int bytes, bytes_wrote=0;

/* --- Create socket, connect to server --- */

while ( (bytes = write(sockfd, buffer, msg_len)) > 0 )

if ( (bytes_wrote += bytes) >= msg_len )

break;

if ( bytes < 0 )

perror("write");
```

# close()

关闭所有描述符（文件或套接字）。如果套接字已连接到服务器或客户端，它请求执行 `close()`。通道在 `close` 之后实际上仍然保持活动状态，直到通道排空或超时。每个进程对其可以拥有的打开描述符数量都有一个限制。

`getdtablesize()` 在 Linux 2.2.14 中返回 1024，并且 `/usr/include/linux/limits.h` 文件使用 `NR_OPEN` 定义了此限制。此外，前三个描述符默认为 `stdin` (0)、`stdout` (1) 和 `stderr` (2)。

## 原型

```c
#include <unistd.h>

int close(int fd);
```

## 返回值

如果一切正常，返回零。如果发生错误，你可以在 `errno` 中找到原因。

## 参数

- `fd`
  文件或套接字描述符

## 可能的错误

- `EBADF`
  `fd` 不是一个有效的打开文件描述符。

## 示例

```c
int sockfd;

sockfd = socket(PF_INET, SOCK_RAW, htons(99));

if ( sockfd < 0 )

PANIC("Raw socket create failed");

...

if ( close(sockfd) != 0 )

PANIC("Raw socket close failed");
```

## 对象类

## 附录 D

## 本附录内容

- C++ 异常 478
- C++ 支持类 479
- C++ 消息类 480
- C++ 套接字类 481
- Java 异常 485
- Java 支持类 486
- Java I/O 类 488
- Java 套接字类 494

本附录列出了书中和本书网站上描述的 Java API 中定义的类以及自定义 C++ 库。每个类都有一个三种指定类型之一：`Class`（可以实例化的普通类）、`Abstract Class`（为派生类定义骨架的类）和 `Superclass`（可实例化的父类）。

## C++ 异常

本节描述书中定义的异常类。该层次结构遵循尽可能少的原则，以最小化潜在灾难性类创建的可能性。

![](img/2591af4bdf00a0f382331fc9481f785e_497_0.png)

> 图 D.1
> C++ 异常类层次结构。

### Exception (Superclass)

构造函数：`Exception(SimpleString s);`

通用描述：具有 `SimpleString` 类型的通用异常消息。

方法：`const char* Getstring()` 获取字符串消息。

子异常：
`RangeException` 任何范围异常。由 `MessageGroup` 类使用。
`FileException` 任何文件异常。由 `Socket` 类使用。

### NetException (Class)

构造函数：`NetException(SimpleString s);`

通用描述：通用网络异常。

父类：`Exception`（异常）

子类异常：

| 异常 | 描述 |
|---|---|
| `NetConversionException` | 主机（`inet_ntop`/`inet_pton`）地址转换异常。由 `HostAddress` 类使用。 |
| `NetDNSException` | 无法解析主机名的异常。由 `HostAddress` 使用。 |
| `NetIOException` | `send()`/`recv()` 异常。由 `Socket` 使用。 |
| `NetConnectException` | 在尝试使用 `bind()`、`connect()`、`listen()` 或 `accept()` 时发生的异常。由 `ServerSocket`、`ClientSocket` 和 `MessageGroup` 使用。 |
| `NetConfigException` | 在尝试设置或获取套接字选项时发生的异常。由所有 `Socket` 类使用。 |

## C++ 支持类

本节描述了几个与框架相关的类，但比其他类库中的类更简单。请随意使用标准 C++ 类库替换这些类。

### SimpleString（类）

构造函数：

```cpp
SimpleString(const char* s);

SimpleString(const SimpleString& s);
```

一般描述：非常简单和轻量的字符串类型。

方法：

| 方法 | 描述 |
|---|---|
| `operator+(SimpleString& )` | 将字符串追加到当前实例。 |
| `const char* GetString()` | 获取字符串消息。 |

抛出异常：（无）

### HostAddress（类）

构造函数：

```cpp
HostAddress(const char* Name=0, ENetwork Network=IPv4);

HostAddress(HostAddress& Address);
```
