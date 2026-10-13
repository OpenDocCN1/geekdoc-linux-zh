
通常，以 `#` 字符开头的行是注释，`xinetd` 在解析文件时会忽略这些注释。每个非注释行由逗号分隔的守护程序列表组成，后跟一个冒号 (`:`) 字符，然后是逗号分隔的待检查客户端地址列表。在此上下文中，客户端是指尝试访问你系统上网络服务的任何计算机。

客户端条目可以是数字 IP 地址（如 `199.170.177.25`）或主机名（如 `dexter.glaci.com`），但更常见的是指定整个地址范围的通配符变体。客户端条目可以取四种不同的形式。`hosts.allow` 文件的联机手册页对此描述如下：

- 以点 ( `.` ) 字符开头的字符串。如果主机名的最后部分与指定模式匹配，则匹配该主机名。例如，模式 `.tue.nl` 匹配主机名 `wzw.win.tue.nl`。

- 以点 ( `.` ) 字符结尾的字符串。如果主机地址的前几个数字字段与给定字符串匹配，则匹配该主机地址。例如，模式 `131.155.` 匹配（几乎所有）Eindhoven 大学网络上的主机地址 (`131.155.x.x`)。

- 以 `@` 符号开头的字符串被视为 NIS（前身为 YP）netgroup 名称。如果主机名是指定 netgroup 的成员，则匹配该主机名。Netgroup 匹配不适用于守护程序进程名称或客户端用户名。

- 形式为 `n.n.n.n/m.m.m.m` 的表达式被解释为 net/mask 对。如果 net 等于地址与掩码的按位与，则匹配该主机地址。例如，net/mask 模式 `131.155.72.0/255.255.254.0` 匹配 `131.155.72.0` 到 `131.155.73.255` 范围内的每个地址。

示例 `hosts.allow` 包含前两种类型的客户端指定。条目 `199.170.177.` 将匹配以该字符串开头的任何 IP 地址，如 `199.170.177.25`。客户端条目 `.glaci.com` 将匹配 `dexter.glaci.com` 或 `scooby.glaci.com` 等主机名。

让我们看看当名为 `daffy.glaci.com`（IP 地址为 `199.170.179.18`）的主机使用 Telnet 协议连接到你的 Red Hat Linux 计算机时会发生什么：

1. `Xinetd` 接收连接请求。

2. `Xinetd` 开始将 `daffy.glaci.com` 的地址和名称与 `/etc/hosts.allow` 中列出的规则进行比较。它从文件顶部开始，向下查找直到找到匹配项。守护程序（处理你的 Red Hat Linux 计算机上网络服务的程序）和连接客户端的 IP 地址或名称都必须与 `hosts.allow` 文件中的信息匹配。在这种情况下，遇到的第二条规则与请求匹配：

```
in.telnetd: 199.170.177., .glaci.com
```

3. Daffy 不在 `199.170.177` 子网中，但它位于 `glaci.com` 域中。`Xinetd` 在找到此匹配项后立即停止搜索文件。

如果 Daffy 使用 IMAP 协议连接到你的计算机会怎样？在这种情况下，它不匹配 `hosts.allow` 中的任何规则；唯一引用 `imapd` 守护程序的行并未引用 `199.170.179` 子网或 `glaci.com` 域。`Xinetd` 继续处理 `hosts.deny` 文件。条目 `ALL: ALL` 匹配任何内容，因此 `tcpd` 拒绝该连接。

`ALL` 通配符也用于 `hosts.allow` 文件。在这种情况下，我们要告诉 `xinetd` 允许任何主机连接到 Linux 计算机上的 FTP 服务。这对于运行任何人都可以访问的匿名 FTP 服务器是合适的。如果你没有运行匿名 FTP 站点，你通常不应使用 `ALL` 标志。

一个好经验法则是，尽可能严格地限制 `hosts.allow` 和 `hosts.deny` 文件，然后仅显式启用你真正需要的服务。此外，仅授予真正需要访问权的系统的访问权限。使用 `ALL` 标志来授予特定服务的通用访问可能比输入长长的子网或域列表更容易，但花几分钟时间采取适当的安全措施比花几个小时从入侵中恢复要好得多。

> **提示：** 你可以使用 `/etc/xinetd.conf` 文件中的各种选项进一步限制对服务的访问，甚至可以将对某些服务的访问限制在一天中的特定时段。阅读 `xinetd` 的手册页（在命令提示符下输入 `man xinetd`）以了解有关这些选项的更多信息。

# 使用防火墙保护你的网络

什么是防火墙？在非计算机世界中，防火墙是防止火势蔓延的物理屏障。计算机防火墙起类似的作用，但它们试图阻止的“火灾”是互联网上攻击者的攻击。在此上下文中，防火墙是位于你的网络和互联网之间的计算机硬件，它调节和控制信息的流动。

## 使用过滤型或代理型防火墙

防火墙的两种主要类型是过滤型防火墙和代理型防火墙。通常，这两种类型都会用于保护网络。单台计算机甚至可以同时承担这两种角色。

## 过滤型防火墙

过滤型防火墙过滤在你网络和互联网之间流动的流量，阻挡某些可能使你的网络面临风险的内容。它可以将互联网上的访问限制为你网络中的特定计算机。它还可以限制通信类型，有选择地允许或拒绝各种互联网服务。

要使 Linux 充当过滤型防火墙，你可以使用 `ipchains` 或 `iptables` 功能。`iptables` 功能是两者中较新的，旨在取代 `ipchains` 以配置 Linux 防火墙。然而，Red Hat Linux 在安装期间使用 `ipchains` 为你设置防火墙，因此你必须禁用它并启用 `iptables` 才能使用 `iptables` 代替。

本章将描述 `ipchains` 和 `iptables`。

> **注意：** 你可以在 `iptables HOWTO` 中阅读 `ipchains` 和 `iptables` 之间的差异，地址为 `http://netfilter.samba.org/unreliable-guides/packet-filtering-HOWTO/packet-filtering-HOWTO.linuxdoc-7.html`。

它自行处理各种网络服务，而不是直接转发。在这个意义上，它是发起请求系统的“代理”。

代理防火墙对互联网服务器“隐藏”了你的计算机存在的事实。此外，代理防火墙通常还会处理来自互联网的所有传入连接（例如 Web 流量、FTP 下载和电子邮件投递）。再次强调，这是为了最大限度地减少外部世界看到你内部网络的机会。

## 配置 ipchains 过滤防火墙

`Ipchains` 通过检查在网络接口上发送和接收的数据包，并决定哪些数据包应被投递，哪些应被阻止来工作。它通过检查一个规则列表（也称为链）来实现这一点。它会在第一个匹配数据包的规则处停止，并检查该规则的目标。

如果你在 Red Hat Linux 安装过程中配置了防火墙，那么一些规则已经为你设置好了。这些规则可能相当严格。安装后系统启动并运行，你应该做的第一件事就是检查防火墙的当前状态。作为 root 用户输入以下内容即可做到：

```
# ipchains -L
Chain input (policy ACCEPT):
target  prot opt source       destination  ports
ACCEPT  all  --  anywhere       anywhere     n/a
ACCEPT  udp  --  a.myisp.net  anywhere     domain - any
ACCEPT  udp  --  b.myisp.net  anywhere     domain - any
DENY    tcp  --  anywhere       anywhere     any - any
DENY    udp  --  anywhere       anywhere     any - any
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

上述是在 Red Hat Linux 安装期间选择默认防火墙设置（高安全性）时我得到的输出结果。请注意，只有输入受到限制。换句话说，限制的是外部用户可以请求的服务。第一个 `ACCEPT` 行是由一条允许本地系统用户发起的所有请求的规则产生的（即，它允许回环驱动程序，如端口列下的 `n/a` 所示）。启用此规则后，你可以请求本地系统的任何服务，而数据包不会被拒绝。

接下来的两个 `ACCEPT` 行允许我指定为 DNS 服务器的计算机（`from /etc/resolv.conf`）请求我计算机的 DNS 服务（`domain`）。最后两条规则（`DENY`）导致所有不匹配之前规则的 `tcp` 和 `udp` 请求被拒绝。

这个默认防火墙配置在 `/etc/sysconfig/ipchains` 文件中设置。当 `ipchains` 服务在系统启动时启动（`/etc/init.d/ipchains`）时，服务从 `/etc/sysconfig/ipchains` 读取规则。以下是该文件中的规则，用于创建上述配置：
