
```c
struct sockaddr {
    unsigned short sa_family;
    unsigned char sa_data[14];
};
#define UNIX_PATH_MAX 108
struct sockaddr_un {
    sa_family_t sun_family;
    char sun_path[UNIX_PATH_MAX];
};
struct sockaddr_in {
    sa_family_t sin_family;
    unsigned short sin_port;
    struct in_addr sin_addr;
    unsigned char pad[];
};
```

#### 表 A.1 续

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| `PF_AX25` | 业余无线电 `AX.25`<br><br>`#include <linux/AX25.h>` | `typedef struct {`<br>`char ax25_call[7];`<br>```} ax25_address; ```<br><br>`struct sockaddr_ax25 {`<br>`sa_family_t sax25_family;`<br>`ax25_address sax25_call;`<br>`ax25_address sax25_ndigis;`<br>`int ...;`<br>`};` |
| `PF_IPX` | `Novell` 互联网协议<br><br>`#include <linux/ipx.h>` | `struct sockaddr_ipx`<br>`{`<br>`sa_family_t sipx_family;`<br>`__u16 sipx_port;`<br>`__u32 sipx_network;`<br>`unsigned char sipx_node[IPX_NODE_LEN];`<br>`__u8 ...;`<br>`};`<br><br>`struct sockaddr_in_at {`<br>`unsigned char si...;`<br>`__u8 padding;`<br>`unsigned char si...;`<br>`};` |
| `PF_APPLETALK` | `Appletalk` `DDP`<br><br>`#include <linux/atalk.h>` | `struct sockaddr_at {`<br>`sa_family_t sat_family;`<br>`struct s_net {`<br>`u16 s_net;`<br>`__u8 ...;`<br>```} ...; ```<br>`struct s_node {`<br>`u16 s_addr;`<br>`sat_addr;`<br>`char sat_zero1[...]`<br>`};` |

#### 表 A.1 续

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| `PF_NETROM` | 业余无线电 `Net-ROM` | |
| `PF_ATMUBRIDGE` | 多协议网桥 | |
| `PF_AIMCPVC` | `ATM` `PVCs` | |
| `PF_X25` | （保留用于 `X.25` 项目）<br><br>`#include <linux/x25.h>` | |
| `PF_INET6` | `IPv6` 协议族<br><br>`#include <linux/in6.h>` | `typedef struct {`<br>`char x25_addr[16];`<br>`} x25_address;`<br><br>`struct sockaddr_x25 {`<br>`sa_family_t x25_family;` /* `X.121` family */<br>`x25_address x25_addr;`<br>`};`<br><br>`struct in6_addr`<br>`{`<br>`union {`<br>`__u8 in6_addr8[16];`<br>`__u16 in6_addr16[8];`<br>`__u32 in6_addr32[4];`<br>```} __u32 in6_addr32[4]; ```<br>`#if ( < 0UL) _RELAX_IN6ADDR_ALIGNMENT`<br>/* 别名，协议不遵守<br>`64` 位对齐。`rsvp/pim/...` 是<br>损坏的。但是，如果<br>可能，强制正确的<br>对齐是个好主意。 */<br>`#endif`<br>`__u64 in6_addr64[2];`<br>`};`<br>`#endif` |

*(注意：表格单元格包含混合的文本和代码块。`X.25` 和 `INET6` 行的“关联数据”列分别包含代码片段和注释。)*

![](img/2591af4bdf00a0f382331fc9481f785e_418_0.png)

![](img/2591af4bdf00a0f382331fc9481f785e_418_1.png)

#### 表 A.1 续

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| `PF_ROSE` | 业余无线电 `X.25` `PLP` | `#define s6_addr8 int6 u.u6_addr8`<br>`#define s6_addr16 int6 u.u6_addr16`<br>`#define s6_addr32 int6 u.u6_addr32`<br>`#define s6_addr64 int6 u.u6_addr64`<br>`};`<br>`#include <linux/rose.h>`<br>`struct sockaddr_rose {`<br>`    sa_family_t rose_family;`<br>`    rose_addr rose_addr;`<br>`    int ax25_addr rose_indig;`<br>`    ax25_addr rose_dig;`<br>`};`<br>`struct full_sockaddr_rose {`<br>`    sa_family_t rose_family;`<br>`    rose_addr rose_addr;`<br>`    ax25_addr rose_call;`<br>`};`<br>`struct sockaddr_int {`<br>`    unsigned short int sing_family;`<br>`    ___u32 sing_port;`<br>`    ___u32 sing_flowinfo;`<br>`    struct int6_addr sing_addr`<br>`};`<br>`typedef struct {`<br>`    char rose_addr[5];`<br>`} rose_address;` |
| `PF_DESIGN` | （保留用于 `DECint` 项目） | `unsigned int rose_ndigis;`<br>`ax25_address rose_digis[ROSE_MAX_DIGIS];` |
| `PF_NETBEUI` | （保留用于 `802.2LLC` 项目） | `#define NB_NAME_LEN 20`<br>`struct sockaddr_netbeui`<br>`{`<br>`    char sa_family;`<br>`    char nr_name[NB_NAME_LEN];`<br>`    char nr_devhint[FNAME1SZ];`<br>`};` |
| `PF_SECURITY` | 安全回调伪 `AF` | `struct sockaddr_n1`<br>`{`<br>`    sa_family_t nl_family;`<br>`    unsigned short nl_pad;`<br>`    u32 __32`<br>`    u32`<br>`};`<br>`struct sockaddr_pkt`<br>`{` |
| `PF_KEY` | `PF_KEY` 密钥管理 `API` | |
| `PF_NETLINK` | 用于模拟 `4.4BSD` 的消息 | `#include <linux/netlink.h>` |
| `PF_ROUTE` | | |
| `PF_PACKET` | 数据包族 | `#include <linux/netlink.h>`<br>`struct sockaddr_netbeui`<br>`{` |

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| `PF_ATMSVC` | `ATM` `SVCS` | `/* 控制/标志字节。 */` |
| `PF_SNA` | `Linux` `SNA` 项目 | `unsigned char cb;` |
| `PF_IRDA` | `IRDA` 套接字 | `unsigned char type;`<br>`#include <linux/irda.h>`<br>`struct eo_addr addr;`<br>`unsigned long cookie;`<br>`});`<br>`struct sockaddr_irda {`<br>`    sa_family_t sir_family;`<br>`    /* USAP/TSAP 选择器 */`<br>`    unsigned char sir_isap_sel;`<br>`    /* 设备地址 */`<br>`    unsigned int sir_addr;`<br>`    /* 通常为 <server:IRDALinTP *>`<br>`    char sir_name[25];`<br>`};` |

*注意：以下表格结构是根据第 `421-422` 页关于套接字结构和额外协议的碎片化数据重构的。*

| 类型 | 描述和示例 | 关联数据 |
| :--- | :--- | :--- |
| `PF_PACKET` | 数据包族 | `spkt_family; spkt_device[14]; spkt_protocol;`<br>`sill_family;`<br>`sill_protocol;`<br>`sill_index;`<br>`sill_nettype;`<br>`sill_pkttype;`<br>`sill_naten;`<br>`sill_addr[8];`<br>`struct sockaddr_ll {`<br>`    unsigned short`<br>`    unsigned short`<br>`    unsigned int`<br>`    unsigned short`<br>`    unsigned char`<br>`    unsigned char`<br>`    unsigned char`<br>`    unsigned char`<br>`};`<br>`struct ec_addr {`<br>`    /* 站点号。 */`<br>`    unsigned char station;`<br>`    /* 网络号。 */`<br>`    unsigned char net;`<br>`};`<br>`struct sockaddr_ec {`<br>`    unsigned short sec_family;`<br>`    unsigned char port;` |
| `PF_ECONET` | `Acorn` `Econet` | `#include <linux/if_econet.h>` |

## 类型：`socket()` 的第二个参数

第二个参数（`type`）选择协议层。表 A.2 中定义的一些常数仅仅是当内核支持该协议时的占位符。

### 表 A.2 `socket()` 调用中 `type` 参数的协议值

| 协议类型 | 描述 |
| :--- | :--- |
| `SOCK_STREAM` | (`TCP`) 可靠的流式双向通信。你可以在涉及 `FILE*` 类型的高级 `I/O` 函数调用中使用这种类型的套接字。该协议使用端口和专用客户端通道为你提供到网络的虚拟连接。连接后，`accept()` 调用返回一个专门用于新客户端的新套接字描述符。 |
| `SOCK_DGRAM` | (`UDP`) 不可靠的无连接通信。每个消息都是独立的，可能在传输过程中丢失。该协议使用端口虚拟化网络，允许你在不重新连接的情况下与许多对等方发送和接收消息。 |
| `SOCK_RAW` | (`IP`) 访问内部网络接口和字段。如果你想创建 `ICMP` 消息，你需要创建一个原始套接字。仅限 `Root` 访问。 |
| `SOCK_RDM` | (`RDM`—可靠交付消息) 确保每个数据包安全到达目的地，但不保证正确的数据包顺序。（尚未在 `Linux` 和其他 `UNIX` 操作系统中实现。） |
| `SOCK_SEQPACKET` | 有序、可靠的基于连接的固定长度数据报。（尚未在 `Linux` 中实现。） |
| `SOCK_PACKET` | (物理层) 将套接字置于混杂模式（如果可用），在那里它将接收网络上的任何和所有数据包。这是一个仅适用于 `Linux` 的工具。仅限 `Root` 访问。（已弃用—请改用 `PF_PACKET`。） |

## 协议定义

列表 A.1 摘自你的发行版中 `/etc/protocols` 文件 `[RFC2292]`。它包含网络数据包中使用的通用和标准协议标准。修改此文件*不是一个好主意*。

### 列表 A.1 `/etc/protocols` 文件

```
