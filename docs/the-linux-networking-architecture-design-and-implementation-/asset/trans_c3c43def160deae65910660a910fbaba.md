

# 368 第18 章 使用流量控制支持服务质量 (QoS)

以及令牌桶。更复杂的队列规则（queuing disciplines）也可以管理队列。队列规则定义在以 `sch_` 开头的文件中（位于 net/sched 目录下）。

- **类 (Classes)**：队列规则可以有多个接口，这些接口用于在队列管理中插入数据包。这允许我们根据类来区分数据包。在一个队列规则内部，我们可以将数据包分配到不同的类（例如，以不同的优先级处理它们）。类定义在队列规则内部（即也定义在以 `sch_` 开头的文件）。

- **过滤器 (Filters)**：过滤器通常用于将输出数据包分配到队列规则内的类中。过滤器定义在以 `cls_` 开头的文件中。

就像构建套件一样，单个元素可以递归地连接：其他队列规则及其相应的类和过滤器可以在单个队列规则内部使用。

图 18-2 显示了生成的流量控制树的示例。在外部，我们首先只看到上层队列规则的入队（enqueue）和出队（dequeue）函数。在这个示例中，通过 `enqueue()` 函数传递的数据包将由过滤器规则逐一检查，并分配到过滤器首次访问的类。如果没有一个过滤器规则匹配，则可以使用默认过滤器来定义分配系统。在类之后是其他的队列规则。由于这是一棵树，我们也称队列规则为“父节点”。例如，队列规则 1:0 是所谓的外部队列规则，是类 1:1 和 1:2 的父节点。队列规则 2:0 和 3:0 也称为内部队列规则。

数据包从这棵树中递归移除以便传输：当调用外部队列规则的 `dequeue()` 函数时，该函数会根据队列规则的类型，递归搜索相应类的队列规则中准备好发送的数据包。

![](img/5a25b942ec3329b8799f2b5f0de564f6_391_0.png)

图 18–2
由队列规则、类和过滤器组成的树的示例。

# 18.4 内核结构与接口 369

![](img/5a25b942ec3329b8799f2b5f0de564f6_392_0.png)

图 18-3 在 Linux 内核传输过程中插入流量控制树。

数据包通过内核的路径在第 6 章中详细描述过。图 18–3 显示了流量控制示例与图 6–4 所示传输过程的关系。相比于一个 FIFO（先进先出）队列，我们现在插入了一个更广泛且可配置的树来处理传输数据流；对传输过程的功能不需要其他更改。

接下来的章节描述了队列规则、类和过滤器的接口。

# 18.4 内核结构与接口

队列规则和过滤器可用的接口大多与元素内部可用的功能独立。

## 18.4.1 句柄 (Handles)

流量控制树中的所有元素都可以通过 32 位标识符（称为句柄）进行寻址。例如，下文讨论的队列规则实例用 32 位标识符标记，这些符分为主号（major number）和小号（minor number）。然而，这些数字与设备文件的主号、小号无关。这些标识符对于每个网络设备是唯一的，但在多个网络设备上可能会出现多次。

相比之下，队列规则的小号始终为零，除了输入队列规则编号 `ffff:fff1 TC_INGRESS`（在 include/linux/pkt_sched.h 中）和顶层队列输出队列规则编号 `ffff:ffff TC_ROOT`。主号由用户分配，范围在 0x0001 到 0x7 之间。如果用户指定主号为 0，则内核分配一个 0x8000 到 0xffff 之间的主号。

对于类，主号对应关联的队列规则，而小号指定队列规则内的类。在这种情况下，小号的范围可以在 0x0 到 0xffff 之间。小号在一个队列规则的所有类中是唯一的。

```
include/linux/pkt_sched.h 定义了几个你可以用于掩码主号和小号的宏。
```

## 18.4.2 队列规则 (Queuing Disciplines)

队列规则提供的函数定义在 include/net/pkt_sched.h 的 `Qdisc_ops` 结构中。

```
struct Qdisc_ops {
    struct qdisc *next;
    struct qdisc_class *class;
    struct Qdisc_class_ops *cl_ops;
    char id[IFNAMSIZ];
    int priv_size;

    int min;
    int max;
    int (*enqueue)(struct sk_buff *, struct Qdisc *);
    int (*dequeue)(struct Qdisc *);
    int (*requeue)(struct sk_buff *, struct Qdisc *);
    int (*drop)(struct Qdisc *);

    int start;
    int interval;
    void (*init)(struct Qdisc *, struct rtattr *arg);
    void (*reset)(struct Qdisc *);
    void (*destroy)(struct Qdisc *);
    int (*change)(struct Qdisc *, struct rtattr *arg);

    int cb;
    int count;
    int (*dump)(struct Qdisc *, struct sk_buff *);
};
```

前四个项目是指向列表的链接（`struct qdisc *next`）、类操作的引用（`struct Qdisc_class_ops *cl_ops`，将在后描述）。它们代表一个标识符（`char id[IFNAMSIZ]`）以及内部使用的值。

以下是外部可用的函数：

```
enqueue() include/pkt_sched.h
```

`enqueue()` 函数用于将数据包传递给队列规则。如果队列规则接受了数据包，结果为 `NET_XMIT_SUCCESS`（见 include/netdevice.h）。如果在排序数据包时丢弃了该包或其他包，则返回：
- XMIT_DROP：刚刚通过的数据包被丢弃。
- XMIT_CN：由于缓冲区溢出丢弃了数据包（CN 代表拥塞）。
- XMIT_POLED：由于策略机制检测到违反规则（例如超过了允许速率）。
- XMIT_BYPASS：通过的数据包被接受，但不会通过常规 `dequeue()` 函数离开队列规则。

```
当 ` `dequeue()` 函数被调用时，队列规则返回一个可以发送的数据包指针（skb）。返回空并不意味着队列规则中没有更多数据包，而是调用时没有准备好发送的数据包。队列规则中等待的数据包总数在 `struct qdisc*q->len` 中说明。当队列规则管理多个队列时，该值是有效的。

```
enqueue() include/pkt_sched.h
```

`enqueue()` 函数将之前移除的数据包放回队列中。与 `dequeue()` 相，数据包应该被安排在队列规则中之前的位置，并且通过该规则的数据包计数不应增加。此函数用于当数据包被 `dequeue()` 移除以发送，但最终由于意外原因无法发送的情况。

```
drop() include/pkt_sched.h
```

该函数从队列中移除数据包并将其丢弃。

```
reset() include/pkt_sched.h
```

`reset()` 函数将队列规则置于初始状态（空队列、重置计数器、删除定时器等）。如果此队列规则管理其他队列规则，则它们的 `reset()` 函数也将被调用。

```
init() include/pkt_sched.h
```

`init()` 函数用于初始化一个新的实例化的队列规则。

```
destroy() include/pkt_sched.h
```

`destroy()` 函数释放在队列规则初始化和运行期间预留的资源。

