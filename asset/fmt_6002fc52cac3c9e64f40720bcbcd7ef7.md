
关于通过数字定义规则，你也可以通过规则的名称或数字来引用规则。由于 `iptables` 是线性的，每条添加到内核的规则都会被分配一个数字，要么是按照添加的顺序（如使用 `-A` 时），要么是根据 `-I` 默认决定的位置（即倒序），或者是由用户定义的显式顺序。例如，假设你想在 `INPUT` 链的顶部添加一条新规则，作为链中的第一条规则，并且你想拒绝所有发送到主机 `113` 端口的 `SYN` 数据包。你将使用以下语法：

```
$IPTABLES -I INPUT 1 -p tcp -m tcp --dport 113 \n--syn -j REJECT
```

由于 `-I` 的默认行为是将新规则插入到链的位置 1 位置，因此以下命令与上一个示例相同：

```
$IPTABLES -I INPUT -p tcp -m tcp --dport 113 \n--syn -j REJECT
```

如果你只想将此规则添加到 `INPUT` 链中当前规则set的末尾，你将使用此语法：

```
$IPTABLES -A INPUT -p tcp -m tcp --dport 113 \
--syn -j REJECT
```

除了添加规则外，可能还需要在规则当前位置删除或替换规则。替换规则的方法与这里的示例类似，你可以在替换时选择规则的名称或数字。

```
$IPTABLES -R INPUT 1 -p tcp -m tcp --dport 113 \
--syn -j ACCEPT
```

而删除规则的过程更加简单：

```
$IPTABLES -D INPUT 1
```

除了创建规则外，你还可以使用 `-N` 命令通过 `iptables` 创建自己的链：

```
$IPTABLES -N my_chain
```

与规则一样，你也可以删除、替换或重命名链。删除链通过使用 `-X` 选项完成：

```
$IPTABLES -X my_chain
```

重命名链可以通过使用 `-E` 选项实现，如示例所示：

```
$IPTABLES -E my_chain new_name_for_my_chain
```

最后，可以使用 `-P` 选项为链设置默认策略。这允许为链创建默认行为，可能是为了调试或防止可能导致安全漏洞的错误。例如，想象一下你不希望防火墙允许任何进入防火墙自身的连接。这不应与转发连接混淆，转发连接不是指向防火墙本身，而是指向防火墙另一侧的系统。创建一个阻止访问防火墙数据包的默认策略，可以将 `INPUT` 链的策略更改为 `DROP` 或 `REJECT`：

```
$IPTABLES -P INPUT DROP
```

`iptables` 有几个常用的管理命令：列表（`-L`）和置零（`-Z`）选项。列表提供了列出系统中当前加载的 `iptables` 规则的方法；`-Z` 选项将为每条 `iptables` 规则计数清零。稍后我们会回顾计数器，但首先，要在没有计数器的情况下查看系统上的所有当前规则，你的 `iptables` 命令将如下：

```
iptables -L
Chain INPUT (policy ACCEPT)

target     prot opt source destination

RH-Lokkit-0-50-INPUT all -- anywhere anywhere

SILENT udp -- anywhere anywhere udp

SILENT tcp -- anywhere anywhere tcp

SILENT udp -- anywhere anywhere udp

SILENT tcp -- anywhere anywhere tcp

SILENT udp -- anywhere anywhere udp

SILENT tcp -- anywhere anywhere tcp

LOG all -- anywhere anywhere limit: avg 1/sec burst S

LOG level info tcp-sequence tcp-options ip-options prefix "STEALTH -- DROP"

Chain FORWARD (policy ACCEPT)

target     prot opt source destination

RH-Lokkit-0-50-INPUT all -- anywhere anywhere

Chain OUTPUT (policy ACCEPT)

target     prot opt source destination

TCPMSS tcp -- anywhere anywhere tcp flags:SYN,RST,SYN

TCPMSS clamp to PTMU

Chain RH-Lokkit-0-50-INPUT (2 references)

target     prot opt source destination

ACCEPT udp -- localhost.localdomain anywhere udp spt:domain

dpts:1025:65535
```

`-L` 命令还具有报告规则附加信息的能力，例如该规则处理的流量大小、上述的计数器、规则编号，以及在最详尽（verbose）模式下关于规则的非常详细的信息。传递给 `iptables` 最常用的命令是 `-L` 带有 `-v` 开关，这将导致 `iptables` 报告与一个示例相同的信息，以及关于该规则处理的流量量或规则计数器的额外信息。

```
iptables -n -v
Chain INPUT (policy ACCEPT 78 packets, 4208 bytes)
pkts bytes target prot in out source destination
458K 277M RH-Lokkit-0-50-INPUT all * * 0.0.0.0/0 0.0.0.0/0
0 SILENT udp eth0 * * 0.0.0.0/0 0.0.0.0/0
0 SILENT tcp eth0 * * 0.0.0.0/0 0.0.0.0/0
70 3536 LOG all * * limit: avg 1/sec burst 5 LOG flags 7 level 6 prefix --STEALTH -- DROP 
Chain FORWARD (policy ACCEPT 0 packets, 0 bytes)
pkts bytes target prot in out source destination
0 RH-Lokkit-0-50-INPUT all * * 0.0.0.0/0 0.0.0.0/0
Chain OUTPUT (policy ACCEPT 449K packets, 143M bytes)
pkts bytes target prot in out source destination
10413 625 TCPMSS tcp * * ppp0 0.0.0.0/0 0.0.0.0/0
tcp flags:06x06/0x02 TCPMSS clamp to PMU
Chain RH-Lokkit-0-50-INPUT (2 references)
pkts bytes target prot in out source destination
12981 2380K udp * * 127.0.0.1 0.0.0.0/0
dp spt:53 dports:1025:65535
0 ACCEPT esp * * 0.0.0.0/0 0.0.0.0/0
0 ACCEPT ah * * 0.0.0.0/0 0.0.0.0/0
0 ACCEPT 61 * * 0.0.0.0/0 0.0.0.0/0
0 ACCEPT udp * * 0.0.0.0/0 0.0.0.0/0
dp dpt:500
0 ACCEPT udp * * 0.0.0.0/0 0.0.0.0/0
dp dpt:4500
0 ACCEPT tcp * * 0.0.0.0/0 0.0.0.0/0
tcp dpt:22 flags:0x16/0x02
0 ACCEPT tcp * * 0.0.0.0/0 0.0.0.0/0
```
