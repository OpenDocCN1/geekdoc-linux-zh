
| `/etc/shadow` | `root` | `400` |

## 事件响应

事件响应是当系统发生异常情况时该如何做的策略。

你对事件的响应取决于你如何使用系统以及系统对你有多重要。对于全面的事件响应，关键点如下：

- *弄清楚*你的计算机和网络有多关键，并识别哪些人员或资源可以帮助你的系统。
- *采取措施*防止并减少潜在损害。
- *制定*并记录一份全面的应急计划。
- *定期测试*应急计划并根据需要进行修订。

# 学习安全测试方法 581

`chkconfig --list | more`

在输出中，查找包含以下内容的行：

`xinetd based services:`

这些行列出了 `xinetd` 可以启动的所有服务，以及它们是处于开启还是关闭状态。例如，这里有几行显示了系统上 `xinetd` 服务的状态：

```
chargen-udp: off
rsync: off
chargen: off
daytime-udp: off
daytime: off
echo-udp: off
echo: off
services: off
servers: off
time-udp: off
time: off
cups-lpd: off
sgi_fam: on
tkalk: off
imap: off
... 行已删除 ...
```

在这种情况下，`sgi_fam`（一个报告任何文件更改的服务器）服务是开启的，但其他所有服务都是关闭的。

此外，还要检查以下文件以查看与 `xinetd` 服务一起使用的任何访问控制：

- `/etc/hosts.allow` 列出允许访问特定服务的主机列表。
- `/etc/hosts.deny` 列出应该被拒绝访问服务的列表。

## 独立服务

许多服务如 `httpd`（Web 服务器）和 `sendmail`（邮件服务器）在启动时启动，前提是它们被配置为在启动时启动。你可以使用 `chkconfig` 命令来检查这些独立服务中哪些被设置为不同的运行级别（`run levels`）（有关运行级别的更多信息请参见第 VI 卷第 1 章）。通常，你的 Red Hat Linux 系统启动于级别 3（文本登录）或级别 5（图形化登录）。因此，重要的是级别 3 和 5 中服务器的设置。要查看服务器列表，请输入以下命令：

```
chkconfig --list | more
```

第七 卷

第 4 章

执行安全审计

## 582 学习安全测试方法

以下是你可能会看到的部分列表：

| | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
|---|---|---|---|---|---|---|---|
| `gpm` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `kudzu` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `syslog` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `rawices` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `netfs` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `network` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `random` | 0:off | 1:off | 2:on | 3:on | 4:on | 5:on | 6:off |
| `lasthd` | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| `pcmlia` | 0:off | 1:off | 2:off | 3:off | 4:off | 5:off | 6:off |
| `keytable` | 0:off | 1:off | 2:on | 3:on | 4:on | 5:on | 6:off |
| `apmd` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `atd` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `autofofs` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `iptables` | 0:off | 1:off | 2:on | 3:on | 4:on | 5:on | 6:off |
| `isdn` | 0:off | 1:off | 2:on | 3:on | 4:on | 5:on | 6:off |
| `sshd` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `portmap` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `nfs` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `nflock` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `sendmail` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `rhndd` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |
| `crond` | 0:off | 1:off | 2:off | 3:on | 4:on | 5:on | 6:off |

第一列显示服务器的名称。查看以 `3:` 开头和以 `5:` 开头的条列：这些显示了服务器在运行级别 3 和 5 下的状态。如果你正在对网络进行自评估，并发现某些服务器不应该运行，你可以使用 `chkconfig` 命令在运行级别 3 和 5 下关闭它们：

```
chkconfig --level 3 servicename
```

将 `servicename` 替换为你想要关闭的服务器名称。

如果你正在审计网络，请记录所有已开启的服务器——然后根据你对系统的了解（例如，Web 服务器或桌面系统）以及它如何连接到互联网（例如，通过防火墙或直接连接），来判断它们是否应该开启。

## 渗透测试

渗透测试是了解 Red Hat Linux 系统上实际运行哪些服务的最佳方法。渗透测试涉及从攻击者的角度尝试访问你的系统。通常，你从互联网上的系统执行此操作，并尝试查看是否可以入侵。

## 探索安全工具 583

渗透测试的一个方面是查看 Red Hat Linux 系统上开放了哪些端口。端口号只是识别到系统特定 TCP/IP 连接的数字。只有当该端口的连接请求到达时服务器做出响应，连接端口的尝试才会成功。渗透测试的第一步是执行端口扫描。“端口扫描”一词用于描述尝试连接端口号以查看是否返回有效响应的自动化过程。Red Hat Linux 带了一个名为 `nmap` 的端口扫描工具（稍后介绍）。

执行端口扫描后，识别可能被利用的漏洞。并不是所有服务器都有安全问题，但许多自动化工具可以扫描并发现它们。

## 探索测试工具

许多自动化工具可用于安全测试。某些工具用于发现 IP 地址范围内的开启端口。另一些工具用于与开启端口相关的漏洞。`nmap` 可以在 [www.insecure.org/tools.html](http://www.insecure.org/tools.html) 浏览工具列表。表 4-4 列出了这些工具。

| 表 4-4 | 计算机安全工具 |
|---|---|
| 类型 | 名称 |
|---|---|
| 端口扫描器 | `nmap`, `Strobe` |
| 漏洞扫描器 | `Nessus`, `SAINT`, `Whisker`, `Internet Scanner`, `Retina Network` |
| 表 4-4 (续) | |
| 类型 | 名称 |
|---|---|
| 网络工具 | `Netcat`, `hping2`, `ntop`, `ping` |
| 主机安全工具 | `Tripwire`, `lsof` |
| 数据包嗅探器 | `tcpdump`, `Ethereal`, `dsniff` |
| 入侵检测系统 (IDS) | `Snort`, `Abacus portsentry`, `scanlog`, `NFR`, `LIDS` |
| 密码检查工具 | `John the Ripper`, `LC4` |
| 日志分析与监控工具 | `logcolour`, `tcpdstats`, `nlog`, `logcheck`, `Swatch` |

## nmap
