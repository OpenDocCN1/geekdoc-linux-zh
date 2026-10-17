
- `address/broadcast new_link_layer_address`
- `mtu MTUvalue`（最大传输单元）
- `nets PID`
- `vf NUM`（虚拟函数设备编号）
- `add`——可以有 `add`、`del`、`show` 和 `flush` 命令，用于从设备添加或删除 IP 地址，显示当前的 IP 地址，或根据某些特定标准冲空（删除）地址。使用 `add`，你可以为设备、对等或广播地址、标签或范围指定新名称。`show` 命令可以跟随一个设备名、`scope scope_val`、`to addr`、`label value`、`dynamic`、`permanent`、`tentative`、`deprecated` 或 `secondary`。
- `addrlabel` 为一个 IPv6 地址标记以便以后使用，该对象后可以跟随 `add`、`del` 或 `list` 之一。
- `route`——此对象允许你操作或检查任何一个路由表。系统维护有多种类型的路由表：unicast（单播）、unreachable（不可达）、black-hole（黑洞）、prohibit（禁止）、local（本地）、broadcast（广播）、throw（丢弃）、nat（网络地址转换）、anycast（任播）和 multicast（组播）。`route` 的命令是 `add`、`change`、`replace`、`del`（删除）、`show`、`flush` 之一。对于 `add`、`change` 和 `replace`，你可以后面跟着单词 `to`，然后是表类型（例如 unicast、nat）以及 IP 或 IPv6。`add`、`change` 和 `replace` 的替代选项是指定新的偏好数、表 ID、新设备名、新的 src 或 via 地址以及新的 mtu 值等。`del` 命令的参数用法与 `add` 略有不同，且 `show` 有额外的参数可用。`flush` 命令冲空表，而 `get` 命令可用于从表中检索一个特定值。以下是几个 `route` 命令的示例：

```
ip route add 10.11.12.0/24 dev eth0
ip route add default via 10.11.12.13
ip route add 10.11.1.2 via 10.11.30.1
ip route add nat 192.51.185.16 via 10.11.12.1
ip route change default via 10.11.30.6 dev eth0
ip route show cache
```

- `rule`——更改路由选择算法，以便特定设置下使用的路由表发生变化。
- `neigh`——添加、更改、删除、替换或显示，其中邻居是指定为协议地址和链路层地址绑定的对象。
- `maddress`——组播地址，命令为 `show`、`add` 和 `delete`。
- `mroute`——组播路由缓存管理，`show` 是唯一的命令。
- `tunnel`——添加、更改和删除网络隧道。
- `monitor` 和 `rtmon`（状态监控）。

## 15.2.2 其他网络命令

`ip` 指令取代了之前的 `route`，后者允许你查看和操作 IP 路由表。该表将包含网关地址和网关路由地址，以及每个接口设备的子网掩码（排除 `lo`）。

要查看 IP 地址，请使用 `ip addr`。或者，`ifconfig` 命令也会响应相同的信息。`ifconfig` 语句像 `ip` 一样也允许你配置网络接口。该命令后面跟着相关的接口（例如 `lo` 或 `eth0`）以及你想要建立的任何选项或该接口的新地址（如果你省略了选项/地址，`ifconfig` 将响应已建立的地址）。命令看起来像以下之一：

```
ifconfig interface options
```

或

```
ifconfig interface address
```

其中 `options` 包括更改接口名称的 `interface`（例如通过 `ifconfig eth0 interface foobar` 将 `eth0` 重命名为 `foobar`）、`up/down` 用于启动或停止接口、`arp/-arp` 用于启用或禁用此设备上使用 ARP 协议、`promis/-promisc` 用于启用或禁用此接口的混杂模式，或 `allmulti/-allmulti` 用于启用或禁用设备上的组播模式。此外，你可以更改 MTU 参数、如果设备是 `ppp` 则更改目的 IP 地址、更改子网掩码并更改设备的 IP 地址。

`route` 或 `ifconfig` 都并非必须，因为 `ip` 可以完成所有这些任务。然而，`route` 和 `ifconfig` 在当前的 Linux 版本中仍然可用。你可能会发现它们比相当复杂的指令更容易用，但最终，这些指令可能会过时；因此，学习 `ip` 是最好的。

我们已经在第 5 章中讨论了 `ping` 和 `traceroute`。作为系统管理员，你可能会发现这些命令在测试网络访问以及你负责的其他设备的可用性时非常有用。然而，这两个命令都可能导致你的网络出现安全漏洞，因为其他人会尝试通过这些程序调查你的局域网。通过 `ping` 或 `traceroute`，黑客可以收集你网络的合法 IP 地址。此类黑客可以利用这些信息进行攻击。

# 512 操作系统概念中的 Linux

表 12.5 Iptables-config 指令

| 指令 | 含义 | 默认值 |
| :--- | :--- | :--- |
| `IPTABLES_MODULES` | 应用防火墙规则后加载的模块列表 | `""` (无) |
| `IPTABLES_UNLOAD` | 在防火墙停止或重启时卸载模块 | `Yes` |
| `IPTABLES_SAVE_ON_STOP` | 可能会从命令行向防火墙添加规则；如果此指令被设置为 `yes`，则在停止防火墙时将所有当前规则保存到 `iptables` | `No` |
| `IPTABLES_SAVE_ON_RESTART` | 如果设置为 `yes`，则在重启防火墙时将所有当前规则保存到 `iptables` | `No` |
| `IPTABLES_SAVE_COUNTER` | 在防火墙停止、重启或执行命令 `/sbin/service iptables save` 时，将所有链和规则的计数器保存到 `iptables` | `No` |
| `IPTABLES_STATUS_NUMERIC` | 在请求防火墙状态时，以数字格式打印 IP 地址和端口 | `Yes` |
| `IPTABLES_STATUS_VERBOSE` | 在请求防火墙状态时，打印关于数据包和字节的统计信息 | `Yes` |
| `IPTABLES_STATUS_LINEMBERS` | 在请求防火墙状态时，打印行号 | `Yes` |

表: `filter`

链 `INPUT` (策略 `ACCEPT` 0 bytes)

| 序号 | 包数 字节 目标 | 入 | 出站 | 源 | 目的 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1899 `ACCEPT` | all | * | 0.0.0.0/0 | 0.0.0.0/0 |
| 2 | 41 `ACCEPT` | all | * | 0.0.0.0/0 | 0.0.0.0/0 |
| 3 | 0 `ACCEPT` | all | * | 0.0.0.0/0 | 0.0.0.0/0 state NEW dpt: 22 |
| 4 | 205 4314 `ACCEPT` | all | * | 0.0.0.0/0 | 0.0.0.0/0 `reject-with-icmp-host-prohibit` |

链 `FORWARD` (策略 `ACCEPT` 0 bytes)

| 序号 | 包数 字节 目标 | 入 | 出站 | 源 | 目的 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 `REJECT` | all | * | 0.0.0.0/0 | 0.0.0.0/0 `reject-with-icmp-host-prohibit` |

链 `OUTPUT` (策略 `ACCEPT` 36 packets, 6678 bytes)

| 序号 | 包数 字节 目标 | 入 | 出站 | 源 | 目的 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 `REJECT` | all | * | 0.0.0.0/0 | 0.0.0.0/0 |

图 12.6 `iptables` 的详细状态。

以及转发 (`FORWARD`) 消息将如何被。最关键的规则是入站消息规则。如果没有适当的（或没有）`INPUT` 规则，你的计算机将开放接收任何类型的消息。你希望确保只有特定类型的消息被程序化到你的计算机。虽然 `OUTPUT` 规则不常见，但你可能希望使用某些规则来控制出站消息，例如防止用户访问特定网站。
