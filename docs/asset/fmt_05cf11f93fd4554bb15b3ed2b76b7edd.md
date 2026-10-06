
列表 10-3 显示了结果。

## 列表 10-3. 带有计数器接口的当前规则

Chain RH-Firewall-1-INPUT (2 references)

| pkts | target | prot | in | out | source | destination |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | ACCEPT | all | - | 10 * 0 | 0.0.0.0/0 | 0.0.0.0/0 |
| 0 | ACCEPT | icmp | * | * | 0.0.0.0/0 | 0.0.0.0/0 |
| 0 | ACCEPT | esp | * | * | 0.0.0.0/0 | 0.0.0.0/0 |
| 0 | ACCEPT | ah | * | * | 0.0.0.0/0 | 0.0.0.0/0 |
| 0 | ACCEPT | udp | * | * | 0.0.0.0/0 | 224.0.0.251 |
| 0 | ACCEPT | udp | * | * | 0.0.0.0/0 | 0.0.0.0/0 dpt:631 |
| 0 | ACCEPT | tcp | * | * | 0.0.0.0/0 | 0.0.0.0/0 dpt:631 |
| 0 | ACCEPT | all | * | * | 0.0.0.0/0 | 0.0.0.0/0 state RELATED,ESTABLISHED |
| 0 | ACCEPT | tcp | * | * | 0.0.0.0/0 | 0.0.0.0/0 state NEW dpt:22 |
| 0 | REJECT | all | -- | -- | 0.0.0.0/0 | 0.0.0.0/0 |
| | icmp-host-prohibited | | | | 0.0.0.0/0 | 0.0.0.0/0 |

（注：列表 10-3 中的表格数据是根据 OCR 源提供的碎片文本重构的。）

一旦我们加载了模块，就可以分别使用 `--sport` 和 `--dport` 参数来指定源和目的详情。每个端口可以指定为单个端口号或连续的端口范围，格式为 `低数字:高数字`。你也可以使用 `!` 对端口进行取反，表示可以使用该端口以外的所有端口。作为主机选择，这可能会令人困惑，因此最好匹配端口并使用不同的目标。列表 10-5 显示了一些协议和端口匹配的示例。

## 列表 10-5 协议和端口匹配的示例

```
-m state --state NEW -m tcp -p tcp --dport 80 # 端口 80 用于 http 流量

-m state --state NEW -m tcp -p tcp --dport 5000:5999 # VNC 端口范围

-m udp -p udp --dport 514 # syslog 是一个 udp 协议

-m udp -p udp --dport 123 # ntp 使用相同的端口发送和接收

-m tcp -p tcp ! 22 # 除 ssh 以外的所有端口
```

当你使用 TCP 规则时，源端口通常并不重要。大多数连接都是使用随机的高号源端口到相同的已知目的端口建立的。

许多基于 UDP 的协议将源端口设置为与目的端口相同。虽然我们可以根据源端口进行过滤，但这并没有提供任何优势，因此我们仅根据目的端口进行过滤。

我们在 TCP 协议中使用的另一个额外选项是状态检查（state inspection）。这需要加载状态模块。你通过 `--state NEW` 加载的状态模块将只匹配连接请求。一旦连接建立，数据包将匹配另一个规则，该规则匹配 `ESTABLISHED` 和 `RELATED` 连接。列表 10-6 显示了如何使用状态模块。我们使用默认防火墙配置中自动添加的规则来允许已建立和相关的数据包。

## 列表 10-6 使用状态匹配

```
-m state --state NEW -m tcp -p tcp --dport n

-m state --state ESTABLISHED, RELATED
```

在我们构建规则之前，谜题最后一部分是目标（target）。它告诉 netfilter 在发现数据包匹配规则时做什么。目标通过 `-j target` 指定。主要目标有 `ACCEPT`、`DROP` 和 `REJECT`。你也可以跳转到另一个链并从那里开始处理。

`ACCEPT` 目标将允许数据包继续未过滤通过，直到你指定你想要允许的流量。

`DROP` 将导致数据包被丢弃。数据包发送者不会收到，因此任何尝试连接的人都必须等待连接超时后才能收到错误。

`REJECT` 目标将丢弃数据包，但不会向发送者发送 ICMP 错误消息。通过这种方式，发送者会立即知道无法使用服务。

每个内置链都可以有一个默认目标，该目标适用于任何到达链末尾且未匹配任何规则的数据包。此默认目标可以通过 `-P` 参数指定。

# 第 10 章 网络安全

> 提示：ICMP 是网络控制消息协议。它的主要用途是通知客户端或服务器网络错误。常见的错误是“主机不可达”（No Route to Host）和“拒绝连接”（Connection Refused）。这也是 ping 命令使用的协议。

使用这些参数，你将能够构建用于 `iptables` 的规则。为了将你的规则添加到链中，你必须指定将它们放在哪个链。记住，链中的规则按从第一个到最后一个顺序处理。当找到匹配项时，处理停止并应用目标。有几种方法可以排列规则序列。简单的方法是使用 `-A`，它将你的规则附加到链的末尾。在编辑 `/etc/sysconfig/iptables` 时这样做很好，但从命令行执行影响所有流量的全规则命令则不起作用。

你也可以使用 `-I` 进行插入（insert）。对于链的开头或链中的任何位置，大多数情况下，使用 `-I` 在链的开头插入是足够的。你可以通过指定规则编号在任何规则之前插入，例如：`-I 规则数字`。规则从 1 开始编号，因此 `-I 2` 将将规则插入到位置 2。当前位于位置 2 的规则将移动到位置 3，依此类推。你还可以使用 `-R 规则数字` 替换链中的任何点。在链中数出确切的位置可能很难，因此先删除规则然后在链的开头插入新规则通常更简单。

从链中删除规则有两种方法：可以使用 `-D` 配合规则规格；或者，你可以使用 `-D 规则数字` 指定规则在链中的位置，该位置的规则将被删除。

> 提示：如果你使用命令 `iptables -I 规则` 或 `iptables -A 规则` 添加规则，你可以使用命令 `iptables -D 规则` 该规则。

你现在应该对可以构建的规则类型有了了解。通过回顾使用 shell 提示符添加规则的第一种方法，列表 10-7 显示了一些你可以在服务器上尝试的示例规则。添加每条规则后，检查哪些工作站连接到该服务。然后删除该规则。

## 列表 10-7 示例规则

```
# 允许特定主机连接所有服务

iptables -A Firewall-1-INPUT -s 192.168.3.20 -j ACCEPT

### 之前的规则

iptables -D Firewall-1-INPUT -s 192.168.3.20

### 允许特定子网连接

iptables -A Firewall-1-INPUT -s 192.168.3.0/24 -j ACCEPT

### 允许特定主机连接

iptables -A Firewall-1-INPUT -s 192.168.3.20 -j ACCEPT

### 允许特定主机连接

iptables -A Firewall-1-INPUT -s 192.168.3.20 -j ACCEPT
```

# 第 10 章 网络安全

现在你已经制定了规则并测试了它们有效，你想确保它们在重启后生效。实现此点的简单方法是使用 `iptables save` 命令。此脚本允许你通过编辑 `/etc/config` 文件来调整某些操作。一些变量是 `IPTABLES_ON_STOP` 和 `IPTABLES_REST`。如果你使用 `IPTABLES_ON_STOP-yes`，那么每当你使用 `shutdown` 或 `restart` 命令系统时，你的当前规则将被保存。如果你使用 `IPTABLES_REST-yes`，那么每当你使用 `restart` 命令时，你的当前规则将被保存。使用这种方法管理规则在你频繁手动更改时非常方便，但仍然可以使用 `iptables save` 管理服务。

这种方法并不是万无一失的，因为服务器可能会崩溃、断电或其他原因导致正常关机。由于不断向列表开头添加规则，规则将以一种奇怪的顺序排列，可能变得难以管理。无法通过注释记录每条规则的作用。

第三种方法是描述对 `/etc/config/iptables` 文件的编辑。通过结合测试 shell，这种方法提供了维护文档良好的防火墙脚本的能力，这应该始终保持系统处于一致的状态。添加一个空白文件。使用你喜欢的文本编辑器开始，运行 `system-config-securitylevel` 并编辑 `/etc/config/iptables`，添加列表 10-8 中以 `#` 开头的注释。一旦你开始对配置文件进行手动更改，就不应再运行 `system-config-securitylevel service iptables save`，否则可能会覆盖你的更改。你应该确保在你的 `/etc/config/iptablesconfig` 文件中，两个 `IPTABLES_ON_STOP`。

### 列表 10-8 /etc/config/iptables 骨架

```
# 此文件手动维护

# 不要运行 system-config-securitylevel

*filter

:INPUT ACCEPT [0:0]

:FORWARD ACCEPT [0:0]

:OUTPUT ACCEPT [0:0]

:RH: Firewall-1-INPUT - [0:0]

-A INPUT -j RH Firewall-1-INPUT

-A FORWARD -j RH Firewall-1-INPUT

-A Firewall-1-INPUT -i lo -j ACCEPT

-A Firewall-1-INPUT -p icmp --icmp-type -j ACCEPT

-A Firewall-1-INPUT -p 50 -j ACCEPT

-A Firewall-1-INPUT -p 51 -j ACCEPT
```

```bash
-A RH-Firewall-1-INPUT -p udp --dport 5353 -d 224.0.0.251 -j ACCEPT
-A RH-Firewall-1-INPUT -p udp -m udp --dport 631 -j ACCEPT
-A RH-Firewall-1-INPUT -p tcp -m tcp --dport 631 -j ACCEPT
-A RH-Firewall-1-INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
# 在此行下方输入您的规则
# 不要修改此行下方
-A RH-Firewall-1-INPUT -j REJECT --reject-with icmp-host-prohibited
COMMIT
```

现在你已经准备好根据需要向文件添加规则了。请将你的规则添加到注释之间，以防它们被默认规则覆盖。添加完规则后，你可以使用 `service iptables` 命令来应用它们。

既然已经涵盖了过滤命令的基础知识，默认防火墙配置中的条目应该更容易理解了。以下是对每个条目的简要说明以及它们存在的原因。以*: COMMENT` 开头的行会被初始化脚本解释。以 -A 开头的行是初始化脚本传递给 `iptables` 命令的规则。

```bash
### 选择 'filter' 表：
*filter
# 将 INPUT 链的默认动作设置为 ACCEPT并将计数器设置为 0
:INPUT ACCEPT [0]
# 将 FORWARD 链的默认动作设置为 ACCEPT并将计数器设置为 0
:FORWARD ACCEPT [0]
# 将 OUTPUT 链的默认动作设置为 ACCEPT并将计数器设置为 0
:OUTPUT ACCEPT [0]
# 创建一个名为 RH-Firewall-1-INPUT 的新链并将计数器设置为 0
:RH-Firewall-1-INPUT [0]
### 让所有输入数据包跳到 RH-Firewall-1-INPUT 链
-A INPUT -j RH-Firewall-1-INPUT
### 让所有转发的数据包跳到 RH-Firewall-1-INPUT 链
-A FORWARD -j RH-Firewall-1-INPUT
### 允许所有本地流量
-A RH-Firewall-1-INPUT -i lo -j ACCEPT
### 根据正确的 TCP/IP 运行所需的，允许 ICMP 流量
-A RH-Firewall-1-INPUT -p icmp --icmp-type any -j ACCEPT
### 允许 ESP 流量，IPsec 使用的协议
-A RH-Firewall-1-INPUT -p 50 -j ACCEPT
### 允许 AH 流量，IPsec 使用的协议
-A RH-Firewall-1-INPUT -i eth0 -j ACCEPT
# 允许多播流量，可用于 Zeroconf 和 bonjour
-A RH-Firewall-1-INPUT -p udp --dport 5353 -d 224.0.0.251 -j ACCEPT
### 允许 Internet协议 (IPP)
-A RH-Firewall-1-INPUT -p udp -m udp --dport 631 -j ACCEPT
### 允许 Internet协议 (IPP)
-A RH-Firewall-1-INPUT -p tcp -m tcp --dport 631 -j ACCEPT
# 允许正在被状态检测管理的的连接
-A RH-Firewall-1-INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
### 拒绝目前为止未匹配的任何数据包
-A RH-Firewall-1-INPUT -j REJECT --reject-with icmp-host-prohibited
### 激活此表的配置
COMMIT
```

带有剑号 (†)标记的规则到目前为止保持不变，因为它们包含在默认的 CentOS 配置中。如果你不使用这些协议，删除它们是安全的。没有标记剑号的规则是重要的，在不理解更改影响的情况下不应修改它们。

> 提示：防火墙对 CUPS/IPP 有特殊处理，默认的 CUPS 配置为仅监听本地。如果你启用了网络打印，则你应该创建自己的防火墙规则，只允许所需的工作站打印。

## 将 CentOS 作为路由器

具有多个接口的服务器被称为多宿主主机（multihomed）。接口通常是网卡，例如以太网卡。这些接口通常命名为 `eth0` 和 `eth1`。还有其他类型的接口，例如环回接口、拨号上网 PPP 接口等。在本节中，我们将处理两个以太网接口，但对于任何类型的接口行为都是相同的。

虽然多宿主主机有很多可能的配置，但最简单是为不同的 IP 网络为每个接口分配一个唯一的 IP 地址。

我们将查看实现这一点的两种方法。首先，我们将查看 CentOS 如何作为路由器并在一个子网和另一个子网之间转发流量。然后，我们将查看 IP 伪装（masquerading），它允许私有子网通过共享单个 IP 地址访问互联网。

将你的 CentOS 服务器变成路由器非常简单。只需要启用 IP 转发。执行此操作，编辑 `/etc/sysctl.conf` 并设置 `net.ipv4.ip_forward = 1`。要应用此更改，运行 `sysctl -p`。

如果你有多个接口，需要配置哪些流量在接口之间转发。转发的数据包由 RH-Firewall-1-INPUT 链处理，你必须向链中添加规则。因此，呈现的规则中没有说明数据包是从哪个接口到达的。在具有多个接口的路由器上，这是一个问题。`iptables` 命令提供了参数来允许数据包从哪个接口进入以及从哪个接口输出。每个参数接收一个接口。

要允许数据包从哪个接口进入并从哪个接口输出，通用格式为：

```bash
iptables -A RH-Firewall-1-INPUT -i eth0 -o eth1 -j ACCEPT
```

## 使用 netfilter 进行伪装

到目前为止我们只查看了用于过滤的 netfilter。如果你的服务器有多个接口，netfilter 可以做很多事情。一个非常实用的功能是 IP 伪装。这通常被称为网络转换（NAT）。然而，伪装与转发有微妙的区别，因为它需要对地址和协议进行修改。

要使用伪装，你需要使用 `MASQUERADE` 目标，它只能在 nat 表的 POSTROUTING 链中使用。目标通过 `iptables` 命令的 `-t` 参数指定。除了 MASQUERADE 目标还需要指定输出接口。它是连接服务器到互联网的接口。

IP 伪装的主要目的是允许许多主机使用单个 IP 地址访问互联网。Windows 用户可能熟悉 Internet 连接共享，这与我们通过 NAT 实现的类似。

设置伪装请使用以下命令：

```bash
### 假设 eth0 是接口，对内部流量进行互联网伪装
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
### 假设我们 eth0 上的子网是 192.168.3.0/24，且
### 服务器是 192.168.3.1，允许互联网流量被转发
iptables -I RH-Firewall-1-INPUT -i eth0 -s 192.168.3.0/24 \
  -d 192.168.3.1 -j ACCEPT
```
