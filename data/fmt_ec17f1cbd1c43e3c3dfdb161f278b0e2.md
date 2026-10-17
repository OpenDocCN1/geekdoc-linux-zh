
```c
#ifdef CONFIG_IP_ROUTE_FWMARK

    (r->r_fmark && r->r_fmark != key->fmark) ||

#endif

    if (r->r_ifindex && r->r_ifindex == key->iif)

        continue;

}
```

当找到匹配的规则时，我们检查路由类型。如果是 `RTN_UNICAST` 或 `RTN_NAT`，我们就得到了有效值。否则，我们返回一个错误。

```c
FPprint("tb %d r %d\n", r->r_table, r->r_action);

switch (r->r_action) {

    case RTN_UNICAST:

    case RTN_NAT:

        policy = r;

        break;

    case RTN_UNREACHABLE:

        read_unlock(&fib_rules_lock);

        return -ENETUNREACH;

    default:

    case RTN_BLACKHOLE:
```

```c
read_unlock(&fib_rules_lock);

return -EINVAL;

case RTN_PROHIBIT:

    read_unlock(&fib_rules_lock);

    return -EACCES
}
```

现在我们获取用于匹配的 FIB 表 `r`。如果成功获取了表，我们就调用 FIB 表的查找函数，该函数会将 FIB 结果返回到 `res` 中。

```c
if (tb = fib_get_table(r->r_table) == NULL)
    continue;
    err = tb->tb_lookup(tb, flp, res);
```

如果我们正在寻找 NAT 路由，策略将指向 NAT 路由，因此我们更改 `res` 使其指向 NAT FIB 规则。这就是地址被重映射的原理，因为指向 `r` 的 FIB 规则将包含映射后的地址。

```c
if (err == 0) {
    res->r = policy;
    if (policy)
        atomic_inc(&policy->r_clntref);
    read_unlock(&fib_rules_lock);
    return 0;
}
if (err < 0 && err != -EAGAIN) {
    read_unlock(&fib_rules_lock);
    return err;
}
```

`prprintk("FAILURE \n");`
`read_unlock(&fib_rules_lock);`
`return -ENETREACH;`

下一个函数 `fib_select_default` 负责选择默认路由。
`void fib_select_default(const struct flow *flp, struct fib_result *res);`

这实际上通过 `fib_table` 中的函数指针调用了 `tb_select_default`。不过，首先，FIB 规则会检查几项内容。它确保路由类型为 `RT_UNICAST`，`res` 中的 FIB 结果关联了下一跳（网关），并且该网关是直接连接的。它知道网关连接在下一跳结构体的 `nh_scope` 字段中为 `RT_SCOPE_LINK`。如果满足所有这些条件，它将调用 `tb_select_default`；否则，直接返回。

## 9.6.3 FIB 初始化

IPv4 的 FIB 初始化由函数 `ip_fib_init` 完成，该函数定义在 `linux/net/ipv4/fib_frontend.c` 中。

```c
void __init ip_fib_init(void);
```

```c
{
```

如果配置了多个表，我们调用 `fib_rules_init` 来设置 RPDB 的规则部分。否则，我们为全局定义的两个表中的每个直接调用 `fib_hash_init`。

```c
#ifndef CONFIG_IP_MULTIPLE_TABLES
local_table = fib_hash_init(RT_TABLE_LOCAL);
main_table = fib_hash_init(RT_TABLE_MAIN);
#else
fib_rules_init();
#endif
```

接下来，我们在网络设备的通知机制（notifier facility）中注册自己。我们这样做是为了让自己放入网络接口状态发生变化时调用的函数链中。现在，当接口启动或关闭导致从 FIB 添加或删除路由时，我们就能收到通知。有关通知机制的更多信息，请参阅第 4 章“Linux 网络接口与设备驱动程序”。

```c
register_netdevice_notifier(&fib_netdev_notifier);
register_inetaddr_notifier(&fib_inetaddr_notifier);
```

特定 FIB 表的初始化由函数 `fib_hash_init` 完成，该函数定义在 `linux/ipv4/fib_hash.c` 中。根据是否定义了多个表，我们有两个不同的函数接口。

```c
#ifdef CONFIG_IP_MULTIPLE_TABLES
struct fib_table * fib_hash_init(int id)
#else
struct fib_table * __init fib_hash_init(int id)
#endif
{
```

该变量将指向新的 FIB 表。

```c
struct fib_table *tb;
```

我们做的第一件事是创建 FIB 缓存。这是一个 slab 缓存，`fib_node` 结构中的 FIB 条目将从中处分配。新的 `fib_table` 通过调用 `kmalloc` 分配。我们不需要为 `fib_table` 创建 slab 缓存，因为每个系统只有几个路由表。`fib_table` 至少有两个实例：`RT_TABLE_MAIN` 和 `RT_TABLE_LOCAL`。如果配置了内核选项 `CONFIG_IP_MULTIPLE_TABLES`，则会有更多的 `fib_table` 实例。

```c
if (fib_hash_kmem == NULL)
    fib_hash_kmem = kmem_cache_create("ip_fib_hash",
        struct fib_node,
        0, SLAB_HWCACHE_ALIGN,
        NULL, NULL);
```

```c
tb = kmalloc(sizeof(struct fib_table) + sizeof(struct fib_hash), GFP_KERNEL);
if (tb == NULL)
    return NULL;
```

现在我们初始化 `fib_table` 的字段。首先，`tb_id` 被设置为 FIB 表号。然后，设置操作函数。

```c
tb->tb_id = id;
```

接下来的六个操作函数将在本章的其他部分讨论。

```c
tb->tb_lookup = fib_hash_lookup
tb->tb_insert = fib_hash_insert
tb->tb_delete = fib_hash_delete
tb->tb_flush = fib_hash_flush
tb->tb_select_default = fib_hash_select_default
tb->tb_dump = fib_hash_dump;
```

每个 FIB 表条目中的信息包含在名为 `fib_node` 的结构中。`tb_data` 字段指向 `fib_node` 结构数组。

```c
memset(tb->tb_data, 0, sizeof(struct fib_node));
return tb;
```

## 9.6.4 FIB 应用程序接口

多个应用程序处理路由信息。需要访问和设置路由的应用程序示例包括 `zebra` 等路由守护进程。为了使用这些应用程序，Linux 提供了一个存储在 FIB 中的内核信息接口。通常在 Linux 中，当应用程序想要添加或删除路由时，会使用 `rtmsg` 结构并通过 `netlink` 套接字传递。`rtmsg` 结构在第 5 章“Sockets”中讨论过。`route.h` 中定义的结构是另一种检索并进入 FIB 的方式。该结构实际上不直接用于 FIB。在本节中，我们将使用 `netlink`，它是交换路由信息的一种。`rtentry` 结构通过 `ioctl` 调用 `SIOCADDRT` 和 `SIOCDELRT` 来添加和删除路由信息。

```c
struct rtentry {
    unsigned long rtlen;
```
