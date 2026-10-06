

# 400 第 20 章 连接跟踪

要查找连接条目，我们可以使用所谓的元组（tuple，见第 20.2.2 节）而不是带有完整 IP 数据包的 sk_buff 缓冲区。这种元组包含源地址、目的地址以及额外的协议信息。`ip_conntrack_find_get()` 就用于此目的。

## 20.2 实现

连接跟踪模块的模块接口位于 `net/ipv4/netfilter/ip_conntrack_standalone.c` 文件。`net/ipv4/netfilter/ip_conntrack_core.c` 文件包含了实际的跟踪功能。

### 20.2.1 基础结构

连接跟踪模块以非常高的优先级挂钩 netfilter 的 `NF_IP_PRE_ROUTING` 和 `NF_IP_LOCAL_OUT`（见第 19.3.1 节和图 20-1）（在 `<linux/netfilter_ipv4.h>` 中 `NF_IP_PRI_CONNTRACK` 被设置为 -200）。这意味着每个入数据包首先被传递给连接跟踪模块。随后，其他挂钩在这些钩子上的优先级较低的模块将获得处理机会。

![](img/5a25b942ec3329b8799f2b5f0de564f6_423_0.png)

图 20–1 连接跟踪模块使用的 Netfilter 钩子。

### 20.2.2 连接条目

| struct ip_conntrack | linux/netfilter/ipv4/ip_conntrack.h |
| :--- | :--- |

连接条目在 Linux 内核中通过 `ip_conntrack` 结构表示，由以下字段组成：

- 一个 `nf_conntrack` 类型的结构（定义在 `<linux/skbuff.h>` 中），包含一个引用计数器（use），用于统计指向该连接条目的打开引用数量。
- 两个用于正向和反向方向的元组（`tuplehash[0]`, `tuplehash[1]`），包含地址和协议信息，可引用此条目。
- 一个状态字段（`status`），包含一个带有以下位位的位向量：
    - `IPS_EXPECTED`: 连接是预期的。
    - `IPS_SEEN_REPLY`: 两个方向已经发生了数据包。
    - `IPS_ASSURED`: 连接条目不应被提前删除，即使在超时时也是如此。
- 一个指向函数的指针（`timeout`），该函数在该连接超时时立即被调用（即当该连接长时间未被使用时）。
- 一个 `ip_conntrack_expect` 类型的数据结构，可用于将预期连接（例如，在控制连接上发送命令后的 FTP 数据连接）分配到现有连接中（在这种情况下为分配到控制连接）。
- 多个 `nf_ct_info` 类型的结构，每个属于一个特定的状态。匹配 IP 数据包的条目指针被输入相应 `sk_buff` 结构的 `nft` 字段中。枚举类型 `ip_conntrack_info`（定义在 `<linux/netfilter/ipv4/ip_conntrack.h>` 中）作为包含 `nf_ct_info` 结构表的索引，它可以取以下任何值：
    - `IP_CT_ESTABLISHED`: 数据包属于一个完全建立的连接。
    - `IP_CT_RELATED`: 数据包属于一个新连接，但该连接引用一个已存在的连接（即预期连接）。
    - `IP_CT_NEW`: 数据包属于一个新连接。
    - `IP_CT_IS_REPLY`: 数据包属于连接的反向方向。
- 一个指向可选辅助模块的指针，用于扩展连接跟踪功能。（见第 20.2.4 节）。

# 402 第 20 章 连接跟踪

```
struct ip_conntrack_tuple_hash linux/netfilter/ipv4/ip_conntrack_tuple.h
```

连接条目存储在哈希表中，使用链表来解决冲突。哈希表中的条目类型为 `ip_conntrack_tuple_hash`，并包含一个指向该连接的 `ip_conntrack` 结构反向指针。除了实际的地址信息（元组）（即源地址和目的地址）和特定协议信息（例如端口号）。如图 20–2 所示，需要此指针来访问连接状态或检查该条目是否代表连接的正向或反向方向的元组。

![](img/5a25b942ec3329b8799f2b5f0de564f6_425_0.png)

图 20–2
连接跟踪模块的数据结构。

## 20.2 实现

```
struct ip_conntrack_tuple      linux/netfilter/ipv4/ip_conntrack_tuple.h
```

`ip_conntrack_tuple` 分为可操作部分（用于地址并处理源端口，`ip_conntrack_manip`）以及用于目的地址、协议和可能存在的目的端口的不可操作部分。这种划分便于 NAT 模块对连接条目的使用。

### 20.2.3 传输协议

```
struct ip_conntrack_protocol  linux/netfilter/ipv4/ip_conntrack_tuple.h
```

为了能够使用不同的协议，有一个带有 `protocol_list` 的全局列表。协议由 `ip_conntrack_protocol` 类型的结构表示。`ip_conntrack_register()` 和 `ip_conntrack_unregister()` 函数用于从列表中添加或删除协议。目前实现了以下功能：

- 输出有关连接的具体信息。
- 从 `sk_buff` 中提取源目的地址。
- 跟踪预期连接的状态。
- 当连接长时间未被使用时更新超时。

### 20.2.4 辅助模块

```
struct ip_conntrack_helper      linux/netfilter/ipv4/ip_conntrack.h
```

所谓的辅助模块提供了扩展连接跟踪功能的接口。`ip_conntrack_register()` 和 `ip_conntrack_unregister()` 用于从列表中添加或删除 `ip_conntrack_helper`。到达钩子的数据包都会传递给辅助模块。这允许我们支持 FTP，其中辅助模块可以将数据连接分配给现有控制连接。

# 404 第 20 章 连接跟踪

## 20.2.5 全局变量

以下全局变量对连接跟踪功能非常重要：

- `ip_conntrack`: 包含连接条目的哈希表——见 20.2.2。
- `expect_list`: 预期连接列表。例如，当在连接上启动传输时，连接是预期。
- `protocol_list`: 已注册的传输协议列表。TCP、UDP、ICMP 以及一个具有最小功能的通用协议（在找到匹配协议时使用）。
- `helpers`: 已注册的辅助模块列表——见 20.2.4。

## 20.2.6 函数

```
print_tuple() net/ipv4/netfilter/ip_conntrack_standalone.c
```

该函数由 `print_conntrack()` 调用，并文本形式输出单个元组（正向和反向方向）：

```
src=129.13.65.4 dst=168.42.17.1 sport=8080 dport=80
```

```
print_expect() net/ipv4/netfilter/ip_conntrack_standalone.c
```

该函数以文本形式输出预期列表中的单个元组：

```
EXPECTING: proto=23 src=129.13.65.4 dst=168.42.17.1 sport=8080 dport=80
```

```
print_conntrack() net/ipv4/netfilter/ip_conntrack_standalone.c
```

该函数以文本形式输出整个连接（正向和反向方向）的连接条目。除了两个元组外，还包含了状态和超时计时器的状态。

```
conntrack_iterate() net/ipv4/netfilter/ip_conntrack_standalone.c
```

这是一个遍历所有连接的辅助函数：它被 `list_conntracks()` 调用。

```
list_conntracks() net/ipv4/netfilter/ip_conntrack_standalone.c
```

该函数输出所有连接（当前活跃和预期的）的连接条目。为 proc 文件系统中生成条目是必需的。

