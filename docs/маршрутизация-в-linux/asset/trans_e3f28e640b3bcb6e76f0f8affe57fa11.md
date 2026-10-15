

## 表 5.22 egp 组类型子语句中 gated 的 peer 子句可用选项

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| analretentive | 告诉 gated 对其通常忽略的事件发出警告，例如重复的更新数据包。 | analretentive | N/A |
| gateway | 告诉 gated BGP 邻居未直接连接，并通过另一台路由器发送数据以与邻居通信。 | gateway IP | 需要充当中介的接口的 IP 地址。 |
| holdtime | 设置 gated 在断开与 BGP 邻居连接之前等待生命证明的时间长度。 | holdtime value; | 等待的秒数，从 0 到 3。 |
| indelay | 设置路由必须以相同方式通告的时间长度，然后 gated 才会将其添加到其 BGP 路由表中。 | indelay value; | 等待的秒数。默认值为 0。 |
| keep all | 告诉 gated 即使这些路由具有您的 AS 号，也将其路由放入其 BGP 路由表中。 | keep all; | N/A |
| keepalivesalways | 告诉 gated 即使其 BGP 邻居应假定 UPDATE 已足够时，也发送 keepalive 消息。 | keepalivesalways; | N/A |

## 表 5.22 继续

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| lcaddr | 告诉 gated 连接到此 BGP 邻居时使用哪个接口。 | lcaddr IP; | IP 的规则因所使用的组类型而异。外部类型需要与对等体或其指定网关相同的网络上的地址。对于任何其他类型，网络信息无关紧要。 |
| localas | 告诉 gated 哪个 AS 由此 BGP 路由器处理。 | localas AS; | 此边界路由器管辖的 AS 号。默认值为全局 autonomoussystem 选项中设置的值。 |
| logupdown | 每次 gated 的 BGP 功能进入 ESTABLISHED 状态或离开该状态时，都添加日志文件条目。 | logupdown; | N/A |
| metricout | 设置分配给发送到此邻居的路由的 BGP 成本。 | metricout cost; | 通过此邻居发送数据的 BGP 成本。 |
| noaggregatorid | 防止 gated 在路由数据包中包含路由器 ID 信息到此邻居，因此这些路由无法聚合为更大的语句。 | noaggregatorid; | N/A |
| noauthcheck | 告诉 gated 忽略传入 BGP 数据包的身份验证部分。此部分由 gated 设置为完全开启，但并非所有 gated 实现都如此。 | noauthcheck; | N/A |

## 表 5.22 继续

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| outdelay | 设置路由必须在路由表中保持相同的时间长度，然后 gated 才会向其邻居通告它。 | outdelay value; | 等待的秒数。默认值为 0。 |
| passive | 告诉 gated 此 BGP 路由器不应响应其他 BGP 路由器的 OPEN 数据包，但可以发送自己的数据包。 | passive; | N/A |
| preference | 设置 gated 的 BGP 实现如何将从此邻居学习到的路由与其他路由进行比较。 | preference value; | 值越低，从此邻居学习到的路由越重要。 |
| preference2 | preference 的平局打破子集。 | preference2 value; | 再次，值越低，从此邻居获得的路由被选中的可能性就越大。默认值为 0。 |
| ttl | 您通常不需要此项。它用于覆盖默认的 IP 生存时间设置。 | ttl value; | 如果 BGP 邻居忽略来自此路由器的包，请尝试将值设置为 2 而不是默认的 1。 |
| traceoptions | 设置 gated 为此特定 BGP 对等体记录数据的设置。 | traceoptions settings; | 可用于所有协议的选项列在表 5.11 中，而专门在 peer 和组类型语句中可用的选项列在表 5.21 中。 |
| version | 告诉 gated 使用哪个 BGP 版本。 | version value; | 有三种受支持的 BGP 版本：2、3 和 4。默认值为 4。 |

## IS-IS 协议

gated 支持一种协议未在任何细节中介绍，但如果您需要它，您应该知道。它是中间系统-中间系统 IS-IS 协议。这种路由协议用于内部使用，在许多种类的网络硬件和软件上运行各种子网的情况下。

IS-IS 是一种无连接协议，这意味着它不会与交换信息的机器保持开放连接——使其更像 UDP 而不是 TCP；以便给您一个参考点。如果您认为您可能需要使用此协议，您可以从 RFC 1142 开始了解更多关于它的信息，或者最好是 ISO DP 10589 父文档。

## 配置 SNMP 交互

让我们转换一下思路，离开路由协议，来看一下简单网络管理协议 SNMP。管理员使用此工具来帮助管理大型计算机网络。gated 守护进程实际上并不运行 SNMP 协议，但它确实允许您的 Linux 或其他路由器在您将其用作网络管理解决方案的一部分时与 SNMP 接口。有关 SNMP 本身的更多信息，请参阅 RFC 1157。

SNMP 交互的配置语句实际上相当简短。它以可预测的方式开始：

```
snmp on {
```

在括号内，只有三个选项可用：

- debug;: 如果您在 Linux 机器上的 SNMP 守护进程遇到问题，请添加此行以激活调试功能。
- port value;: 如果您正在运行 SNMP 但将其设置为使用非默认端口 167 的端口，请使用此语句告诉 gated。
- traceoptions options. 像往常一样，您使用此语句来配置日志记录。您可以使用表 5.11 中可用的所有项目，以及表 5.23 中列出的项目。

## 表 5.23 gated SNMP 设置的 traceoptions 部分可用选项

| Option | Purpose |
| --- | --- |
| receive | 记录来自 Linux SNMP 守护进程的 SNMP 请求，以及发送给它们的响应。 |
| register | 记录创建新变量的 SNMP 请求。 |
| resolve | 记录对变量内容的 SNMP 请求。 |
| trap | 记录 SNMP trap 消息。 |

