

```c
#define SOCKETNAME "MySocket"

int main(void)
{
    struct sockaddr_un sa;
    int nclient;

    (void)unlink(SOCKETNAME);
    strcpy(sa.sun_path, SOCKETNAME);
    sa.sun_family = AF_UNIX;
    for (nclient = 1; nclient <= 4; nclient++)
        ec_false( run_client(&sa) )
        ec_false( run_server(&sa) )
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
        exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

以下是我们获得的输出：

```
Server got "Hello from 31786!"
Client got "Goodbye!"
Server got "Hello from 31785!"
Client got "Goodbye!"
Server got "Hello from 31784!"
Client got "Goodbye!"
Server got "Hello from 31787!"
Client got "Goodbye!"
```

我们已经拥有了实现一个相当复杂的客户端-服务器系统所需的大部分要素。我们需要进一步了解的是如何设置套接字地址（`AF_UNIX` 本身并不特别有趣）以及如何设置套接字选项。在我们处理完字节序问题后，这一部分马上就会到来。

## 8.1.4 字节序

通过网络在不同机器之间传递如 “Hello” 和 “Goodbye” 这样的字符串时从来不会有问题，因为所有通信都保持了字节的顺序。然而，在传递二进制数字时可能会遇到问题，因为数字中字节的排列方式确实在不同机器之间存在差异。

为了理解这一点，请参见图 8.2，它展示了在内存位置 106204 存储一个十六进制表示为 0xD04C 的两字节整数的两种方法。

![](img/41b4c8f6d6a5c349eee321a301703d97_545_0.png)

![](img/41b4c8f6d6a5c349eee321a301703d97_545_1.png)

**图 8.2** 小端序与大端序。

在所谓的“小端序”机器中，数字的地址是其最低有效字节的地址；而在“大端序”机器中，它是其最高有效字节的地址。³ 两者都是给数字编址的完全有效方式，但问题是，如果一台机器向另一台使用不同字节序的机器发送二进制数字，数字就会被打乱。也就是说，如果小端序机器将数字作为字节序列发送（数据发送的唯一方式），发送的顺序将是先 4C 后 D0，而如果接收方机器是大端序的，它会将其解释为 4CD0，因为它将接收到的第一个字节视为高有效字节。

解决方案是以约定的网络字节序发送二进制数字。因此，所有发送方都必须从主机（本地）字节序转换为网络字节序，所有接收方都必须从网络字节序转换为主机字节序。但这仅在数据尚未以标准方式结构化的情况下执行。例如，如果你有一张编码为 JPEG 的照片，你会原样发送它——你不会尝试将 JPEG 的任何部分转换为网络字节序。

在大多数情况下，你不需要知道你的主机字节序或网络字节序，因为有一套标准的转换函数用于对 16 位和 32 位整数进行转换：

- `htons` — 将 16 位值从主机字节序转换为网络字节序

```c
#include <arpa/inet.h>

uint16_t htons(
    uint16_t hostnum /* 主机字节序下的 16 位数 */);
/* 返回网络字节序下的数字（无错误返回） */
```

- `htonl` — 将 32 位值从主机字节序转换为网络字节序

```c
#include <arpa/inet.h>

uint32_t htonl(
    uint32_t hostnum /* 主机字节序下的 32 位数 */);
/* 返回网络字节序下的数字（无错误返回） */
```

- `ntohs` — 将 16 位值从网络字节序转换为主机字节序

```c
#include <arpa/inet.h>

uint16_t ntohs(
    uint16_t netnum /* 网络字节序下的 16 位数 */);
/* 返回主机字节序下的数字（无错误返回） */
```

- `ntohl` — 将 32 位值从网络字节序转换为主机字节序

```c
#include <arpa/inet.h>

uint32_t ntohl(
    uint32_t netnum /* 网络字节序下的 32 位数 */);
/* 返回主机字节序下的数字（无错误返回） */
```

不幸的是，16 位函数使用后缀 “s” 代表 short，即使 short 类型可能超过 16 位；类似地，32 位函数使用后缀 “l” 代表 long。事实上，这些函数甚至不操作 short 和 long 类型；它们操作的是 `uint16_t`（16 位无符号整数）和 `uint32_t`（32 位无符号整数）类型。

为了演示其中两个函数的实际效果，下面是一个将 0xD04C 转换为网络字节序、显示字节再转换回原顺序的程序：

```c
int main(void)
{
    uint16_t nhost = 0xD04C, nnetwork;
    unsigned char *p;

    p = (unsigned char *)&nhost;
    printf("%x %x\n", *p, *(p + 1));
    nnetwork = htons(nhost);
    p = (unsigned char *)&nnetwork;
    printf("%x %x\n", *p, *(p + 1));
    exit(EXIT_SUCCESS);
}
```

输出显示运行该程序的 Intel Pentium CPU 使用的字节序与网络字节序不同：

```
4c d0
d0 4c
```

我们可以进一步得出结论：Pentium 处理器采用小端序，而网络字节序是大端序。⁴

通常，当你使用的协议要求发送二进制数字时（我们在下一节中会看到），你会使用这些标准转换函数。对于你自己的用途，请尽量设计应用程序以发送字符而不是二进制数据，除非你正在发送具有标准化格式的对象（JPEG、MP3 等）。这正是 HTTP（Web 协议）的做法（第 8.4.2 节）。

## 8.2 套接字地址

本节的全部内容仅关乎如何确定一个套接字地址（`struct sockaddr`），以便在调用 `bind` 和 `connect` 时使用。我们已经看到了如何针对 `AF_UNIX` 域执行此操作，其中地址主要只是一个路径名：

```c
struct sockaddr_un sa;
strcpy(sa.sun_path, SOCKETNAME);
sa.sun_family = AF_UNIX;
```

但这只是唯一简单的情况。其他域更为复杂。

### 8.2.1 套接字地址结构

每个地址家族都有自己的结构体结构和头文件。`AF_UNIX` 有 `sockaddr_un`，`AF_INET` 有 `sockaddr_in`，`AF_X25` 有 `sockaddr_x25`，等等，尽管只有前两个域在 [SUS2002] 中是标准化的。一种方法（我们在 `AF_UNIX` 中一直使用的方法）是声明一个你需要使用的特定结构体的变量，以某种方式填充其成员，并在调用 `bind` 或 `connect` 时将其地址强制转换为指向 `struct sockaddr`（通用类型）的指针。

从可移植性的角度来说，结构体 `sockaddr` 仅定义了一个抽象类型；你不能用它来声明要使用的结构体，因为它可能没有足够的空间。相反，有一个名为 `sockaddr_storage` 的标准结构体，它保证有足够的空间，但其成员并未针对任何特定域进行定制。

听起来很混乱，但其实没那么糟糕：

- 如果你确切知道你正在使用哪个域，请声明合适类型的结构体（例如 `sockaddr_un`），或动态分配足以容纳该结构体的空间（例如使用 `malloc`）。
- 如果你需要足以容纳任何域结构体的空间，请使用 `sockaddr_storage`，但在使用前将指针强制转换为合适类型的指针。
- 在调用 `bind` 和 `connect` 时使用强制转换为 `struct sockaddr *` 的操作——根据它们的函数原型，你别无选择。

下面是最后两条规则结合使用的示例：

```c
struct sockaddr_storage sas;
struct sockaddr_un *sa = (struct sockaddr_un *)&sas;
sa->sun_family = AF_UNIX;
...
ec_neg!( bind(fd, (struct sockaddr *)sa, sizeof(*sa)) )
```

不要过于担心最后一条规则。如果你做错了，编译器会告诉你。也不要担心直接使用 `sockaddr_storage`——它不包含你打算使用的任何成员。但是，由于你进行了强制转换，编译器在编译时不会检查你是否为你的域使用了正确的域特定结构体。这一点你必须在第一次时就做对。

### 8.2.2 AF_UNIX 套接字地址

![](img/41b4c8f6d6a5c349eee321a301703d97_548_0.png)

³ 术语本身很直观，但 “大端序” 这一术语实际上出自乔纳森·斯威夫特的*《格列佛游记》*，书中描述了关于从蛋的大头还是小头敲开的争议。事实上，“有一万一千个 [大头派] 曾数次宁愿承受死亡，也不愿服从从蛋的小头敲开的法令。”

