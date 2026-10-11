
### iptables 命令选项

| `-P \| --policy <chain> <policy>` | 为内置链 `INPUT`、`OUTPUT` 或 `FORWARD` 之一定义默认策略。策略是 `ACCEPT` 或 `DROP`。 |
| `-L \| --list [<chain>]` | 列出链中的规则，如果未指定则列出所有链。 |
| `-Z \| --zero` | 重置与每个链关联的数据包和字节计数器。 |
| `-h \| <some command> -h` | 列出 `iptables` 命令和选项，或者如果前面有 `iptables` 命令，则列出该命令的语法和选项。 |
| `--modprobe=<command>` | 在向链中添加或插入规则时，使用 `<command>` 加载必要的模块。 |
| `-E \| --rename-chain <old_chain> <new_chain>` | 将用户定义的链 `<old_chain>` 重命名为用户定义的链 `<new_chain>`。 |

`-h` 帮助命令显然不是对链的操作，`--modprobe=<command>` 也不是，但我不知道在哪里列出这些命令更合适。

## 表 3.3

列表链命令的选项

| **选项** | **描述** |
| :--- | :--- |
| `-L -n` | `--numeric` | 以数字形式列出 IP 地址和端口号，而不是以名称列出 |
| `-L -v` | `--verbose` | 列出每条规则的额外信息，例如字节和分组计数器、规则选项以及相关的网络接口 |
| `-L -x` | `--exact` | 列出计数器的精确值，而不是四舍五入后的值 |
| `-L -line-numbers` | 列出规则在其所属链中的位置 |

### 过滤器表的操作规则

在链内创建或删除规则最常用的命令如表 3.4 所示。

## 表 3.4

针对单个规则的链命令

| **命令** | **描述** |
| :--- | :--- |
| `-A` | `--append <chain>` | 将规则附加到链的末尾 |
| `-I` | `--insert <chain>` | 在链的开头插入规则 |
| `-R` | `--replace <chain> <rule number> <rule specification>` | 替换链中的规则 |
| `-D` | `--delete <chain> <rule number>` | 删除链中位于 `rule_number` 位置的规则 |

### 基础过滤器表匹配操作

默认 `iptables` 过滤器表中支持的基础过滤器匹配操作如表 3.5 所列。

## 表 3.5

过滤器表规则操作

| 选项 | 描述 |
|---|---|
| `-i \| --in-interface [!] [<interface>]` | 对于 `INPUT` 或 `FORWARD` 链或其用户定义子链上的入站分组，指定规则适用的接口名称。如果未指定接口，则隐含所有接口。 |
| `-o \| --out-interface [!] [<interface>]` | 对于 `OUTPUT` 或 `FORWARD` 链或其用户定义子链上的出站分组，指定规则适用的接口名称。如果未指定接口，则隐含所有接口。 |
| `-p \| --protocol [!] [<protocol>]` | 指定规则适用的 IP 协议。内置协议包括 `tcp`、`udp`、`icmp` 和 `all`。协议值可以是 `/etc/protocols` 中列出的名称或数值。 |
| `-s \| --source \| --src [!] <address>[</mask>]` | 指定 IP 头中的主机或网络源地址。 |
| `-d \| --destination \| --dst [!] <address>[</mask>]` | 指定 IP 头中的主机或网络目标地址。 |
| `-j \| --jump <target>` | 指定如果分组匹配规则时的目标处置方式。默认目标包括内置目标、扩展或用户定义的链。 |
| `[!] -f \| --fragment` | 指定第二个及后续的片段分组。该选项的否定形式指定非片段分组。 |
| `-c \| --set-counters <packets> <bytes>` | 初始化分组和字节计数器。 |

> **规则目标是可选的**
>
> 如果分组匹配一个没有目标处置方式的规则，分组计数器会被更新，但列表遍历会继续。

### TCP 过滤器表匹配操作

TCP 头匹配选项如表 3.6 所列。

## 表 3.6

**TCP 过滤器表匹配操作**

| 选项 | 描述 |
| :--- | :--- |
| `--source-port` \| `--sport` [!] `<port>[:port]` | 此命令指定源端口。 |
| `--destination-port` \| `--dport` [!] `<port>[:port]` | 此命令指定目标端口。 |
| `--tcp-flags` [!] `<mask>,<mask>` [!] `<set>,<set>` | 此命令测试掩码列表中的位，其中下列位必须被设置才能匹配。 |
| `[!] -syn` | `SYN` 标志必须设置为初始连接请求。 |
| `--tcp-option` [!] `<number>` | 唯一的合法 TCP 选项是发送主机愿意接受的最大分组大小。 |

### UDP 过滤器表匹配操作

UDP 头匹配选项如表 3.7 所列。

## 表 3.7

**UDP 过滤器表匹配操作**

| 选项 | 描述 |
| :--- | :--- |
| `--source-port` \| `--sport` [!] `<port>[:port]` | 指定源端口 |
| `--destination-port` \| `--dport` [!] `<port>[:port]` | 指定目标端口 |

### ICMP 过滤器表匹配操作

ICMP 头匹配选项如表 3.8 所列。

## 表 3.8

**ICMP 过滤器表匹配操作**

| 匹配 | 描述 |
| :--- | :--- |
| `--icmp-type` [!] `<type>` | 指定 ICMP 类型名称或编号。ICMP 类型用于代替源端口。 |

主要支持的 ICMP 类型名称和数值如下：

- `echo-reply` (0)
- `destination-unreachable` (3)
    - `network-unreachable`
    - `host-unreachable`
    - `protocol-unreachable`
    - `port-unreachable`
    - `fragmentation-needed`
    - `network-unknown`
    - `host-unknown`
    - `network-prohibited`
    - `host-prohibited`
- `source-quench` (4)
- `redirect` (5)
- `echo-request` (8)
- `time-exceeded` (10)
- `parameter-problem` (11)

> **额外的 ICMP 支持**
>
> `iptables` 支持许多额外的、不太常见或路由器特定的 ICMP 消息类型和子类型。要查看完整列表，请使用以下 `iptables` 帮助命令：
>
> ```
> iptables -p icmp -h
> ```

## 过滤器表目标扩展

过滤器表目标扩展包括日志记录功能以及拒绝（而不是丢弃）分组的能力。

表 3.9 列出了 `LOG` 目标可用的选项。表 3.10 列出了 `REJECT` 目标可用的单一选项。

## 表 3.9

`LOG` 目标扩展

`-j LOG` 选项

| 选项 | 描述 |
| :--- | :--- |
| `--log-level <syslog level>` | 日志级别是 `/usr/include/sys/syslog.h` 中列出的数值或符号日志优先级。这些与 `/etc/syslog.conf` 中使用的日志级别相同。级别包括 `emerg` (0)、`alert` (1)、`crit` (2)、`err` (3)、`warn` (4)、`notice` (5)、`info` (6) 和 `debug` (7)。 |
| `--log-prefix <"descriptive string">` | 前缀是一个带引号的字符串，将打印在规则的日志消息开头。 |
| `--log-ip-options` | 此命令在日志输出中包含任何 IP 头选项。 |
| `--log-tcp-sequence` | 此命令在日志输出中包含 TCP 分组的序列号。 |
| `--log-tcp-option` | 此命令在日志输出中包含任何 TCP 头选项。 |

## 表 3.10

`REJECT` 目标扩展

`-j REJECT` 选项

| 选项 | 描述 |
| :--- | :--- |
