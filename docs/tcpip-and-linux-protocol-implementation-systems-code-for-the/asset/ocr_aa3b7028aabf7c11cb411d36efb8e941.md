# Forwarding 815

```
465 #ifdef CONFIG_RTNETLINK
466 dsmark_dump /* dump */
467 #endif
468 };
470 471 #ifdef MODULE
472 int init_module(void)
473 {
474 return register_qdisc(&dsmark_qdisc_ops);
475 }
476
477
478 void cleanup_module(void)
479 {
480 unregister_qdisc(&dsmark_qdisc_ops);
481 }
```

# 9.13.4 Red and Red Friends

Random early detection is one of several scalable queue management techniques.

**Figure 9.249** Random Early Detection (RED) queue—introductory remarks: linux/net/sched/sch_red.c.

```
44 #define RED_ECT 0x02
45 #define RED_ECN_CE 0x01
46
47 /* Random Early Detection (RED) algorithm.
48
50
51 Source: Sally Floyd and Van Jacobson, "Random Early Detection Gateways
52 for Congestion Avoidance", 1993, IEEE Transactions on Networking.
53
54 This file codes a "dimensionless" version of RED algorithm
55 as written down in Fig.17 of the paper.
56
57 Short description.
58
59
60 When a new packet arrives we calculate the average queue length:
61
62 avg = (1-W)*avg + W*current_queue_len,
63
64 W is the filter time constant (chosen as 2^-(Wlog)), it controls
65 the inertia of the algorithm. To allow larger bursts, W should be
66 decreased.
```