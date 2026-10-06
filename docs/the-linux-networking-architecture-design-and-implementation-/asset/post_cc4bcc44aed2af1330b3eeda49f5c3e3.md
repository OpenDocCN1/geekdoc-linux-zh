
## Chapter 18 Using Traffic Control to Support Quality of Service (QoS)

```c
change() include/net/pkt_sched.h
```

The change() function can be used to change parameters of a queuing discipline.

```c
dump() include/net/pkt_sched.h
```

The dump() function serves to output configuration parameters and statistics of a queuing discipline.

The central structure of each queuing discipline, which is referred to by all functions introduced so far, is the structure Qdisc (include/net/pkt_sched.h). printed as follows:

```c
struct Qdisc {
    int (*enqueue(struct sk_buff *skb, struct Qdisc*));
    unsigned sk_buffer * (*dequeue(struct Qdisc *dev));
#define TQ_F_BUILTIN 1
#define TQ_F_THROTTLED 2
#define TQ_F_INGRES 4
    struct Qdisc_ops {
        void *ops;
        void *next;
        u32 handle;
        atomic_t refcnt;
        struct sk_buffer_head q;
        struct net_device *dev;
        struct tc_stats *stats;
        int (*reshape_fail)(struct sk_buff *skb, struct Qdisc *q);
    };
};
```

> * This file is deprecated, but it is still used by CBQ * and it will live until better solution will be invented.

```c
struct Qdisc {
    struct *parent;
    char *data[0];
}
```

In addition to a reference to the Qdisc_ops structure, there is a pointer to link Qdisc structures and a handle for unique marking of an instance of the structure within the kernel. For a simple queuing discipline with only one queue, the entry struct sk_buffer_head q represents the header of this queue. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

## 18.4 Kernel Structures and Interfaces 373

The structure struct tc_stats (include/linux/pkt_sched.h) serves to carry statistics (in addition to the q.qlen entry described earlier for the number of packets to be ordered). The following counters exist in the structure tc_stats:

- _u64 bytes: Number of enqueued bytes
- _u32 packets: Number of enqueued packets
- _u32 drops: Packets dropped because of lack of resources
- _u32 overlimits: Number of throttle events when this flow goes out of allocated bandwidth
- _u32 bps: Current flow rate
- _u32 qlen: Current flow packet rate
- _u32 backlog:

These statistics can have certain inaccuracies if a queuing discipline manages additional inner queuing disciplines. This is the case, for example, when a packet is dropped in an inner queuing discipline, the number of ordered bytes can then deviate from the real value. If a queuing discipline has classes, then separate statistics can be maintained for each class.

A queuing discipline can be added in either of the following ways:

```c
pktsched_init() net/sched/sch_api.c
```

This function is used when a queuing discipline is permanently compiled in the kernel. In this case, the RT-NETLINK interface, which will be introduced later, is initialized, and the function register_qdisc is invoked. Unless additional disciplines were selected when the kernel was configured, only the bfifo and pifo queuing disciplines (defined in net/sched/sch_fifo.c) are selected here.

```c
register_qdisc() net/sched/sch_api.c
```

This function is evoked by the above described function, pktsched_init(), or by init_module(), if we want to include the queuing discipline as a module. Initially, this function checks for whether a queuing discipline with the same identification—id[IFNAMSIZ]—of the qdisc_ops structure already exists. If this is not the case, then the new queuing discipline is appended to the end of the list.

### 18.4.3 Classes

Classes can be thought of as independent elements. They relate closely to the queuing discipline, which is always allocated to exactly one network device. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

The structure struct tc_stats (include/linux/pkt_sched.h) serves to carry statistics (in addition to the q.qlen entry described earlier for the number of packets to be ordered). The following counters exist in the structure tc_stats:

- _u64 bytes: Number of enqueued bytes
- _u32 packets: Number of enqueued packets
- _u32 drops: Packets dropped because of lack of resources
- _u32 overlimits: Number of throttle events when this flow goes out of allocated bandwidth
- _u32 bps: Current flow rate
- _u32 qlen: Current flow packet rate
- _u32 backlog:

These statistics can have certain inaccuracies if a queuing discipline manages additional inner queuing disciplines. This is the case, for example, when a packet is dropped in an inner queuing discipline, the number of ordered bytes can then deviate from the real value. If a queuing discipline has classes, then separate statistics can be maintained for each class.

A queuing discipline can be added in either of the following ways:

```c
pktsched_init() net/sched/sch_api.c
```

This function is used when a queuing discipline is permanently compiled in the kernel. In this case, the RT-NETLINK interface, which will be introduced later, is initialized, and the function register_qdisc is invoked. Unless additional disciplines were selected when the kernel was configured, only the bfifo and pifo queuing disciplines (defined in net/sched/sch_fifo.c) are selected here.

```c
register_qdisc() net/sched/sch_api.c
```

This function is evoked by the above described function, pktsched_init(), or by init_module(), if we want to include the queuing discipline as a module. Initially, this function checks for whether a queuing discipline with the same identification—id[IFNAMSIZ]—of the qdisc_ops structure already exists. If this is not the case, then the new queuing discipline is appended to the end of the list.

The structure struct tc_stats (include/linux/pkt_sched.h) serves to carry statistics (in addition to the q.qlen entry described earlier for the number of packets to be ordered). The following counters exist in the structure tc_stats:

- _u64 bytes: Number of enqueued bytes
- _u32 packets: Number of enqueued packets
- _u32 drops: Packets dropped because of lack of resources
- _u32 overlimits: Number of throttle events when this flow goes out of allocated bandwidth
- _u32 bps: Current flow rate
- _u32 qlen: Current flow packet rate
- _u32 backlog:

These statistics can have certain inaccuracies if a queuing discipline manages additional inner queuing disciplines. This is the case, for example, when a packet is dropped in an inner queuing discipline, the number of ordered bytes can then deviate from the real value. If a queuing discipline has classes, then separate statistics can be maintained for each class.

A queuing discipline can be added in either of the following ways:

```c
pktsched_init() net/sched/sch_api.c
```

This function is used when a queuing discipline is permanently compiled in the kernel. In this case, the RT-NETLINK interface, which will be introduced later, is initialized, and the function register_qdisc is invoked. Unless additional disciplines were selected when the kernel was configured, only the bfifo and pifo queuing disciplines (defined in net/sched/sch_fifo.c) are selected here.

```c
register_qdisc() net/sched/sch_api.c
```

This function is evoked by the above described function, pktsched_init(), or by init_module(), if we want to include the queuing discipline as a module. Initially, this function checks for whether a queuing discipline with the same identification—id[IFNAMSIZ]—of the qdisc_ops structure already exists. If this is not the case, then the new queuing discipline is appended to the end of the list.

Classes can be thought of as independent elements. They relate closely to the queuing discipline, which is always allocated to exactly one network device. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

The structure struct tc_stats (include/linux/pkt_sched.h) serves to carry statistics (in addition to the q.qlen entry described earlier for the number of packets to be ordered). The following counters exist in the structure tc_stats:

- _u64 bytes: Number of enqueued bytes
- _u32 packets: Number of enqueued packets
- _u32 drops: Packets dropped because of lack of resources
- _u32 overlimits: Number of throttle events when this flow goes out of allocated bandwidth
- _u32 bps: Current flow rate
- _u32 qlen: Current flow packet rate
- _u32 backlog:

These statistics can have certain inaccuracies if a queuing discipline manages additional inner queuing disciplines. This is the case, for example, when a packet is dropped in an inner queuing discipline, the number of ordered bytes can then deviate from the real value. If a queuing discipline has classes, then separate statistics can be maintained for each class.

A queuing discipline can be added in either of the following ways:

```c
pktsched_init() net/sched/sch_api.c
```

This function is used when a queuing discipline is permanently compiled in the kernel. In this case, the RT-NETLINK interface, which will be introduced later, is initialized, and the function register_qdisc is invoked. Unless additional disciplines were selected when the kernel was configured, only the bfifo and pifo queuing disciplines (defined in net/sched/sch_fifo.c) are selected here.

```c
register_qdisc() net/sched/sch_api.c
```

This function is evoked by the above described function, pktsched_init(), or by init_module(), if we want to include the queuing discipline as a module. Initially, this function checks for whether a queuing discipline with the same identification—id[IFNAMSIZ]—of the qdisc_ops structure already exists. If this is not the case, then the new queuing discipline is appended to the end of the list.

The function dump() function serves to output configuration parameters and statistics of a queuing discipline.

The central structure of each queuing discipline, which is referred to by all functions introduced so far, is the structure Qdisc (include/net/pkt_sched.h). printed as follows:

```c
struct Qdisc {
    int (*enqueue(struct sk_buff *skb, struct Qdisc*));
    unsigned sk_buffer * (*dequeue(struct Qdisc *dev));
#define TQ_F_BUILTIN 1
#define TQ_F_THROTTLED 2
#define TQ_F_INGRES 4
    struct Qdisc_ops {
        void *ops;
        void *next;
        u32 handle;
        atomic_t refcnt;
        struct sk_buffer_head q;
        struct net_device *dev;
        struct tc_stats *stats;
        int (*reshape_fail)(struct sk_buff *skb, struct Qdisc *q);
    };
};
```

> * This file is deprecated, but it is still used by CBQ * and it will live until better solution will be invented.

```c
struct Qdisc {
    struct *parent;
    char *data[0];
}
```

In addition to a reference to the Qdisc_ops structure, there is a pointer to link Qdisc structures and a handle for unique marking of an instance of the structure within the kernel. For a simple queuing discipline with only one queue, the entry struct sk_buffer_head q represents the header of this queue. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

The function dump() function serves to output configuration parameters and statistics of a queuing discipline.

The central structure of each queuing discipline, which is referred to by all functions introduced so far, is the structure Qdisc (include/net/pkt_sched.h). printed as follows:

```c
struct Qdisc {
    int (*enqueue(struct sk_buff *skb, struct Qdisc*));
    unsigned sk_buffer * (*dequeue(struct Qdisc *dev));
#define TQ_F_BUILTIN 1
#define TQ_F_THROTTLED 2
#define TQ_F_INGRES 4
    struct Qdisc_ops {
        void *ops;
        void *next;
        u32 handle;
        atomic_t refcnt;
        struct sk_buffer_head q;
        struct net_device *dev;
        struct tc_stats *stats;
        int (*reshape_fail)(struct sk_buff *skb, struct Qdisc *q);
    };
};
```

> * This file is deprecated, but it is still used by CBQ * and it will live until better solution will be invented.

```c
struct Qdisc {
    struct *parent;
    char *data[0];
}
```

In addition to a reference to the Qdisc_ops structure, there is a pointer to link Qdisc structures and a handle for unique marking of an instance of the structure within the kernel. For a simple queuing discipline with only one queue, the entry struct sk_buffer_head q represents the header of this queue. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

The function dump() function serves to output configuration parameters and statistics of a queuing discipline.

The central structure of each queuing discipline, which is referred to by all functions introduced so far, is the structure Qdisc (include/net/pkt_sched.h). printed as follows:

```c
struct Qdisc {
    int (*enqueue(struct sk_buff *skb, struct Qdisc*));
    unsigned sk_buffer * (*dequeue(struct Qdisc *dev));
#define TQ_F_BUILTIN 1
#define TQ_F_THROTTLED 2
#define TQ_F_INGRES 4
    struct Qdisc_ops {
        void *ops;
        void *next;
        u32 handle;
        atomic_t refcnt;
        struct sk_buffer_head q;
        struct net_device *dev;
        struct tc_stats *stats;
        int (*reshape_fail)(struct sk_buff *skb, struct Qdisc *q);
    };
};
```

> * This file is deprecated, but it is still used by CBQ * and it will live until better solution will be invented.

---

In addition to a reference to the Qdisc_ops structure, there is a pointer to link Qdisc structures and a handle for unique marking of an instance of the structure within the kernel. For a simple queuing discipline with only one queue, the entry struct sk_buffer_head q represents the header of this queue. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

## 18.4.3 Classes

Classes can be thought of as independent elements. They relate closely to the queuing discipline, which is always allocated to exactly one network device. Each queuing discipline is always allocated to exactly one network device, which is referred to by struct net_device *dev.

The function reshape_fail() can be used to implement more complex traffic shaping mechanisms. When an outer queue sends a packet to an inner queue, then it can happen that the packet be discarded—for example, when there is no buffer space available. If the outer queuing discipline implements the callback function reshape_fail(), it can be invoked by the inner queuing discipline in this case. Subsequently, the outer queuing discipline can select a different class.

## 18.4.4 Filters

The class packets that passed by the enqueue() function in a queuing discipline belongs to is decided by filters.
