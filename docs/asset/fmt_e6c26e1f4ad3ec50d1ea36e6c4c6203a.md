
```
interfaces {
statement1
settings
...
statementN
settings
}
```

在 `interfaces` 语句中，你可以使用三种类型的语句：`options`、`interface` 和 `define`。虽然这三种语句的使用顺序没有严格要求，但最好还是按照我们这里列出的顺序来。第一个，同样是 `options`。这与全局选项不同，而是针对所有接口的本地选项集——看起来像是全局接口选项。这里有两个选择，如表 5.5 所示。

### Table 5.5 Values Available in the gated.conf options Portion of the interfaces Statement

| Option | Purpose | Format | Value(s) |
|--------|---------|--------|----------|
| scaninterval | 设置 `gated` 检查内核文件以查找新接口或已移除接口的频率。默认是每 15 秒检查一次。 | `scaninterval time` | 两次检查之间等待的秒数。 |
| strictinterfaces | 设置当 `gated` 发现一个在启动后添加但未在配置文件中明确定义的接口时 `gated` 的行为。默认是报错但继续运行。如果包含此选项，在此情况下 `gated` 将会崩溃。 | `strictinterfaces` | N/A |

接下来在 `interfaces` 语句中是 一个或多个 `interface` 语句。是的，这可能会让人感到困惑。请务必仔细核对，不要把这两项弄反。你可以把多个接口配置在同一个语句中，也可以根据需要拆分，让它们具有不同的设置。`interface` 语句本身的格式为 `interface list`，其中 `list` 是你希望用这组特定设置进行配置的每个接口所属的一系列 IP 地址。可以在 `interface` 语句中配置的项目列在表 5.6 中。

### Table 5.6 Values Available in the gated.conf interface Portion of the interfaces Statement

| Option | Purpose | Format | Value(s) |
|--------|---------|--------|----------|
| down preference | 设置偏好值——当 `gated` 将接口标记为可能出现故障时，该接口的受青睐程度或不受青睐程度。 | `down preference value` | 整数值越高，`gated` 选择该接口的可能性越低。默认是 120。 |
| passive | 阻止 `gated` 将此接口更改为 `down preference` 值。 | `passive` | N/A |
| preference | 设置偏好值——当 `gated` 将接口标记为正常工作时，该接口的受青睐程度或不受青睐程度。 | `preference value` | 值越低，`gated` 使用该接口的可能性越大。默认是 0。 |
| simplex | 阻止接口听到自己的广播包，因此无法使用它们来确定其是否正常工作。 | `simplex` | N/A |

最后，在 `interfaces` 语句中还有 `define` 语句。如果你之前在 `interfaces` 选项语句中设置了 `strictinterfaces`，就需要包含此项。对于 `gated` 需要使用但在路由守护进程启动时可能尚未运行的每个接口，你都需要创建一个 `define` 语句，告诉 `strictinterfaces` 该接口可以被添加到路由表中。`define` 语句本身的使用格式为 `define address`，其中 `address` 是该接口的 IP 地址。表 5.7 列出了 `define` 中可用的选项。

### Table 5.7 Values Available in the gated.conf define Portion of the interfaces Statement

| Option | Purpose | Format | Value(s) |
|--------|---------|--------|----------|
| broadcast | 告诉 `gated` 接口可以处理广播消息——以太网卡和令牌环卡都可以做到——以及使用哪个地址。 | `broadcast address` | 该接口可访问的广播 IP 地址。 |
| multicast | 告诉 `gated` 接口可以处理多播流量。 | `multicast` | N/A |

## 表 5.7 继续

| 选项 | 目的 | 格式 | 值 |
|---|---|---|---|
| netmask | 告诉 `gated` 该接口对 IPv4 应用的网络掩码适用于此接口。 如果设置了 `pointopoint` 则无效。 | `netmask address` | 接口的网络掩码。 |
| pointopoint | 告诉 `gated` 该接口是调制解调器或其他使用 SLIP 或 PPP 的设备。 | `pointopoint address` | 该接口的本地地址。 在这种情况下，`define` 地址必须引用接口的远程地址。 |

因此，既然你可能对典型的 `interfaces` 语句可能是什么样子感到有点困惑，这里有一个更详细的示例：

```
interfaces {
    options
        strictinterfaces
    ;
    interface 192.168.232.*
        simplex
    ;
    interface 192.168.251.*
        simplex
        passive
    ;
    define 192.168.232.*
        broadcast 192.168.232.255
        netmask 255.255.255.0
    ;
    define 192.168.251.*
        broadcast 192.168.251.255
        netmask 255.255.255.127
    ;
}
```

请注意，并非所有的 IP 信息都严格以 IP 地址的形式出现。 你可以使用几种不同的格式：

- `all` 词 `all` 与仅使用通配符 `*` 相同。
- `xxx.xxx.xxx.xxx` 完整 IP 地址。
- `xxx.xxx.xxx.*`, `xxx.xxx.*`, `xxx.*` 以通配符结尾的部分 IP 地址。

对于网络部分，你指定所讨论网络的 IP 信息。 在这种情况下，规则要么是关键字 `exact`，要么是关键字 `refines`。 这两个关键字决定网络信息如何被解释。 `exact` 告诉 `gated` 严格按整体网络解释 `martians` 语句中的网络信息，忽略不在类边界上的网络掩码，因此忽略子网。 主机也被忽略。 然而，如果你对规则使用 `refines`，则会利用掩码和主机信息——不过在这种情况下掩码被隐含为类掩码。

这种格式的更复杂版本如下：

```
martians {
    network mask mask rules;
}
```

这里，`rules` 的 `refines` 选项更有意义。 `mask` 项指的是网络掩码。 更精细的版本如下：

```
martians {
    network masklen bit_mask rules;
}
```

你可能还记得第 4 章“IPv4 和 IPv6 地址”中，在“IPv6 数学”部分开头介绍过位掩码。 A 类位掩码是 `/8`，B 类是 `/16`，C 类是 `/24`。 从那里开始，子网和 IPv6 的位掩码变得更复杂。 就是这个值填入位掩码槽位。

`martians` 语句不一定只有一行 你可以在语句中混合使用这里看到的所有网络定义。 还有一个你可以使用的项目：你可以使用 `allow` 选项在这些项目的末尾将被屏蔽范围内的特定地址或范围设为有效。 例如，以下忽略来自整个 B 类 `192.168.0.0` 的路由信息，除了特别来自 C 类子网 `192.168.10.0`：

```
martians {
    192.168.0.0 exact;
    192.168.10.0 mask 255.255.255.0 refines allow;
}
```

## RIP 配置

每个路由协议必须在 `gated` 中单独配置。 让我们从最老且最简单的开始：RIP。 无论你是否希望此路由器能够与 RIP-1 或 RIP-2 路由器通信，都应以以下内容开始 RIP 配置部分：

```
rip status
```

`status` 条目可以是以下之一：

- `no`; 不处理 RIP 流量。
- `off`; 不处理 RIP 流量。
- `on` { 处理 RIP 流量。
- `yes` { 处理 RIP 流量。

设置此信息之外的内容并不是强制性的。 你可以在 `on` 或 `yes` 的情况下有以下内容：

```
rip on;
```

然而，使用大括号构建语句可以让你更好地控制 `gated` 如何处理 RIP。 `rip` 语句中可用的选项在表 5.9 中列出。
