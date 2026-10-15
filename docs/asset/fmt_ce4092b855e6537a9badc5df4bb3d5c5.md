
下一次调用时为 1，意味着第一个参数指向广播地址。随后我们将 `IFI_ALIAS` 标志传递给我们的 `bind_XXX` 函数，让每个函数决定如何处理地址，正如我们很快将看到的。

## 加入多播组

如果接口支持，我们为每个单播地址调用我们的 `bind_mcast` 函数，因为我们想在每个接口上加入多播组。

# SNTP (续)

## 绑定通配符地址

在处理所有接口信息后，我们分配另一个 socket 结构体，并从 `udp_client` 填充的内容复制其。随后我们调用 `sock_set_wild` 函数在结构体中存储适当的通配符地址。`bind_ucast` 创建 socket 并通配符地址绑定到它。这处理了到达某些其他地址（例如 255.255.255，我们无法绑定它）的数据报。

## 初始请求和读取回复

`ntp` 向所有支持广播的接口发送 SNTP 请求，并从所有支持多播的接口通过多播发送 SNTP 请求。`read_loop` 随后读取这些请求的回复，以及收到的任何未来广播或多播包。

图 19.23 显示了将为我们的主机创建的 socket。回想图 16，主机是一个具有两个以太网接口的路由器。图 16 之后的示例中的接口及其它们的单播和广播地址现在假设没有别名地址。我们将创建新的 socket 并绑定九次相同的端口。

![](img/aeda3be9ee318bedd42850d461da0f28_522_0.png)

图 19.23 我们的 SNTP 客户端在主机上创建的 socket。我们将 socket 标记为 u、h 或 m，如果该 socket 具有单播地址、广播地址或多播地址。我们显示了将在每个 socket 上收到的数据包的目的 IP 地址，并注意绑定到 0.0.0.0 的 socket 可以接收发往任何地址（如 255.255.255）的数据包。

我们的 `bind_ucast` 函数创建 socket 并通配符地址绑定到它。这处理了到达某些其他地址（例如 255.255.255，我们无法绑定它）的数据报。

多播

# 第 19 章

```c
#include "ntp.h"

void
bind_ucast(struct sockaddr *sabind, socklen_t salen, int port,
            int alias, int bcast)
{
    int i, fd;
    /* 检查是否已经绑定此地址 */
    for (i = 0; i < naddrs; i++) {
        if (sock_cmp(addrs[i].sa, salen) == 0)
            return;
    }

    fd = socket(sabind->family, SOCK_DGRAM, 0);
    setsockopt(fd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));
    printf("binding %s\n", sock_ntop(sabind, salen));
    if (bind(fd, sabind, salen) < 0) {
        if (errno == EADDRINUSE)
            printf("address in use\n");
        close(fd);
        return;
    } else {
        err_sys("bind error");
    }
    addrs[naddrs].sa = sabind; /* 保存 sockaddr 指针 */
    addrs[naddrs].salen = salen;
    addrs[naddrs].fd = fd;
    if (bcast)
        addrs[naddrs].flags = ADDR_BCAST;
    naddrs++;
}
```

图 19.24 `bind_ucast` 函数：为单播或广播地址创建 socket。

## 地址已绑定

我们首先检查此地址是否已经绑定。对于单播地址这不会发生，对于共享相同广播地址的别名，我们只绑定广播地址。

## 创建 socket 并绑定地址

我们创建一个 UDP socket、端口并设置 `SO_REUSEADDR` 选项（因为我们要为每个地址绑定相同的端口）。我们将地址绑定到 socket。在其中存储绑定端口的 socket 地址结构体是由 `get_ifi_info` 返回的。我们允许绑定失败，这只有当 NTP 守护进程在此主机上运行时才会发生。

## 保存此 socket 的信息

信息保存在我们的 `Addrs` 结构体中，如果此绑定地址是广播地址。

对于多播接口，我们需要创建一个 socket、已知端口并在接口上加入多播组。这是通过我们的 `bind_mcast` 函数实现的，见图 19.25。

```c
#include "ntp.h"
void
bind_mcast(const char *ifname, struct sockaddr *mcastsa, socklen_t salen, int alias)
{
#ifdef MCAST
    int fd;
    struct sockaddr *msa;
    if (alias) {
        return;
    }
#endif
    /* 每个接口只加入一次多播 */
    printf("joining %s on %s\n", sock_ntop(mcastsa, salen), ifname);
    fd = socket(SOCK_DGRAM, 0);
    setsockopt(fd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on));
    bind(fd, mcastsa, salen);
    mcast_join(fd, mcastsa, salen, ifname);
    addrs[naddrs].sa = mcastsa;
    addrs[naddrs].salen = salen;
    addrs[naddrs].ifname = ifname; /* 保存指针，不是字符串拷贝 */
    addrs[naddrs].fd = fd;
    addrs[naddrs].flags = ADDR_MCAST;
    naddrs++;
#endif
}
```

> 图 19.25 `bind_mcast` 函数：在接口上加入多播组。

# 第 19 章：组播

`addr_ifname` 指向 `ifi_info` 结构体中接口名称字符串的指针，这是好的，因为我们的 `free_ifi_info` 函数从未被调用来释放这块内存。

下一个函数是 `sntp_send`，如图 19.26 所示，它在所有接口信息处理完毕且所有 socket 都创建后由 `main` 函数调用。
