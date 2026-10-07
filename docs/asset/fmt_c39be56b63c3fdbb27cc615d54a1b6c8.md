
通过 `IGNORE_PROTOCOLS` 变量，可以指示 psad 忽略整个协议。通常情况下，更好的做法是调整你的 `iptables` 策略，从一开始就不记录你想要忽略的协议，但如果你想让 psad 忽略所有 `ICMP` 数据包，例如，可以像这样设置 `IGNORE_PROTOCOLS`：

```
IGNORE_PROTOCOLS      icmp;
```

## IGNORE_LOG_PREFIXES

你会发现 `iptables` 策略可能非常复杂，并包含许多不同的日志规则——每条规则都可能有其特定的日志前缀。如果你想让 psad 忽略某个日志前缀，例如 `DROP:INPUT:eth1`，你可以这样设置 `IGNORE_LOG_PREFIXES`：

```
IGNORE_LOG_PREFIXES      DROP:INPUT:eth1;
```

## EMAIL_LIMIT

在某些情况下，`iptables` 策略被配置为记录非恶意流量，而这些流量在网络中可能会反复出现，例如，向特定 `DNS` 服务器的 `DNS` 请求。如果 psad 将此类流量解释为扫描，psad 可能会因为流量重复出现而针对该流量发送大量邮件警报。你可以使用 `EMAIL_LIMIT` 变量强制 psad 对扫描 `IP` 地址发送的邮件警报数量进行限制。默认值为零，意味着不进行任何限制，但如果你将其设置为 `50`，那么 psad 对给定的 `IP` 地址发送的邮件警报将不超过 `50` 封：

```
EMAIL_LIMIT              50;
```

## ALERTING_METHODS

大多数管理员使用 psad 提供的电子邮件和系统日志 `syslog` 报告模式，`ALERTING_METHODS` 变量允许你控制 psad 是否生成邮件或系统日志警报。`ALERTING_METHODS` 变量接受三个值：`noemail`、`syslog` 和 `ALL`。`noemail` 和 `syslog` 值指示 psad 不发送邮件或系统日志警报；这些值可以组合以禁用所有警报。默认是同时生成邮件和系统日志警报：

```
ALERTING_METHODS         ALL;
```

## FW_MSG_SEARCH

`FW_MSG_SEARCH` 变量定义了 psad 搜索 `iptables` 日志消息的方式。要限制 psad 仅分析包含特定日志前缀在 `iptables` 规则中通过 `--log-prefix` 参数定义的日志消息，请用 `FW_MSG_SEARCH` 变量定义该前缀。这允许配置为数据包分配其他日志前缀，而不让 psad 分析它们。

例如，要让 psad 仅分析包含 `DROP` 字符串的 `iptables` 日志消息，可以这样配置 `FW_MSG_SEARCH` 变量：

```
FW_MSG_SEARCH               DROP;
```

## `/etc/psad/auto_dl`

与任何入侵检测系统 `IDS` 一样，误报的可能性总是存在的。因此，每个 `IDS` 都应该具备白名单功能，通过该功能可以将某些系统、网络、端口或协议从任何检测机制以及最重要的任何自动响应功能中排除。由于某些 `IP` 地址或网络可能是已知的恶意源，还应该有将其加入黑的机制。

这些需求在 psad 的 `auto_dl` 文件中实现，它遵循以下语法：

| ip/network | 危险等级 | 可选协议/可选端口 |
| :--- | :--- | :--- |

如果将危险等级设置为零，psad 将完全忽略该 `IP` 地址或网络。然而，危险等级可以非常高，如果某个特定的 `IP` 地址或网络已知是极其恶意的。以下两行的第一行确保 psad 将忽略来自 `IP` 地址 `192.168.10.3` 的所有流量；第二行立即将来自 `10.10.0/24` 网络的所有 `TCP` 端口 `22` `SSH` 流量的危险等级提升至五：

```
192.168.10.3    0;
10.10.0/24      5 tcp/22;
```

## `/etc/psad/signatures`

正如任何 `IDS` 一样，误报的可能性总是很高的。因此，每个 `IDS` 都应该配备白名单功能，通过该功能可以将某些系统、网络、端口或协议排除在任何检测机制以及最重要的任何自动响应功能之外。由于某些 `IP` 地址或网络可能是已知的恶意行为，还应该有将其加入黑的规定。

这些需求在 psad 的 `auto_dl` 文件中满足，该文件遵循以下语法：

| ip/network | 危险等级 | 可选协议/可选端口 |
| :--- | :--- | :--- |

如果危险等级设置为零，psad 将完全忽略该 `IP` 地址或网络。然而，危险等级可以非常高，如果某个特定的 `IP` 地址或网络已知是极其恶意的。以下两行的第一行确保 psad 将忽略来自 `IP` 地址 `192.168.10.3` 的所有流量；第二行立即将来自 `10.10.0/24` 网络的所有 `TCP` 端口 `22` `SSH` 流量的危险等级提升至五：

```
192.168.10.3    0;
10.10.0/24      5 tcp/22;
```

`/etc/psad/signatures` 文件包含了 psad 能够检测的约 `200` 条 `Snort` 规则。这些规则是对 `iptables` 日志的修改。以下是 `UDP` 的 `Snort` 规则示例：

```
alert udp $EXTERNAL_NET -> $HOME_NET (msg:"attack"; class:bad-activity; reference:http://example.com/attack; sid:1029; rev:1;)
```

## 使用 psad 检测端口扫描

尽管许多攻击已移动到应用层，但仍有大量的可疑活动会在传输层及以下层表现出来。

`TCP/IP` 协议族的任何完整实现都是一组庞大且复杂的代码，这种复杂性使其成为从侦察活动到拒绝服务 `DoS` 攻击等极具吸引力的目标。本节将说明针对 `iptables` Linux 系统的几种攻击和探测，并引用图 `1-2` 中的网络图重复为图 `6-1`。在此期间，psad 也部署在 `iptables` 系统上，并带有第 `1` 章描述的由 `iptables.sh` 脚本构建的默认策略，该脚本位于 `http://cipherherdyne.org/LinuxFirewalls/`。本节中讨论的所有攻击都是针对在内核中带有 `iptables` 策略的 `iptablesfw` 系统发送的。psad 检测可疑活动只需要策略的默认日志扫描；不需要任何额外功能如字符串匹配。

![](img/84e6ec42d170b9df6cf29b40151f3d15_121_0.png)

图 `6-1`：默认网络图

端口扫描是查询远程目标的一种重要技术，psad 开发的主要目标是为 Linux 系统提供高级的端口扫描检测。首要任务是说明各种类型的端口扫描以及它们在你的 `iptables` 日志中是如何显示的。

与第 `3` 章一样，我们使用 `Nmap` 对系统进行扫描。然而，扫描目标运行着 psad，以便分析 `iptables` 日志。我们将使用 `Nmap` 生成以下类型的端口扫描，然后查看 psad 如何检测它们：

- `TCP` `connect()` 扫描
- `TCP` `FIN`、`XMAS` 和 `NULL` 扫描
- `TCP` `SYN` 或半开放扫描
- `UDP` 扫描

注意：请参考第 `3` 章获取这些扫描技术的技术描述。

每次扫描都如图 `6-1` 所示，从 `ext_scanner` 系统启动针对 `iptables` 防火墙的外部 `71.157.X.IP` 地址。在发送第一次扫描之前，我们确保 psad 运行在 `iptables` 防火墙上，并具有 `/etc/psad/psad.conf` 文件中的默认 `DANGER_level(n)` 设置：

## NMAP 与往返时间
