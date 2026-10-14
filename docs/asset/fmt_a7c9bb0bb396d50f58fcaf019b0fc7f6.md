
`input_pkt_queue` 用于处理接收到的包。它指向准备好传递给网络层协议的数据包或 `sk_buff` 列表的头部。数据包由 `netif_rx` 函数放入队列。

`poll_list` 是一个待处理的网络接口列表。它被积压处理使用。

`output_queue` 是准备好发送数据包的网络接口驱动的 `net_device` 结构列表。输出队列与 Linux 特定驱动程序的队列规则列表中安装的任何队列规则配合。

一个伪 `net_device` 结构用于队列维护；仅使用几个标志和字段。

`softnet_data` 实例存储在一个按 CPU 索引的数组中，以支持 SMP 配置下每个 CPU 的独立队列。除了 `softnet_data` 结构外，队列层还包含几个独立于特定网络接口驱动程序安装的队列规则的队列处理函数，这些函数在第 4 章中进行了详细描述。

## 6.5.3 发送的数据包

在本节中，我们将讨论如何准备输出发送。例如，我们关注输出函数 `ip_output`。

```c
int ip_output(struct sk_buff *skb);
```

对于解析到外部目的地的目标缓存，`hh_output` 将设置为 `dev_queue_xmit`，这是我们从 IP 调用来发送数据包的函数。

## 6.6 数据包队列层接收数据包，NET_RX_SOFTIRQ

从之前的讨论（第 4 章第 4.4 节），我们知道每个网络接口驱动的中断服务程序都会调用一个通用函数，将传入的数据包排队以便进行后续处理。回顾第 6.4 节，Linux TCP/IP 提供了一个软 IRQ 内核线程 `NET_RX_SOFTIRQ` 来处理队列中的数据包。实际上，该内核线程（softIRQ）负责 TCP/IP 协议栈中大部分的数据包处理，包括传输层协议 UDP 和 TCP。通常，该线程的目的是从输入队列中移除每个数据包，并为任何类型与链路层数据包中协议字段匹配的数据包处理器执行其数据包处理函数。数据包处理器可以是任何接收传入数据包且已数据包队列层注册的协议模块（图 6.2）。

![图 6.2：接收数据包序列。](img/296413c166cb1a4dbce2e3ed88300315_151_0.png)

图 6.2：接收数据包序列。

正如我们在第 6.4 节中所知，每个 softIRQ 都有一个动作函数。与网络线程 `NET_RX_SOFTIRQ` 相关的动作函数是 `net_rx_action`，定义在 `linuxnet/core/dev.c` 文件中。该过程的本质是处理输入数据包队列上的数据包，该队列由前面 `softnet_data` 结构中的 `_pkt_queue` 字段指向。如第 4 章所述，当每个网络驱动程序调用 `net_rx_action` 从队列中移除数据包并调用数据包处理器时，数据包会被放入输入数据包队列。然而，它并没有直接移除数据包。相反，每个驱动程序的 `poll` 函数通过 `net_device` 结构中的 `poll` 字段查找数据包来源输入网络接口。实际上，大多数网络设备驱动程序并没有 `poll` 函数。通常，`poll` 函数用于没有中断的伪驱动程序。然而，我们还有一个被称为积压设备的“假”设备，即 `backlog_dev`。如前所示，`backlog_dev` 在 `softnet_data` 创建时初始化，它的 `poll` 函数 `process_backlog` 承担了从队列中移除输入数据包并调用各种协议*数据包处理程序*的大部分“真实”工作。`net_rx_action` 在 `NET_RX_SOFTIRQ` 的文中运行。`net_rx_action` 遍历所有连接的网络接口的 `poll` 列表，如果存在，则执行驱动程序 `net_device` 结构中 `poll` 字段指向的函数。

```c
static void net_rx_action(struct softIRQ *h)
{
```

`softnet_data` 结构按 CPU 编号分配在数组中，且 `get_cpu_var` 返回对应 CPU 的队列。

```c
struct softnet_data *queue = __get_cpu_var(softnet_data);
unsigned long start_time = jiffies;
```

`Netdev_max_backlog` 是一个 sysctl 常量，定义了可以队列的最大包数。

```c
int budget = net_dev_max_backlog;
preempt_disable();
local_irq_disable();
```

在这里我们通过 `poll` 列表获取每个接口驱动程序。其中一个将是伪设备 `backlog_dev`。

```c
while (!list_empty(&queue->poll_list)) {
    struct net_device *dev;
    if (budget <= 0 || jiffies - start_time > 1)
        goto start_break;
    local_irq_enable(dev);
    dev = list_entry(queue->poll_list.next, struct net_device,
    poll_list);
```

在这里我们为每个网络接口驱动程序调用函数。如果 `dev` 指向积压伪设备 `backlog_dev`，则 `process_backlog` 就是我们通过 `poll` 指针实际调用的函数。如果 `poll` 函数成功处理了输入队列上的所有数据包，则返回 1；如果超过配额则返回负值。

```c
if (dev->quota <= 0 || dev->poll(dev, budget)) {
    local_irq_disable(dev);
    list_del(&dev->poll_list);
    list_add_tail(&dev->poll_list, &queue->poll_list);
    if (dev->quota < 0)
        dev->quota += dev->weight;
    else
        dev->quota = dev->weight;
} else {
    dev_put(dev);
    local_irq_disable();
}
```

```c
}
out:
local_irq_enable();
br_read_unlock(BR_NETPROTO_LOCK);
return;
softnet_break:
    _get_cpu_var(netdev_rx_stat).time_squeeze++;
    _raise_softIRQ_irqoff(NET_RX_SOFTIRQ);
```

### 6.6.1 Process_backlog 函数

如前所述，积压设备为传入的数据包处理提供了流控制，输入数据包处理节点将数据包放入积压设备的输入队列中。积压设备的 `poll` 字段指向执行数据包处理下一步操作的函数。该函数是 `process_backlog`。

```c
static int process_backlog(struct net_device *backlog_dev, int *budget)
{
    int work = 0;
    int quota = min(backlog_dev->quota, *budget);
```

我们从 `softnet_data` 获取队列实例。这将指向当前队列。

```c
struct softnet_data *queue = __get_cpu_var(softnet_data);
unsigned long start_time = jiffies;
```

`Netdev_max_backlog` 是一个 sysctl 常量，定义了可以队列的最大包数。

```c
int budget = net_dev_max_backlog;
preempt_disable();
local_irq_disable();
```

在这里我们通过 `poll` 列表获取每个接口驱动程序。其中一个将是伪设备 `backlog_dev`。

```c
while (!list_empty(&queue->poll_list)) {
    struct net_device *dev;
    if (budget <= 0 || jiffies - start_time > 1)
        goto start_break;
    local_irq_enable(dev);
    dev = list_entry(queue->poll_list.next, struct net_device,
    poll_list);
```
