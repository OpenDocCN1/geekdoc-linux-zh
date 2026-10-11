
| -A | --append <chain> <rule specification> | 在链末尾追加规则。 |
| -I | --insert <chain> [<rule number> <rule specification> | 在链开头插入规则。 |
| -R | --replace <chain> <rule number> | 替换链中的规则。 |
| -D | --delete <chain> <rule number> | 删除链中位置为 <rule number> 的规则或指定的规则。 |
| -C | --check <chain> <rule specification> | 检查链是否匹配该规则。 |

### 表 3.5 filter 表操作

| 选项 | 说明 |
| --- | --- |
| -i | --interface [<interface>] | 针对 INPUT 或 FORWARD 链或其用户定义的子链的入站数据包指定接口。如果未指定，则包含所有接口。 |
| -o | --out-interface [<interface>] | 针对 OUTPUT 或 FORWARD 链或其用户定义的子链的出站数据包指定接口。如果未指定，则包含所有接口。 |
| -p | --protocol [<protocol>] | 指定指定的 IP 协议。内置协议有 tcp、udp、icmp 和 all。协议值为： |
| -s | --source [<address>] | 指定源地址。 |
| -d | --destination [<address>] | 指定目的地址。 |

### 表 3.5 filter 表操作（续）

| 选项 | --jump <target> | 说明 |
|---|---|---|
| -j | --jump <target> | `filter` 表命令由 `ip_tables` 模块提供。该功能通过加载模块启用，这在首次调用 `iptables` 命令时自动完成，或者它可以编译到内核本身，这意味着你完全不需要担心模块加载的问题。 |
| -g | --goto <target> | `filter` 表命令由 `ip_tables` 模块提供。该功能通过加载模块启用，这在首次调用 `iptables` 命令时自动完成，或者它可以编译到内核本身，这意味着你完全不需要担心模块加载的问题。 |
| -c | --set-counters <number> | `filter` 表命令由 `ip_tables` 模块提供。该功能通过加载模块启用，这在首次调用 `iptables` 命令时自动完成，或者它可以编译到内核本身，这意味着你完全不需要担心模块加载的问题。 |

### 表 3.5 filter 表操作

| 选项 | 说明 |
| --- | --- |
| -i | --interface [<interface>] | 针对 INPUT 或 FORWARD 链或其用户定义的子链的入站数据包指定接口。如果未指定，则包含所有接口。 |
| -o | --out-interface [<interface>] | 针对 OUTPUT 或 FORWARD 链或其用户定义的子链的出站数据包指定接口。如果未指定，则包含所有接口。 |
| -p | --protocol [<protocol>] | 指定规则适的 IP 协议。内置协议有 tcp、udp、icmp 和 all。协议值为 |
| -s | --source [<address>] | 指定源地址。 |
| -d | --destination [<address>] | 指定目的地址。 |

### 表 3.5 filter 表操作（续）

| 选项 | --jump <target> | 说明 |
|---|---|---|
| -j | --jump <target> | `filter` 表命令由 `ip_tables` 模块提供。该功能通过加载模块启用，这在首次调用 `iptables` 命令时自动完成，或者它可以编译到内核本身，这意味着你完全不需要担心模块加载的问题。 |
| -g | --goto <target> | `filter` 表命令由 `ip_tables` 模块提供。该功能通过加载模块启用，这在首次调用 `iptables` 命令时自动完成，或者它可以编译到内核本身，这意味着你完全不需要担心模块加载的问题。 |
| -c | --set-counters <number> | `filter` 表命令由 `ip_tables` 模块提供。该功能通过加载模块启用，这在首次调用 `iptables` 命令时自动完成，或者它可以编译到内核本身，这意味着你完全不需要担心模块加载的问题。 |

### 表 3.6 tcp 表匹配操作

| 选项 | 说明 |
|---|---|
| --source-port | --sport [!] <port>[:<port>] | 该命令指定源端口。 |
| --destination-port | --dport [!] <port>[:<port>] | 该命令指定目的端口。 |
| --tcp-flags | [!] <mask> [,mask> | 该命令测试掩码中的位，以下位必须设置以进行匹配。 |
| [] -syn | SYN 标志必须作为初始连接请求设置。 |
| --tcp-option | <number> | 唯一法的 tcp 选项是发送主机愿意接受的最大数据包大小。 |

### 表 3.7 udp 表匹配操作

| 选项 | 说明 |
| --- | --- |
| --source-port | --sport [!] <port>[:<port>] | 该命令指定源端口。 |
| --destination-port | --dport <port>[:<port>] | 该命令指定目的端口。 |

### 表 3.8 icmp 表匹配操作

| 选项 | 说明 |
| --- | --- |
| --icmp-type | [!] <type> | 指定 ICMP 类型或数字。ICMP 类型用于替代源端口。 |

## 额外的 ICMP 和 ICMP6 支持

`iptables` 支持许多额外的、不常用的或特定特定的 ICMP 消息类型和子类型，还可以通过 `icmp6` 扩展与 IPv6 ICMP 数据包配合工作。要查看完整列表，请使用以下 `iptables` 命令：

```
iptables -p icmp -h
iptables -p ipv6-icmp -h
```

### filter 表目标扩展

`filter` 表目标扩展包含了日志功能，以及拒绝数据包而非丢弃数据包的能力。

表 3.9 列出了 REJECT 目标可用的选项。REJECT 目标有一个单一可用选项。对于其他选项，你可以在 `-j <TARGET>` 之后添加 `-h` 标志来查看更多选项，例如：`iptables -j <TARGET> -h`。

### ULOG 表目标扩展

与 LOG 目标相关的是 ULOG 目标，它将日志消息发送到用户态程序进行日志记录。在 ULOG 的后台，数据包包会通过你选择的 `netlink` socket（默认是 socket 1）被内核复制。用户态守护进程随后将从 socket 中读取消息并按其意愿进行处理。ULOG 目标通常用于提供比标准 LOG 目标更详的日志记录。

与 LOG 目标一样，在匹配 ULOG 目标规则后处理继续。ULOG 目标有四个配置选项，如表 3.11 所示。

| -j LOG Option | 描述 |
| --- | --- |
| --log-level <syslog level> | 日志级别可以是数字或符号链接优先级，如 `/usr/include/sys/syslog.h` 所示。这些级别与 `/etc/syslog.conf` 中使用的日志级别相同。级别包括 emerg (0), alert (1), crit (2), warn (3), notice (4), notice (5), info (6), memerg (0), alert (1), crit (2), err (3), warn (4), notice (5), info (6), 以及 debug (7)。 |
| --log-prefix <descriptive string> | 前缀是一个带引号的字符串，将打印在规则日志消息的开头。 |
| --log-ip-options | 此命令在日志输出中包含任何 IP 头部选项。 |
| --log-tcp-sequence | 此命令在日志输出中包含 TCP 数据包的序列号。 |
| --log-tcp-options | 此命令在日志输出中包含任何 TCP 头部选项。 |
| --log-uid | 此命令在日志输出中包含生成数据包的用户 ID。 |

## 第 3 章 iptables：遗留 Linux 防火墙管理程序

### 表 3.10 REJECT 目标扩展

| -j REJECT Option | 描述 |
| --- | --- |
