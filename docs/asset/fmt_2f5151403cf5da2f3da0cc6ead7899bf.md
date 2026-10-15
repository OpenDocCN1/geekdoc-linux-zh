
`sysctl`手页详细说明了可以使用此函数获取的所有各种系统信息：文件系统、虚拟内存、内核限制、硬件等信息。我们感兴趣的是网络子系统，通过将`name`数组的第一个元素设置为`CTL_NET`来指定。`CTL___`常量通过包含`<sys/sysctl.h>`来定义。第二个元素随后可以是

## 路由套字

- `AF_INET`：获取或设置影响 Internet 协议的变量。下一层使用`IPPROTO_xxx`常量之一来指定协议。BSD/OS 3.0 在此层提供了约 30 个变量，控制诸如如下功能：内核是否应该生成 ICMP 重定向、`TCP`是否应该使用 RFC 1323 选项、是否应该发送 UDP 校验和。我们在本节末尾展示了该`sysctl`的示例。

- `AF_LINK`：获取或设置链路层信息，例如 PPP 接口的数量。

- `AF_ROUTE`：返回有关路由表或接口列表的信息。我们稍后会描述这些信息。

- `AF_UNSPEC`：获取或设置某些 socket 层变量，例如 socket 或接收缓冲区的最大 own。

当`*name*`的第二个元素为`AF_ROUTE`时，第三个元素（协议号）为 0（因为`AF_ROUTE`族内没有协议，就像`AF_INET`族内那样），第四个元素是地址，第五和第六级指定要执行的操作。我们在图 17.12 中对其进行了总结。

| name[] | 返回 IPv4 路由表 | 返回 IPv4 ARP 缓存 | 返回接口列表 |
| --- | --- | --- | --- |
| 0 | `CTL_NET` | `CTL_NET` | `CTL_NET` |
| 1 | `AF_ROUTE` | `AF_ROUTE` | `AF_ROUTE` |
| 2 | 0 | 0 | 0 |
| 3 | `AF_INET` | `AF_INET` | `AF_INET` |
| 4 | `NET_RT_DUMP` | `NET_RT_FLAGS` | `NET_RT_IFFLIST` |
| 5 | 0 | `RTF_LLINFO` | 0 |

图 17.12 路由域返回的`sysctl`信息。

支持三种操作，通过包含`<sys/socket.h>`头文件定义的`*NET_RT_xxx*`常量来指定。这三种操作返回的信息通过调用`sysctl`时的`*oldp*`指针返回。该缓冲区包含数量数量的`RTM_xxx`消息（图 17.2）。

- 1. `NET_RT_DUMP`返回由`*name[3]*`指定的地址族的路由表。如果此地址为 0，则返回所有地址族的路由表。

  路由表以数量数量的`RTM_GET`消息返回，每条消息后跟多多四个 socket 地址条目：路由表条目的目的地、网关、网络掩码和克隆掩码。我们在图 17.5 的右侧展示了这些消息之一，并在图 17.7 的代码中解析了其中一条消息。通过此此`sysctl`操作进行的所有更改都是将一个或多个此类消息返回给内核。

- 2. `NET_RT_FLAGS`返回由`*name[3]*`指定的地址族的路由表，但仅返回`RTF_xxx`标志值包含`*name[5]*`所指定的标志的路由条目。路由表中所有的 ARP 缓存条目都设置了返回的`RTF_LLINFO`标志位。

  信息的返回格式与上一项相同。

- 3. `NET_RT_IFLIST`返回所有已配置接口的信息。如果`*name[5]*`非零，则它是一个接口索引号，只返回该接口的信息。（我们在第 17.6 节中详细介绍了接口索引。）分配给每个接口的地址也会返回，如果`*name[3]*`非零，则只返回该地址族的地址。每个接口返回一个`RTM_IFINFO`消息，随后是对应每个地址的`RTM_NEWADDR`消息。`RTM_IFINFO`消息后面跟着三个 socket 地址结构：接口地址、网络掩码和广播地址。我们在图 17.13 中展示了这两个消息。

```c
buffer returned by kernel

if_msghdr() {
    if_type = RTM_IFINFO ) // 每个接口:
        interface name, index,
        and hardware address
    datalink
        socket
        address
        structure;
}

ifs_msghdr() {
    ifam_type = RTM_NEWADDR
    netmask
        socket
        structure; // 每个地址
            configured for
    broadcast
        socket
        structure
}
```

## 17.5 get_ifi_info 函数

我们现在回到第 16.6 节的示例，该示例通过返回`ifi_info`结构体的链表来返回所有已启动的接口（图 16.5）。`prifno`程序保持不变（图 16.6），但我们现在展示`get_ifi_info`函数的一个版本，它使用`sysctl`代替了第 16.7 节中使用的`SIOCGIFCONF`。

我们首先在图 17.15 中显示函数`get_rt_ifilist`。该函数调用带有`NET_RT_IFLIST`命令的`sysctl`来返回指定地址族的接口列表。

```c
#1 #include "unproute.h"
2 char *flags = flags;
3 int net_rt_ifilist(int family, int flags, size_t *lenp)
4 {
5     int mib[6];
6     char *buf;
7     mib[0] = NET_RT;
8     mib[1] = AF_ROUTE;
9     mib[2] = 0;
10    mib[3] = family; /* only addresses of this family */
11    mib[4] = NET_RT_IFLIST;
12    mib[5] = flags; /* interface index, or 0 */
13    if (sysctl(mib, 6, NULL, lenp, 0) < 0)
14        return (NULL);
15    if ((buf = malloc(*lenp)) == NULL)
16        return (NULL);
17    if (sysctl(mib, 6, buf, lenp, NULL, 0) < 0)
18        free(buf);
19        return (NULL);
20    }
21    return (buf);
22 }
```

图 17.15 调用`sysctl`返回接口列表。

7-14 数组`mid`由第 17.12 节初始化，以返回指定族的接口列表和所有配置地址。`sysctl`被调用了两次。在第一次调用中，第三个参数为`null`，它返回`len`指向的变量，即存储所有信息所需的缓冲区大小。

15-21 然后为缓冲区分配空间并再次调用`sysctl-2`，这次第三个参数为`null`。`len`指向的变量在返回时将包含缓冲区中存储的信息量，该变量由调用者分配。还会返回一个缓冲区指针给调用者。

> 由于路由表的大小或接口的数量在两次调用`sysctl`之间发生变化，因此第一次调用返回的值包含一个 10% 的余量因子（见 TCP2 第 639–640 页）。

图 17.16 显示了`get_ifi_info`函数的前半部分。
