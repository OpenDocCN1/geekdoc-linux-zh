
该字段 `fib_presrc` 是首选源地址。它是 RFC 1122 作为 UDP 多宿主（multihoming）的一部分指定的“特定目的地址”。被 UDP 用作响应数据包的源地址。

```c
u32 fib_presrc;

u32 fib_priority;

unsigned fib_metrics[RTAX_MAX];

#define fib_mtu fib_metrics[RTAX_MTU-1]

#define fib_window fib_metrics[RTAX_WINDOW-1]

#define fib_rtt fib_metrics[RTAX_RTT-1]

#define fib_advmms fib_metrics[RTAX_ADVMSS-1];
```

`fib_nh` 是下一跳的数量。如果此路由定义了网关，则它应为1；否则为0。如果配置了多路径路由，它的值可以大于1。下一个字段 `fib_power` 仅在配置了多路径路由时使用。

```c
int fib_nh;
#ifdef CONFIG_IP_ROUTE_MULTIPATH
int fib_power;
#endif
```

`Fib_nh` 包含关于下一跳的信息，如果有多个下一跳，则包含下一跳列表。`fib_dev` 是用于向下一跳发送数据包的网络接口设备。

```c
struct fib_nh {
    struct fib_nh[0];
};
#define fib_dev fib_nh[0].nh_dev
```

下一个感兴趣的数据结构是 `fib_nh`，同样位于 `linux/include/net/ip_fib.h` 中。路由机制通过它来提取关于下一跳或网关机器的信息。

```c
struct fib_nh {
    struct net_device *nh_dev;
    unsigned nh_flags;
```

该字段 `nh_scope` 与流结构中的字段相似。它并没有真正定义路由的范围，而是与目的机器（在此情况下为网关机器）的概念性区别。

```c
unsigned char nh_scope;
#ifdef CONFIG_IP_ROUTE_MULTIPATH
int nh_weight;
int nh_power;
#endif
```

下一个字段是网关的流量分类标识符 `nh_tclass`。这与目的缓存条目中的 `tclassid` 类似，主要用于流量整形（traffic shaping）。

```c
#ifdef CONFIG_NET_CLS_ROUTE
__u32 nh_tclassid;
#endif
```

`nh_oif` 是到达网关机器将使用的输出接口索引号。

```c
int nh_oif;
u32 nh_gw;
};
```

## 9.6.2 FIB 规则

FIB 规则是 RPDB（路由策略数据库）的一部分，当 FIB 配置了多个表时它们最为有用。当配置了多个表时，实际上我们拥有了多个逻辑路由器，每个路由器由一个 FIB 表实例进行路由。在实际意义上，路由策略是选择其中一个路由表的一种。当我们配置了多个表时，我们仍然拥有默认表、包含本地地址的本地表以及包含路由信息的主表。然而，其他表是通过 FIB 规则进行访问的。

在本节中，我们展示了 `fib_rule` 数据结构以及如何使用 FIB 规则在两个“永久”默认路由表中进行选择。我们还展示了如何添加和删除 FIB 规则，以及如何创建一个新的路由表。

`fib_rule` 结构定义在源文件 `linux/net/ipv/fib_rules.c` 中。它不会从其他模块的函数直接访问。

```c
struct fib_rule {
```

FIB 规则通过 `r_next` 实现为链表。`r_clntref` 是引用计数，必须进行原子操作。

```c
struct fib_rule *r_next;
atomic_t *r_clntref;
```

下一个字段 `r_preference` 包含路由偏好，`r_table` 是该规则选择的 FIB 表索引。

```c
u32 r_preference;
unsigned char r_table;
```

该字段 `r_action` 与 `rtmsg` 结构中的路由类型值相同。这些值定义在第 9.1 节。

```c
unsigned char r_action;
unsigned char r_dst_len;
unsigned char r_src_len;
```

接下来两个字段是源地址及其掩码。

```c
u32 r_src;
u32 r_srcmask;
```

这两个字段是目的地址及其掩码。

```c
u32 r_dst;
u32 r_dstmask;
```

下一个字段 `r_srcmap` 包含源地址映射的地址。它用于地址转换规则。

```c
u32 r_srcmap;
u8 r_flags;
u8 r_tos;
#ifdef CONFIG_IP_ROUTE_FWMARK
u32 r_fwmark;
#endif
```

`r_ifindex` 是规则中使用的网络接口索引。

```c
int r_ifindex;
```

下一个字段是该规则的流量分类标识符。只有在内核配置了流量分类路由时才使用。

```c
#ifdef CONFIG_NET_CLS_ROUTE
u32 r_tclassid;
#endif
```

该字段 `r_ifname` 是网络接口设备的名称。

```c
char r_ifname[IFNAMESIZE];
int r_dead;
};
```

三个 `fib_rule` 实例用于选择每个“永久” FIB 表：主表、本地表以及指定的默认表。如果定义了新的 FIB 规则，它们将被添加到列表末尾。

这是默认表，编号 253。

```c
static struct fib_rule default_rule = {
  r_clntref: ATOMIC_INIT(2),
  r_preference: 0x7FF,
  r_table: RT_TABLE_DEFAULT,
  r_action: RTN_UNICAST,
};
```

这是主表，254。

```c
static struct fib_rule main_rule = {
  r_next: &default_rule,
  r_clntref: ATOMIC_INIT(2),
  r_preference: 0xFFE,
  r_table: RT_TABLE_MAIN,
  r_action: RTN_UNICAST,
};
```

这是本地表，255。

```c
static struct fib_rule local_rule = {
  r_next: &main_rule,
  r_clntref: ATOMIC_INIT(2),
  r_preference: 0x7FFF,
  r_table: RT_TABLE_LOCAL,
  r_action: RTN_UNICAST,
};
static struct fib_rule *fib_rules = &local_rule;
```

接下来，我们检查一些使用 FIB 数据库的函数。许多声明在 `linux/include/net/ip_fib.h` 中，定义在 `linux/net/ipv4/fib_rules.c` 中。第一个函数是 `fib_lookup`，其完整形式如下：

```c
int fib_lookup(const struct flowi *flp, struct fib_result *res)
{
    int err;
    struct fib_rule *r, *policy;
    struct fib_table *tb;
    u32 daddr = flp->fl4_dst;
    u32 saddr = flp->fl4_src;
    FPprint("Lookup: %u.%u.%u.%u < %u.%u.%u.%u\n",
           NIPQUAD(key->dst), NIPQUAD(flp->fl4_src));
    read_lock(&fib_rules));
```

我们搜索 FIB 规则寻找与源地址、目的地址、ToS（如果配置了 TOS 路由）以及网络接口设备密切匹配的规则。我们的目标是获取路由的缓存表。

```c
for (r = fib_rules; r = r->r_next) {
    if (((saddr&r->r_src) & &r->r_srcmask) ||
        (daddr&r->r_dst) & &r->r_dstmask) ||
    #ifdef CONFIG_IP_ROUTE_TOS
    (r->r_tos && r->r_tos == key->tos) ||
    #endif
```
