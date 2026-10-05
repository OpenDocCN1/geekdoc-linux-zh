

# 图 25-14 扩展动作框

图 25-13 中的规则允许来自任何端口（右上角文本框中没有输入）、IP 地址为 10.10.4.15 的系统的流量进入 IP 地址为 10.10.4.91 的系统的端口 22（在此情况下为本地系统）。

# 显示扩展动作（SHOW EXTENDED ACTIONS）复选框

勾选显示扩展动作（Show extended actions）复选框会向添加规则窗口添加两个项目：左侧的一个数字调节框（spin box）以及指向方向（Direction）和协议（Protocol）列表的下拉列表（图 25-14）。数字调节框指定你正在添加的规则的序号。当你添加多个规则时，它可以允许你将规则放在其他规则之前。当你只添加单个规则时，它没有用。因为第一个管理流量的规则将控制流量，因此规则的顺序可能非常重要。下拉列表指定你希望规则创建的日志（Log）类型。你可以指定无日志（No log）、日志（Log）和所有日志（Log all）。第二个选项指定的是最小日志记录，而最后一个选项指定的是详细日志记录。

# iptables 简介

被称为 iptables 的功能由两个组件组成：netfilter 和 iptables。运行在内核空间（第 1156 页），netfilter 组表，包含了内核用于控制网络包过滤的规则。运行在用户空间（第 1179 页），iptables 工具用于设置、维护和显示由 netfilter 存储的规则。

规则由一个或多个标准（匹配项或分类器）和一个单一动作（目标）组成。当规则应用于数据包时，如果数据包匹配所有标准，则对包执行动作。规则存储在链（chains）中。链中的每条规则按顺序应用，直到找到匹配项为止。如果没有匹配项，则将链的策略（或默认动作）应用于数据包（第 886 页）。

在内核中，iptables 取代了早期的 iptchains 作为过滤网络包的方法。它提供了多个链以增加过滤的灵活性。iptables 工具还提供状态数据包检测（第 882 页）。

作为规则工作的一个示例，一个链包含两条规则（图 25-15）。第一条规则测试数据包的目的地是否为端口 23（TELNET），如果是，则丢弃数据包。第二条规则测试数据包是否来自 IP 地址 192.168.1.1，如果是，则更改数据包的目的地。当数据包被示例链处理时，内核应用链中的第一条规则来检查数据包是否到达了端口 23。如果答案是肯，数据包被丢弃，该数据包的处理此结束。

![](img/45ff4cd21497435daa35084a84b95d07_931_0.png)

图 25-15 链中规则工作的示例

如果答案是否，内核应用链中的第二条规则来检查数据包是否来自指定的 IP 地址。如果答案是肯，数据包头中的目的地将被更改，修改后的数据包将继续发送。如果答案是否，数据包将在不经更改的情况下发送。

链收集在三个表中：Filter、NAT 和 Mangle。每个表都有内置链（下文将描述）。你可以在 Filter 表（默认表）中创建额外的用户定义链。

Filter 表：默认表主要用于根据内容丢弃（DROP）或接受（ACCEPT）包；它不会更改包。内置链有 INPUT、FORWARD 和 OUTPUT。所有用户定义链都进入此表。

NAT 表：网络地址转换表。创建新连接的数据包通过此表路由，该表专门用于翻译源或目的字段。内置链有 PREROUTING、OUTPUT 和 POSTROUTING。仅对 DNAT、SNAT 和 MASQUERADE 目标使用此表。

- DNAT（目标 NAT）更改连接中第一个入站包的目标 IP 地址，以便将其重定向到另一个主机。连接中的后续数据包会自动进行 DNAT 处理。DNAT 有助于重定向指向防火墙或 NAT 服务器的互联网包（第 896 页）。
- SNAT（源 NAT）更改连接中第一个出站包的源 IP 地址，使其看起来来自固定的 IP 地址——例如防火墙或路由器。连接中的后续数据包会自动进行去 SNAT 处理。回复将进行 SNAT 处理以便返回原始发送者。SNAT 有助于向局域外的系统隐藏 LAN 地址，并使用单个 IP 地址为多个本地主机提供服务。
- MASQUERADE（伪装）与 SNAT 的区别仅在于它会检查并应用于每个出站包的 IP 地址，适用于如 DHCP 提供的动态 IP 地址（第 470 页）。MASQUERADE 比 SNAT 稍慢。

Mangle 表：专门用于更改数据包中的 TOS（服务类型）、TTL（存活时间）和 MARK 字段。内置链有 PREROUTING 和 OUTPUT。

![](img/45ff4cd21497435daa35084a84b95d07_932_0.png)

第 25 章 firestarter, gufw 和 iptables：设置防火墙

接下来，当数据包进入内核栈时，它会通过一些基本测试，包括校验和验证。通过这些测试后，数据包通过 PREROUTING 链，其目的地可能会被更改。如果指向另一个主机，它将通过 FORWARD 链进行路由。如果它是本地地址，它将通过 INPUT 链被接受。如果它是本地生成的，它将通过 OUTPUT 链被发送。

状态（State）：连接跟踪机（也称为状态化）提供数据包状态的信息。这允许你识别流量类型，如 NEW、ESTABLISHED 和 RELATED。连接跟踪由内核中的 conntrack 模块处理。

# iptables 简介 883

跳转和目标（Jumps and targets）：跳转或目标（第 890 页）指定了当数据包匹配标准时内核采取的动作。

# 更多信息

- Web 文，HOWTOs，FAQs：www.netfilter.org
- 教程：www.faqs.org/docs/iptables
- 多播态 DNS：www.multicastdns.org
- 脚本及更多：www.yourwebexperts.com/forum.php?f=35
- HOWTO KernelAnalysis-HOWTO IP-Masquerade-HOWTO（包含实用脚本）
- Netfilter Extensions HOWTO：www.netfilter.org
- Netfilter Hacking-HOWTO：www.netfilter.org
- 书籍 TCP/IP Illustrated，作者 W. Richard Stevens，Addison-Wesley，2002

# 前提条件

- 安装以下内容：
- iptables
iptables init 脚本：iptables 包不包含 init 脚本，因为在 Ubuntu 下，它由 gufw 调。。本章包含了配置和运行 iptables 的说明。

# 注意事项

- 启动：iptables 工具是一个操纵内核规则的工具。它与守护进程（服务器）的区别在于设置和使用方式。虽然像 Apache、vsftpd 和 sshd 这样的 Linux 守护进程从配置文件处理控制其操作的数据，但你必须为 iptables 提供一系列命令，以构建一组保留在内核中的数据包过滤规则。
- 规则：你可以按照第 891 页所解释的那样保存和重载 iptables 规则。使用 -L 选项运行 iptables 显示内核正在使用的数据包过滤规则。你可以在 /etc/rc.local 中放置加载 iptables 规则的命令，或者如果你想在启动过程的早期启动 iptables，可以写一个简单的 init 脚本，将其放在 /etc/init.d，并使用 sysv-rc-conf（第 441 页）告诉 init 何时运行它。
- 重置 iptables：如果你遇到与防火墙规则相关的问题，可以通过以下命令在不重启的情况下将内核中的包处理规则恢复到默认状态：

```
$ sudo iptables --flush
$ sudo iptables --delete-chain
```

