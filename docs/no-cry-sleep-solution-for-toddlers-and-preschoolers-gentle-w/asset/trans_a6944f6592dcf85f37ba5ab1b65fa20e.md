

## 添加和更改规则

你使用 iptables 命令添加和修改链规则。iptables 命令由关键字 iptables 组成，后跟表示要执行的命令的参数。例如，iptables -A 是添加新规则的命令，而 iptables -D 是删除规则的命令。iptables 命令列在表 19-4 中。以下命令仅列出为系统当前定义的链及其规则。输出显示由 iptables 命令创建的默认值。

```
iptables -L -n
Chain input (policy ACCEPT):
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

要向链添加新规则，请使用 -A。使用 -D 删除它，并使用 -R 替换它。在命令之后，列出规则适用的链，例如 INPUT、OUTPUT 或 FORWARD 链，或用户定义的链。接下来，你列出不同的选项来指定要执行的操作（大多数与 ipchains 使用的相同，只有少数例外）。-s 选项指定附加到数据包的源地址，-d 指定目标地址，而 -j 选项指定规则的目标。ACCEPT 目标将允许数据包通过。-i 选项现在表示输入设备，只能与 INPUT 和 FORWARD 链一起使用。-o 选项表示输出设备，只能用于 OUTPUT 和 FORWARD 链。表 19-5 列出了几个基本选项。

| Option | Function |
|---|---|
| -A chain | Appends a rule to a chain. |
| -D chain [ rulenum ] | Deletes matching rules from a chain. Deletes rule rulenum (1 = first) from chain. |
| -I chain [rulenum] | Inserts in chain as rulenum (default 1 = first). |
| -R chain rulenum | Replaces rule rulenum (1 = first) in chain. |
| -L [chain] | Lists the rules in chain or all chains. |
| -E [chain] | Renames a chain. |
| -F [chain] | Deletes (flushes) all rules in chain or all chains. |
| -R chain | Replaces a rule; rules are numbered from 1. |
| -Z [chain] | Zero counters in chain or all chains. |
| -N chain | Creates a new user-defined chain. |
| -X chain | Deletes a user-defined chain. |
| -P chain target | Changes policy on chain to target. |

## iptables 选项

iptables 包设计为可扩展的，并且有许多带有选择标准的选项可以与 iptables 一起使用。例如，TCP 扩展包括 --syn 选项，用于检查 SYN 数据包。ICMP 扩展提供 --icmp-type 选项，用于指定 ICMP 数据包，例如 ping 操作中使用的数据包。limit 扩展包括 --limit 选项，可用于限制指定时间段内匹配数据包的最大数量，例如一秒。

| Option | Function |
|---|---|
| -p [1] proto | Specifies a protocol, such as TCP, UDP, ICMP, or ALL. |
| -s [1] address[/mask] [1] [port[:port]] | Source address to match. With the port argument, you can specify the port. |
| --sport [1] [port[:port]] | Source port specification. You can specify a range of ports using the colon, port:port. |
| -d [1] address[/mask] [1] [port[:port]] | Destination address to match. With the port argument, you can specify the port. |
| --dport [1] [port[:port]] | Destination port specification. |
| --icmp-type [1] typename | Specifies ICMP type. |
| -i [1] name[*] | Specifies an input network interface using its name (for example, eth0). The + symbol functions as a wildcard. The + attached to the end of the name matches all interfaces with that prefix (eth+ matches all Ethernet interfaces). Can be used only with the INPUT chain. |
| -j target [port] | Specifies the target for a rule (specify [port] for REDIRECT target). |
| --to-source < ipaddr> [ -< ipaddr> ] [: port- port] | Used with the SNAT target, rewrites packets with new source IP address. |
| --to-destination - ipaddr> [ -< ipaddr> ] [: port- port] | Used with the DNAT target, rewrites packets with new destination IP address. |
| -n | Numeric output of addresses and ports, used with -L. |
| -o [1] name[*] | Specifies an output network interface using its name (for example, eth0). Can be used only with FORWARD and OUTPUT chains. |
| -t table | Specifies a table to use, as in -t nat for the NAT table. |
| -v | Verbose mode, shows rule details, used with -L. |
| -x | Expands numbers (displays exact values), used with -L. |
| [1] -f | Matches second through last fragments of a fragmented packet. |

