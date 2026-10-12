
# iptables 规则选项

## --replace -R

用规则规范和目标替换链中的规则编号。如果规则编号或规则规范解析为多个地址，则命令执行失败。

```
iptables -R chain rule-number rule-specification --jump target
```

## --list -L

显示链中的规则。省略链名（`chain`）则以显示所有链的规则。使用 `--line-numbers` 显示规则编号，或从第 887 页的列表中选择其他显示标准。

```
iptables -I [chain] display-criteria
```

## --flush -F

删除链中的所有规则。当未指定链时，省略链名将删除所有链中的所有规则。配合 `-L` 使用以便在清除之前显示计数器。

```
iptables -Z [-L] [chain]
```

## --zero -Z

当未指定链时，更改链或所有链中所有数据包和字节计数器的零值。配合 `-L` 使用以便在之前显示计数器。

## --delete-chain -X

删除名为 `chain` 的用户定义链。如果不指定链，则删除所有用户定义链。你不能删除一个目标指向的链。

```
iptables -X chain
```

## --policy -P

为内置链 `builtin-chain` 设置默认目标或内置目标 `builtin-target`。此策略适用于不匹配链中任何规则的数据包。如果链没有策略，则未匹配的数据包将被 `ACCEPT`。

## --rename-chain -E

将链的名称 `old` 重命名为 `new`。

```
iptables -E old new
```

## --help -h

显示 `iptables` 命令语法的摘要。

```
iptables -h
```

遵循扩展协议，使用 `-h-h` 配合 `-h` 显示可以在该协议下使用的选项。更多信息请参阅第 888 页的“帮助扩展”。

# 数据包匹配标准 CRITERIA

以下标准匹配网络数据包。当在标准前加感叹号（`!`）时，规则匹配不符合该标准的数据包。

### --protocol [face] proto

### -p

如果数据包使用 `proto` 协议，则匹配。此标准是一个匹配扩展。

### --source [address][mask]

或 `--src`

如果数据包来自 `address`，则匹配。地址可以是名称或 IP 地址。有关可选掩码的格式（仅适用于 IP 地址），请参见第 462 页。

### --destination [address][mask]

### -d --dst

如果数据包发往 `address`，则匹配。地址可以是名称或 IP 地址。有关可选掩码的格式（仅适用于 IP 地址），请参见第 462 页。

### --interface [face]+

用于接收到的接口名称。在 `face` 后面加上加号（`+`）以匹配任何以 `iface` 开头的接口。如果不指定接口，规则匹配来自任何接口的数据包。

### --out-interface [face]+

### -o

对于 `INPUT`、`FORWARD` 和 `PROUTING` 链，如果 `iface` 是数据包将要出的接口，则匹配。在 `face` 后面加上加号（`+`）以匹配任何以 `iface` 开头的接口。如果不指定输出接口，规则匹配发往任何接口的数据包。

### -fragment

匹配分片数据包的第二个后续碎片。由于这些数据包不包含源或目的信息，它们不匹配任何其他规则。

# 显示 CRITERIA

以下标准显示信息。所有数据包匹配这些标准。

### --verbose -v

显示额外的输出。

### --numeric -n

显示 IP 地址和端口号，而不是名称。

# 匹配扩展 EXTENSIONS

规则规范（数据包匹配标准）扩展（称为匹配扩展）根据协议和状态为之前描述的匹配添加匹配。每个协议扩展都保存在模块中，该模块必须在匹配之前加载。

## 使用 iptables 构建规则集

### --source-port [port][:port]

### --sport

匹配源端口号或服务名称（参见 `/etc/services`）。你也可以指定端口号范围。具体来说，`:sport` 指定从端口 0 到 `port` 的端口，而 `port:port` 指定从 `port` 到 65535 的端口。

### --syn

匹配设置了 `SYN` 位且清除了 `ACK` 和 `FIN` 位的数据包。此匹配扩展是 `--tcp-flags SYN,RST,ACK SYN` 的简写。

### --tcp-flags mask comp

定义哪些 TCP 标志位触发匹配。有效的标志有 `SYN`, `ACK`, `FIN`, `RST`, `URG`, `PSH`, `ALL` 和 `NONE`。`mask` 是一个用逗号分隔的列表，表示要检查的标志；`comp` 是列表的某个用逗号分隔的子集，指定为了发生匹配时必须设置的标志。标志必须为未设置状态。

### --tcp-option! n

匹配具有 `n` 个未指定的标志的 TCP 选项，对于十进制值 `n`，必须设置 `n` 个标志。

## UDP

当你指定 `--protocol udp` 时，你指定源和/或目的端口的方式与前一页“TCP”部分相同。

## ICMP

当你指定 `--protocol icmp` 时，加载此节中的扩展。`ICMP`（第 1153 页）数据包仅携带消息。

### --icmp-type! n name

当数据包是类型为 `name` 的 ICMP 包时匹配。`name` 可以数字 ICMP 类型，也可以是命令返回的名称之一：

```bash
$ iptables -p icmp -h
```

## 显式匹配扩展

显式匹配扩展与隐式匹配扩展的区别在于，在使用扩展之前，你必须使用 `-m` 或 `--match` 选项来指定模块。有许多显式匹配扩展模块可用；本节涵盖了其中最重要的一个。

## 状态

状态匹配根据数据包所处的状态（第 882 页）来匹配标准。

### --state name

匹配状态由 `state` 定义的数据包，`state` 是以下列表中用逗号分隔的状态列表：

- `ESTABLISHED` -- 在特定连接中，在 `fact` 连接双向交换包后的任何数据包。
- `INVALID` -- 无状态或不可识别的数据包。
- `NEW` -- 特定连接中的第一个数据包，通常是 `SYN` 数据包。
- `RELATED` -- 从 `ESTABLISHED` 连接派生的连接中交换的任何包。例如，`FTP` 数据连接可能与 `FTP` 连接相关。（跟踪 `FTP` 连接跟踪需要 `ip_conntrack_ftp` 模块。）

以下命令加载状态扩展并建立规则，匹配并丢弃无效数据包以及来自新连接的数据包：

```bash
$ iptables --match state --state INVALID,NEW --jump DROP
```

# 目标 Targets

所有目标都是内置的，没有用户定义的目标。本节列出了 `iptables` 可用的某些目标。目标选项列在每个目标之后。

### ACCEPT

继续处理数据包。

### DNAT

目的网络地址转换重写数据包的目的地址（第 881 页）。

`to-destination [ip:port]` 与 `to-source` 的 NAT 相同，不同是将数据包的目的地址改为指定的地址，且仅在 NAT 表的 `PREROUTING` 或 `OUTPUT` 链以及从这些链调用的任何自定义链中有效。以下命令在 NAT 表的 `PREROUTING` 链中添加一条规则，将目的为 `66.187.232.50` 的 TCP 数据包头部的目的地址更改为 `192.168.0.10`。

### DROP

在不通知的情况下结束数据包的生命。

### LOG

记录正在处理的数据包。内核使用 `syslog()`（第 625 页）处理由该目标生成的输出。`LOG` 是非终止目标，因此处理将继续到下一个规则。使用两条规则来记录 `REJECT` 或 `DROP` 的包，一个使用 `LOG` 目标，另一个使用 `REJECT` 或 `DROP`，具有相同的标准。

- `-log-level` 指定 `syslog.conf`（第 626 页）中的级别 `n`。
- `-log-prefix` 记录带有字符串条目，最多 14 个字符
- `-log-tcp-options` 记录 TCP 数据包头部的选项。
- `-log-ip-options` 记录 IP 数据包头部的选项。

### MASQUERADE

作用类似于 `to-source` 的 `SNAT`，不同是从指定的端口接口获取 IP 信息。适用于动态分配 IP 地址的系统，例如使用 DHCP 的系统，包括拨号链路。仅在 NAT 表的 `POSTROUTING` 链规则中有效。

## 与内核之间复制规则

### --to ports [port|--port]

指定你想要伪装的接口的端口。当接口掉线时忘记连接，这适用于拨号链路。使用此目标时必须指定 TCP 或 UDP 协议（`--protocol tcp` or `udp`）。

### REJECT

与 `DROP` 类似，不同之处它会通知发送系统数据包已被拦截。
