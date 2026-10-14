
`inet_sendmsg()`

`skb->prot->sendmsg()` ...

`tcp_ipv4.c`：

```c
struct proto tcp_proto {
```

`tcp.c`：

`tcp_sendmsg()`

`tcp_output.c`：

`tcp_send_skb()`

`tcp_transmit_skb()`

`err = tp->af_specific-xmit(skb);`

maps to `ip.queue_xmit`

```

然后在 `tcp_transmit_skb()` 中，管理了状态/头部的变化。这在第 7 章中讨论。

图 3.3 填充某些关键字段：`linux/net/ipv4/tcp_output.c`。

```
th = (struct tcphdr *)skb_push(skb, tcp_header_size);

skb->th = th;

skb_set_window(w, skb);

/* 构建 TCP 头部并计算校验和。 */

th->source = skb->port;

th->dest = skb->port;

th->seq = htons(th->seq);
```

### 3.2.3 IP 输出

等待，`ip_output()`，状态/头部的变化被管理了。这在第 7 章中讨论。

```c
ip_output_c:
```

（注：OCR 提供的文本在代码块中存在大量重复内容，已清理以恢复逻辑流。）

# TCP/IP 与 Linux 协议实现

```c
1062  softnet_data[cpu].cng_level = NET_RX_DROP;
1063  #endif
1064  else if (avg_blog > lo_cong) {
1065      softnet_data[cpu].cng_level = NET_RX_MOD;
1066  #ifdef RAND_LIE
1067      rd = net_random();
1068      rq = rd % netdev_max_backlog;
1069          if (rq < avg_blog) /* 不幸的队列队列 */
1070              softnet_data[cpu].cng_level = NET_RX_HIGH;
1071  #endif
1072  else if (avg_blog > no_cong) {
1073      softnet_data[cpu].cng_level = NET_RX_LOW;
1074  else /* 没有 no_cong */
1075      softnet_data[cpu].cng_level = NET_RX_SUCCESS;
1076  softnet_data[cpu].avg_blog = avg_blog;
1077  }
```

网络设备中断通过 `linux/net/core/dev.c` 中的 `net_devices` 结构体调用 `netif_rx()` 函数。

# 图 3.7 网络设备驱动 Rx iii：`linux/net/core/dev.c`。

```c
1135  enqueue:
1136      dev_bound(skb->dev);
1137      __skb_queue_tail(&queue->input_pkt_queue, skb);
1138      __skb_queue_raise_softirq(this->cpu, NET_RX_SOFTIRQ);
1139          local_irq_restore(flags);
1140  #ifdef OFFLINE_SAMPLE_SAMPLE
1141      get_sample_stats(this->cpu);
1142  #endif
1143      return softnet_data[cpu].cng_level;

1145  }

1146  if (queue->throttle) {
1147      queue->throttle = 0;
1148  #ifdef CONFIG_NET_HW_FLOWCONTROL
1149      if (atomic_dec_and_test(&netdev_dropping))
1150          netdev_wakeup();
1151  #endif
1152  }

1153      goto enqueue;
1154  }

1156  if (queue->throttle == 0) {
1157      queue->throttle = 1;
1158      netdev_rx_stat[this->cpu].throttled++;
1159  #ifdef CONFIG_NET_HW_FLOWCONTROL
1160      atomic_inc(&netdev_dropping);
1161  #endif
1162  }
```

1164 drop：

```c
netdev_rx_stat[this->cpu].dropped++;
local_irq_restore(flags);
```

```c
kfree_skb(skb);
return NET_RX_DROP;
```
}

# 图 3.8 网络设备驱动 RX iv：`linux/net/core/dev.c`。

/* 将 skb 交付给旧协议，这些协议没有经过良好的线程化，
或者无法理解共享 skb。
 */ 
static int dev_to_old_ones(struct packet_type *pt, struct sk_buff *skb, int, last last 
{
```c
static spinlock_t net_sk_bb_lock = SPIN_LOCK_UNLOCKED;
int ret = NET_RX_DROP;
```

```c
if (last) {
    skb = skb_clone(skb, GFP_ATOMIC);
    if (skb == NULL)
        return ret;
}
```
/* （正确的假设是）旧协议并不依赖于 BH 和 TIMER_BH。
/* 使用特殊的自旋锁模拟 BH */
```c
spin_lock(net_bh_lock);
```

/* 禁用定时器并等待所有定时器完成 */
```c
tasklet_disable(bh_task_vec);
```

```c
ret = pt->func(skb, skb->dev, pt);
```

```c
tasklet_enable(bh_task_vec);
```

然后软中断调度剩余部分，最终调用 `net_rx_action`。

接下来，`net_rx_action()` 取出包，根据数据包类型（通过表）：如果是 IP，则调用 `ip_input.c` 中的 `rcv()` 检查各种情况。

### 3.2.6 IP 工作

IP 输入必须解析数据包，因此首要工作是确定它是否真的是 IP，例如 IPv4 版本。

在 `ip_input` 中，`rcv()` 检查并调用 `NH_HOOK`（运行过滤器），或者直接入队，调用 `route.c` 中的 `ip_input()` 填充内部路由。

这包括一个函数（转发或本地交付），并再次调用 `ip_input` 中的 `local_deliver()`，它会队列 socket。

该指针之前在 `protocol.c` 的 `inet_protocol` 结构中填充，匹配协议处理函数——在这种情况下为 `tcp_v4_recv()`。

在第 6 章中对此进行了详细研究。

### 3.2.7 TCP 输入

IPv4 情况，相关的输入在 `tcp_ipv4.c` 中编码，它查找我们是否有连接，然后在进程上下文中尝试入队，否则调用 `tcp_v4_do_recv()`，它实际上处理 TCP 头部（预测等）并调用 `tcp_event_recv()`，检查是否需要确认，最后函数队列 socket。

### 3.2.8 Socket 输入

在 `core/sock.c` 中，我们看到由于 `sk->ready = sock_def_readable()...` 触发了主要。

# 图 3.9 Socket 接收：`struct sock *sk, int len` `linux/net/core/sock.c`。

```c
void sock_def_readable(struct sock *sk, int len)
{
  read_lock(sk->callback_lock);
  if (sk->sleep & wake_active(sk))
    wake_up_interruptible(sk->sleep);
  sk_wake_async(sk, U_IN);
```
