1163

1164 drop:

1165

```
netdev_rx_stat[this->cpu].dropped++;
local_irq_restore(flags);
```

1166

1167

1168

1169

```
kfree_skb(skb);
return NET_RX_DROP;
```

1170 }

# Figure 3.8 Network device driver RX iv: linux/net/core/dev.c.

1172 /* Deliver skb to an old protocol, which is not threaded well

1173 or which do not understand shared skbs.

1174 */

1175 static int dev_to_old_ones(struct packet_type *pt, struct sk_buff *skb, int, last last

1176 {

```
static spinlock_t net_sk_bb_lock = SPIN_LOCK_UNLOCKED;
int ret = NET_RX_DROP;
```

1177

1178

1179

1180

1181

```
if (last) {
    skb = skb_clone(skb, GFP_ATOMIC);
    if (skb == NULL)
        return ret;
}
```

1182

1183

1184

1185

1186

> /* The assumption (correct one) is that old protocols

1187

> did not depend on BH different of NET_BH and TIMER_BH.

1188

> /*

1189

> /* Emulate NET_BH with special spinlock */

```
spin_lock(net_bh_lock);
```

1190

1191

> /* Disable timers and wait for all timers completion */

```
tasklet_disable(bh_task_vec+TIMER_BH);
```

1192

1193

1194

1195

1196

1197

```
ret = pt->func(skb, skb->dev, pt);
```

1198

1199

```
tasklet_enable(bh_task_vec+TIMER_BH);
```

Then the software interrupt reschedules the rest, which eventually results in a call
to net_rx_action.

Next, net_rx_action(), which dequeues the packet, calls a packet han-
dler based on the packet type (via a table)—if it is IP, this calls ip_rcv() in
ip_input.c, which checks various things.