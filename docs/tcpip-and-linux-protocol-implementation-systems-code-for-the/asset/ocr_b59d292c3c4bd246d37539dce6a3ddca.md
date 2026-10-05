# 9.13.5 Explicit Congestion Notification

Explicit congestion notification (ECN) is an alternative to packet dropping that TCP can act on (as discussed in Chapter 6).

Figure 9.254 RED–ECN handling: linux/net/sched/sch_red.c.

```
161 static int red_ecn_mark(struct sk_buff *skb)
162 {
163     if (skb->nh->raw + 20 > skb->tail)
164         return 0;
165 
166     switch (skb->protocol) {
167         case __htons(constant_ETH_P_IP):
168             {
169                 u8 tos = skb->nh->iph->tos;
171                 if ((tos & RED_ECN_ECT))
172                     return 0;
173                 
174                 if ((tos & RED_ECN_CE))
175                     IP_ECN_set_ce(skb->nh->iph);
177                 return 1;
178                 
179             }
180         case __constant_htons(ETH_P_IPV6):
181             {
182                 u32 label = (*u32*)skb->nh->raw;
184                 if ((label & __constant_htonl(RED_ECN_ECT<<20)))
185                     return 0;
187                 label |= __constant_htonl(RED_ECN_CE<<20);
188                 return 1;
189             }
190             default:
191                 return 0;
192             }
193 }
```

# RED Enqueue and Dequeue Functions

Here's an interesting comment, too.

Figure 9.255 RED–enqueue i: linux/net/sched/sch_red.c.

```
195 static int
196 red_enqueue(struct sk_buff *skb, struct qdisc* sch)
197 {
```