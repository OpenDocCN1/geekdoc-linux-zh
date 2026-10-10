
如果你在一个接口上有多个 IP 地址，可以使用 `--to-source` 选项指定使用哪一个。例如：

```
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 192.168.1.10
```

如果你想掩装来自特定子网的流量，可以使用 `-s` 选项。例如：

```
# iptables -t nat -A POSTROUTING -o eth0 -s 192.168.1.0/24 -j MASQUERADE
```

如果你想掩装去往特定目的地的流量，可以使用 `-d` 选项。例如：

```
# iptables -t nat -A POSTROUTING -o eth0 -d 10.0.0.1 -j MASQUERADE
```

如果你想在特定端口转发流量，可以使用 `--dport` 选项。例如：

```
# iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -j DNAT --to-destination 192.168.1.10
```

如果你想从特定端口转发流量，可以使用 `--sport` 选项。例如：

```
# iptables -t nat -A PREROUTING -i eth0 -p tcp --sport 8080 -j DNAT --to-destination 192.168.1.10
```

如果你想为特定协议转发流量，可以使用 `-p` 选项。例如：

```
# iptables -t nat -A PREROUTING -i eth0 -p udp -j DNAT --to-destination 192.168.1.10
```

如果你想从特定接口转发流量，可以使用 `-i` 选项。例如：

```
# iptables -t nat -A PREROUTING -i eth1 -j DNAT --to-destination 192.168.1.10
```

如果你想向特定接口转发流量，可以使用 `-o` 选项。例如：

```
# iptables -t nat -A PREROUTING -o eth1 -j DNAT --to-destination 192.168.1.10
```

如果你想根据多个标准转发流量，可以组合这些选项。例如：

```
# iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 80 -s 192.168.1.50 -j DNAT --to-destination 192.168.1.10
```

# 第14章：计算机安全问题 595

## 通过 iptables 防火墙允许 FTP 和 IRC 服务

在被动 FTP 中，FTP 客户端向服务器发送其 IP 地址和它将监听数据的端口号。如果该客户端位于你防火墙后的计算机上（你正对其进行 NAT），则信息也必须翻译，否则 FTP 服务器将无法与客户端通信。

`iptables` 使用连接跟踪模块来跟踪连接。使用此功能，它可以查看每个 FTP 数据包的数据区域（即不在 IP 包头中），以获取执行 NAT 所需的信息（记住来自互联网的计算机无法直接与你的私有 IP 地址通信）。为了进行 FTP 跟踪（允许被动 FTP 连接到 LAN），你需要加载以下模块：

- `nf_ip_conntrack`
- `nf_ip_conntrack_ftp`
- `nf_ip_nat_ftp`

对于聊天和 DCC 发也是如此，它们用于建立和监控到 IRC 聊天会话的直接连接。地址和端口号存储在 IRC 协议包中，因此这些数据包也必须翻译。为了允许 LAN 客户端使用 IRC 服务，你需要加载以下模块：

- `nf_ip_conntrack_irc`
- `nf_ip_nat_irc`

IRC 连接的默认端口是 6667。如果你不想使用默认端口，可以在加载连接跟踪模块时添加不同的端口：

```
modprobe nf_ip_conntrack_irc ports=6669
```

## 了解 iptables

现在你已经了解了 `iptables` 规则的样式以及你如何获取它们，让我们回溯一下，看看 `iptables` 是如何工作的。

`iptables` 功能的工作原理是让进入或离开防火墙的 IP 包（即网络数据）遍历一组链，这些链定义了对数据包进行的操作。你添加的每条规则都同时执行以下两项操作：

- 检查是否符合特定标准（例如数据包是否请求特定服务或来自特定地址）
- 采取动作（例如丢弃、接受或进一步处理数据包）

针对不同类型的表实现了不同的规则集。例如，存在用于过滤（`filter`）、网络地址转换（`nat`）和修改数据包头（`mangle`）的表。根据数据包的源和目的，它会遍历不同的链。你涉及的规则将与 `filter` 表（如果没有提供其他表，则隐含为 `filter`）。

与 `filter` 表关联的链有 `INPUT`、`OUTPUT` 和 `FORWARD`。你也可以添加用户自定义链。你可能最感兴趣的是使用上一个示例所示的基本规则添加或移除特定的 TCP 和 UDP 服务。对你想要通过的数据包分配 `ACCEPT`，对你想要丢弃的数据包分配 `DROP`。你还可以分配 `REJECT` 来丢弃数据包但向发送者返回消息，或分配 `LOG` 既不丢弃也不接受消息，而是记录有关数据包的信息。

`iptables` 内置了许多优秀功能。接下来的描述将告诉你你可以使用 `iptables` 进行的一些酷炫操作，并提供一些使用技巧。

## 通过 iptables 防火墙允许 FTP 和 IRC 服务

在被动 FTP 中，FTP 客户端向服务器发送其 IP 地址和它将监听数据的端口号。如果该客户端位于你防火墙后的计算机上（你正对其进行 NAT），则信息也必须翻译，否则 FTP 服务器将无法与客户端通信。

`iptables` 使用连接跟踪模块来跟踪连接。使用此功能，它可以查看每个 FTP 数据包的数据区域（即不在 IP 包头中），以获取执行 NAT 所需的信息（记住来自互联网的计算机无法直接与你的私有 IP 地址通信）。为了进行 FTP 跟踪（允许被动 FTP 连接到 LAN），你需要加载以下模块：

- `nf_ip_conntrack`
- `nf_ip_conntrack_ftp`
- `nf_ip_nat_ftp`

对于聊天和 DCC 发也是如此，它们用于建立和监控到 IRC 聊天会话的直接连接。地址和端口号存储在 IRC 协议包中，因此这些数据包也必须翻译。为了允许 LAN 客户端使用 IRC 服务，你需要加载以下模块：

- `nf_ip_conntrack_irc`
- `nf_ip_nat_irc`

IRC 连接的默认端口是 6667。如果你不想使用默认端口，可以在加载连接跟踪模块时添加不同的端口：

```
modprobe nf_ip_conntrack_irc ports=6669
```

## 使用 iptables 使用记录功能

使用 `LOG` 目标可以记录符合标准的数据包的信息。特别是你可能想将其用于你认为不当的操作。换句话说，如果你出于某些原因不想丢弃数据包，可以只记录其活动稍作决定。`LOG` 目标将信息重定向到 Fedora 中标准的日志工具：`dmesg` 和 `syslog`。这里有一个使用 `LOG` 目标的规则示例：

```
-A FORWARD -p tcp -j LOG --log-level info
```

除了 `info`，你可以使用以下 `syslog` 可用的任何日志级别：`emerg`、`alert`、`crit`、`err`、`warning`、`notice`、`info` 或 `debug`。通过如下所示使用 `--log-prefix` 选项，你还可以在此操作产生的所有消息前面添加信息：

```
-A FORWARD -p tcp -j LOG --log-prefix "Forward "
```

- 限制（Limiting）——使用 `--limit` 选项允许匹配项每秒产生有限次数的消息（默认为每小时三次，允许突发性的五次）。

- 拒绝服务 (DOS) 攻击——你可以使用 `--limit` 选项来减少 DOS 攻击的影响，但仍然无法阻止所有攻击。只要流量指向你的服务器，你的网络带宽就会被消耗，机器仍然需要资源来忽略这些数据。

- 表类型（Table types）——默认表类型为 `filter`。其他类型有 `nat` 和 `mangle`（用于修改数据包）。要使用 `filter` 以外的表，你必须添加 `-t table_type` 选项，其中 `table_type` 为 `nat` 或 `mangle`。

## 使用 TCP Wrappers 控制服务的访问
