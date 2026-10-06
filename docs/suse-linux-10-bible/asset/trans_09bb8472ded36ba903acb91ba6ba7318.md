

## 第 24 章 ✦ 在 SUSE Linux 中实现防火墙

互联网控制消息报协议（ICMP）是互联网运行不可或缺的一部分。ICMP 用于向相关方发送有关网络状态的状态和错误消息。例如，当你 ping 一台机器时，ping 包及其回显是通过 ICMP 发送的。如果你因为网络连接故障而无法访问某台机器，ICMP 会告知你，此时你的应用程序会提示“目标不可达（Destination Unreachable）”。

一种黑客破坏你网络的传统尝试是发布 ICMP 重定向消息。这告诉服务器该路由不可用，通往该目的流量应该通过另一个目的地路由。

至少，你应该允许目标不可达（destination unreachable）、源抑制（source quench，当你需要发送较小的数据包时）以及生存时间（TTL）错误，后者是指数据包在到达目的地之前经过了过多的路由器。是否允许 ping 请求取决于你自己的决定。通常情况下，你不会启用这些功能，因为这为恶意用户在攻击初始调查期间提供了另一个工具。

为了允许这些类型的 ICMP 流量，你需要允许入站 ICMP 和某些出站 ICMP 包：

```bash
iptables: # iptables -I INPUT -p icmp --type-destination-unreachable -j ACCEPT
iptables: # iptables -I INPUT -p icmp --type-source-quench -j ACCEPT
iptables: # iptables -I INPUT -p icmp --type-time-exceeded -j ACCEPT
```

对于你允许的每种 ICMP 协议类型，你都在接受入站（即针对防火墙！）报告目标不可达、源抑制和 TTL 超出的 ICMP 流量。

## 允许环回（Loopback）

建议在你的防火墙上允许环回流量，因为许多你通常认为可以内部相互通信的服务，如果不这样做，它们将会失败。要做到这一点，请指定环回设备不应限制：

```bash
iptables: # iptables -A INPUT -i lo -j ACCEPT
iptables: # iptables -A OUTPUT -o lo -j ACCEPT
```

在此示例中，通过向 INPUT 链添加规则，你接受了任何发往（-i）或离开（-o）环回（lo）设备的类型流量。

由于环回设备不具备转发数据包的能力，因此你不需要启用通过 FORWARD 链的流量。

## 记录丢弃的数据包

当你的防火墙按照喜好配置完成后，你可能希望记录任何未经你显式许可的流量。要做到这一点，需要在数据包进入链的默认策略之前，设置一个目标为 `LOG` 的最终规则。

`LOG` 目标解析 TCP/IP 数据包并通过 syslog 设施将其记录，以便你监控未经授权的流量。

仅仅记录原始的未经授权的流量非常难以管理，幸运的是 `LOG` 目标允许你指定日志前缀，以便根据其源链来区分条目：

```bash
bash: # iptables -A INPUT -j LOG --log-prefix=INPUT:
bash: # iptables -A OUTPUT -j LOG --log-prefix=OUTPUT:
bash: # iptables -A FORWARD -j LOG --log-prefix=FORWARD:
```

在此示例中，对于数据包经过的每条链，你都添加了一条规则，将所有数据包发送到 LOG 目标（- LOG）。`-log-prefix` 参数将确保每个记录的数据包都带有 INPUT、OUTPUT 或 FORWARD 前缀（取决于与其所属链相关的流量）。

任何触发规则的流量都将在触及默认策略之前使用 `LOG` 目标进行记录。对于每条链，你都在记录数据包详情，并带有一个与其源链相关的前缀。

> LOG 规则的位置至关重要。如果将 LOG 目标插入到链的开头，所有流量（无论是否允许）都会被记录。如果你犯了这种错误，你会发现日志很快就会填满。

## 使用 SuSEfirewall2

SUSE 包含了它自己的基于 `sysconfig` 的防火墙脚本，称为 SuSEfirewall2。SuSEfirewall 脚本自多年前构思以来已经取得了了长的进步，并提供了一套可以通过 YaST 配置的健壮工具。

对于需要快速设置防火墙的新用户来说，这是完美的选择。在过去的多年里，我们曾建议你编写自己的防火墙脚本，但如果你觉得没有必要显式控制你的规则，SuSEfirewall2 可以为大多数环境生成一个健壮且安全的防火墙。

## 第 24 章 + 在 SUSE Linux 中实现防火墙

要使用 YaST 管理系统为家里配置一个小型防火墙，请遵循以下步骤：

- 1. 在 YaST 中，选择“安全和用户 -> 防火墙”（见图 24-3）。当模块加载时，你可以继续进行防火墙配置。
- 2. 一旦防火墙配置加载，系统将询问你希望如何让 SuSEFirewall 在系统上启动（图 24-4）。如果此系统需要被完全保护，你需要确保选中了“启动时（When Booting）”。使用初始配置屏幕，你还可以手动停止或启动防火墙（你也可以在命令行中使用 `rcSUSEfirewall2=start/stop`）。
- 3. 要选择参与防火墙配置的网络接口，请点击“接口（Interfaces）”。确保这一点非常重要，否则你的配置将反反且无法按预期工作。在本文章之前的示例网络配置中，你将 eth0 作为内部网络接口，eth1 作为外部公共接口（见图 24-5）。
- 5. 对于许多防火墙，你可能希望对所有出站连接进行伪装。要做到这一点，请点击“伪装（Masquerading）”。如果你希望对内部网络到外部网络接口的所有出站连接进行伪装，请选择“网络（Networks）”。一旦你对伪装规则满意，点击“添加（Add）”。
- 6. 记录任何命中防火墙的恶意数据包始终是一个好主意，你可以选择记录的详细程度。在图 24-8 中，你可以看到我们选择了记录所有拒绝的数据包，并且仅记录关键数据包。
- 7. 当你对配置满意时，点击“下一步（Next）”保存并继续提交防火墙。你将看到防火墙配置的概述。如果你对配置满意，点击“接受（Accept）”。

