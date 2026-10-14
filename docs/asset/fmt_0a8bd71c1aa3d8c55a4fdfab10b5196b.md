
```
$iptables -A OUTPUT -o eth0 -p udp -dport 53 -m state -state NEW -j ACCEPT

$iptables -A OUTPUT -o eth0 -p tcp -dport 53 -m state -state NEW -j ACCEPT

$iptables -A INPUT -i eth0 -p udp -dport 53 -m state -state NEW, ESTABLISHED,RELATED -j ACCEPT

$iptables -A INPUT -i eth0 -p tcp -dport 53 -m state -state NEW, ESTABLISHED,RELATED -j ACCEPT
```

# DNS 查询失败：名称服务器运行在内部网络和/或 DMZ 网络

在此配置中，内部/DMZ 上的名称服务器主机 `Host-B` (`10.10.10.53`) 无法通过防火墙 `Host-A` 向根服务器进行 DNS 查询。正如此处所示，这最可能是由两种场景引起的：a) 没有允许该服务建立外部连接的规则，或 b) 假设该服务允许外部连接，但未启用跟踪（tracking）。

首先，假设该防火墙对允许的外部连接有限制性策略，我们确保通过以下规则允许服务通过防火墙：

```
# 其中 eth1 是防火墙上的内部接口

IPTABLES -A FORWARD -p tcp -dport 53 -m state --state NEW, ESTABLISHED, RELATED -j ACCEPT

IPTABLES -A FORWARD -p udp -dport 53 -m state --state NEW, ESTABLISHED,RELATED -j ACCEPT

IPTABLES -A FORWARD -p udp -i eth1 -s 10.10.10.53 -d 0/0 -dport 53 -j ACCEPT

IPTABLES -A FORWARD -p tcp -i eth1 -s 10.10.10.53 -d 0/0 -dport 53 -j ACCEPT
```

# 误导性的反 DNS 问题：新邮件或到远程系统的 FTP 连接需要 30 秒或更才能启动

这实际上根本不是 DNS 问题，但有足够的人将其与反 DNS 查询（reverse DNS lookups）联系起来，因此我们决定将其放在本节。该问题的详细描述是：通常情况下，网页浏览或即时消息等其他服务的响应很快。只有那些似乎在防火墙涉及 DNS 查询的连接（例如 FTP 连接）需要 30 秒才能启动。这里可能发生的情况是另一端的服务器向你的服务器发送了 `identd` (`Auth`) 请求，而它在等待回复时超时了。

在仅主机防火墙上，有三种方法可以修复此问题。第一是最不理想的——在你的主机上运行 `identd` 服务器。这会增加一个可能被利用并泄露系统信息的服务，这是不希望的。第二种修复方法是添加一条规则来拒绝任何发往你系统的 `identd` 请求。例如下：

```
# 这将发送一个 icmp 响应，指示 identd/auth 服务不可用

IPTABLES -A INPUT -p tcp -dport 113 -j REJECT
```

第三个是添加连接跟踪规则，这也适用于处理 NAT/MASQUERADED 流量的防火墙：

```
$IPTABLES -A INPUT -m state --state ESTABLISHED,RELATED
```

# DHCP：随 IP 动态更新防火墙规则

这是一个相当常见的场景——你有一个动态分配 IP 地址的防火墙，当该 IP 地址更改时，你需要相应地更新防火墙规则。大多数 DHCP 客户端已经内置了钩子（hooks），在 IP 地址续租时调用外部脚本。我们将在下面的示例中介绍两个流行的客户端：`DHClient` 和 `DHCPcd`：

`DHClient` 是 Redhat 和 Fedora 系统的默认 DHCP 客户端（这通常已经默认配置好了）：

- 1. 创建文件 `/etc/dhcpclient-exit-hooks`。
- 2. 用你喜欢的编辑器加载该文件并添加对你的防火墙脚本的引用，例如：

```
sh /etc/rc.d/rc.firewall
```

`DHCPcd` 是另一个流行的 DHCP 客户端，你可以在 Gentoo 等发行版中找到：

- 1. 用你喜欢的编辑器加载 `/etc/dhcpc/dhcpcd.conf`
- 2. 找到末尾的 switch case 部分。在这里你会注意到几个关于接口状态的条件（刚激活/新 IP、相同 IP 续租）。
- 3. 在 New IP 情况下，插入对防火墙脚本的调用。例如：

```
sh /etc/rc.d/rc.firewall
```

# 第 18 章 DNS/DHCP

注意
确保你的防火墙脚本在加载前始终刷新（flush）规则。
确保如下内容位于你的防火墙脚本顶部。

```
$IPTABLES -F

$IPTABLES -X
```
第一行将刷新表；第二行将删除链。

# 阻止外部 DHCP

这个问题被问得足够多，足以书中给出回答。如果你已经读过本书的第 2 章，可能已经了解关于桥接环境中阻止 DHCP（或通过 MAC 地址阻止 DHCP 响应）的问题。本节假设你面临的问题是在非桥接防火墙上限制 DHCP 请求。这里有一个好消息——DHCP 响应不会跨越该防火墙。如果你担心的是这个，那么没问题了。如果 DHCP 运行在服务器本身上，所需要的只是简单地重新配置 DHCP 服务。在下面的示例中，我们的防火墙 `Host-A` 有两个接口 `eth0`（外部）和 `eth1`（内部，`10.10.10.0/24`）。此配置使用了 ISC DHCP (`http://www.isc.org/`)，它是大多数 Linux 发行版的默认 DHCP 服务器。为了限制响应到内部网络 `eth1`，你需要使用想要监听的接口名称启动 `dhcpd`。例如：

```
/usr/sbin/dhcpd eth1
```

在某些发行版中（如 Red Hat 系统），你也可以将其设为配置文件：

- 1. 用你喜欢的编辑器加载 `/etc/sysconfig/dhcpd` 并设置：

```
DHCPARGS="eth1"
```

其中 `eth1` 是你想要监听的物理接口。如果文件中定义了其他接口，那么你的工作就完成了。

# 这只是主配置文件的一个示例：

```
subnet 10.10.10.0 netmask 255.255.255.0 {

option routers 10.10.10.1;

option subnet-mask 255.255.255.0;

range 10.10.10.100 10.10.10.200;

option time-offset 0; # 标准时间

option domain-name-servers 10.10.10.1;

default-lease-time 3600;

max-lease-time 43200;

}
```

示例配置了 `10.10.10.100-10.10.10.200` 的 DHCP 范围，租约时间为 12 小时。还将默认路由设置为防火墙的内部接口 `10.10.10.1` 以及默认 DNS 服务器 `10.10.10.1`。

# DHCP：外部接口上的两个地址

这是一个非常独特的问题。它发布在邮件列表中，我们认为它奇特到需要在书中提到。尽管如此，该帖子的主题是为防火墙的外部接口分配额外的 DHCP 地址，以便连接他的游戏机。该设备可能需要端口来运行游戏，而从普通 IP 转发这些端口会破坏其他服务。遗憾的是，由于不知道这些端口是什么，很难判断这是否真的是一个无法解决的端口问题，但这并不。最初使用 IP 别名租用第二个 IP 的尝试是不可行的，因为别名设备 (`eth0:1`) 没有 MAC 地址，而这正是末端 DHCP 服务器所寻找的。根据作者，以下是错误的方法：

```
/sbin/dhcpd -t 60 -h -d eth0
```

然而，以下方法不起作用，因为没有 MAC 地址：

```
/sbin/dhcpd -t 60 -h -d eth0:1
```

此时，我们进入了“有多种方法”的领域。我们可以使用 `ebtables`（第 15 章）并对想要获取 DHCP 地址的设备进行 MAC 层处理。然而，事实证明用户客户端可以连同发送 MAC 地址。

```
/sbin/dhcpd -n -t 60 -h -I 00:11:22:33:44:55 eth0:1
```
