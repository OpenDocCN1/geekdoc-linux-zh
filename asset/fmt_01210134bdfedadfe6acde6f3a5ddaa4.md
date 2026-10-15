
```c
if ((skb == skb_share_check(skb, GFP_ATOMIC)) == NULL)
    goto out_of_mem;
```

如果一切正常，我们通过网络调用 `arp_process`。

```c
return NF_HOOK(NF_ARP, NF_ARP_IN, skb, dev, NULL, arp_process);
freeskb:
    free_skb(skb);
out_of_mem:
    return 0;
```

下一个函数 `arp_process` 同样实现在 `linux/net/ipv4/arp.c` 文件中，它处理所有的 ARP 请求数据包。它从底层数据包处理函数 `arp_recv` 调用。

```c
int arp_process(struct sk_buff *skb)
struct net_device *dev = skb->*dev;
struct in_device *in_dev = in_dev_get(dev);
```

`arp` 指向传入数据包中的 ARP 头部。

```c
struct arphdr *arp;
unsigned char *arp_ptr;
struct rtable *rt;
```

`sha` 指向源硬件地址，`tha` 指向目标硬件地址。

```c
unsigned char *sha, *tha;
```

`sip` 和 `tip` 用于 ARP 数据包中指定的源 IP 和目的 IP 地址。

```c
u32 sip, tip;
u16 dev_type = dev->dev_type;
int addr_type;
struct neighbour *n;
```

首先，我们验证接收数据包的接口使用了 ARP 协议，并且该数据包不是环回包。

```c
if (arp->hr_len != dev->addr_len ||
dev->flags & IFF_NOARP ||
skb->pkt_type == PACKET_OTHEROTHER ||
skb->pkt_type == PACKET_LOOPBACK ||
arp->pl_len != 4)
    goto freeskb;
```

接下来，我们确保传入的数据包不是共享的。如果另一个协议接收了该包并正在修改它，就会出现这种情况。这种情况不太可能，但可能。

```c
if ((skb == skb_share_check(skb, GFP_ATOMIC)) == NULL)
    goto out_of_mem;
```

如果一切正常，我们通过网络调用 `arp_process`。

```c
return NF_HOOK(NF_ARP, NF_ARP_IN, skb, dev, NULL, arp_process);
freeskb:
    free_skb(skb);
out_of_mem:
    return 0;
```

下一个函数 `arp_process` 同样实现在 `linux/net/ipv4/arp.c` 文件中，它处理所有的 ARP 请求数据包。它从底层数据包处理函数 `arp_recv` 调用。

```c
int arp_process(struct sk_buff *skb)
struct net_device *dev = skb->*dev;
struct in_device *in_dev = in_dev_get(dev);
```

`arp` 指向传入数据包中的 ARP 头部。

```c
struct arphdr *arp;
unsigned char *arp_ptr;
struct rtable *rt;
```

`sha` 指向源硬件地址，`tha` 指向目标硬件地址。

```c
unsigned char *sha, *tha;
```

`sip` 和 `tip` 用于 ARP 数据包中指定的源 IP 和目的 IP 地址。

```c
u32 sip, tip;
u16 dev_type = dev->dev_type;
int addr_type;
struct neighbour *n;
```

首先，我们验证接收数据包的接口使用了 ARP 协议，并且该数据包不是环回包。

```c
if (arp->hr_len != dev->addr_len ||
dev->flags & IFF_NOARP ||
skb->pkt_type == PACKET_OTHEROTHER ||
skb->pkt_type == PACKET_LOOPBACK ||
arp->pl_len != 4)
    goto freeskb;
```

接下来，我们确保传入的数据包不是共享的。如果另一个协议接收了该包并正在修改它，就会出现这种情况。这种情况不太可能，但可能。

```c
if ((skb == skb_share_check(skb, GFP_ATOMIC)) == NULL)
    goto out_of_mem;
```

如果一切正常，我们通过网络调用 `arp_process`。

```c
return NF_HOOK(NF_ARP, NF_ARP_IN, skb, dev, NULL, arp_process);
freeskb:
    free_skb(skb);
out_of_mem:
    return 0;
```

下一个函数 `arp_process` 同样实现在 `linux/net/ipv4/arp.c` 文件中，它处理所有的 ARP 请求数据包。它从底层数据包处理函数 `arp_recv` 调用。

```c
int arp_process(struct sk_buff *skb)
struct net_device *dev = skb->*dev;
struct in_device *in_dev = in_dev_get(dev);
```

`arp` 指向传入数据包中的 ARP 头部。

```c
struct arphdr *arp;
unsigned char *arp_ptr;
struct rtable *rt;
```

`sha` 指向源硬件地址，`tha` 指向目标硬件地址。

```c
unsigned char *sha, *tha;
```

`sip` 和 `tip` 用于 ARP 数据包中指定的源 IP 和目的 IP 地址。

```c
u32 sip, tip;
u16 dev_type = dev->dev_type;
int addr_type;
struct neighbour *n;
```

首先，我们验证接收数据包的接口使用了 ARP 协议，并且该数据包不是环回包。

```c
if (arp->hr_len != dev->addr_len ||
dev->flags & IFF_NOARP ||
skb->pkt_type == PACKET_OTHEROTHER ||
skb->pkt_type == PACKET_LOOPBACK ||
arp->pl_len != 4)
    goto freeskb;
```

接下来，我们确保传入的数据包不是共享的。如果另一个协议接收了该包并正在修改它，就会出现这种情况。这种情况不太可能，但可能。

```c
if ((skb == skb_share_check(skb, GFP_ATOMIC)) == NULL)
    goto out_of_mem;
```

如果一切正常，我们通过网络调用 `arp_process`。

```c
return NF_HOOK(NF_ARP, NF_ARP_IN, skb, dev, NULL, arp_process);
freeskb:
    free_skb(skb);
out_of_mem:
    return 0;
```

下一个函数 `arp_process` 同样实现在 `linux/net/ipv4/arp.c` 文件中，它处理所有的 ARP 请求数据包。它从底层数据包处理函数 `arp_recv` 调用。

```c
int arp_process(struct sk_buff *skb)
struct net_device *dev = skb->*dev;
struct in_device *in_dev = in_dev_get(dev);
```

`arp` 指向传入数据包中的 ARP 头部。

```c
struct arphdr *arp;
unsigned char *arp_ptr;
struct rtable *rt;
```

`sha` 指向源硬件地址，`tha` 指向目标硬件地址。

```c
unsigned char *sha, *tha;
```

`sip` 和 `tip` 用于 ARP 数据包中指定的源 IP 和目的 IP 地址。

```c
u32 sip, tip;
u16 dev_type = dev->dev_type;
int addr_type;
struct neighbour *n;
```

首先，我们验证接收数据包的接口使用了 ARP 协议，并且该数据包不是环回包。
