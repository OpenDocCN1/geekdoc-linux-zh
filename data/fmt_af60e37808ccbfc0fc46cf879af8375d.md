
`Lastuse` 被设置为该条目被分配时的滴答数（ticks）。它表示缓存条目的年龄。`Expires` 是该缓存条目过期的时间。它被垃圾回收机制用于确定哪些条目是过期的。例如，当这些条目用于路由缓存时，`expires` 表明哪些路由已经过期。

```c
unsigned long   lastuse;
unsigned long   expires;
```

接两个字段用于 ICMP 协议的速率限制。

```c
unsigned long   rate_last;
unsigned long   rate_tokens;
int             error;
```

下一个字段 `neighbour` 是指向用于地址解析的邻居缓存条目的指针。关于邻居缓存的更多信息，参见第 6.8.4 节。如果不为 NULL，`hh` 指向该目的的硬件缓存。如果目的缓存条目是内部目的的数据包，则 `hh` 将为 NULL。对于输出数据包，`hh` 将用于获取链路层头部。

```c
struct neighbour   *neighbour;
struct hh_cache     *hh;
```

下一个字段 `xfrm_state` 指向安全策略数据库（SPD）的转换实例。

```c
struct xfrm_state   *xfrm;
```

接两个字段 `input` 和 `output` 指向在使用特定目的缓存条目处理数据包时调用的函数。`input` 是默认输入函数。当首次创建 `dst_entry` 时，该字段被初始化为 `dst_discard`。例如，对于用于本地消费的路由输入数据包的缓存目的，此字段指向 `function_ip_local`。`output` 是默认输出函数。如果 `hh` 和 `neighbour` 都为 NULL，协议的输出函数会调用此函数。当创建目的缓存时，`output` 被初始化为 `dst_blackhole`。例如，当目的缓存条目指示 IPv4 输出数据包被路由时，`output` 将指向 `ip_forward`。

```c
int (*input)(struct sk_buff *);
int (*output)(struct sk_buff *);
```

`Tclassid` 包含流量分类并用于流量整形。如果配置了基于类的路由选项，则定义该字段。

```c
#ifdef CONFIG_CLS_ROUTE
__u32             tclassid;
#endif
```

下一个字段 `ops` 是目的缓存的操作集。该结构在网络层协议初始化时进行初始化。例如，IPv4 在 `linux/ipv4/route.c` 中初始化 `dst_ops`。

```c
struct dst_ops      *ops;
struct rcu_head     rcu_head;
char                info[0];
```

尽管它有一个初始化函数，但目的缓存在作为 ARP 或 ND 使用时被实例化。初始化函数 `dst_init` 定义在 `linux/net/core/dst.c` 中。

```c
void __dst_init(void)
{
```

在该函数中所做的唯一是将目的缓存注册到网络设备通知器，这样当接口设备下线或断开时，目的缓存条目会自动移除。

```c
register_netdevice_notifier(&dst_dev_notifier);
```

通知器块 `dst_dev_notifier` 包含一个函数 `dst_dev_event`，该函数见第 6.8.3 节。

```c
struct notifier_block dst_dev_notifier = {
    dst_dev_event,
    NULL,
    0
};
```

## 6.8.2 目的操作结构 (Destination Operation structure)

目的结构包含指向目的缓存操作函数的指针。很大程度上通过它，目的缓存具有了 ARP 缓存或邻居发现缓存的特性。`dst_ops` 结构通过之前描述 `dst_entry` 中的 `ops` 字段访问。

```c
struct dst_ops
{
```

第一个字段 `family` 是此缓存条目的地址族，例如 `AF_INET`。下一个字段 `protocol` 与链路层头部协议值相同。例如，如果此条目用于 IP，`protocol` 将是 `ETH_P_IP`。

```c
unsigned short      family;
unsigned short      protocol;
```

`Gc_thresh` 是垃圾回收阈值。如果目的缓存条目是路由缓存条目的倍增，该字段等于路由缓存哈希表的大小加一。

```c
unsigned      gc_thresh;
```

`Gc` 是该条目的垃圾回收函数，通过检查该函数的指针来检查此缓存条目的有效性。

```c
int (*gc)(void);
struct dst_entry *(*check)(struct dst_entry *, __u32 cookie);
```

下一个字段 `destroy` 指向该条目的析构函数。

```c
void (*destroy)(struct dst_entry *);
```

下一个字段是负面建议指针函数 `negative_advice`，当我们收到直接 ICMP 包且否定了目的缓存中的此条目时，会调用该函数。`link_failure` 是指向一个函数的指针，由于链路中断导致之前良好的条目不再有效。

```c
struct dst_entry *(*negative_advice)(struct dst_entry *);
void (*link_failure)(struct sk_buff *);
void (*update_pmtu)(struct dst_entry *dst, __u32 mtu);
int (*get_mss)(struct dst_entry *dst, __u32 mtu);
```

`Entry_size` 是目的缓存的大小。`Entries` 包含特定目的缓存中的条目数量，并以原子方式递增或递减。`Kmem_cache` 是指向分配目的缓存条目的 slab 缓存的指针。

```c
int entry_size;
atomic_t entries;
kmem_cache_t *kmem_cachep;
```

### 6.8.3 目的缓存实用函数

与目的缓存相关的重要实用函数很少。其中一些是通用函数，用于操作在目的缓存创建时初始化的条目。这些函数定义在 `linux/net/core/dst.c` 文件。目的缓存条目通过 `dst_alloc` 分配。

```c
void *dst_alloc(struct dst_ops *ops)
```

在此函数中，我们分配了一个 `dst_entry` 结构实例。在大多数情况下，调用者会在编译时初始化一个 `dst_ops` 结构实例。然后，每次请求目的缓存条目时，我们都会收到一个指向 `dst_ops` 实例的指针。

```c
struct dst_entry *dst;
```

我们检查 `dst_ops` 中的 `entries` 是否大于垃圾回收阈值 `gc_thresh`。通过检查目的操作中的值，我们实际上是在检查特定于目的缓存用户的值。

```c
if ops->gc && atomic_read(&ops->thresh) > ops->gc_thresh {
```

如果超过阈值，将通过 `dst_ops` 的 `gc` 字段调用缓存垃圾回收函数。

```c
if (ops->gc())
    return NULL;
}
```

从 `dst_ops` 结构中 `kmem_cache` 指向的 slab 缓存分配条目。

```c
dst = kmem_cache_alloc(ops->kmem_cache, SLAB_ATOMIC);
if (!dst)
    return NULL;
memset(dst, 0, ops->entry_size);
atomic_set(&dst->refcnt, 0);
```

然后它将参数中的 `ops` 字段设置为 `dst_ops` 条目。它将 `lastuse` 设置为当前时间 `jiffies` 并原子地递增 `entries`。它将其设置为 `dst_discard` 并输出到 `dst_blackhole`。

```c
dst->ops = ops;
dst->lastuse = jiffies;
dst->path = dst;
dst->input = dst_discard;
dst->output = dst_blackhole;
#if RT_CACHE_DEBUG >= 2
    atomic_inc(&dst->total);
#endif
return dst;
```
