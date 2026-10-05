# 862 TCP/IP and Linux Protocol Implementation

Figure 9.324 ATM scheduling-destroy all filters: linux/net/sched/atm.c

Figure 9.325 ATM scheduling-pop vc: linux/net/sched/atm.c.

```
static void atm_sch_pop(struct atm_vcc *vcc, struct sk_buff *skb)
{
    struct atm_tc_qdisc_data *prev = VCC2FLOW(vcc)->parent;
    PRINTK("*atm_sch_pop(vcc %p, skb %p, [qdisc %p])\n", vcc, skb, skb);
    VCC2FLOW(vcc)->old_pop(vcc,skb);
    tasklet_schedule(&p->task);
```