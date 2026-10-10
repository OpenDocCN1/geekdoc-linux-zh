
nat 和 `mangle` 表包含两种额外的链类型。`PREROUTING` 链在数据包进入接口时对其修改。`POSTROUTING` 链用于在数据包准备离开主机时对其修改。`POSTROUTING` 链对于连接的伪装至关重要。

## 内置目标和用户定义链

`Ipchains` 和 `iptables` 使用内置目标来指定数据包的去地。到目前为止，最常见的内置目标是 `DROP` 和 `ACCEPT`。表 9.3 详细描述了这些目标。（还存在其他目标。你可以通过查阅 `Ipchains` 或 `Iptables` 的 man 页面来了解它们。）

### 表 9.3 常见的 Ipchains 和 iptables 目标

| 目标 | 描述 |
| --- | --- |
| DROP | 数据包被立即丢弃。也使用 `REJECT` 目标。 |
| ACCEPT | 允许数据包通过链的其余部分。默认情况下，所有默认链都配置为允许任何所有连接。 |

如果你想创建大量的规则条目，但不希望链变得太长，用户定义链通常很有用。过长的链会减慢数据包处理，而且难以阅读和组织。以下是一个创建、修改并调用用户定义链的序列：

```bash
ipchains -N custom
ipchains -A custom -s 0/0 -d 0/0 -p icmp -j REJECT
ipchains -A input -s 0/0 -d 0/0 -j custom
```

当然，这是一个简单的示例。`-A` 选项向规则“追加”（append），意味着它被放置在链的开头。`-I` 选项将规则添加到链的末尾。创建了 james 的用户定义规则，并在此 `custom` 链中添加了丢弃所有 ICMP 数据包的规则。然后，在默认 `input` 链中添加了一条规则，让所有数据包都由 `custom` 链处理。结果是，任何 ICMP 数据包将被丢弃。如果你犯了错误，忘记让 `input` 链引用链名 `custom`，那么 `custom` 链将永远不会被读取。

在 `iptables` 中，上述命令序列的对应命令非常相似（当然，也可以创建更歧义的用户定义链）。

```bash
ipchains -N custom
ipchains -A custom -s 0/0 -d 0/0 -p icmp -j DROP
ipchains -A input -s 0/0 -d 0/0 -j custom
```

## 指定接口

如果没有指定接口，则假设为第一个接口（通常是 `eth0`）。如果你有多个接口，必须指定你想要添加到链中的接口。因此，在多网卡（NIC）系统中，当你使用 `INPUT` 链拒绝所有 ICMP 流量时，你必须指定它。例如，如果你有一个拥有两个接口且处理所有流量的系统，你必须遵循以下命令：

```bash
ipchains -A input -i eth0 -s 0/0 -d 0/0 -p icmp -j REJECT
ipchains -A input -i eth1 -s 0/0 -d 0/0 -p icmp -j REJECT
```

现在，该系统将不在 `eth0` 或 `eth1` 接口上转发 ICMP 数据包。对于 `iptables`，命令如下：

```bash
iptables -A INPUT -i eth0 -s 0/0 -d 0/0 --protocol icmp --icmp-type echo-reply -j REJECT
iptables -A INPUT -i eth1 -s 0/0 -d 0/0 --protocol icmp --icmp-type echo-reply -j REJECT
```

在 `iptables` 和 `Ipchains` 中，`FORWARD` 链允许你指定源和目的接口。这是因为 `FORWARD` 链用于连接伪装。因此，`-i` 和 `-o` 选项允许你标记在接口之间通过的数据包。

## 设置策略

`Ipchains` 和 `iptables` 默认接受所有连接。安全的选项是将默认策略设置为拒绝所有流量。你可以创建规则来显式允许某些流量类型。你可以使用 `-P` 选项更改此默认立场。例如，以下 `ipchains` 命令将 `INPUT` 链的默认策略更改为拒绝：

```bash
ipchains -P input DENY
```

以下命令在 `iptables` 中执行相同：

```bash
iptables -P input DROP
```

要将策略重置为接受，只需使用 `ACCEPT` 目标。

## 列出表和链

一旦生成 `Ipchains` 或 `iptables`，就可以列出它们。以下命令将列出所有链：

```bash
ipchains -L
iptables -L
```

## 保存、刷新和恢复规则

一旦你在 `Ipchains` 或 `iptables` 中创建了规则，可以使用以下命令保存它们：

```bash
/sbin/ipchains-save
/sbin/iptables-save
```

这些命令有两个用处：首先，你可以将规则保存到文本文件中。其次，以防防火墙丢失，备份规则是重要的。例如，要将你的 `iptables` 信息保存到文本文件中，你应该执行以下命令：

```bash
/sbin/iptables-save > iptables.txt
```

要刷新现有规则，可以使用 `-F` 选项：

```bash
ipchains -F
iptables -F
```

如果不带参数，此命令将清除 `Ipchains` 中所有规则的内容，以及 `iptables` 中 `filter` 表中的所有规则。要刷新特定的链，你需要执行以下命令：

```bash
ipchains -F input
iptables -F INPUT
```

`-F` 函数同样不会将策略从 `DROP` 更改为 `ACCEPT`。你必须使用之前讨论过的 `-P` 选项。

如果你需要恢复备份信息，可以使用以下命令：

```
iptchains-restore
iptables-restore
```

例如，要使用之前创建的 `iptables.txt` 文件恢复 `Iptables` 数据库，你应该使用以下命令：

```
/sbin/iptables-restore iptables-restore.txt
```

默认情况下，`iptables-restore` 会将任何恢复信息追加到任何现有的规则中。如果你需要，可以使用 `-f` 选项来刷新现有规则。

然而，`iptables-restore` 命令在每次使用时会自动删除任何 `Iptables` 规则。你可以使用 `-n` 选项，它会将恢复文件的内容追加到，而不会覆盖任何现有规则。

# 使用 Ipchains 进行连接伪装（Masquerade）

`Ipchains` 命令只有一个表和三个链（`INPUT`、`FORWARD` 和 `OUTPUT`）。使用 `FORWARD` 命令和 `MASQ` 目标，你可以伪装任何你所需的 IP 地址。例如，假设你有一个路由器连接了 `192.168.1.0/24` 网络和 `10.100.0.0/24` 网络。进一步假设该防火墙的 `eth0` 接口包含互联网可访问的 IP 地址 `66.151.1/8`。在路由器上发出的以下 `Ipchains` 命令将允许提供 IP 网络通过互联网通信：

```
iptchains -A forward -i eth0 -s 192.168.1.0/24 -j MASQUERADE
iptchains -A forward -i eth0 -s 10.100.0.0/24 -j MASQUERADE
```

此规则指定 `192.168.1.0/24` 和 `10.100.0.0/24` 网络将在 `eth0` 上被伪装为 `66.151.1/8`。`-A` 选项向 `forward` 命令添加路由，`-I` 选项指定了 `eth0` 接口。`-s` 选项指定了相关的网络。

这种特定的配置实际上暴露了网络。任何远程主机都能够使用你的伪装防火墙来访问你的主机。在 `filter` 表的 `FORWARD` 链中添加以下内容可以确保你的伪装路由器仅对你的内部网络进行伪装：

![](img/a7a9caa80ec85507179284d91e216f9f_467_0.png)

```
ipchains -A forward -s 192.168.1.0/24 -j ACCEPT
ipchains -A forward -d 192.168.1.0/24 -j ACCEPT
ipchains -A forward -s 10.100.100.0/24 -j ACCEPT
ipchains -A forward -d 10.100.100.0/24 -j ACCEPT
ipchains -A forward -j DROP
```

# Iptables 伪装模块

你可以在互联网上使用的许多协议（如 FTP 或 RealAudio）都需要额外的支持。`Iptables` 提供了几个模块，允许伪装的客户端访问这些资源。其中一些描述在表 9.4 中。

### 表 9.4 Ipchains 伪装模块

| 模块 | 描述 |
