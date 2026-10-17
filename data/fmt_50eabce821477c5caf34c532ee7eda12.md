
```c
925  return skb;
```

```c
net/sched/sch_cbq.c

cbq_dequeue_prio( ) cont ...

927  skip_class:
      if (cl->q->q.qlen == 0 || prio != cl->cpriority) {

943    q->active[prio] = NULL;

944    q->activemask &= ~(1<<prio);
```

```c
net/sched/sch_cbq.c

cbq_dequeue_prio() cont ...

958    next_class:
959        cl_prev = cl;
960        cl = cl->next_alive;
961    } while (cl_prev != cl_tail);
962    } while (deficit);

965    break;
966    return NULL;
967 }
```

```c
net/sched/sch_cbq.c

cbq_dequeue() cont ...

1044    if (q->toplevel == TC_CBQ_MAXLEVEL &&
1045        PSCHED_PERFECT(q->link_update))
1046        break;
1048    q->toplevel = TC_CBQ_MAXLEVEL;
1049        PSCHED_PERFECT(q->link_update);
1050 }

1055    if (sch->q_len) {
1056        sch->stats_overlimit++;
1057        if (q->wd_expires && !queue_stopped(sch->dev)) {
1058            long delay = PSCHED_JIFFIES(q->wd_expires);
1059            del_timer(&q->wd_timer);
1062        q->wd_expires = jiffies + delay;
1063        add_timer(&q->wd_timer);
1065        sch->flags |= TC_CBQ;
1067    return NULL;
```

# NETFILTER 框架

```c
net/core/netfilter.c

41 #define NF_IP_PRE_ROUTING 0
43 #define NF_IP_LOCAL_IN 1
45 #define NF_IP_FORWARD 2
47 #define NF_IP_LOCAL_OUT 3
49 #define NF_IP_POST_ROUTING 4
50 #define NF_IP_NUMHOOKS 5
```

cs 16.3. Netfilter 钩子编号。

每个钩子（hook）都对应数据包在穿越协议栈时的一个检查点点（cs 16.3）。

`NF_IP_PRE_ROUTING`。这是一个用于 NAT/IP地址伪装（masquerading）的防火墙钩子。在入站数据包路由之前，如果对连接应用了地址伪装，我们需要修改其目标地址（注：原文为destination，但根据NAT 逻辑通常指修改源地址），否则我们可能会将数据包传递到本地。如果规则不允许我们操作，或者我们没有找到该包的任何转换，则应该丢弃请求。这实际上是针对第一个包执行的，其结果将用于连接的后续包。不仅是 NAT/伪装，IPsec 模块也可以在此钩子处进行处理。

`NF_IP_POST_ROUTING`。这是一个用于 NAT/地址伪装以修改数据包源地址的防火墙钩子。NAT 服务器需要将源者的 IP 地址替换为直接连接到 Internet 的接口的 IP 地址，以及源端口（以区分连接）。NAT 可能仅使用可用的公网 IP 修改 IP 地址。因此，此防火墙检查我们是否可以这样做以及该修改是否允许；否则，它将拒绝数据包。这是在出站数据包做出路由决策之后。不仅是 NAT/伪装，IPsec 模块也可以在此钩子处进行处理。

`NF_IP_LOCAL_IN`。这是一个应用于目标我们的数据包的防火墙钩子；即数据包需要被传递到本地。我们在路由决策确定数据包需要传递到本地后进行此检查。防火墙会检查是否需要从特定源接收特定端口（网络服务）的数据包。

`NF_IP_LOCAL_OUT`。这是一个针对所有本地生成的用于传输的数据包的防火墙钩子。该钩子在数据包路由完成后立即安装。

`NF_IP_FORWARD`。这是一个针对需要通过不同接口转发的数据包的防火墙钩子。该钩子适用于到达一个接口并需要通过另一个接口传输的数据包。Linux 机器必须充当路由器时，该钩子才能生效。

## 16.2 IP 栈上的 NETFILTER 钩子

在这一节中，我们将看到在 IP 栈的什么位置安装了防火墙检查点。首先，我们将讨论本地生成数据包的路径，然后讨论入站数据包。IP 栈上的 Netfilter 检查点如图 16.1 所示。我们将保持简单，仅使用最少数量的 netfilter 条目。

### 16.2.1 出站数据包的钩子

在被高层协议层（TCP/UDP）处理后，数据包需要找到通目的地的路由。数据包被发送到 IP 层，路由找到

![](img/b3f231108facab5be0138b2cfd3f681a_654_0.png)

图 16.1。安装在 IP 栈上的防火墙钩子。

```c
net/ipv4/ip_output.c

339 int ip_queue_xmit(struct sk_buff *skb)
340 {
341     struct sock *sk = skb->sk;
341    ....

399

400     return NF_HOOK(PF_INET, INET_NF_IP_LOCAL_OUT, skb, NULL, rt->u.dst_dev,
401     ip_queue_xmit(2);
402

406

400 return -EHOSTREACH;
407 }
```

> cs 16.4. `ip_queue_xmit()`.

```c
net/ipv4/ip_output.c

184 __inline_int ip_finish_output(struct sk_buff *skb)
185 {
186     struct net_device *dev = skb->dst_dev;
191     return NF_HOOK(PF_INET, INET_NF_IP_POST_ROUTING, skb, NULL, dev,
192     ip_finish_output(2);
193 }
```

> cs 16.5. `ip_finish_output()`.

找到数据包并根据路由信息构建 IP 头部。这在`ip_queue_xmit()`（cs 16.4）中完成。一旦构建了 IP 头部，数据包将通过防火墙钩子`NF_IP_LOCAL_OUT`进行筛选。在此时，我们需要检查来自源端口/IP 的数据包是否允许路由到该路径。通过它，我们可以向给定目的地发送数据包，并对运行在指定目的地的服务发出请求。如果钩子未确认数据包，它将被丢弃。

如果我们通过了第一个检查点，在最后将数据包放入设备队列进行首次传输之前，还需要通过最后一个检查点。这通常用于 NAT/伪装目的，也可以供 IPsec 模块使用以拥有自己的钩子。此检查在`ip_finish_output()`中完成。

如果防火墙允许，我们最终传输该段。在此。

### 16.2.2 入站数据包的钩子

一旦数据包被接收并识别为 IP 报文，`ip_rcv()`处理它（cs 16.6）。它通过`NF_IP_PRE_ROUTING`钩子执行所有 IP 头部检查。在这里，我们处理 NAT 伪装逻辑。下一步是检查数据包是需要传递到本地还是需要转发。通过`NF_IP_LOCAL_IN`钩子。

```c
net/ipv4/ip_input.c

379 int ip_rcv(struct sk_buff *skb, struct net_device *dev, struct packet_type *type) {
380     struct iphdr *ip;
387     return NF_HOOK(PF_INET, skb, NULL, dev,
388             ip_finish());
399 }
```

> cs 16.6. `ip_rcv()`.

```c
net/ipv4/ip_input.c
```
