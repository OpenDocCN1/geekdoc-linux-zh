
## IPv6 的局限性及 Linux 支持情况

IPv6 存在三个局限性。首先，它使开销加倍。典型的 IPv4 消息头宽度约为 20 字节。如果你的消息宽度为 1500 字节，那么 IP 开销约占消息的 1%。IPv6 将其加倍至 40 字节，使典型消息开销增加到约 2%。然而，与 IPv4 不同，IPv6 的有效载荷长度中不包含包的长度。这节省了几个字节——IPv4 的最大包大小为 65,535 字节，而 IPv6 非巨型包的最大值为 65,535+40 字节。

IPv6 已弃用 IPv4 的广播支持。实际上，这并不是一个问题。多播比广播具有更大的灵活性和控制性，而且现代项目中已不再真正使用广播。

最后，IPv6 不再在头部中包含校验和字段。在简化 IP 头部的过程中，他们删除了一些冗余字段。然而，这可能会给那些物理帧中不包含校验和或 CRC 的旧接口带来问题。较新的硬件接口会代替操作系统完成所有的数据完整性检查。如果你拥有旧硬件，可能需要就此进行详细调查。

### 预期的 Linux 整合情况

Linux 开发社区一直紧跟 IPv6 的发展。从 2.2.0 开始的所有版本都完全支持当前版本的 IPv6。不幸的是，IPv6 有一个主要缺点：它尚未被完全接受为标准，其中许多部分仍未定义。

Linux 在有限的定义范围内尽可能提供支持。你仍然可以在开发中使用它，但要记住 IPv6 是一个不断变化的目标，因此目前没有操作系统能 100% 合规。你可以预期它将继续保留在内核的实验选项部分中。

> **互联网支持及 6bone**
> 
> 正如最初对多播的支持曾带来问题并导致了 Mbone 的出现，许多路由器也不支持 IPv6。与 Mbone 类似，IPv6 爱好者创建了 6bone，这是一个 IPv6-over-IPv4（IP-in-IP）消息子系统。6bone 将 IPv6 数据包封装在 IPv4 数据包内部，由一个路由服务器传递给另一个。虽然不像 Mbone 服务器那样普及，但其支持正在增长（特别是在欧洲和远东地区）。

最后一点说明：请注意，由于 IPv6 的实验性质，它可能会在你的系统中造成一些安全漏洞。你可能不希望在一个将互联网连接到内部网的网络上进行操作。

## 总结：让你的代码面向未来

IPv6 解决了当前 IPv4 寻址结构中的局限性。通过多个数量级扩展寻址范围，IPv6 看起来是互联网清晰的未来方向。尽管仍处于婴儿期，其寻址分配已采用诸如 IPX 等标准网络。它已在欧洲和远东网络中获得支持。

随着地址的扩展，物理外观发生了变化，并包含了一些简写符号以便于表示和编程。只要你遵循本书中的指南和示例，从 IPv4 移植程序到 IPv6 是 straightforward（直接的/简单的）。`socket()` 系统调用真正帮助网络编程适应不同的网络。

IPv6 网络涵盖了 IPv4 网络，因此所有 IPv4 地址仍然有效。支持 IPv6 的大多数操作系统很可能使用双栈来支持和转换这两种网络。这些双栈中的寻址方案和转换允许某种隐式协作——支持这种协作只需重新编写很少的代码。

Linux 内核从 2.2.0 版本开始支持 IPv6，但并非所有操作系统发行版都安装了启用此功能的编译内核。事实上，如果你的发行版不包含编译了 IPv6 的内核，该发行版很可能也没有更新的相关工具。本章描述了如何在你的 Linux 主机上让 IPv6 正常工作。

此外，本章通过示例展示了如何转换 IPv4 程序。它还介绍了两个用于辅助地址转换的新工具。在你的程序中支持 IPv6 增加了你的工作在未来被使用的可能性。

## 附录

### 第五部分

### 本部分内容

-   A 数据表 395
-   B 网络 API 421
-   C 内核 API 子集 449
-   D 对象类 477

## 数据表

### 本附录内容

-   **域 (Domains)**：`socket()` 的第一个参数 396
-   **类型 (Types)**：`socket()` 的第二个参数 404
-   **协议定义** 404
-   **标准互联网端口分配**（前 100 个端口） 405
-   **HTTP 1.1 状态代码** 407
-   **套接字选项**（`get/setsockopt()`） 408
-   **信号定义** 414
-   **ICMP 代码** 415
-   **IPv4 多播分配** 417
-   **拟议的 IPv6 地址分配** 417
-   **ICMPv6 代码** 418
-   **IPv6 多播作用域字段** 419
-   **IPv6 多播标志字段** 420

本附录识别并列举了所有与套接字编程相关的表格和数据格式。

### 域：socket() 的第一个参数

表 A.1 列出了 `socket()` 系统调用第一个参数的值。你也可以在 `bind()` 系统调用中使用这些类型。虽然大多数程序在 `socket()` 和 `bind()` 中都使用 AF 风格，但正确的做法是在 `socket()` 中使用 PF 风格，在 `bind()` 中使用 AF 风格。如果你对使用 PF 风格感到不安，可以安全地使用 AF 风格，因为 C 头文件将 AF 风格定义为 PF 风格。结构定义位于 `<bits/socket.h>` 中。

#### 表 A.1 socket() 域参数的协议族值

| 类型 | 描述和示例 |
| :--- | :--- |
| PF_UNSPEC | 未指定 |
| PF_LOCAL<br>PF_UNIX | BSD 访问本地命名管道的方法<br><br>```c<br>#include <linux/un.h><br>struct sockaddr_un addr;<br>addr.sun_family = AF_UNIX;<br>strcpy(addr.sun_path,<br>"/tmp/mysocket");<br>``` |
| PF_INET | Internet IPv4 协议族<br><br>```c<br>#include <linux/in.h><br>struct sockaddr_in addr;<br>bzero(&addr, sizeof(addr));<br>addr.sin_family = AF_INET;<br>addr.sin_port = htons(9999);<br>if ( inet_pton("127.0.0.1",<br>      &addr.sin_addr) == 0 )<br>    perror("Addr conversion");<br>``` |

| 关联数据 |
| :--- |
| ```c<br>struct sockaddr {<br>    unsigned short sa_family;<br>    unsigned char sa_data[14];<br>};<br>#define UNIX_PATH_MAX 108<br>struct sockaddr_un {<br>    sa_family_t sun_family;<br>    char sun_path[UNIX_PATH_MAX];<br>};<br>struct sockaddr_in {<br>    sa_family_t sin_family;<br>    unsigned short sin_port;<br>    struct in_addr sin_addr;<br>    unsigned char pad[];<br>};<br>``` |

#### 表 A.1 续

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| PF_AX25 | 业余无线电 AX.25 <br><br> `#include <linux/AX25.h>` | `typedef struct {` <br>`char ax25_call[7];` <br>} ax25_address; <br><br>`struct sockaddr_ax25 {` <br>`sa_family_t sax25_family;` <br>`ax25_address sax25_call;` <br>`ax25_address sax25_ndigis;` <br>`int ...;` <br>`};` |
| PF_IPX | Novell 互联网协议 <br><br> `#include <linux/ipx.h>` | `struct sockaddr_ipx` <br>`{` <br>`sa_family_t sipx_family;` <br>`__u16 sipx_port;` <br>`__u32 sipx_network;` <br>`unsigned char sipx_node[IPX_NODE_LEN];` <br>`__u8 ...;` <br>`};` <br><br>`struct sockaddr_in_at {` <br>`unsigned char si...;` <br>`__u8 padding;` <br>`unsigned char si...;` <br>`};` |
| PF_APPLETALK | Appletalk DDP <br><br> `#include <linux/atalk.h>` | `struct sockaddr_at {` <br>`sa_family_t sat_family;` <br>`struct s_net {` <br>`u16 s_net;` <br>`__u8 ...;` <br>} ...; <br>`struct s_node {` <br>`u16 s_addr;` <br>`sat_addr;` <br>`char sat_zero1[...]` <br>`};` |

#### 表 A.1 续

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| PF_NETROM | 业余无线电 Net-ROM | |
| PF_ATMUBRIDGE | 多协议网桥 | |
| PF_AIMCPVC | ATM PVCs | |
| PF_X25 | （保留用于 X.25 项目） <br><br> `#include <linux/x25.h>` | |
| PF_INET6 | IPv6 协议族 <br><br> `#include <linux/in6.h>` | `typedef struct {`<br>`char x25_addr[16];`<br>`} x25_address;`<br><br>`struct sockaddr_x25 {`<br>`sa_family_t x25_family;` /* X.121 family */<br>`x25_address x25_addr;`<br>`};`<br><br>`struct in6_addr`<br>`{`<br>`union {`<br>`__u8 in6_addr8[16];`<br>`__u16 in6_addr16[8];`<br>`__u32 in6_addr32[4];`<br>} __u32 in6_addr32[4];`<br>`#if ( < 0UL) _RELAX_IN6ADDR_ALIGNMENT`<br>/* 别名，协议不遵守`<br>`64 位对齐。rsvp/pim/... 是`<br>`损坏的。但是，如果`<br>`可能，强制正确的`<br>`对齐是个好主意。 */`<br>`#endif`<br>`__u64 in6_addr64[2];`<br>`};`<br>`#endif` |

*(注意：表格单元格包含混合的文本和代码块。X.25 和 INET6 行的“关联数据”列分别包含代码片段和注释。)*

![](img/2591af4bdf00a0f382331fc9481f785e_418_0.png)

![](img/2591af4bdf00a0f382331fc9481f785e_418_1.png)

