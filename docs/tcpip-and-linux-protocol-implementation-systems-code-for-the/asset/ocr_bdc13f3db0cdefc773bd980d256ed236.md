# Figure 9.110 Scheduler API-notify RTNetlink: linux/net/sched/sch_api.c.

```
769 static int qdisc_notify(struct sk_buff *skb, struct nlmmsagdr *n,
770     u32 client, struct qdisc *old, struct qdisc *new)
771     {
772         struct sk_buff *skb;
773         u32 pid = skb ? NETLINK_CB(skb).pid : 0;
774 
775             skb = alloc(NLMSG_GOODSIZE, KERN_KERNEL);
776             if (!skb)
777                 return -ENOMBUFS;
778 
779                 if (old && old->handle)
780                     if (tc_fill_qdisc(skb, old, pid, n->nlmsg_seq, 0, NLM_DELQDISC) < 0)
781                         goto err_out;
782                 }
783                 if (new)
784                     if (tc_fill_qdisc(skb, new, clid, pid, n->nlmsg_seq, old ? NLM_F_REPLACE : 
n785                         RTM_NEWQDISC) < 0)
786 
787 
788 
789                 if (skb->len)
790                     return rtnetlink_send(skb, pid, RTMRGRP_TC, n->nlmsg_flags&NLM_F_ECHO);
791 
792 err_out:
793     kfree_skb(skb);
794     return -EINVAL
795     }
```

# Figure 9.111 Scheduler API-dump statistics to RT: linux/net/sched/sch_api.c.

```
796 static int tc_dump_qdisc(struct sk_buff *skb, struct netlink_callback *cb)
797     {
798         int idx, q_idx;
799         int s_idx, s_q_idx;
800         struct net_device *dev;
801         struct qdisc *q;
802 
803             s_idx = cb->args[1];
804             s_q_idx = q_idx = cb->args[1];
805             read_lock(&dev->base_lock);
806             for (dev = dev->next, idx = 0; dev = dev->next, idx++) {
807                 if (idx < s_idx)
808                     continue;
809                     if (idx < s_q_idx)
810                         q_idx = 0;
811                         read_lock(&q->qdisc_tree_lock);
812                         for (q = dev->qdisc_list, q_idx = 0; q = q->next, q_idx++) {
813                                 if (q_idx < s_q_idx)
814                                 continue;
815                                 if (tc_fill_qdisc(skb, q, 0, NETLINK_CB(cb->skb).pid,
```