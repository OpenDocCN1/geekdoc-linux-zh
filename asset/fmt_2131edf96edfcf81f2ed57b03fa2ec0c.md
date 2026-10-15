
Chain INPUT (policy ACCEPT)     destination
  target opt source

Chain FORWARD (policy ACCEPT)    destination
  target opt source

Chain OUTPUT (policy ACCEPT)    destination
  target opt source

在这种情况下，所有三条链——`INPUT`、`FORWARD` 和 `OUTPUT` 都显示相同的 `ACCEPT` 策略，这意味着一切都是开放的。

如果你正在设置数据包过滤器，要做的事情是指定你想要接受的数据包。例如，要接受来自 `192.168.0.0` 网络地址的数据包，向 `INPUT` 链添加规则：

```
iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT
```

现在使用以下命令添加规则以丢弃除本地回环（`lo` 网络接口）以外的所有流量，并停止所有转发：

```
iptables -A INPUT !i lo -j REJECT
iptables -A FORWARD -j REJECT
```

例如，第一个 `iptables` 命令向 `INPUT` 链 (`-A INPUT`) 追加了如下规则：如果数据包不是来自 `lo` 接口 (`-i lo`)，则拒绝该数据包 (`-j REJECT`)。

在拒绝所有其他数据包之前，你可能会向每个 `INPUT` 链添加更多规则以允许特定数据包进入。你可以根据许多不同的参数选择要接受的数据包，例如 IP 地址、协议类型（`TCP`、`UDP`）、网络接口和端口号。

## 设置简单的防火墙 427

你可以使用 `iptables` 进行所有专门的数据包过滤。例如，假设你设置了一个 Web 服务器，并且你想接受针对 HTTP（端口 80）和安全外壳（SSH）服务的数据包。安全外壳（端口 22）是你安全登录和管理服务器的地方。假设服务器的 IP 地址为 `192.168.0.10`。以下是你可能为服务器设置规则的方法：

```
iptables -P DROP
iptables -A INPUT -s 0 -d 192.168.0.10 -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -s 0 -d 192.168.0.10 -p tcp --dport 22 -j ACCEPT
```
