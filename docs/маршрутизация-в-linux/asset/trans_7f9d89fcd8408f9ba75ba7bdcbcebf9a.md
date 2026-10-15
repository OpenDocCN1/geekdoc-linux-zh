

## 表 5.7 继续

| 选项 | 目的 | 格式 | 值 |
|---|---|---|---|
| netmask | 告诉 gated 该接口对 IPv4 应用的网络掩码适用于此接口。 如果设置了 pointopoint 则无效。 | netmask address | 接口的网络掩码。 |
| pointopoint | 告诉 gated 该接口是调制解调器或其他使用 SLIP 或 PPP 的设备。 | pointopoint address | 该接口的本地地址。 在这种情况下，define 地址必须引用接口的远程地址。 |

因此，既然你可能对典型的 interfaces 语句可能是什么样子感到有点困惑，这里有一个更详细的示例：

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

- all. 词 all 与仅使用通配符 * 相同。
- xxx.xxx.xxx.xxx. 完整 IP 地址。
- xxx.xxx.xxx.*, xxx.xxx.*, xxx.*. 以通配符结尾的部分 IP 地址。

对于网络部分，你指定所讨论网络的 IP 信息。 在这种情况下，规则要么是关键字 exact，要么是关键字 refines。 这两个关键字决定网络信息如何被解释。 exact 告诉 gated 严格按整体网络解释 martians 语句中的网络信息，忽略不在类边界上的网络掩码，因此忽略子网。 主机也被忽略。 然而，如果你对规则使用 refines，则会利用掩码和主机信息——不过在这种情况下掩码被隐含为类掩码。

这种格式的更复杂版本如下：

```
martians {
    network mask mask rules;
}
```

这里，rules 的 refines 选项更有意义。 mask 项指的是网络掩码。 更精细的版本如下：

```
martians {
    network masklen bit_mask rules;
}
```

你可能还记得第 4 章“IPv4 和 IPv6 地址”中，在“IPv6 数学”部分开头介绍过位掩码。 A 类位掩码是 /8，B 类是 /16，C 类是 /24。 从那里开始，子网和 IPv6 的位掩码变得更复杂。 就是这个值填入位掩码槽位。

martians 语句不一定只有一行 你可以在语句中混合使用这里看到的所有网络定义。 还有一个你可以使用的项目：你可以使用 allow 选项在这些项目的末尾将被屏蔽范围内的特定地址或范围设为有效。 例如，以下忽略来自整个 B 类 192.168.0.0 的路由信息，除了特别来自 C 类子网 192.168.10.0：

```
martians {
    192.168.0.0 exact;
    192.168.10.0 mask 255.255.255.0 refines allow;
}
```

## RIP 配置

每个路由协议必须在 gated 中单独配置。 让我们从最老且最简单的开始：RIP。 无论你是否希望此路由器能够与 RIP-1 或 RIP-2 路由器通信，都应以以下内容开始 RIP 配置部分：

```
rip status
```

status 条目可以是以下之一：

- no; 不处理 RIP 流量。
- off; 不处理 RIP 流量。
- on { 处理 RIP 流量。
- yes { 处理 RIP 流量。

设置此信息之外的内容并不是强制性的。 你可以在 on 或 yes 的情况下有以下内容：
rip on;

然而，使用大括号构建语句可以让你更好地控制 gated 如何处理 RIP。 rip 语句中可用的选项在表 5.9 中列出。

## 表 5.9 gated.conf rip 语句中可用的选项

| 选项 | 目的 | 格式 | 值 |
|---|---|---|---|
| broadcast | 设置 gated 即使机器中只有一个活动接口也广播 RIP 数据包。 | broadcast; | N/A |
| defaultmetric | 设置从其他协议学习到的路由的默认 RIP 成本。 | defaultmetric cost; | 要使用的 RIP 成本。 默认值为 16，表示路由不可用。 |
| interface | 设置特定接口对 RIP 的行为。 该项目将在本章中更详细地介绍。 | interface list value1 ... valueN; | 在这种情况下，值是另一组选项，list 指的是此规则涵盖的特定接口。 值在表 5.10 中单独介绍。 对于 list，如果你想匹配所有内容，使用 all；匹配完整 IP 地址使用格式 xxx.xxx.xxx.xxx；匹配部分 IP 地址使用格式 xxx.xxx.xxx.*, xxx.xxx.*, xxx.*, 或 *；使用通配符设备名使用 eth*；或使用设备全名如 eth0。 |

