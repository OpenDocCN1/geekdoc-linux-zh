

# 否定条件

在条件前加上感叹号（!）可以对该条件进行否定。例如，对 `-p` 选项的条件进行否定将匹配“任何非指定协议的数据包”。这种否定也适用于所有其他条件。

`-s address` 或 `-s network/mask` 条件匹配数据包的源地址。相应地，`-d address` 或 `-d network/mask` 匹配目的地址。

`-i interface` 条件选择来自网络接口的包。`-o interface` 选择从特定接口发出的包。

`--state state` 条件匹配数据包在连接中的状态（这需要 `ipt_conrack` 内核模块以进行连接跟踪）。`NEW` 状态描述启动新连接的数据包，`ESTABLISHED` 匹配属于已存在连接的数据包，而 `RELATED` 匹配与现有连接建立新关系的数据包（这对于 FTP 协议“活动”模式下的 `ftp-data` 连接非常有用）。

`iptables` 和 `ip6tables` 有许多可用选项，精通它们需要大量的学习和经验。然而，你最经常使用的选项之一是阻止来自主机或主机范围的恶意网络流量。例如，要静默拦截来自 IP 地址 `10.0.1.5` 和 `31.13.74.0/24` C 类子网的入站流量：

```bash
# iptables -A INPUT -s 10.0.1.5 -j DROP
# iptables -A INPUT -s 31.13.74.0/24 -j DROP
# iptables -n -L INPUT
```

```
Chain INPUT (policy ACCEPT)
target prot opt source
DROP all 10.0.1.5 0.0.0.0/0
DROP all 31.13.74.0/24 0.0.0.0/0
```

另一个常用的 `iptables` 命令是防止特定服务或端口的网络流量。要允许连接 SSH、HTTP、IMAP，你可以运行以下命令：

```bash
# iptables -A INPUT -m state --state NEW -p tcp --dport 22 -j ACCEPT
# iptables -A INPUT -m state --state NEW -p tcp --dport 80 -j ACCEPT
# iptables -A INPUT -m state --state NEW -p tcp --dport 143 -j ACCEPT
# iptables -n -L INPUT
```

```
Chain INPUT (policy ACCEPT)
target prot opt source
DROP all 10.0.1.5 0.0.0.0/0
DROP all 31.13.74.0/24 0.0.0.0/0
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:143
```

清理旧且不必要的规则被认为是良好的习惯。删除 `iptables` 规则最简单的方法是通过行号引用规则，你可以通过 `--line-numbers` 获取这些行号。但要小心，删除一条规则将导致链中后续出现的所有规则重新编号。

```bash
# iptables -n L INPUT --line-numbers
Chain INPUT (POLICY ACCEPT)
num target prot source destination
1 DROP all 10.0.0.1 0.0.0.0/0
2 DROP all 31.13.74/24 0.0.0.0/0
3 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
4 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
5 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:143
# iptables -D INPUT 2
# iptables -n L INPUT --line-numbers
Chain INPUT (POLICY ACCEPT)
num target prot source destination
1 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:22
2 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:80
3 ACCEPT tcp 0.0.0.0/0 0.0.0.0/0 state NEW tcp dpt:143
```

还有更多特定的条件，取决于上述通用条件。更多信息请参阅 `iptables(8)` 和 `ip6tables(8)`。

## 7.4.3 创建规则

每条规则的都需要调用 `iptables` 或 `ip6tables`。手动输入这些命令非常繁琐，因此通常将它们存储在脚本中，以便在每次机器启动时自动配置。也可以使用如 `fwbuilder` 等高级工具来准备。

```bash
# apt install fwbuilder
```

原理很简单。在第一步中，描述实际规则所需的元素：
- 防火墙本身及其网络接口
- 相应的网络范围
- 服务器
- 托管在服务器上的端口

接下来，通过对对象进行拖拽操作创建规则，如图 7.2 所示的 `fwbuilder` 主窗口。上下文菜单可以更改指定（例如）。然后需要选择并配置动作（action）。

至于 IPv6，你可以为 IPv4 和 IPv6 创建两个规则集，或者只创建一个并让 `fwbuilder` 分配规则。

## 防火墙构建器 - [iptables.fw]

# fwbuilder / Policy

| 源 | 目的 | 服务 | 接口 | 方向 | 动作 | 注释 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Any | udp | 3478-3479 (STUN) | Any | Both Accept | |
| 2 | Any | udp | 5000-5501 (SIP) | Any | Both Accept | |
| 3 | Any | udp | | Any | Both | | Accept
 | 4  Any | Any | | Any | Any | Inbound Accept | |
| 5 | Any | | | | Any | Outbound Accept | |
| 6 | Any | | | | Any | Outbound Accept | |

(img/4d3527b185_0.png)

`fwbuilder` 将生成针对不同系统的脚本，包括 Linux 的 `iptables`、FreeBSD 的 `pf` 以及 OpenBSD 的 `pf`。

## 7.4.4 启动时安装规则

为了在每次机器启动时实现规则，你需要在 `/etc/network/interfaces` 文件的指令中注册脚本。

```text
iface eth0 inet static
  address 192.168.0.1
  netmask 255.255.255.0
  gateway 192.168.0.254
  up /usr/local/etc/iptables.fw
```

此示例假设你使用的是 `ifdown`。如果你使用的是其他工具（如 `NetworkManager` 或 `systemd-networkd`），请参考各自的文档查找在接口后执行脚本的方法。

## 7.5 监控与日志

数据机性和保护是安全的一个重要方面，但确保服务的可用性同样重要。作为管理员和安全从业人员，你必须确保一切运行正常，并且及时检测异常行为和服务下降是你的责任。监控和日志软件在安全这一方面起着关键作用，可以洞察系统和网络发生的情况。

在本节中，我们将审查一些用于监控 Kali 多个方面的工具。

### 7.5.1. 使用 logcheck 监控日志

`logcheck` 程序默认每小时监控文件一次，并将异常日志通过电子邮件发送给管理员进行进一步分析。

被监控的文件列表存储在 `/etc/logcheck/logcheck.logfiles`。如果 `/etc/rsyslog.conf` 文件没有被完全重写，默认值运行良好。

`logcheck` 可以以不同的详细程度进行报告：`paranoid`（偏执）、`server`（服务器）和 `workstation`（工作站）。`paranoid` 非常详细，可能应限制用于特定的防火墙服务器。`server` 是默认模式，推荐大多数服务器使用。`workstation` 为工作站设计，极其简洁，过滤掉比其他选项更多的消息。

在所有情况下，`logcheck` 可能应该经过自定义以排除某些额外消息（取决于安装的服务），除非你真的想接收每小时批日志邮件。由于消息选择机制相当复杂，`/usr/share/doc/logcheck-database/README.logcheck-database.gz` 是必读的（尽管具有挑战性）。

适用的规则可以分为几种类型：

- 属于破解尝试的规则（存储在 `/etc/logcheck/cracking.d/` 目录的文件）；
- 忽略的破解尝试（`/etc/logcheck/cracking.ignore.d/`）；
- 将消息分类为安全警报的规则（`/etc/logcheck/violations.d/`）；
- 忽略的安全警报（`/etc/logcheck/violations.ignore.d/`）；
- 最后，适用于剩余消息的规则（视为系统事件）。

