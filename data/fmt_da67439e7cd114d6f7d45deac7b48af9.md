
## Sockets

1. 包含必要的头文件并设置变量。

```c
#include <sys/types.h>

#include <sys/socket.h>

#include <stdio.h>

#include <sys/un.h>

#include <unistd.h>

int main()
{
    int sockfd;
    int len;
    struct sockaddr_un address;
    int result;
    char ch = 'A';
```

2. 为客户端创建一个套字。

```c
sockfd = socket(AF_UNIX, SOCK_STREAM, 0);
```

3. 按与服务器约定的为套字命名。

```c
address.sun_family = AF_UNIX;
strncpy(address.sun_path, "server_socket",
len = sizeof(address));
```

4. 将我们的套字连接到服务器的套字。

```c
result = connect(sockfd, (struct sockaddr *)&address, len);
if(result == -1) {
    perror("oops: client1");
    exit(1);
}
```

5. 现在可以通过 `sockfd` 进行读写。

```c
write(sockfd, &ch, 1);
read(sockfd, &ch, 1);
printf("char from server = %c\n", ch);
close(sockfd);
exit(0);
```

当你运行此程序时它会失败，因为你还没有创建服务器端的命名套字。具体的错误信息可能因系统而异。

```bash
$ ./client1

oops: client1: Connection refused
$
```

## 第 15 章

## 尝试一下——一个简单的本地服务器

这里有一个简单的服务器程序 `server1.c`，它接受来自我们客户端的连接。它创建了服务器套字，绑定到一个名称，创建一个监听队列并接受连接。

- 1. 包含必要的头文件并设置变量。

```c
#include <sys/types.h>

#include <sys/socket.h>

#include <stdio.h>

#include <sys/un.h>

#include <unistd.h>

int main()
{
    int server_sockfd, client_sockfd;
    int server_len, client_len;
    struct sockaddr_un server_address;
    struct sockaddr_un client_address;
```

- 2. 删除任何旧的套字并为服务器创建一个未命名的套字。

```c
unlink("server_socket");

server_sockfd = socket(AF_UNIX, SOCK_STREAM, 0);
```

- 3. 为套字命名。

```c
server_address.sun_family = AF_UNIX;
strncpy(server_address.sun_path, "server_socket", sizeof(...));

server_len = sizeof(server_address);

bind(server_sockfd, (struct sockaddr *)&server_address, server_len);
```

- 4. 创建连接队列并等待客户端。

```c
listen(server_sockfd, 5);

while (1) {
    char ch;
    printf("server waiting\n");
```

- 5. 接受连接。

```c
client_len = sizeof(client_address);
client_sockfd = accept(server_sockfd, (struct sockaddr *)&client_address, &client_len);
```

- 6. 在 `client_sockfd` 上对客户端读写。

```c
read(client_sockfd, &ch, 1);
ch++;
write(client_sockfd, &ch, 1);
close(client_sockfd);
```

此示例中的服务器程序一次只能服务一个客户端。它只是从客户端读取一个字符，将其加 1，然后写回。在更复杂的系统中，服务器必须代表客户端执行更多工作，这种做法是不可接受的，因为在服务器完成之前，其他客户端将无法连接。稍后你将看到允许多个连接的解决方法。

当你运行服务器程序时，它会创建一个套字并等待连接。如果你在后台启动它使其独立运行，那么你就可以在前台启动客户端了。

```bash
$ server1 &

[1] 1094

$ server waiting
```

当服务器等待连接时，它会打印一条消息。在前面的示例中，服务器在等待一个文件系统套字，你可以通过普通的 `-l` 命令看到它。

记住，在使用完套字后将其删除是礼貌的，即使程序通过信号正常终止。

```bash
$ ls -lf server_socket

srwxr-xr-x  1  root  users  0 2023-06-21 13:42  server_socket
```

设备类型是 `"socket"`，由权限前面的 `s` 和结尾的 `=` 显示。该套字是作为普通文件创建的，但权限被当前的 `umask` 修改了。如果你使用 `ps` 命令，可以看到服务器正在后台运行。它显示为休眠状态（`STAT` 为 `S`），因此不消耗 CPU 资源。

```bash
$ ps lx

F  UID  PID  PPID  NI  VSZ  WCHAN STAT TTY  TIME COMMAND

0  500 3165 2154  15   0 1344 280 solu S pts/1  0:00 ./server1
```

现在，当你在运行客户端程序时，你成功地连接到了服务器。由于该套字存在，你可以连接到它并与服务器通信。

```bash
$ ./client1

server waiting

char from server = B
```

## 第 15 章

## Socket 协议

底层传输机制允许使用多个协议来提供请求的 socket 类型；你可以为 socket 选择特定的协议。在本章中，我们将集中于 UNIX 网络工作和文件系统 socket，这些工作不需要你选择默认协议以外的协议。

## 创建 Socket

`socket` 系统调用创建一个 socket 并返回一个可以用于访问该 socket 的描述符。

```c
#include <sys/types.h>

#include <sys/socket.h>

int socket(int domain, int type, int protocol);
```

创建的 socket 是通信通道的一个端点。`domain` 参数指定地址族，`type` 参数指定与该 socket 使用的通信类型，而 `protocol` 则指定要采用的协议。

地址域包括以下内容：

| 域 (Domain) | 描述 |
| :--- | :--- |
| AF_UNIX | UNIX 内部（文件系统 socket） |
| AF_INET | ARPA Internet 协议（UNIX 网络协议） |
| AF_ISO | ISO 标准协议 |
| AF_NS | Xerox 系统协议 |
| AF_IPX | Novell IPX 协议 |
| AF_APPLETALK | Appletalk DDS |

常见的 socket 域是 `AF_UNIX`，它用于通过 UNIX 和 Linux 文件系统实现的本地 socket；以及 `AF_INET`，它用于 UNIX 网络 socket。`AF_INET` socket 可用于跨互联网在内的 TCP/IP 网络进行通信的程序。Windows Winsock 接口也提供了对此域 socket 的访问。

socket 类型（type）指定了新 socket 使用的通信特性。可能的值包括 `SOCK_STREAM` 和 `SOCK_DGRAM`。

`SOCK_STREAM` 是一个有序的、可靠的、基于连接的双向字节流。对于 `AF_INET` 域连接，这是由流 socket 在连接时两个端点之间建立的 TCP 连接提供的。数据可以沿流连接进行双方向传输。TCP 协议包含了分段和重组消息循环的机制，以及重传网络中可能丢失任何部分的机制。

`SOCK_DGRAM` 是数据报服务。你可以使用此 socket 发送固定（通常很小）最大长度的消息，但不能保证消息会被送达，或者消息在网络中不会被重排序。对于 `AF_INET` socket，这种通信是由 UDP 数据报提供的。

用于通信的协议通常由 socket 类型和域决定。通常没有选择。在有选择时，使用 `protocol` 参数。`0` 选择默认协议，我们将在所有的示例中都使用它。

`socket` 系统调用返回一个描述符，它在许多方面与低级文件描述符相似。当 socket 连接到另一个端点时，你可以使用该描述符配合 `read` 和 `write` 系统调用在 socket 上发送和接收数据。`close` 系统调用用于结束 socket 连接。

## Socket 地址

每个 socket 域都需要其自己的地址格式。对于 `AF_UNIX` socket，地址由定义在 `sys/un.h` 头文件中的 `sockaddr_un` 结构描述。

```c
struct sockaddr_un {
    sa_family_t  sun_family;   /* AF_UNIX */
    char            sun_path[];    /*路径名 */
};
```

为了将不同类型的地址传递给处理 socket 的系统调用，每个地址格式都由一个类似的结构描述，其中一个字段（在本例中为 `sun_family`）指定地址类型（即 socket 域）。在 `AF_UNIX` 域中，地址通过结构中 `sun_path` 字段的指定指定。

在当前的 Linux 系统上，由 X/Open 定义在 `sys/un.h` 中的类型 `sa_family_t` 必须是 `short`。此外，`sun_path` 中指定的路径名大小有限（Linux 规定为 108 个字符；其他可能使用常量 `UNIX_MAX_PATH`）。由于地址结构的大小各异，许多 socket 调用需要或作为输出提供一个长度，用于拷贝特定的地址结构。

在 `AF_INET` 域中，地址使用名为 `sockaddr_in` 的结构指定，它定义在 `netinet/in.h` 中，至少包含以下内容：

```c
struct sockaddr_in {
    short int           sin_family;    /* AF_INET */
    unsigned short int sin_port;      /* 端口号 */
    struct in_addr      sin_addr;      /* Internet 地址 */
};
```

IP 地址结构 `in_addr` 定义如下：

```c
struct in_addr {
    unsigned long int s_addr;
};
```

IP 地址的四个字节组成一个 32 位的值。一个 `AF_INET` socket 由其域、IP 地址和端口号完整描述。从应用程序的角度来看，所有 socket 的作用都像文件描述符，并通过唯一的整数值进行寻址。

## 为 Socket 命名

为了让通过调用 `socket` 创建的 socket 可供其他进程使用，服务器程序需要给 socket 起一个名字。因此，`AF_UNIX` socket 与文件系统路径关联，正如你在服务器示例中看到的。`AF_INET` socket 与 IP 端口号关联。

```c
#include <sys/socket.h>

int bind(int socket, const struct sockaddr *address, size_t address_len);
```

`bind` 系统调用将参数 `address` 指定地址分配给与文件描述符 `socket` 关联的未命名 socket。地址结构的长度作为 `address_len` 传递。

## 请求连接

客户端程序通过在未命名 socket 和服务器监听 socket 之间建立连接来连接服务器。它们通过调用 `connect` 实现这一点。

```c
#include <sys/socket.h>

int connect(int socket, const struct sockaddr *address, size_t address_len);
```
