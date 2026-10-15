
```c
#include <sys/param.h>
#include <sys/sysctl.h>

sysctl(int *name, u_int namelen, void *oldp, size_t *oldlen,
       void *newp, size_t newlen);
返回值：如果成功返回 0，错误返回 -1
```

此函数使用一个类似于 SNMP 管理信息库（MIB）名称的数组。TCP1 第 25 节详细讨论了 SNMP 及其 MIB。这些名称是分级结构的。

参数是一个整数数组，用于指定`*name*`，而`*namelen*`指定数组中的元素个数。数组中的第一个元素指定请求指向内核的哪个子系统。第二个元素指定该子系统的一部分，依此类推。图 18.11 显示了这种分级结构，其中前三级使用了一些常量。

![](![](img/1cc56227d30f6730abd74fbc5905c5ff_519_0.png)

图 18.11 `sysctl` 名称的分级结构。

要获取值，`*oldp*`指向一个缓冲区，内核将值存储在其中。`*oldlen*`是一个输入/输出参数：当调用该函数时，`*oldlen*`指向的值指定此缓冲区的大小，返回时，该值包含存储在缓冲区中的数据量。如果缓冲区不够，则返回 `ENOMEM`。作为一种特殊情况，`*oldp*`可以是空指针而`*oldlen*`是非空指针，内核可以确定本应返回多少数据，并通过`*oldlen*`返回此大小。

要设置一个新值，`*newp*`指向一个大小为`*newlen*`的缓冲区。如果没有指定新值，`*newp*`应为空指针，且`*newlen*`应为 0。

`*sysctl*`1) 手页详细列出了可以使用此函数获取的所有各种系统信息：文件系统、虚拟内存、内核限制、硬件等信息。我们感兴趣的是网络子系统，由以下指定：

路由表以变数量的 `RTM_GET` 消息返回，每条消息后跟多达四个套接字结构：路由表条目的目的、网关、网络掩码和克隆掩码。我们在图 18.5 的右侧展示了这些消息之一，并在图 18.7 的代码解析了其中一条消息。通过此 `sysctl` 操作的所有更改都是由内核返回的一个或多个此类消息实现的。

- 2. `NET_RT_FLAGS` 返回由 `name[3]` 指定地址族的路由表，但仅返回 `RTF_XXX` 标志值包含 `name[5]` 中指定标志的路由表条目。路由表中的所有 ARP 缓存条目都设置了 `RTF_LLINFO` 位。

返回信息的格式与上一个项目相同。

- 3. `NET_RT_IFLIST` 返回所有已配置接口的信息。如果 `name [5]` 不零，则它是一个索引号，仅返回该接口的信息。（我们将在第 18.6 节中详细介绍接口索引）。还会返回每个接口的所有地址，如果 `name [3]` 不零，则只返回该地址族的地址。

对于每个接口，会返回一个 `RTM_IFINFO` 消息，随后是分配给该接口的每个地址的 `RTM_NEWADR` 消息。`RTM_IFINFO` 消息之后是一个链路栈地址结构，`RTM_NEWADR` 消息之后是多达三个套接字地址结构：网络掩码和广播地址。这两条消息如图 18.14 所示。

# 示例：确定是否启用了 UDP 校验

我们提供了一个使用 Internet 协议的 `sysctl` 简单示例，用于检查是否启用了 UDP 校验。某些 UDP 应用（例如 BIND）在启动时会检查 UDP 校验是否启用，并尝试在它们运行时启用。通常情况下，启用此类功能需要超级用户权限，但我们现在只需检查该功能是否启用。图 18.3 是我们的程序。

```c
#include "unroute.h"
#include <netinet/udp.h>
#include <netinet/ip_var.h>
#include <netinet/udp_var.h> /* 用于 UDPCTL_xxx 常量 */

int
main(int argc, char **argv)
{
    int mib[4], val;
    size_t len;
    mib[0] = CTL_NET;
    mib[1] = AF_INET;
    mib[2] = IPPROTO_UDP;
    mib[3] = UDPCTL_CHECKSUM;

    len = sizeof(int);
    sysctl(mib, 4, &len, NULL, 0);
    printf("*udp checksum flag: %d\n", val);

    exit(0);
}
```

图 18.13 检查是否启用了 UDP 校验。

# 18.4 节

# sysctl 操作 499

```c
if_msghdr() {
    ifm_type = RTM_INFO
}
ifa_msghdr() {
    ifam_type = RTM_NEWADDR
}
```

| 结构名称 | 描述 |

| :--- | :--- |

| if_msghdr() | 链路套接字结构，每个接口一个 |

| ifa_msghdr() | 套接字结构，每个地址一个 |

| | 接口名称、索引、掩码、广播地址 |

图 18.14 用于 `sysctl`, `CTL_NET`, `NET_RT_IFLIST` 命令的信息。

- 包含头文件：必须包含 `<netinet/udp_var.h>` 以获取 `sysctl` 常量。

- 调用 `sysctl`：我们分配一个四个元素的整数数组，对应图 18.11 所示的分级结构。由于我们只是填充变量而不是设置新值，对 `sysctl` 的 `newp` 参数指定空指针，对 `newlen` 指定 0。`oldp` 指向存储结果的整数变量，`oldlen` 指向该整数的大小。该标志将为 0（禁用）或 1（已启用）。

# 18.5 get_ifi_info 函数（重温）

我们现在返回第 17.6 节的示例：以 `if_info` 结构链的形式返回所有开启的接口（图 17.5）。程序保持不变（ 17.6），我们现在显示使用 `sysctl` 代替图 17.7 中 `ioctl` 的 `get_ifi_info` 版本。我们首先在图 18.15 中显示如何解析 `net_rt_iflist`。

```c
#include "unroute.h"
char *net_rt_iflist(int family, int flags, size_t *len) {
    int mib[6];
    char *buf;
    mib[0] = CTL_NET;
    mib[1] = AF_ROUTE;
    mib[2] = 0;
    mib[3] = family;      /* 该族的地址 */
    mib[4] = NET_RT_IFLIST;
    mib[5] = flags;       /* 接口索引或 0 */
    if (sysctl(mib, 6, NULL, len, 0) < 0)
        return (NULL);

    if ((buf = malloc(*len)) == NULL)
        return (NULL);
    if (sysctl(mib, 6, buf, len) < 0)
        free(buf);

    return (buf);
}
```

图 18.5 调用 `sysctl` 返回接口列表。

`mib` 数组初始化如图 18.12 所示，以返回指定族的所有配置地址的接口列表。然后调用两次 `sysctl`。在第一次调用中，第三个参数为空，它返回 `llen` 所向变量容纳所有接口所需的缓冲区大小。然后为缓冲区分配空间并再次调用 `sysctl`，这次使用非空第三参数。`llen` 指向的变量将返回缓冲区中的数据，该变量由调用者分配。缓冲区也返回给调用者。

由于路由表的大小或接口的数量在两次 `sysctl` 调用之间可能会变化，第一次调用返回的值包含 10% 的余量因子（TCP2 第 639–640 页）。

图 18.16 显示了 `get_ifi_info` 函数的前半部分。
