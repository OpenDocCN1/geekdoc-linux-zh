
# 使用 `iptables` 命令

`iptables` 存在三种表类型：`mangle`、`nat` 和 `filter`。除非你在 `iptables` 的使用方面非常高级，否则你 99% 的时间都会花在 `filter` 表上。所有不包含 `-t` 选项后跟 `mangle` 或 `nat` 的命令默认影响 `filter`。

`iptables` 中存在的表包括：

- **Mangle**——此表用于设置服务类型、生存时间（time to live）和标记目标。本质上，它用于特殊路由和 `iptables` 目的修改数据包。
- **Nat**——`nat` 表仅用于网络地址转换（NAT）流量。当你拥有一组内部主机和一个外部网络，并希望将地址进行匹配和转换，从而有效地将你的内部网络从外部世界屏蔽时，就会使用 NAT。
- **Filter**——默认表，包含预构建的链 `input`、`output` 和 `forward`。

要查看机器上的 `filter` 表，请使用以下命令：

```
iptables -L
```

这将返回以下输出：

```
Chain INPUT (policy ACCEPT)
target      prot opt source                destination
Chain FORWARD (policy ACCEPT)
target      prot opt source                destination
Chain OUTPUT (policy ACCEPT)
target      prot opt source                destination
```

要查看 `nat` 或 `mangle` 表，你只需包含 `-t` 选项，后跟所需的表类型：

```
iptables -t mangle -L
```

# 配置 `iptables` 链

你不太可能在考试中看到任何链，但走到这一步而没有实际为机器配置防火墙将是令人遗憾的。

完成某些任务的简单规则示例包括：

```
iptables -A INPUT -s 223.107.1.101 -j DROP
```

此规则仅丢弃来自特定主机 IP 的所有流量，例如那些不断试图闯入你的公共服务器之一的主机。

另一个示例是必须阻止整个网络访问你的公共服务器，使用以下命令：

```
iptables -A INPUT -s 223.107.1.0/24 -j DROP
```

此规则阻止提到的 C 类网络上的每个主机。斜杠表示法（`/24`）意味着正在阻止 254 个主机地址。

另一个方便的规则是拒绝地址块使用特定服务，例如 Telnet：

```
iptables -A INPUT -s 223.107.1.0/24 -p tcp -destination-port telnet -j DROP
```

> 你也可以使用端口号 23 来阻止这些地址。之前使用名称 Telnet 取决于该服务是否在 `/etc/services` 文件中定义。

假设你想保护你的防火墙系统，防止任何未由你发起的连接到主机。当你使用私有地址并且不希望人们追踪你的地址回到防火墙并尝试入侵时，这很有用。你可以使用以下内容：

```
iptables -A INPUT -i eth0 -p tcp -syn -j DROP
```

这导致任何发起连接的计算机最终会超时等待 TCP 同步包，因为你在接口处丢弃了它。如果你发起连接（并且它没有对你做同样的事！），你的系统可以正常连接到远程主机。

前一条规则的问题在于它会丢弃所有数据，但你可能希望保留 SSH 端口，并且可能还希望有一台 Web 服务器在那台机器上监听。

在这种情况下，你可以使用对之前使用的 `DROP` 规则的例外来实现，尽管实现两个开放端口需要两行规则。在我们的示例中，链中规则的顺序并不重要。

若要屏蔽系统中除 80 端口（www）之外的所有端口，你可以使用如下所示的命令：

```
iptables -A INPUT -i eth0 -p tcp --syn --destination-port ! 80 -j DROP
```

若要向链中添加另一个端口，例如 22 端口（ssh），你可以使用以下命令：

```
iptables -A INPUT -i eth0 -p tcp --syn --destination-port ! 22 -j DROP
```

如果你显示过滤表的内容，你会发现这两条规则都在那里，并且将在本会话中生效：

```
iptables -L
```

这将返回以下输出：

```
Chain INPUT (policy ACCEPT)
   target     prot opt source        destination
DROP     tcp  --  anywhere anywhere tcp dpt:www flags:SYN,RST,ACK/SYN
DROP     tcp  --  anywhere anywhere tcp dpt:ssh flags:SYN,RST,ACK/SYN

Chain FORWARD (policy ACCEPT)
   target     prot opt source        destination
Chain OUTPUT (policy ACCEPT)
   target     prot opt source        destination
```

既然你已经看到了如何使用 `iptables` 命令保护系统的一些良好示例，请务必使用 `iptables-save` 命令保存你定义的规则。

当运行时，`iptables-save` 命令（存在于 Red Hat 和 Debian 中）会将你的 `iptables` 表的内容保存到 `/etc/sysconfig/iptables` 文件。系统重启时，`iptables-restore` 命令会自动恢复表规则。

在 Debian 机器上，可以通过保存规则来自动化 `iptables-save` 功能，使用以下命令：

```
iptables-save > firewall.txt
```

然后，你可以在启动脚本中使用此命令来恢复配置：

```
iptables-restore < firewall.txt
```

> 请注意防火墙相关的基于逻辑的问题，例如你会把拒绝内部用户访问外部资源的规则放在哪里（在内部接口的输入链上）。

也要注意那些询问 Linux 可用的不同类型防火墙选项的问题，例如 `ipfwadm`、`ipchains` 和 `iptables`。

# 备考问题

1. 当 `host1` 上的用户首次使用 SSH 客户端成功连接到 `host2` 时，哪个文件会被更新以包含与 SSH 相关的信息？

   - A. `host1` 上的 `~/.ssh/known_hosts`
   - B. `host2` 上的 `/etc/ssh/known_hosts`
   - C. `host2` 上的 `~/.ssh/authorized_keys`
   - D. `host1` 上的 `/etc/ssh/authorized_keys`

答案 A 是正确的，因为当用户首次通过 SSH 连接到主机时，RSA 主机密钥会被复制到该用户的本地 `~/.ssh/known_hosts` 文件中。答案 B 是错误的，因为 `known_hosts` 文件仅存在于用户配置中。答案 C 是错误的，因为 `host2` 上的 `authorized_keys` 文件与此连接无关。答案 D 是错误的，因为 `authorized_keys` 文件仅用于用户配置。

2. 你被要求拒绝 `snuffy2` 主机访问你服务器上的 Telnet 服务，并使用 TCP wrappers 文件和工具来实现这一点。在下面的空白处，写下应包含此条目的文件的完整路径和文件名：

正确答案是 `/etc/hosts.deny`。没有其他正确的答案。

3. 你是受管系统上的 `root` 用户。你需要将 `/root/file6` 从 `host1` 发送到 `host3` 的相同位置，但你目前在 `host2` 上。以下哪些命令可以完成此任务？（选择所有适用的选项。）

   - A. `scp root@host1:~/file6 root@host3`
   - B. `scp root@host1:/root/file6 root@host3`
   - C. `scp root@host1:/root/file6 root@host3:-`
   - D. `scp root@host1:file6 root@host3`

答案 A、B 和 D 是正确的，因为它们都能正确地将文件从 `host1` 复制到 `host3`。答案 C 是错误的，因为在 `host3` 目标末尾添加 `:-` 会导致尝试向一个无法解析的目录写入文件的错误。

4. 你刚从一个供应商的网站下载了一个安全补丁，并想验证包的完整性。在下面的空白处填入在 Red Hat 或基于 RPM 的系统上完成此操作所需的命令和必要选项（无文件名）：
