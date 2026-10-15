
# 570 组播 第 21 章

`mcast_join` 加入由 `grp` 指向的套接字地址结构所包含的 IP 地址且长度由 `grplen` 指定的任意源组播组。我们可以通过接口名称（一个非空的 `ifname`）或非零的接口索引（`ifindex`）来指定加入该组的接口。如果两者都未指定，内核将选择加入该组的接口。对于 IPv6，接口通过其索引指定给套接字选项。如果为 IPv6 套接字指定了名称，我们调用 `nametoindex` 来获取索引。对于 IPv4 选项，接口通过其单播地址指定。如果为 IPv4 套接字指定了名称，我们调用 `ioctl` 并带上 `SIOCGIFFADDR` 请求来获取接口的单播地址。如果为 IPv4 套接字指定了索引，我们首先调用 `_ifindextoname` 获取名称，然后按照描述的方式处理名称。

接口名称（无论是哪种）通常是用户指定接口的方式，而不是通过地址或索引。例如，`tcpdump` 是少数允许用户指定接口的程序之一，`-i` 选项接受接口名称作为参数。

`mcast_leave` 离开套接字规范中包含的组播组 IP 地址；注意 `mcast_leave` 不接受接口指定；它总是删除第一个匹配的成员身份。这是库的 API，但需要直接控制每个接口成员身份的程序需要使用 `setsockopt` API。

`mcast_block_source` 在指定的套接字上阻塞源，源和组 IP 地址分别包含在 `src` 和 `grp` 指向的套接字地址结构中，长度由 `srlen` 和 `grplen` 指定。对于给定的组，必须在该套接字上调用过 `mcast_join`。

`mcast_unblock_source` 解除从源到组的流量接收。`src`、`srlen`、`grp` 和 `grplen` 必须与之前的 `mcast_block_source` 调用相同。

`mcast_join_source_group` 加入特定源组，源和组 IP 地址分别包含在 `src` 和 `grp` 指向的套接字地址结构中，长度由 `srlen` 和 `grplen` 指定。我们可以通过接口名称（一个非空 `ifname`）或非零的接口索引（`ifindex`）来指定加入该组的接口。如果两者都未指定，内核将选择加入该组的接口。

`mcast_leave_source` 离开特定源组播组，源和组 IP 地址分别包含在 `src` 和 `grp` 指向的套接字地址结构中，长度由 `srlen` 和 `grplen` 指定。与 `mcast_leave` 不同，`mcast_leave_source` 不接受接口指定；它总是删除第一个匹配的成员身份。

`mcast_set_if` 设置传出组播数据报的默认接口索引。如果 `ifindex` 大于 0，则指定接口索引；否则，如果 `ifname` 为 `null`，则指定接口名称。对于 IPv6，名称使用 `_nametoindex` 映射到索引。对于 IPv4，从名称或索引到接口单播 IP 地址的映射是按照在 `mcast_join` 中描述的方式的方式完成的。

`mcast_set_loop` 将回环选项设置为 0 或 1，`mcast_set_ttl` 设置 IPv4 TTL 或 IPv6 跳数限制。三个 `mcast_get_XXX` 函数返回相应的值。

## 示例：mcast_join 函数

图 21.10 显示了我们的 `mcast_join` 函数的前三分之一。这展示了协议无关 API 可以有多么直观。

```c
#include "unp.h"
#include <net/if.h>

int mcast_join(int sockfd, const struct sockaddr *grp, socklen_t grplen,
const char *ifname, u_int ifindex)
{
    struct ip_req mreq;
    struct ifreq ifreq;

    if (ifindex > 0) {
        mreq.im_if = ifindex;
    } else if (ifname != NULL) {
        mreq.im_if = nametoindex(ifname);
        if (mreq.im_if == 0) {
            errno = ENOENT; /* interface not found */
            return (-1);
        }
    } else {
        mreq.im_if = 0;
    }

    if (grplen < sizeof(mreq)) {
        errno = EINVAL;
        return (-1);
    }

    memcpy(&mreq.im_multiaddr, (const struct sockaddr *)grp)->sin_addr,
           sizeof(struct in_addr));

    if (mreq.im_if == 0) {
        mreq.im_interface.s_addr = htonl(INADDR_ANY);
    } else {
        strncpy(ifreq.ifr_name, ifname, IFNAMSIZ);
        if (ioctl(sockfd, SIOCGIFFADDR, &ifreq) < 0)
            return (-1);
        mreq.im_interface.s_addr = ((struct sockaddr_in *)&ifreq.ifr_addr)->sin_addr;
    }

    return setsockopt(sockfd, IPPROTO_IP, IP_ADD_MEMBERSHIP,
        &mreq, sizeof(mreq));
}
```

### 复制地址

首先将 IPv6 组播地址从套接字地址结构复制到 `ipv6_mreq` 结构。

### 处理索引、名称或默认值

如果指定了索引，它将存储在 `ipv6mrq_interface` 中；如果指定了名称，则通过调用 `ifnametoindex` 获取索引；否则，`setsockopt` 会将接口索引设置为 0，告知内核选择接口。

加入该组。

```c
#ifdef IPv6
  case AF_INET6:
    struct ipv6_mreq mreq6;
    memcpy(&mreq6, ipv6_mr_multiaddr,
         &(const struct sockaddr_in6 *)grp)->sin6_addr,
         sizeof(struct in_addr));

    if (index > 0)
      ipv6_mr_interface = index;
    else if (ifname != NULL)
      if ((ipv6_mr_interface = ifnametoindex(ifname)) == 0)
        errno = ENOXIO; /* i/f name not found */
        return (-1);
    else
      mreq6.ipv6_mr_interface = 0;

    return (setsockopt(sockfd, addr, IPPROTO_IPV6, IPv6_JOIN_GROUP,
         &mreq6, sizeof(mreq6)));
  default:
    errno = EAFNOSUPPORT;
    return (-1);
#endif
```

![](img/1cc56227d30f6730abd74fbc5905c5ff_592_0.png)

## 示例：mcast_set_loop 函数

图 21.13 显示了我们的 `mcast_set_loop` 函数。由于参数是套接字描述符而非套接字地址结构，我们调用了 `sockfd_family` 函数来获取套接字的地址族。设置相应的套接字选项。

我们没有显示其余 `mcast_XXX` 函数的源代码，但可以免费获取（见前言）。
