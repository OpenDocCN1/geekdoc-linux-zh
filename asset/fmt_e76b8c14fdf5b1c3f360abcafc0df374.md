
`-p` 加载 proto 模块，并在数据包使用 proto 协议时匹配。proto 可以是 `/etc/protocols` 中的名称或数字，包括 `tcp`、`udp` 和 `icmp`（第 1087 页）。指定 `all` 或 `0`（零）匹配所有协议中的任何一个，等同于不在规则中包含此匹配。

以下条件加载 TCP 模块，并匹配来自端口 22（ssh 数据包）的 TCP 协议数据包：

```
--protocol tcp --source-port 22
```

以下命令扩展了前一个匹配，使内核丢弃所有传入的 ssh 数据包。此命令使用 ssh（`iptables` 在 `/etc/services` 中查找它）代替 22：

```
# iptables --protocol tcp --source-port ssh --jump DROP
```

## TCP

指定 `--protocol tcp` 时，将加载本节中的扩展。

- `--destination-port [!] [port][:port]`  
  `--dport` 匹配目标端口号或服务名称（参见 `/etc/services`）。还可以指定端口号范围。具体来说，`port` 指定端口 0 到 `port`，`port:` 指定端口 `port` 到 65535。

- `--source-port [!] [port][:port]`  
  `--sport` 匹配源端口号或服务名称（参见 `/etc/services`）。还可以指定端口号范围。具体来说，`port` 指定端口 0 到 `port`，`port:` 指定端口 `port` 到 65535。

- `[!] --syn`  
  匹配 SYN 位已设置且 ACK 和 FIN 位已清除的数据包。此匹配扩展是 `--tcp-flags SYN,RST,ACK SYN` 的简写形式。

- `--tcp-flags [!] mask comp`  
  定义构成匹配的 TCP 标志设置。有效的标志包括 SYN、ACK、FIN、RST、URG、PSH、ALL 和 NONE。`mask` 是要检查的标志的逗号分隔列表；`comp` 是 `mask` 的逗号分隔子集，指定发生匹配时必须设置的标志。未在 `mask` 中指定的标志必须未设置。

- `--tcp-option [!] n`  
  匹配十进制值为 `n` 的 TCP 选项。

## UDP

当指定 `--protocol udp` 时，您可以按照之前“TCP”部分描述的方式指定源端口和/或目标端口。

# ICMP

只有当指定 `--protocol icmp` 时，才会加载本节中的扩展。*ICMP*（第 1087 页）数据包仅承载消息。

- `--icmp-type [!] name`  
  当数据包是类型为 `name` 的 ICMP 数据包时匹配。`name` 可以是数字 ICMP 类型或以下命令返回的名称之一：

```
# iptables -p icmp -h
```

## 显式匹配扩展

显式匹配扩展与隐式匹配扩展的不同之处在于，在使用扩展之前，必须使用 `--m` 或 `--match` 选项来指定模块。有许多可用的显式匹配扩展模块；本节介绍 `state`，这是最重要的模块之一。

### STATE

`state` 扩展基于数据包所属连接的状态（第 822 页）进行条件匹配。

- `--state state`  
  匹配状态由 `state` 定义的数据包，`state` 是以下状态列表中状态的逗号分隔列表：

- **ESTABLISHED** — 特定连接中，在该连接进行双向数据包交换之后的任何数据包。
- **INVALID** — 无状态或无法识别的数据包。
- **NEW** — 特定连接中的第一个数据包，通常是 SYN 数据包。
- **RELATED** — 在由 ESTABLISHED 连接生成的连接中交换的任何数据包。例如，FTP 数据连接可能与 FTP 控制连接相关。（您需要 `ip_conntrack_ftp` 模块来进行 FTP 连接跟踪。）

以下命令加载 `state` 扩展，并建立一条规则，匹配并丢弃无效数据包和来自新连接的数据包：

```
# iptables --match state --state INVALID,NEW --jump DROP
```

## 目标

所有目标都是内置的；没有用户自定义的目标。本节列出了 `iptables` 可用的部分目标。适用的目标选项列在每个目标之后。

- **ACCEPT** 继续处理数据包。

- **DNAT**（目标网络地址转换）重写数据包的目标地址（第 821 页）。
  - `--to-destination ip[-ip]:[port-port]` 类似于具有 `to-source` 的 SNAT，但它将数据包的目标地址更改为指定的地址和端口，并且仅在 NAT 表的 PREROUTING 或 OUTPUT 链中以及从这些链调用的任何用户定义链中有效。以下命令向 NAT 表的 PREROUTING 链添加一条规则，将目标为 66.187.232.50 的 TCP 数据包头中的目标更改为 192.168.0.10：

    ```
    # iptables -t NAT -A PREROUTING -p tcp -d 66.187.232.50 -j DNAT --to-destination 192.168.0.10
    ```

- **DROP** 无通知地结束数据包的生命周期。

- **LOG** 开启正在处理的数据包的日志记录。内核使用 `rsyslogd`（第 582 页）处理由此目标生成的输出。`LOG` 是一个非终止目标；处理继续到下一条规则。使用两条规则来记录您 REJECT（拒绝）的数据包，一条使用 LOG 目标，另一条使用 REJECT 目标，并具有相同的匹配条件。
  - `--log-level n` 指定日志级别 `n`，格式遵循 `rsyslog.conf`（第 583 页）。
  - `--log-prefix string` 使用 `string`（最长可为 14 个字符）作为日志条目的前缀。
  - `--log-tcp-options` 记录 TCP 数据包头中的选项。
  - `--log-ip-options` 记录 IP 数据包头中的选项。

**MASQUERADE** 类似于使用 `--to-source` 的 SNAT，区别在于 IP 信息是从指定端口的接口获取的。适用于 IP 地址动态分配的系统，例如使用 DHCP 的系统，包括大多数拨号线路。仅适用于 NAT 表 POSTROUTING 链中的规则。

- `-to-ports port[-port]` 指定用于伪装接口的端口。当接口断开时，会遗忘连接，这适用于拨号线路。使用此目标时必须指定 TCP 或 UDP 协议（`--protocol tcp` 或 `udp`）。

**REJECT** 类似于 DROP，区别在于它会通知发送系统数据包已被阻止。

- `-reject-with type` 向源系统返回错误类型。类型可以是以下任何一种，它们都会返回相应的 ICMP（参见第 1087 页）错误：`icmp-net-unreachable`、`icmp-host-unreachable`、`icmp-port-unreachable`、`icmp-proto-unreachable`、`icmp-net-prohibited` 或 `icmp-host-prohibited`。在需要 ICMP ping（参见第 379 页）数据包返回 ping 响应的规则中，可以指定类型为 `echo-reply`。在 INPUT 链中或从 INPUT 链调用的规则中，可以指定 `tcp-reset` 以返回 TCP RST 数据包。此参数在 INPUT、FORWARD 和 OUTPUT 链以及从这些链调用的用户定义链中有效。

**RETURN** 停止遍历当前链，并将数据包返回到调用链。

**SNAT** 源网络地址转换——重写数据包的源地址。适用于共享互联网连接的局域网中的主机。

- `-to-source ip[-ip][:port[-port]]` 将出站数据包的源 IP 地址以及该连接中所有后续数据包的源 IP 地址更改为 `ip`。跳过其他任何规则。返回的数据包会自动进行非 SNAT 处理，还原到源主机。仅适用于 NAT 表 POSTROUTING 链。

当指定 IP 地址范围（`-ip`）或使用多个 `-to-source` 目标时，`iptables` 以轮询方式分配地址，循环使用这些地址，每个新连接使用一个地址。

当规则指定了 TCP 或 UDP 协议（`-p tcp` 或 `-p udp`）时，可以指定端口范围。如果不指定端口范围，规则将匹配所有端口。NAT 子网上的每个连接必须具有唯一的 IP 地址和端口组合。如果 NAT 子网上的两台计算机试图使用相同的端口，内核会将其中一个端口映射到另一个（未使用的）端口。小于 512 的端口映射到其他小于 512 的端口，512 到 1024 之间的端口映射到其他 512 到 1024 之间的端口，大于 1024 的端口映射到其他大于 1024 的端口。
