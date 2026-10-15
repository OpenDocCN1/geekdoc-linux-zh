
该函数使用了类似于 SNMP 管理信息库（MIB）名称的名称。`TCPv1` 的第 25 章详细讨论了 SNMP 及其 MIB。这些名称是分级结构。

然后 `name` 是一个整数数组，用于指定名称，`namelen` 指定数组中的元素数量。数组的第一个元素指定子系统，第二个元素指定族（family），第三个元素指定协议，第四个元素指定选项（options），第五个元素指定标志（flags），第六个元素指定域（domain）。图 18.11 显示了分级结构。

要获取值，`oldp` 指向一个缓冲区。如果缓冲区不够大，内核返回 `ENOMEM`。要设置值，`newp` 指向一个缓冲区。如果没有指定地址，`oldlen` 为零。这些操作返回的信息通过 `done` 指针返回。此 `sysctl` 操作的所有更改都是内核返回了一个或多个此类消息。

# 图 18.11 sysctl 的分级结构。
(image: 6a7f209d-1433-4b6e-91c4-d84be676f7a2_0.png)

通过 `name[4]` 支持三种操作（`NET_RT_xxx` 常量通过包含 `<sys/route.h>` 定义）。这些操作返回的信息通过 `sysctl` 中的 `done` 指针返回。

- 1. `NET_RT_DUMP` 返回指定地址族的路由表。如果该地址为 0，则返回所有地址族的路由表。

路由表以数量不等的 `RTM_GET` 消息返回，每条消息后跟着四个结构：目标、网关、网络掩码和路由表的掩码。我们在图 18.5 的右侧展示了这些消息之一，图 18.7 中的代码解析了其中之一。

- 2. `NET_RT_FLAGS` 返回指定地址族的路由表，但仅返回 `RTF_xxx` 标志值包含 `name[5]` 的路由条目。路由表中所有的 ARP 条目都设置了 `RT_LLINFO` 标志。

格式与前一项相同。

- 3. `NET_RT_IFLIST` 返回所有配置接口的信息。如果 `name[5]` 非零，则是一个接口索引并返回该接口的信息（我们将在第 18.6 节中详细介绍接口索引）。还会返回分配给每个接口的所有地址，如果 `name[3]` 非零，则只返回该族的地址。）

# 图 18.12 路由返回的 sysctl 信息。

通过数据链路套接字地址结构，每个 `RTM_NEWADDR` 消息都跟随着多达三个套接字地址结构：接口地址、网络掩码和广播地址。这两个消息如图 18.14 所示。

## 示例：确定 UDP 校验和是否启用

我们提供了一个使用 `sysctl` 结合 Internet 协议栈的简单示例，用于检查是否启用了 UDP 校验和。某些 UDP 应用（例如 `BIND`）在启动时会检查 UDP 校验和是否启用，如果它们尝试启用这些功能的话。自然而易见，启用此类这样的功能需要超级用户权限，但我们现在做的是检查该功能是否已启用。图 18.13 是我们的程序。

### 18.13 检查 UDP 校验和是否启用。

`route/checkchecksum.c`

```
1 #include "unproute.h"

2 #include <netinet/udp.h>

3 #include <netinet/ip_var.h>

4 #include <netinet/udp_var.h> /* 用于 UDPCTL_xxx 常量 */

5 int

6 main(int argc, char **argv)

7 {

8 int mib[4], val;

9 size_t len;

10 mib[0] = CTL_NET;

11 mib[1] = AF_INET;

12 mib[2] = IPPROTO_UDP;

13 mib[3] = UDPCTL_CHECKSUM;

14 len = sizeof(val);

15 Sysctl(mib, 4, &val, &len, NULL, 0);

16 printf("udp checksum flag: %d\n", val);

17 exit(0);

18 }
```

> 图 18.14. `sysctl`, `CTL_NET`, `NET_RT_IFLIST` 命令返回的信息。

| 内核返回的缓冲区 | |
| :--- | :--- |
| `if_msghdr{}` | `ifm_type = RTM_IFINFO` | 每个接口一个：接口名称、索引和硬件地址 |
| 数据链路套接字地址结构 | |
| `ifam_msghdr{}` | `ifam_type = RTM_NEWADDR` | |
| 网络掩码套接字地址结构 | 每个接口配置的地址返回一个 |
| 单播地址套接字地址结构 | |
| 广播地址套接字地址结构 | |

## 包含系统头文件

2-4 我们必须包含 `<netinet/udp_var.h>` 头文件以获取 UDP `sysctl` 常量的定义。另外两个头文件是该头文件必需的。

## 调用 sysctl

10-16 我们分配了一个带有四个元素的整数数组，并存储与图 18.11 中的层次结构对应的常量。由于我们只是获取一个变量而不是设置新值，因此我们为 `sysctl` 的 `newp` 参数指定了空指针，并将 `newlen` 参数指定为 0。`oldp` 指向我们的整数变量，结果存储在其中；`oldlenp` 指向一个用于该整数大小的值-结果变量。我们打印的标志将是 0（禁用）或 1（启用）。

## 18.5 get_ifi_info 函数（重回顾）

我们回到第 17.6 节的示例：以 `if_info` 结构体链表的形式返回所有已使用的接口（图 17.5）。`printf` 程序保持不变（图 17.6），但我们现在展示一个 `get_ifi_info` 函数的版本，它使用 `sysctl` 而不是图 17.7 中使用的 `SIOCGIFFICTL`。

我们首先在图 18.15 中显示 `net_rt_iflist` 函数。该函数调用带有 `NET_RT_IFLIST` 命令的 `sysctl`，以返回指定地址族的接口。

## 图 18.15 调用 sysctl 返回接口列表。

```
#include "unproute.h"

char *

int net_rt_iflist(int family, int flags, size_t *lenp)

{

    int mib[6];

    char *buf;

    mib[0] = CTL_NET;

    mib[1] = AF_ROUTE;

    mib[2] = 0;

    mib[3] = family; /* 仅此此族的地址 */

    mib[4] = NET_RT_IFLIST; /* 接口索引或 0 */

    mib[5] = flags;

    if (sysctl(mib, 6, NULL, lenp, NULL, 0) < 0)

        return (NULL);

    if ((buf = malloc(*lenp)) == NULL)

        return (NULL);

    if (sysctl(mib, 6, buf, lenp, NULL, 0) < 0)

        free(buf);

        return (NULL);

    return (buf);

}
```

7-14 数组 `mib` 初始化如图 18.12 所示，以返回接口列表和指定接口的所有配置地址。`sysctl` 第一次调用时第三个参数为空，以返回接口列表所需的大小。15-21 为缓冲区分配空间并再次调用 `sysctl`，此时使用非空第三个参数。`sysctl` 返回的缓冲区包含了接口信息。在 `sysctl` 的两次调用之间，`ifi_info` 结构可能会变化。调用者通过第一次 `sysctl` 填充的 `ifi_info` （v2 版本）。图 18.16 显示了 `ifi_info` 函数的前半部分。

## 18.16 ifi_info 函数的前半部分。

```c
struct if_info
ifi_info(int family, int flags)
{
    int lim;
    char *buf, *next;
    size_t len;
    struct if_msghdr *ifm;
    struct ifam_msghdr *ifam;
    struct sockaddr *sa, *rti_info;
    struct sockaddr_dl *sdl;
    struct if_info *ifi, ifhead, *ifnext;
    buf = net_rt_iflist(family, 0, &len);
    ifnext = NULL;
    ifnext = &ifhead;
    lim = buf + len;
    for (next = buf; next < len; next += sizeof) {
        ifm = (struct if_msghdr *)next;
        if (!(ifm->ifm_ &_FF__))
```
