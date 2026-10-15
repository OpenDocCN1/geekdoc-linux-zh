

## 表 5.9 继续

| Option | Purpose | Format | Value(s) |
|--------|---------|--------|----------|
| no broadcast | 设置 gated 即使该机器中有多个活动接口也不广播 RIP 数据包。 | N/A | N/A |
| nocheckzero | 设置 gated 不拒绝具有非空保留字段的 RIP-1 数据包。 | N/A | N/A |
| preference | 设置 gated 通过 RIP 学习到的路由的优先级级别（与其它路由相比）。优先级级别会替换 value 中的值。默认值为 100。在 gated 的情况下，优先级越低，该路由被使用的可能性越大。 | preference value; | 100 |
| query authentication | 设置 gated 对来自非路由器的 RIP-2 查询是否严格。 此选项的值为以下之一：none（默认）、simple 或 md5（充其量也不比使用密码好多少）。 如果你选择最后两种之一，你还必须在分号前加上密码。 | authentication value; | none, simple, or md5 |
| Sourcegateways | 设置 gated 应向哪些路由器发送单播数据而不是广播。 machines 值由一个或多个空格分隔的 IP 地址组成。 | sourcegateways machines; |  |
| Traceoptions | 设置 gated 记录什么跟踪日志。 settings 值可以由通用协议 gated 跟踪选项和 RIP 特定 gated 跟踪选项组成。这两个选项集在表 5.11 和 5.12 中介绍。 | traceoptions settings; |  |

## 表 5.9 继续

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| Trustedgateways | 设置 gated 接受 RIP 更新的路由器。 | trustedgateways machines; | machines 值由一个或多个空格分隔的 IP 地址组成。 |

正如你所见，gated 的 RIP 设置可能变得相当复杂。其中两个选项无法以表格形式快速解释。这就是 interface 选项（与 interfaces 语句中的 interfaces 选项不同）以及本节讨论的两种跟踪选项。

在 rip 语句下，interface 选项采用以下形式：

```
rip on {
  options
  interface list
  settings
  ;
  options
};
```

构建列表遵循“接口语句”一节中接口覆盖部分给出的相同规则。rip 版本的 interface 可用选项列在表 5.10 中。请记住，这些项目是相对于该节中指定的网络接口而言的。如果需要各种网络连接具有不同的设置，可以有多个 interface 语句。

## 表 5.10 gated.conf rip interface 语句中可用的选项

| Option | Purpose | Format | Value(s) |
|---|---|---|---|
| authentication | 设置用于路由器连接的一个或两种形式的身份验证。仅用于 RIP-2。 | which authentication rule | which 值为空白表示你想使用 primary 或 secondary。 rule 值是 none、md5 或 simple 之一。对于 md5 和 simple，你必须在 rule 后面加上密码。 |
| broadcast | 设置 gated 将与 RIP-1 路由器兼容的 RIP-2 数据作为广播数据包发送给 RIP-1 路由器。 | broadcast | N/A |

## 表 5.10 继续

| Option | Purpose | Format | Value(s) |
|--------|---------|--------|---------|
| metricin | 设置向此接口发送 RIP-1 或 RIP-2 流量的 RIP 成本。 | metricin cost | 如果你希望路由保留在表中，则为 1 到 15 之间的整数；如果希望禁用通过此接口发现的任何路由，则为 16。默认值为 1。 |
| metricout | 设置从接口发送 RIP-1 或 RIP-2 流量的 RIP 成本。 | metricout cost | 如果你希望路由保留在表中，则为 1 到 15 之间的整数；如果希望禁用通过此接口发现的任何路由，则为 16。默认值为 1。 |
| multicast | 设置 gated 通过组播数据包与其他 RIP-2 路由器通信。 | multicast; | N/A |
| noripin | 设置 gated 应忽略到达接口的 RIP 数据包。 | noripin; | N/A |
| noripout | 设置 gated 不应从接口发送 RIP 信息。 | noripout; | N/A |
| ripin | 表示接受通过指定接口的 RIP 流量。默认。 | ripin; | N/A |
| ripout | 指定通过指定接口发送 RIP 流量。默认。 | ripout; | N/A |
| version 1 | 设置 gated 通过指定接口发送 RIP-1 数据包。 | version 1; | N/A |
| version 2 | 设置 gated 通过指定接口发送 RIP-2 数据包。 | version 2; | N/A |

