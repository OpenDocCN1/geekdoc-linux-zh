
[root@fedora-serverA]# `sysctl -w net.ipv4.ip_forward=1 >> /etc/sysctl.conf`

> **注意** 某些发行版已经在 `sysctl.conf` 文件中定义了（但禁用了）内核参数，因此可能需要将现有变量更改为所需的值。确保先检查文件是否存在你想要更改的设置并调整该值，而不是像我们所做的那样在文件末尾追加。

对于其他发行版，这里讨论的方法可能会不同。如果你不确定你的发行版如何工作，或者如果证明它让你头疼的问题多于收益，只需从启动序列中禁用内置脚本并添加你自己的。如果你选择编写自己的脚本，可以使用以下大纲：

```bash
#!/bin/sh

## 定义 iptables 和 modprobe 的位置。

IPT="/sbin/iptables"

MODPROBE="/sbin/modprobe"

## 在此处添加你的代码行。

$MODPROBE ip_tables

$MODPROBE ip_state

$MODPROBE ipt_filter

$MODPROBE ip_contract

$MODPROBE ip_conntrack_ftp

$MODPROBE ipt_nat

$MODPROBE ip_nat_ftp

## 清空当前链，删除非标准链并将计数器清零。

$IPT -t filter -X

$IPT -t filter -Z

$IPT -t mangle -F

$IPT -t mangle -Z

$IPT -t nat -F

$IPT -t nat -X

$IPT -t nat -Z

## 在此处添加你的规则。这里有一个示例供你开始。

$IPT -A INPUT -i lo -j ACCEPT

## 在此处添加任何 /proc 设置。

echo "1" > /proc/sys/net/ipv4/tcp_synccookies
```

# iptables 命令

`iptables` 命令是配置 Netfilter 系统的关键。快速查看 `iptables -h` 命令的在线帮助，可以看到令人惊叹的配置选项。在本节中，我们将介绍其中一些选项并学习如何使用它们。

该命令的核心能够定义作为规则链部分的单个规则。每个单独规则都有一个数据包匹配标准和一个相应的动作。当数据包遍历系统时，它将遍历这些链。当规则匹配成功时，将执行指定的动作。

# 管理链

命令的格式随动作而异。以下是可能的动作：

- 添加规则：`iptables -A`
- 删除规则：`iptables -D`
- 插入规则：`iptables -I`
- 替换规则：`iptables -R`
- 列出规则：`iptables -L`
- 清刷规则：`iptables -F`
- 计数器清零：`iptables -Z`
- 创建新链：`iptables -N`
- 删除链：`iptables -X`
- 设置默认策略：`iptables -P`
- 重命名链：`iptables -E`

# Linux 管理：初学者指南

回想一下有内置表 `NAT`, `mangle`, `raw` 和五个内置链 `PREROUTING`, `POSTROUTING`, `INPUT`, `FORWARD` 和 `OUTPUT`。

然而，随着规则变得越来越复杂，有时有必要将它们分组。Netfilter 允许你通过定义自己的链并将其放置在适当的表中来实现。例如，让我们创建一个名为 `to_net10` 的链，用于处理所有目标为 `10.0.0.0/8` 网络且经过 `FORWARD` 链的数据包。

```bash
[root@fedora-serverA]# iptables -t filter -N to_net10

[root@fedora-serverA]# iptables -t filter -A FORWARD -d 10.0.0.0/8 -j to_net10

[root@fedora-serverA]# iptables -t filter -A to_net10 -j RETURN
```

在这个示例中，`to_net10` 链什么都不做，只是返回 `FORWARD` 链。创建一个名为 `to_net10` 的示例链，我们将使用

```bash
[root@fedora-serverA]# iptables -t filter -N to_net10
```

# 定义规则规范

在前面的章节中，我们提到了规则规范 `rule-spec`。规则规范是 Netfilter 用于匹配数据包的规则列表。如果指定的规则规范匹配了数据包，Netfilter 将对其应用所需的动作。以下是

- `-p []` 协议 指定了要对比的 IP 协议。你可以使用 `/etc/protocols` 文件中定义的任何协议，例如 `"tcp"`、`udp"` 或

## 第 13 章：Linux 防火墙

`icmp.` `all` 的内置值表示所有 IP 数据包都将匹配。该协议未在 `/etc/protocols` 中定义，你可以在此处使用协议数。例如，`47` 代表 `gre.`。感叹号 `!` 表示反转检查结果。因此，指定 `-p tcp` 意味着非 TCP 数据包。如果未提供此选项，Netfilter 将假设为 `all`。`--protocol` 选项是 `other` 的别名。用法示例：

```
[root@serverA ~]# iptables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT
```

对于 `ip6tables`，使用：

```
[root@serverA ~]# ip6tables -t filter -A INPUT -p tcp --dport 80 -j ACCEPT
```

这些规则将接受目标为 `INPUT` 链上 TCP 端口 `80` 的包。

- `-s [] address [mask]` 此选项指定要检查的源 IP 地址。当与可选掩码结合时，源 IP 可以与整个网段进行比较。配合 `-p`，使用感叹号 `!` 会反转规则含义。因此，指定 `-s! 10.13.17.2` 意味着所有并非来自 `10.13.17.2` 的包。注意地址和掩码可以缩写。用法示例：

```
[root@serverA ~]# iptables -t filter -A INPUT -s 172.16/16 -j DROP
```

此规则将丢弃所有来自 `172.16.0.0/16` 网络的包。

要使用 `ip6tables` 丢弃来自 IPv6 网络范围 `2001:DB8::/32` 的所有包，我们将使用如下规则：

```
[root@serverA ~]# ip6tables -t filter -A INPUT -s 2001:DB8::/32 -j DROP
```

- `-d [] address [mask]` 此选项指定要检查的目标 IP 地址。当与可选掩码结合时，目标目标 IP 可以与整个网段进行比较。配合 `-s`，感叹号会反转规则，地址和掩码可以缩写。用法示例：

```
[root@serverA ~]# iptables -t filter -A FORWARD -d 10.100.93.0/24 -j ACCEPT
```

此规则将允许通过 `FORWARD` 链且目标为 `10.100.93.0/24` 节点的所有包。

- `-j target` 此选项指定要“跳转”到的动作。在 `iptables` 术语中，这些动作被称为目标 `targets`。我们目前为止看到的目标有 `ACCEPT`、`DROP` 和 `RETURN`。前两个接受和丢弃包的操作分别与创建额外的链有关。

正如我们在上一节中看到的，可以创建自己的链来保持结构清晰并适应更复杂的规则。如果 `iptables` 正在评估一个不是内置链的规则集，`RETURN` 目标将告诉 `iptables` 返回到父链。使用早前的 `net10` 示例，当 `iptables` 到达 `-j RETURN` 时，它将回到之前停止的 `FORWARD` 链继续处理。如果 `iptables` 在其中一个内置链中看到 `RETURN` 动作，它将执行该链的默认规则。

额外的目标可以通过 Netfilter 模块加载。例如，`REJECT` 目标可以通过 `ipt_REJECT` 加载，它将丢弃包并向服务器返回 ICMP 错误包。另一个有用的目标是 `ipt_REDIRECT`，如果包的目标是其他地方，它可以使包指向 NAT 主机本身。

- `-i interface` 此选项指定接收数据包的接口。这对于当数据包来自物理位置（如 DMZ 接口）时应应用特殊规则的情况非常有用。如果 `eth1` 是你的 DMZ 接口，且你想将包发送到 `10.4.3.2` 主机，可以使用：

```
[root@serverA ~]# iptables -A FORWARD -i eth1 -d 10.4.3.2 -j ACCEPT
```

- `-o interface` 此选项指定数据包离开系统的接口。例如：

```
[root@serverA ~]# iptables -A FORWARD -i eth0 -o eth1 -j ACCEPT
```
