

## 第 25 章 firestarter, gufw 和 iptables：设置防火墙

...可以使用扩展。加载该模块的命令必须与使用该模块的命令出现在同一个规则规范中，并位于其左侧。匹配扩展有两种类型：隐式匹配和显式匹配。

### 隐式匹配扩展

当你使用 `--protocol` 命令（下文描述）时，帮助隐式扩展会（某种程度上）自动加载。每个协议都有其自己的扩展。在协议后跟上 `-h` 可以显示该协议下可可的扩展。例如，以下命令会在输出的末尾显示 TCP 扩展：

```
$ iptables -p tcp -h
...
tcp match options: match when TCP flags & mask == comp
--tcp-flags [!] match comp (Flags: SYN ACK FIN RST RST PSH ALL NONE)
[!] --syn 仅在 SYN 标志设置时匹配（等同于 --tcp-flags SYN, RST, ACK SYN）
--source-port [!][port]: 匹配源端口(s)
--sport --
--destination-port [!][port]: 匹配目的端口(s)
--dport --
--tcp-option [!] number 在 TCP 选项设置时进行匹配
```

本节未描述所有扩展。请像上一个示例一样使用 `-h` 来显示完整列表。

- --protocol [!] -p 加载 proto 模块，并在数据包使用 proto 协议时进行匹配。proto 可以是 `/etc/protocols` 中的名称或数字，包括 tcp、udp 和 icmp（第 1153 页）。指定所有或 0（零）将匹配所有协议，且与规则中不包含此项相同。

以下准则加载 TCP 模块并匹配来自端口 22（ssh 数据包）的 TCP 协议数据包：

```
--tcp tcp --source-port 22
```

以下命令扩展了上述匹配，导致内核丢弃所有入站的 ssh 数据包。该命令使用 `ssh`（iptables 在 `/etc/services` 中查找该名称）来代替 `22`：

```
$ sudo iptables --protocol tcp --source-port ssh --drop
```

#### TCP
本节中的扩展会在你指定 `--protocol tcp` 时加载。

- --destination-port [!] [port][port] 匹配目的端口号或服务名称（见 /etc/services）。你也可以指定端口范围。具体来说，`:port` 指定从 0 到 port 的端口，`port:` 指定从 port 到 65535 的端口。

- --source-port [!] [port][:port] 匹配源端口号或服务名称（见 /etc/services）。你也可以指定端口号范围。具体来说，`:port` 指定从 0 到 port 的端口，`port:` 指定从 port 到 65535 的端口。

- [!]--syn 匹配 SYN 位设置且 ACK 和 FIN 位置零的数据包。此匹配扩展是 `--tcp-flags SYN,RST,ACK` 的简写。

- --tcp-flags [!] mask mask 定义哪些 TCP 标志构成匹配。有效的标志有 SYN、ACK、FIN、 RST、URG、PSH、ALL 和 NONE。mask 是用逗号分隔的待检查标志列表；comp 是 mask 的一个用逗号分隔的标志子集，指定了发生匹配时必须设置的标志。未在 mask 中指定的标志必须为未设置状态。

- --tcp-option [!] n 匹配十进制值为 n 的 TCP 选项。

#### UDP

当你指定 `--protocol udp` 时，可以像前一页“TCP”部分描述的那样指定源和目的端口。

#### ICMP

当你指定 `--protocol icmp` 时，加载本节中的扩展。ICMP (1153) 包仅携带消息。

- --icmp-type [!] name 当数据包是类型为 name 的 ICMP 包时进行匹配。name 可以是数字 ICMP 类型，也可以是命令返回的名称之一：

```
$ iptables -p icmp -h
```

### 显式匹配扩展

显式匹配扩展与隐式匹配扩展的区别在于，在使用扩展之前，必须使用 `-m` 或 `--match` 选项来指定模块。有许多显式匹配扩展模块；本节涵盖了状态或最重要的扩展。

#### 状态

状态扩展根据数据包所处连接的状态匹配准则（第 882 页）。

- --state state 匹配状态由 state 定义的数据包，state 是以下状态的用逗号分隔的列表：
    - ESTABLISHED——在特定连接内，在该连接双向数据包交换后的任何数据包。
    - INVALID——无状态或不可识别的数据包。
    - NEW——特定连接内的第一个数据包，通常是 SYN 包。
    - RELATED——在从 ESTABLISHED 连接派生的连接中交换的任何数据包。例如，FTP 数据连接可能与 FTP 控制连接相关。（你需要 `ip_conntrack_ftp` 模块来跟踪 FTP 连接。）

以下命令加载状态扩展，并建立一条规则，用于匹配并丢弃无效数据包以及来自新连接的数据包：

```
$ iptables --match state --state INVALID,NEW --jump DROP
```

### 目标

所有目标都是内置的，没有自定义目标。本节列出了 iptables 可用的某些目标。每个目标后面列出了相应的选项选项。

- ACCEPT 继续处理数据包。

- DNAT 目的网络地址转换，重写数据包的目的地址（第 881 页）。

- --destination ip[:ip|:port]] 与带有 `to-source` 的 SNAT 相同，但它捕捉的是目的。仅在 NAT 表的 PREROUTING 链中有效。

```
$ sudo iptables --protocol tcp --source-port ssh --drop
```

- DROP 丢弃数据包。

- REJECT 拒绝数据包并向发送者发送错误消息。

- RETURN 停止遍历当前链并将数据包返回到调用链。

- SNAT 源网络地址转换，重写数据包的源地址。适用于具有互联网连接的局域网主机。

- --to-source ip[:ip][:port] 修改出站数据包的 IP 地址，以及该连接中后续所有数据包的 IP 地址 ip。返回的数据包会自动去 NAT，以便其返回到原始主机。仅在 NAT 表的 POSTROUTING 链中有效。

- MASQUERADE 与 SNAT 类似，区别在于它是动态分配 IP 地址。

