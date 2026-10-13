
![](img/3a7e027360b64bc83d5cf9a2db902251_308_0.png)

> `system-config-iptables` 会在启动前存储配置，这非常有用。你可以在 `/etc/sys-config/iptables-config.old` 和 `/etc/sysconfig/iptables-config.old` 文件找到这些配置。如果你犯了错误并想恢复到之前的配置，知道这一点很有帮助。

如果你也为 IPv6 配置了防火墙规则，它们有自己的配置文件：`/etc/sysconfig/ip6tables` 和 `/etc/sysconfig/ip6tables-config`。

# 使用 iptables 设置防火墙

`system-config-firewall` 工具包含一个用于设置基础防火墙的良好实用程序。然而，如果你需要配置一个提供高级功能的防火墙，它真的并不够用。在这种情况下，你最好使用 `iptables` 命令。`iptables` 倾向于生成非常长的命令。

# 表、链和规则

表是 Netfilter 的构建模块。NAT 表经常被使用。链由规则组成。`INPUT`、`OUTPUT` 和 `FORWARD` 链用于数据包。

# 构建 Netfilter 防火墙

在练习中，你将在虚拟机上构建防火墙。你还将确保没有任何规则在使用。此练习的目的是教你如何从命令行配置防火墙。

# 练习 10.3

## 构建 Netfilter 防火墙

在练习中，你将在虚拟机上构建防火墙。你还将确保没有任何规则在使用。此练习的目的是教你如何从命令行配置防火墙。

- 1. 在主机计算机上，输入 `iptables -L` 显示当前配置。此操作的目的是清除当前配置。在在此之前，了解你的防火墙设置是良好的。
- 2. 输入以下命令：`iptables -P INPUT ACCEPT`、`iptables -P OUTPUT ACCEPT` 以及 `iptables -P FORWARD ACCEPT`。现在使用 `iptables -F` 刷新所有规则。
- 3. 此时，主机计算机上不应该防火墙。使用 `iptables -L` 验证所有链策略设置为 `ACCEPT`（参见列表 10.4）。如果是这样，使用 `iptables save` 将当前配置写入配置文件。这确保即使在重启后也能保留此配置。
- 4. 在虚拟机上重复步骤 1 到 3。
- 5. 在清除虚拟机的防火墙后，你必须测试虚拟机是否提供了服务。使用 ping 测试你是否可以到达虚拟机（例如，`ping 192.168.100.176`）。
- 6. 接下来在主机上使用 `yum install nmap` 安装 nmap 网络扫描器。
- 7. 安装完成后，使用 `nmap` 加上虚拟机的 IP 地址扫描虚拟机上的可用服务（例如，`nmap 192.168.100.176`）。你应该看到一些服务被提供。

列表 10.4：继续之前验证未使用防火墙配置

```
```
