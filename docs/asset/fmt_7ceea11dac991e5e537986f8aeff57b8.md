
## 跳转或目标

指定内核对匹配规则所有匹配准则的数据包采取什么操作。使用 `-j target` 或 `--jump target` 指定跳转或目标。本节开头的示例使用以下命令指定 `ACCEPT` 目标：`--jump ACCEPT` 和 `-j ACCEPT`。

跳转将控制权转移到同一表内的不同链。以下命令向 `INPUT` 链添加一条规则（`--append`），该规则将使用 `TCP` 协议（`--protocol tcp`）的数据包转移到名为 `tcp_rules` 的用户定义链（`--jump tcp_rules`）：

```bash
# iptables --append INPUT --protocol tcp --jump tcp_rules
```

当数据包完成遍历 `tcp_rules` 链后（假设它没有被丢弃或拒绝），它将继续从它跳转出来的那条规则之后的 `INPUT` 链规则中遍历。

目标指定内核对数据包采取的操作；最简单的操作是 `ACCEPT`（接受）、`DROP`（丢弃）和 `REJECT`（拒绝）。以下命令向 `FORWARD` 链添加一条规则，该规则拒绝来自 `FTP` 端口（1）（`/etc/services`，`iptables` 用于确定使用哪个端口的文件显示 `FTP` 使用端口 21）的数据包：

```bash
# iptables --append FORWARD --sport ftp --jump REJECT
```

一些目标，如 `LOG`，是非目标性的：执行目标后，控制权传递给下一条规则。有关如何使用目标的信息，请参阅第 831 页。

## 构建一组规则

要指定表，常见的做法是将表声明放在紧跟在 `iptables` 之后的命令行上。例如，以下命令刷新（删除所有规则）`NAT` 表：

```bash
# iptables -t NAT -F
```

## 命令

以下是 `iptables` 命令列表：

- `--append -A` 将由规则规范指定的规则添加到链的末尾。当数据包匹配其中一个规则规范时，目标将处理它。

```bash
iptables -A chain rule-specifications --jump target
```

- `--delete -D` 根据规则号或规则规范从链中删除一个或多个规则。

```bash
iptables -D chain rule-numbers | rule-specifications
```

- `--insert -I` 将由规则规范和目标指定的规则添加到链中由规则号指定的位置。如果未指定规则号，默认为 1，即链的头部。

```bash
iptables -I chain rule-number rule-specifications --jump target
```

- `--replace -R` 用规则规范和目标替换链中规则号的规则。如果规则号或规则规范解析出多于一个地址，命令将失败。

```bash
iptables -R chain rule-number rule-specification --jump target
```

- `--list -L` 显示链中的规则。省略链以显示所有链的规则。使用 `--line-numbers` 显示规则号，或从第 828 页的列表中选择其他显示标准。

```bash
iptables -L [chain] display-criteria
```

- `--flush -F` 从链中删除所有规则。省略链以从所有链中删除所有规则。

```bash
iptables -F [chain]
```

- `--zero -Z` 将链中或未指定链时所有链中所有数据包和字节计数器的值更改为零。与 `-L` 一起使用以在清除之前显示计数器。

```bash
iptables -Z [-L] [chain]
```

- `--delete-chain -X` 删除名为 `chain` 的用户定义链。如果未指定 `chain`，则删除所有用户定义链。不能删除目标指向的链。

```bash
iptables -X chain
```

- `--policy -P` 为内置链 `builtin-chain` 设置默认目标或策略 `builtin-target`。此策略应用于不匹配链中任何规则的数据包。如果链没有策略，未匹配的数据包将被 `ACCEPT`（接受）。

```bash
iptables -P builtin-chain builtin-target
```

- `--rename-chain -E` 将链 `old` 的名称更改为 `new`。

```bash
iptables -E old new
```

- `help -h` 显示 `iptables` 命令语法的摘要。

```bash
iptables -b
```

使用 `-h` 跟随某个匹配扩展协议，以显示可用于该协议的选项。有关更多信息，请参阅第 829 页的“扩展帮助”。

## 数据包匹配条件

以下条件用于匹配网络数据包。如果在条件前加感叹号 `!`，则规则将匹配不符合该条件的数据包。

- `protocol [!] proto`

  `-p` 如果数据包使用 `proto` 协议，则匹配。此条件是一个匹配扩展（第 829 页）。

- `source [!] address/mask`

  `-s` 或 `--src` 如果数据包来自 `address`，则匹配。地址可以是名称或 IP 地址。有关可选掩码的格式（仅适用于 IP 地址），请参阅第 443 页。

- `destination [!] address/mask`

  `-d` 或 `--dst` 如果数据包去往 `address`，则匹配。地址可以是名称或 IP 地址。有关可选掩码的格式（仅适用于 IP 地址），请参阅第 443 页。

- `in-interface [!] iface[+]`

  `-i` 对于 `INPUT`、`FORWARD` 和 `PREROUTING` 链，如果 `iface` 是接收数据包的接口名称，则匹配。在 `iface` 后附加加号 `+` 以匹配任何以 `iface` 开头的接口名称。如果不指定 `in-interface`，规则将匹配来自任何接口的数据包。

- `out-interface [!] iface[+]`

  `-o` 对于 `FORWARD`、`OUTPUT` 和 `POSTROUTING` 链，如果 `iface` 是将要发送数据包的接口，则匹配。在 `iface` 后附加加号 `+` 以匹配任何以 `iface` 开头的接口名称。如果不指定 `out-interface`，规则将匹配去往任何接口的数据包。

- `[!] -fragment -f` 匹配分片数据包的第二及后续分片。由于这些数据包不包含源地址或目标地址信息，因此它们不会匹配任何其他规则。

## 显示条件

以下条件用于显示信息。所有数据包都匹配这些条件。

- `verbose -v` 显示额外的输出。

- `numeric -n` 以数字而非名称的形式显示 IP 地址和端口号。

- `exact -x` 与 `-L` 一起使用，以显示确切的数据包和字节计数，而不是取整值。

- `line-numbers` 在列出规则时显示行号。这些行号也是您可以在规则匹配条件中使用的规则编号（第 826 页）。

## 匹配扩展

规则指定（数据包匹配条件）扩展，称为*匹配扩展*，在之前描述的匹配基础上增加了基于协议和状态的匹配。每个协议扩展都保存在一个模块中，必须在使用该匹配扩展之前加载该模块。加载模块的命令必须出现在使用模块的命令相同的规则指定中，并位于其左侧。匹配扩展有两种类型：隐式和显式。

### 隐式匹配扩展

当您使用 `--protocol` 命令时，隐式扩展会自动（某种程度上）加载。每个协议都有自己独立的扩展。在协议后跟随 `-h` 以显示可用于该协议的扩展。例如，以下命令在帮助输出的*末尾*显示 `TCP` 扩展：

```
# iptables -p tcp -h
```

```
...
tcp match options:
[!] --tcp-flags mask comp match when TCP flags & mask == comp
(Flags: SYN ACK FIN RST URG PSH ALL NONE)
[!] --syn match when only SYN flag set
(equivalent to --tcp-flags SYN,RST,ACK,FIN
SYN)
[!] --source-port port[:port]
--sport ...
match source port(s)
[!] --destination-port port[:port]
--dport ...
match destination port(s)
[!] --tcp-option number match if TCP option set
```

本节并不描述所有扩展。使用前例中描述的 `-h` 以显示完整列表。

- `--protocol [!] proto`
