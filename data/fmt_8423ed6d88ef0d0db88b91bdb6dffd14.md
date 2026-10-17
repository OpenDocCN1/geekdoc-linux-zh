
SuSE 8.0 遵循相似的约定，其 IP Table 启动脚本为：

`S06SuSEfirewall2_setup`

该脚本位于 `/etc/init.rc3d` 或 `/etc/init.rc5d` 中（如果配置为自动启动 X 窗口系统）。准备脚本是：

`S01personal-firewall.initial`

最后的脚本是：

`S22personal-firewall.final`

位于同一目录。然而，SuSE 8.0 并没有提供启动 IP Chains 的脚本。你需要按照本节其他部分的说明提供自己的脚本。Slackware 遵循 BSD 软件发行版 (BSD) UNIX 约定而非 System V，使用 `/etc/rc.d` 中的 `rc.inet1` 脚本启动网络，并使用 `rc.inet2` 启动网络守护进程（包括 IP Chains）。

如你所知，被另一个模块使用的模块无法通过 `rmmod` 移除。这种使用情况通过计数（`count`）指示，并可以通过 `lsmod` 显示。作为一种安全特性，如果 IP Chains 或 IP Tables 定义了任何规则（包括用户定义的链），这些每个模块的使用计数都会增加。由于此特性，在移除 `ipchains` 或 `iptables` 模块之前，必须先移除所有用户定义的规则链。当然，一旦规则被移除，默认策略将应用到所有数据包。如果移除了 `ipchains`（或 `ip_tables`）模块，将不会进行任何防火墙防护，导致系统处于完全开放状态。为了安全起见，建议首先关闭接口（例如执行 `ifconfig eth0 down` 或 `ifconfig eth1 down`）或断开网线。

如果你正在进行远程操作，且防火墙系统没有漏洞服务，那么关闭内部接口（按惯例为 `eth1`）和任何 DMZ 接口（惯例为 `eth2`）是实际的，以便在任何开发期间继续远程工作。本节稍后将提供有关如何安全方便地进行远程防火墙开发的更多技巧。

## 12.5 使用 IP Tables 和 DMZ 的防火墙

以下命令将停止 IP Chains 运行，以便启动 IP Tables。同样的技术也可用于停止 IP Tables 以切换回 IP Chains。重启时，将发生当前设置的任何默认行为。

```
ipchains -X      移除用户定义的链
ipchains -F      清除剩余规则
rmmod ip_masq_ftp 如果已加载
rmmod ip_masq_irc  ...若已加载
...
rmmod ipchains
```

这些 IP Tables 可加载内核模块位于：

`/lib/modules/2.4.*/kernel/net/ipv4/netfilter` 目录。

你需要使用 `modprobe` 或 `insmod` 为你允许的应用程序加载 `ip_conntrack_*` 或 `ip_masq_*` 模块，例如：

```
modprobe ip_conntrack_ftp
```

可以使用 `lsmod` 命令显示当前加载的模块、其使用计数以及使用这些模块的用户列表。

上述命令的替代方案是在重命名或编辑相应的启动脚本（或移除每个 `ipchains` 或 `iptables` 的执行权限）后重启系统。

## 2. 启用防火墙规则的重启功能

任何防火墙规则集的一个至关重要的特性是：在修改规则后能够调用脚本，并安装新版本的规则，且不会导致短暂的安全性失，也不会丢失现有的 TCP 连接或其他失败的通信。虽然实现这一点只需要一点精力，但 SuSE 8.0、Red Hat 7.3 以及我分析的大多数其他基于 Linux 的规则集都未能正确实现这一点。

在设计你的 IP Tables 或 IP Chains 规则顺序（或设计 UNIX、Cisco Pix、Checkpoint 以及其他防火墙的规则）时，需要记住两个设计要求：

### a. 防火墙规则的添加是原子的
每个添加、移除或更改的规则都是作为原子操作完成的。这意味着每个 `iptables` 或 `ipchains` 命令在某个精确的瞬间对内核产生影响。在此之前规则不存在，在此之后则存在。在任何两个命令之间，本质上可以有无限数量的数据包进入接口，并被处理或从其发出或丢弃。

### b. 避免保护的短暂丢失
防火墙宁可为了几秒钟内丢弃所有入数据包（即使是合法的）而承担风险，也不要允许一个恶意数据包进入。所有流行的协议，事实上，任何重要的设计良好的协议都有重试机制。这种重试机制正如其名。如果发送的数据包或其响应丢失，重试会在稍后的一段时间内出现。如果第一个数据包确实通过了，只有响应丢失了，该机制会防止数据包的操作以有害的方式重复。

这种机制可以防止例如由于不稳定的网络导致意外地产生两辆汽车而不是一辆。例如，TCP 中的这种机制可以忍受持续一分钟的数据包丢失。

这对防火墙设计意味着什么？任何防火墙脚本（规则集）中的第一个规则应该是针对所有链（INPUT、OUTPUT 和 forward）的 DROP（IP Tables）或 DENY（IP Chains）策略。

### 3. 大多数防火墙应该采用 DROP 策略
问问自己这一点很重要：“在执行了 `iptables` 命令后，是否可能有人穿过？” 答案应该始终是“否”。许多管理员犯的错误是将策略策略设置为 ACCEPT 然后清空规则。

### 4. 策略操作不记录
在某些情况下，记录被丢弃的数据包是有用的。可以通过以下实现：

```
iptables -A FORWARD -j LOG
iptchains -A input -j LOG
```

### 5. 接口关闭时规则不移除
引用接口的防火墙规则在接口关闭（例如 `ifconfig eth0`）或 PPP 接口关闭时不会被移除。事实上，在 Linux 防火墙中，指定的任何接口存储为字符串。当评估数据包时，数据包的接口将与通配符接口进行匹配。注意，这与路由（使用 `route` 命令指定）不同，路由会在接口关闭时被移除。虽然任何 IP Tables 下 ERADE 规则在临时接口关闭或动态 IP 地址更改时不会被移除，但连接状态信息会从内核内存移除。

### 6. 规则不影响原始套字
原始套字在其与其连接的设备之间建立直接连接。从原始套字接收的数据包不受 IP Tables 或 IP Chains 的过滤，但出站数据包会被过滤。原始套字通常用于嗅探器分析流量。这些嗅探器包括 `tcpdump`、`Ethereal`、`Portsentry`（隐身模式）、`nmap` 和某些黑客工具。原始套字还用于程序向网络注入数据包，例如 `nmap` 和某些黑客工具。

原始套字改变了你处理 Portsentry 锁定无法广播的“嘈”内部系统的方式。通常你会添加规则来阻止广播。相反，你需要编辑 `ipt.conf` 文件并列出要忽略的目标端口，在 `ADVANCED_EXCLUDE_TCP` 变量或 `ADVANCED_EXCLUDE_UDP` 变量中。

在测试规则集时（应在部署前完成），可以使用 `Ethereal` 或 `tcpdump` 查看进入系统的数据包。这可以与通过 IP Tables 或 IP Chains 的包进行对比。

由于出站数据包会被过滤，严格的出站过滤将防止你（或你的敌人）从你的防火墙或内部系统使用 `nmap` 或类似的工具。进行此类测试需要临时放松规则。

### 7. 有用的别名 (Aliases)

多年来，我发现使用短名称可以节省大量重复输入，而且使用注释来解释短名称比我所谓的“为变量、参数或命令写长篇文章来命名”是更高效的解决方案。这并非普遍的观点，因此取决于什么方法对你最有效。我使用 `ipt` 别名来让我能够输入 `ipt` 来代表 IP Tables 或 IP Chains。同样，为了列出现有规则，我设置了 `iptL` 和 `iptLn` 别名。由于列出会包含规则编号（每个链中的每个规则从 1 开始），我还创建了带编号的列出现有规则的别名。我所有的列出别名都通过了 `more` 命令，不过你可能更喜欢功能更强大的 Gnu 防火墙别名：

我的 `ipt` 别名如下：

```
alias ipt ipchains
# 列出规则 ... 并带有编号
alias iptL 'iptchains -L -n v :* | more'
alias iptLn 'iptchains -L -n v --line-numbers :* | more'
```

```
alias ipt iptables
# 列出规则 ... 并带有编号
alias iptL 'iptables -L -n - v :* | sed s/$/......//" | more'
alias iptLn 'iptables -L -n -v --line-numbers :* | sed s/$/......//" | more'
```

```
# 列出 NAT 规则 ... 并带有编号
alias iptLt 'iptables -L -n -v nat :* | sed s/$/......//" | more'
```
