
暂时先看看通用记录和 INET 记录以供比较（来自头文件）：

```c
struct sockaddr {
    unsigned short int sa_family;
    unsigned char sa_data[14];
};
```

```c
struct sockaddr_in {
    sa_family_t sin_family;
    unsigned short int sin_port;
    struct in_addr sin_addr;
    unsigned char __pad[1];
};
```

请注意，`sa_family` 和 `sin_family` 是两个结构体之间的公共字段。每个过程调用在接收到此记录时执行的任务都是检查第一个字段。请注意，这是唯一采用主机字节序的字段（参见第 2 章）。填充字段（名为 `sa_data` 和 `__pad`）在 `sockaddr` 家族中的每个结构体中可能是通用的。按照惯例，通用 `sockaddr` 结构体和 INET `sockaddr_in` 结构体长度必须为 16 字节（IPv6 结构体 `sockaddr_in6` 为 24 字节）。因此，填充字段会用任意未使用的字节填满。

你可能会注意到 `sockaddr_in` 中填充字段的长度缺失。这仅仅是一个惯例。由于填充必须设置为零，实际大小并不重要。（在此 `sockaddr_in` 定义中，其宽度为 8 字节。）某些实现可能会定义额外字段用于内部计算。不要担心它们——也不要使用它们，因为你无法保证字段在不同系统和不同版本之间的可用性。任何更改都可能在你使用非标准字段时导致代码失效。在所有情况下，将整个结构体实例初始化为零是最好的做法。

下表描述了每个字段。它还给出了可能值的示例。

| 字段名称 | 描述 | 字节序 | 示例 |
| :--- | :--- | :--- | :--- |
| `sin_family` | 协议族 | 主机、本机 | `AF_` |
| `sin_port` | 服务器的端口号 | 网络 | 13（时间服务） |
| `sin_addr` | 服务器的数字 IP 地址 | 网络 | 127.0.0.1（本地主机） |

在调用 `connect()` 系统调用之前，程序会填充每个字段。Linux 略微掩蔽了该系统调用，因此不需要将 `sockaddr_in` 强制转换为 `sockaddr`。为了可移植性，你可能仍然希望遵循惯例并添加强制转换。

## 强制转换 `sockaddr` 类型

在其他兼容 UNIX 的操作系统中，你可以将 `sockaddr_*` 家族成员强制转换为 `sockaddr` 以避免警告。这里的示例未使用任何强制转换，仅仅是为了节省空间（并且因为 Linux 允许这样做）。

代码可能看起来像清单 1.2。

### 清单 1.2 `Connect()` 示例

```c
/*** 代码片段展示 connect() 系统调用的初始化和调用 *** */

#define PORT_TIME     13
struct sockaddr_in dest;
char *host = "127.0.0.1";
int sd;
/*** 创建套接字并执行其他工作 *****/

bzero(&dest, sizeof(dest));      /* 从干净的状态开始 */
dest.sin_family = AF_INET;       /* 选择所需的网络 */
dest.sin_port = htons(PORT_TIME); /* 选择端口 */
inet_aton(host, &dest.sin_addr);         /* 远程地址 */

if ( connect(sd, &dest, sizeof(dest)) == 0 )  /* 连接！ */
{
        perror("Socket connection");
        abort();
}
...
```

此代码中的 `connect()` 系统调用在将套接字连接到服务器之前需要几个预备步骤。首先，创建一个 `sockaddr_in` 结构体。使用服务器地址作为第二行的值。如果你想连接到不同的服务器，请将相应的 IP 地址放入此字符串中。程序继续执行其他初始化，包括 `socket()` 系统调用。当你开始处理该结构体时，使用 `bzero()` 将其清零。程序将 family 设置为 `AF_INET`。接下来，程序设置端口和 IP 地址。这里使用的 `htons()` 和 `inet_aton()` 转换工具在第 2 章中有详细介绍。

下一个调用是连接服务器。请注意，代码片段检查了每个过程调用的返回值。该策略是使你的网络程序健壮性的诸多关键因素之一。

在程序建立连接后，套接字描述符 `sd` 成为两个程序之间的读/写通道。我们习惯的大多数服务器提供单次事务然后挂断（例如，HTTP 1.0 服务器发送请求的文件，然后关闭连接）。为了与这些类型的服务器接口，你的程序必须发送请求，获取回复，并关闭连接。

## 获取服务器的回复

套接字已打开，通道已建立。现在，你可以获取第一个“你好”。一些服务器会像接听电话的人一样发起对话。此消息可能包含服务器名称和连接说明。一旦连接打开，你可以使用标准库的底层 I/O 调用进行通信。以下是 `read()` 系统调用：

```c
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t count);
```

你很可能熟悉此调用。除了它具备使用套接字描述符 (`sd`) 代替文件描述符 (`fd`) 的特殊能力外，其他一切几乎与从文件读取相同。你甚至可以使用 `read()` 系统调用，如下面的代码片段所示：

```c
...
int sd, bytes_read;
sd = socket(PF_INET, SOCK_STREAM, 0);    /* 创建套接字 */

/**** 连接到主机 ****/

bytes_read = read(sd, buffer, MAXBUF);  /* 读取消息 */
if ( bytes_read < 0 )
    /* 报告连接错误；退出例程 */
...
```

实际上，你可以将套接字描述符转换为 `FILE*` 以进行更高级的 I/O 操作。例如，若要使用 `fscanf()`，你可以参考下方的示例。（加粗的行表示与前一个列表中的更改。）

```c
char Name[NAME], Address[ADDRESS], Phone[PHONE];
FILE *sp;
int sd;
sd = socket(PF_INET, SOCK_STREAM, 0); /* create socket */

/* Connect to host */

if ( (sp = fdopen(sd, "r")) == NULL) /* convert to FILE* */
  perror("FILE* conversion failed");
else if ( fscanf(sp, "%s, %s, %s\n",
  Name, Address, Phone) < 0 )
{
    perror("fscanf");
...
```

只有流式套接字（stream-style sockets）才能可靠地转换为 `FILE*` 流。原因很简单：数据报套接字（Datagram sockets）通常是无连接的——发送一条消息后过程即结束。此外，流式套接字提供数据完整性和消息可靠性，而数据报则不可靠。数据报类似于将一封写好了地址并贴好邮票的信封放入邮政系统发送：消息可能根本无法到达。`FILE*` 连接必须是一个打开的通道。如果你尝试转换数据报，可能会丢失关键数据。有关流与数据报的更多信息，请参阅第 3 章“不同类型的互联网数据包”（Different Types of Internet Packs）。

`FILE*` 套接字连接为网络程序员提供了优秀的扫描和解析资源。然而，当你使用它们时，必须检查所有返回值，包括 `printf()` 和 `fscanf()`。注意前面的示例：如果 `fscanf()` 的返回值小于零，则表示发生了错误。

## 网络安全与可靠性

在创建网络程序时，安全性和可靠性至关重要。在撰写本书时，微软操作系统面临过几个根本性的安全问题，其中一些涉及网络连接。在编写程序时，请确保缓冲区不会溢出，并且所有返回值都经过检查。在软件集市（software bazaar）的环境中，你可以就你的源代码征求他人的意见。软件集市的同行评审是知识和经验的巨大资源——请利用它。

回顾 `read()` 系统调用，你可能会遇到以下常见错误：

- `EAGAIN` 选择了非阻塞 I/O，且没有可用数据。此错误指示程序再次尝试该调用。

- `EBADF` `fd` 不是有效的文件描述符，或未以读取方式打开。如果套接字调用不成功，或者程序关闭了输入管道（使其变为只写），可能会发生这种情况。

- `EINVAL` `fd` 附着在一个不适合读取的对象上。
