
- 第 50 行的 `if` 语句测试最高位是否为零（请回顾图 3.1，查看 A 类地址）。如果最高位为零，则知道这是一个 A 类地址（执行第 51 和 52 行）。

- 第 53 行的 `if` 语句测试最高位是否为 `1`，且次高位是否为 `0`（请回顾图 3.1 中的 B 类地址）。如果此条件为真，则第 54 和 55 行的语句将该地址分类为 B 类。

- 第 56 行的 `if` 语句测试最高的两位是否为 `11`（二进制），后跟一个 `0` 位。如果此条件为真，则第 57 和 58 行将该地址分类为 C 类地址（请回顾图 3.1 中的 C 类地址）。

- 第 59 行的 `if` 语句测试最高位模式是否为 `1110`。这将导致地址被分类为 D 类地址。注意对于 D 类和 E 类，子网掩码设置为 `255.255.255.255`，因为整个地址都是网络地址。

- 第 62 行的 `else` 语句将剩余的所有情况评估为 E 类地址，并将子网掩码也设置为 `255.255.255.255`（参见步骤 9）。

- 分类结果在第 67 至 74 行报告。

列表 3.2 显示了运行该演示程序后产生的输出。

![](img/961a0296fe36074690a9847b79332eff_89_0.png)

```
Listing 3.2: The Output of the netmask.c Demonstration Program

$ ./netmask
Address 44.135.86.12 is class A netmask 255.0.0.0
Address 127.0.0.1 is class A netmask 255.0.0.0
Address 172.16.23.95 is class B netmask 255.255.0.0
Address 192.168.9.1 is Class C netmask 255.255.255.0
$
```

通过列表 3.1 中展示的示例代码，您将准备好对必须处理的任何 IP 号码进行分类。

当您的注意力仍然集中在 IP 号码上时，现在是涵盖私有 IP 号码分配的好时机。如果您决定建立自己的私有网络，将使用这些地址。

## 分配 IP 地址

您在上一节中学习了 Internet 地址是如何分类的。IP 地址由一个名为 InterNIC 的组织分配给各个个人和团体。然而，某些 IP 地址范围已被保留用于私有使用，还有一些保留用于特殊用途。

## 私有 IP 号码

通常，IP 号码必须由 InterNIC 在 `rs.internic.net` 处注册。（在 1993 年 4 月 1 日之前，这是由 NIC 在 `nic.ddn.mil` 处理的。）但是，如果您的系统不直接连接到 Internet，则不需要拥有全局唯一地址。您可以使用“私有”IP 号码代替。

那么，随之而来的第一个问题就是“我应使用哪些 IP 号码？”本节旨在帮助您做出该决定，并作为未来的参考指南。

`RFC 1597` 是一个 Internet 标准文档，描述了如何分配私有 IP 号码。表 3.3 为您提供了一个快速摘要，包括子网掩码值。

**表 3.3：私有 IP 号码分配**

| 类别 | 最低值 | 最高值 | 子网掩码 |
|---|---|---|---|
| A | `10.0.0.0` | `10.255.255.255` | `255.0.0.0` |
| B | `172.16.0.0` | `172.31.255.255` | `255.255.0.0` |
| C | `192.168.0.0` | `192.168.255.255` | `255.255.255.0` |

您选择 A、B 或 C 类 IP 号码系列将主要取决于您计划建立的独立网络和主机数量。如果网络和主机的总数较少，则 C 类地址可能就足够了。或者，A 类地址允许一个网络（不使用子网划分），但支持非常大的主机总数。B 类提供了大量的网络和主机。

### 保留 IP 号码

有大量保留的 IP 号码，这些块在 `RFC 1166` 中列出。作为一个保留号码系列的例子，表 3.4 展示了业余无线电 IP 号码系列。这些用于使用 Internet 协议在分组无线电设备上操作无线电的业余无线电操作员。现在，随着 `AX.25` 协议集成到 Linux 内核中（自 `2.2.0` 版本起），可以确定将有更多无线电爱好者使用这些 IP 号码！

**表 3.4：业余无线电保留 IP 号码**

| 类别 | 最低值 | 最高值 | 子网掩码 |
|---|---|---|---|
| A | `44.0.0.0` | `44.255.255.255` | `255.0.0.0` |

至此，您对 IP 号码的介绍已接近尾声。现在，是时候将您对套接字地址和 IP 号码的知识应用于 Linux 提供的简化 IP 地址转换功能的函数了。

### 操作 IP 号码

为了减轻将字符串形式的 IP 号码转换为可用套接字地址的编程负担，提供了一系列转换函数。这些及其他有用函数将在以下部分中介绍。

#### 使用 `inet_addr(3)` 函数

您将学习的第一个函数是一个较旧的函数，在新代码中可能不应再使用。但是，您会在很多现有的网络代码中找到它，因此您应该熟悉它并了解其局限性。

`inet_addr(3)` 的概要如下：

```c
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

unsigned long inet_addr(const char *string);
```

该函数接受输入 C 字符串参数 `string`，并将点分四元组表示法解析为 32 位 Internet 地址值。返回的 32 位值处于网络字节序。

如果输入参数 `string` 不代表有效的点分四元组地址，则返回 `INADDR_NONE`。返回的任何其他值都表示转换后的值。

**注意**

`inet_addr(3)` 返回的 32 位值处于网络字节序。不要对返回值使用 `htonl(3)`，因为它已经是网络字节序。

**警告**

`inet_addr(3)` 在返回 `INADDR_NONE` 时不会在 `errno` 中建立原因代码。因此，当此函数返回错误指示时，不要测试 `errno` 或报告它。

列表 3.3 中显示的 `program` 是该函数使用方法的示例。要编译并运行该程序，请执行以下操作：

```
$ make inetaddr
$ gcc -c -D_GNU_SOURCE -Wall inetaddr.c
$ gcc inetaddr.o -o inetaddr
$ ./inetaddr
```

列表 3.3 中的程序在运行时，将包含 IP 号码的 C 字符串常量转换为网络序列化的 32 位 IP 地址。然后，该值被放入 `AF_INET` 套接字地址并绑定到套接字。

![](img/961a0296fe36074690a9847b79332eff_91_0.png)

```
Listing 3.3: inetaddr.c—Example Program Using inet_addr(3)

1:  /* inetaddr.c:
2:  *
3:  * Example using inet_addr(3):
4:  */
5:  #include <stdio.h>
6:  #include <unistd.h>
7:  #include <stdlib.h>
8:  #include <errno.h>
9: #include <string.h>
10: #include <sys/types.h>
11: #include <sys/socket.h>
12: #include <netinet/in.h>
13: #include <arpa/inet.h>
14:
15: /*
16: * 此函数报告错误并
17: * 退出返回到 shell：
18: */
19: static void
20: bail(const char *on_what) {
21: fputs(on_what,stderr);
22: fput('\n',stderr);
23: exit(1);
24: }
25:
26: int
27: main(int argc,char **argv) {
28: int z;
29: struct sockaddr_in adr_inet;/* AF_INET */
30: int len_inet; /* 长度 */
31: int sck_inet; /* 套接字 */
32:
33: /* 创建套接字 */
34: sck_inet = socket(AF_INET,SOCK_STREAM,0);
35:
36: if ( sck_inet == -1 )
37: bail("socket():
38:
39: /* 建立地址 */
40: memset(adr_inet,0,sizeof adr_inet);
41:
42: adr_inet.sin_family = AF_INET;
```
