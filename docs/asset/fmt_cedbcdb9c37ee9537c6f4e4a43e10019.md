
`cs 14.45. fib_rule`。

- `r_next`。指向内核维护的列表中的下一个 `fib_rule`。默认情况下，此列表有 local、main 和 default 规则。
- `r_clintref`。使用的规则的引用计数。
- `r_preference`。规则的优先级。系统中的三个默认规则（即 local、main 和 default）被分配了 `0xff`，local 具有最高优先级。用户可以使用 `ip` 命令为规则分配优先级，如果没有用户分配，则内核将分配最后添加规则的优先级。
- `r_table`。如果此规则应用于数据包，则是查找目的地的路由表。
- `r_action`。此字段包含策略动作，有五种策略动作：`RTN_UNICAST`、`RTN_NAT`、`RTN_REACHABLE`、`RTN_BLACKHOLE` 和 `RTN_FIB`。如果类型是 `RTN_UNICAST` 或 `RTN_NAT`，则匹配规则；否则返回错误。
- `r_dst_len` 和 `r_src_len`。代表位目的和源 IP 地址的长度。
- `r_src` 和 `r_srcmask`。源 IP 地址和掩码。
- `r_dst` 和 `r_dstmask`。目的 IP 地址和掩码。
- `r_flags`。目前未使用。
- `r_tos`。IP 头的 TOS 字段。
- `r_ifindex`。代表输出接口 ID。
- `r_ifname[IFNAMESZ]`。代表设备名称。
- `r_classid`。用于数据包队列的类队列，表示一个类 ID。
- `r_dead`。当规则可用时，该字段值为 0。

## 14.10 使用 ip 命令在路由表中添加新条目 (RT接口)

可以使用 RT Netlink 接口从用户空间更新路由表。关于 RT Netlink 如何工作的更多细节，请参见 netlink 章节（第 13 章）。在这里我们将看到 `ip` 命令的两个选项以及使用这些选项时调用的内核函数——即更新路由表和为新路由表添加新规则（策略）。

1. `ip route`
2. `ip route`

更多细节请参见 'ip command' 的 Linux 手册页。`net/ipv4/devinet.c` 中的 `inet_rtnetlink_table[]` 注册了以下函数：

- `inet_rtm_newroute()`
- `inet_rtm_delroute()`
- `inet_rtm_dump_fib()`

当从用户空间运行带 route 命令的添加、删除和显示路由表时会调用这些函数之一：

- `inet_rtm_newrule`
- `inet_rtm_delrule`
- `inet_rtm_dump_rules`

当从用户空间运行带 route 命令以向新或现有路由表添加新规则时，会调用这些函数之一。

### 14.10.1 当带 route 选项的 ip 命令在路由表中添加条目时发生了什么？

RT Netlink 接口使用 netlink 数据包与内核通信。当带有 'route add' 选项运行 `ip` 命令更新路由表时，用户空间创建一个 netlink 数据包；当此包到达内核时，会调用 `inet_rtnetlink_table` 中由 `RTM_NEWROUTE` 索引的 `doit` 函数（详情参见第 13 章），并调用函数 `inet_rtm_newroute()`。

### 14.10.2 `inet_rtm_newroute()`

向 FIB 添加新路由。传递给此函数的主要输入参数是 `sk_buff` 结构、netlink 头部 `msnlghdr` 结构以及指向可选数据（用户参数）的指针，其类型可以通过 `struct rattr` 转换为 FIB 内部接口 `struct kern_via`（关于 `struct rattr` 的更多细节，参见第 13 章）。

因此在第 369 行 (`cs 14.46`)，我们将可选参数指针分配给 `struct rattr`，在第 370 行，`NLMSG_DATA` 宏（关于 `NLMSG_DATA` 的更多细节参见第 13 章）带你进入 netlink 数据包中 `rtmessage` (`struct rtmmsg`) 的开头。在第 372 行，`check_attr()` 函数遍历可选参数并列出一个仅包含数据的参数数组：这随后被转换为 `kern_via`，这是一个 FIB 内部接口。然后在第 375 行调用函数 `fib_new_table()`，该函数为 `fib_table` 分配内存并通过调用函数 `fn_hash_init()` 初始化函数指针。最后在第 377 行，如果 `fib_new_table()` 返回了 `fib_table`，则会调用 `fn_hash_insert()`，因为 `tb->tb_fib` 在 `fn_hash_init()` 函数的 `fn_hash_init()` 中被初始化。

## 使用 ip 命令在路由表中添加条目 (RT NETLINK 接口)

```c
net/ipv4/fib_frontend.c

366 int inet_rtm_newroute(struct sk_buff *skb, struct nls_lmsghdr *nlh, void *arg)

367 {

368     struct fib_table *tb;

369     struct rtatrier **rta = arg;

370     struct rtmmsg *rm = NLMSG_DATA(nlh);

372     if (inet_check_attr(r, rta))

373         return -EINVAL;

375     tb = fib_new_table(r->rt_table);

376     if (tb)

377         return tb->insert(tb, r, (struct kern_rta*)rta, nlh, &NETLINK_CB(skb));

378     return -ENOMBUFS;

379 }
```

> `cs 14.47`, 函数 `inet_rtm_newroute` (

`fn_hash_insert` 向路由表中添加一个新条目。
这里是用户空间与内核之间用于添加路由条目或向路由表添加新规则交互的重要数据结构：

- 1. `struct rtmmsg`
- 2. `struct kern_rta`

### 14.10.3 `struct rtmmsg`

该结构用于表示通过命令行设置的用户参数，以便在路由表中添加新的路由条目 (`cs 14.47`)。
`rtm_family`。它包含了关于所支持的地址族的信息，例如 `AF_INET` (IP 协议)。

```c
include/linux/rtnetlink.h

83 struct rtmmsg

84 {

85     unsigned char  rtm_family;

86     unsigned char  rtm_dst_len;

87     unsigned char  rtm_src_len;

88     unsigned char  rtm_tos;

90     unsigned char  rtm_table;    /* 路由表 ID */

91     unsigned char  rtm_protocol; /* 路由协议，见下文 */

92     unsigned char  rtm_scope;    /* 见下文 */

93     unsigned char  rtm_type;     /* 见下文 */

95     unsigned int    rtm_flags;

96 };
```

> `cs 14.47`, `rtmmsg`.

`rtm_dst_len` 和 `rtm_src_len`。这代表了为 `AF_INET` 地址创建 32 位或更小的子掩码时使用的位数，适用于源地址和目的地址。

`rtm_tos`。这是 IP 头部中的 ToS（服务类型）字段。

`rtm_table`。它包含路由表 ID。

`rtm_protocol`。这指的是路由消息协议——例如 `RTPROTO_UNSPEC`、`RTPROTO_KERNEL` 等。

`rtm_scope`。这指的是路由消息范围——例如 `RT_SCOPE UNIVERSE` 等。

`rtm_type`。这指的是路由的类型——例如 `UNICAST`（单播）等。

`rtm_flags`。这三个值中的任何一个——`RTM_F_NOTIFY`——都会通知用户路由变化。

`RTM_F_CLONED`。该路由是克隆的。

`RTM_F_EQUALIZE`。该路由尚未实现。

### 14.10.4 `struct kern_rta`

该数据结构代表 FIB 内部值。当路由表发生更新时，它用于将值分配给 FIB 数据结构 (`cs 14.48`)。

`rta_dst`. . 这是目的地址。

`rta_src`. . 这是源地址。

```c
#include <net/ip_fib.h>

struct kern_rta {

    22 :

    void        *rta_dst;
```
