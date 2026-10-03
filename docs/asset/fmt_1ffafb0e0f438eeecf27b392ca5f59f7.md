
### OpenBSD 桥接设置

OpenBSD 通用内核包含了配置和过滤桥接的所有代码。除非你编译了不包含桥接代码的自定义内核，否则设置非常简单。

在 OpenBSD 4.7 及更高版本中，`brconfig` 命令不再存在。桥接配置及相关功能已合并到 `ifconfig` 中。如果你运行可以使用 `brconfig` 的 OpenBSD 版本，你运行的是过时的、不支持的配置。请尽快升级到较新版本。

要在命令行上设置具有两个接口的桥接，首先要创建桥接设备。同类设备通常赋予序列 0，因此我们使用以下命令创建桥接设备：

```
$ ifconfig bridge0 create
```

在下一个 `ifconfig` 命令之前，使用 `ifconfig` 检查预期成员（在本例中为 `ep0` 和 `ep1`）已启用但未分配 IP 地址。接下来，通过输入以下配置桥接：

```
$ ifconfig bridge0 add ep0 ep1 blocknonip ep0 blocknonip ep1
```

OpenBSD `ifconfig` 命令本身包含了大量的代码。在示例中，为每个接口使用 `blocknonip` 选项来阻塞非 IP 流量。

除了配置选项外，OpenBSD `ifconfig` 命令还提供自己的过滤选项。`bridge(4)` 和 `ifconfig(8)` 手册提供了更多信息。由于它在以太网层操作，可以使用 `ifconfig` 指定过滤规则，让桥接根据 MAC 地址进行过滤。利用这些过滤能力，还可以让桥接通过标记关键字标记包，以便在你的 PF 规则集中进行后续处理。出于标记目的，一个具有一个成员接口的桥接即可。

为了使配置持久化，请创建或编辑 `/etc/hostname.ep0` 并输入以下行：

```
up
```

对于另一个接口，`/etc/hostname.ep1` 应该包含相同的行：

```
up
```

最后，在 `/etc/hostname.bridge0` 中输入桥接设置：

```
add ep0 add ep1 blocknonip ep0 blocknonip ep1 up
```

现在你的桥接应该已经启动了，你可以继续创建 PF 规则了。

### FreeBSD 上的基础桥接设置

对于 FreeBSD，操作步骤比 OpenBSD 稍微复杂一些。为了使用桥接功能，运行的内核必须包含 `if_bridge` 模块。默认内核配置已编译此模块；在通常情况下，你可以直接创建接口。要将桥接设备编译进内核，请在内核配置文件中添加以下行：

```
device if_bridge
```

你可以通过在 `/etc/loader.conf` 文件中放入以下行在启动时加载该设备：

```
if_bridge_load="YES"
```

输入以下命令创建桥接：

```
$ sudo ifconfig bridge0 create
```

创建 `bridge0` 接口也会创建一组与桥接相关的 `sysctl` 值：

```
$ sudo sysctl net.link.bridge
net.link.bridge.ipfw: 0
net.link.bridge.pfil_member: 1
net.link.bridge.pfil_bridge: 1
net.link.bridge.ipfw_arp: 0
net.link.bridge.pfil_only: 1
```

值得检查这些 `sysctl` 值是否可用。如果可用，则确认桥接已启用。如果不可，请回溯检查哪里出了问题。注意：这些值适用于桥接本身的过滤。你不需要触碰它们，因为成员接口（管道的末端）上的 IP 级过滤是默认开启的。在执行下一个 `ifconfig` 命令之前，检查成员接口（在我们的案例中为 `ep0` 和 `ep1`）已启动但未分配 IP 地址。然后，通过输入以下命令配置桥接：

```
$ sudo ifconfig bridge0 add ep0 ep1
```

要使配置永久生效，将以下行添加到 `/etc/rc.conf`：

```
ifconfig_ep0="up"
ifconfig_ep1="up"
clone_interfaces="bridge0"
ifconfig_bridge0="add ep0 ep1"
```

这意味着你的桥接已启动，你可以继续创建 PF 规则。有关 FreeBSD 的特定信息，请参阅 `if_bridge(4)` 手页。

### NetBSD 上的基础桥接设置

在 NetBSD 上，默认内核配置没有编译桥接支持。你需要通过在内核配置文件中添加以下选项来编译自定义内核。一旦拥有新内核并重启，设置将非常直观。要创建一个包含两个接口的桥接，首先创建桥接设备：

```
$ sudo ifconfig bridge0 create
```

在执行下一个 `ifconfig` 命令之前，使用 `ifconfig` 检查成员接口（在我们的案例中为 `ep0` 和 `ep1`）已启动但未分配 IP 地址。然后，通过以下命令配置桥接：

```
$ sudo ifconfig bridge0 add ep0 ep1
```

接下来，启用 `bridge0` 设备上的过滤：

```
$ sudo pfctl bridge0
```

要使配置永久生效，创建或编辑 `/etc/ifconfig.ep0` 并输入以下行：

```
up
```

对于另一个接口，`/etc/ifconfig.ep1` 应该包含相同的行：

```
up
```

最后，在 `/etc/ifconfig.bridge0` 中输入桥接设置：

```
add ep0 add ep1
```

现在你的桥接应该已经启动，你可以继续创建 PF 过滤器。有关更多信息，请参见 FreeBSD 上的 PF 文档：http://www.netbsd.org/Documentation/network/pf.html。

### 桥接规则集

图 5-3 显示了本章开始的基础规则集的“线缆桥接”版本的 `pf.conf` 文件。如你所见，网络发生了微变化。本地网络中的机器共享一个公共默认网关，该网关不是桥接，但可以放在桥接内部或外部。

```
ext_if = ep0
int_if = ep1
localnet = "192.0.2/24"
webserver = "192.0.2.27"
webports = { http, https }
emailserver = "192.0.2.25"
mail = { smtp, pop3, imap2, imap3, imaps, pop3 }
nameservers = { 192.0.2.221, 192.0.2.223 }
client_out = { ssh, domain, pop3, auth, http, https, 443, cvpserver, 2628, 5999, 8000, 8080 }
udp_ports = { domain, ntp }
icmp_types = { echo, unreach }
set skip on $int_if
block all
pass quick on $ext_if inet proto { tcp, udp } from $localnet to port $udp_ports
pass log on $ext_if inet proto all icmp-type $icmp_types
pass on $ext_if inet proto tcp from $localnet to $client_out
pass on $ext_if inet proto { tcp, udp } to $nameservers port domain
pass on $ext_if proto tcp to $webserver port webports
pass log on $ext_if proto tcp from $emailserver port $email
pass log on $ext_if proto tcp from $emailserver to port smtp
```

可以实现显著复杂的设置。但请记住，虽然重定向可以生效，但你无法在没有 IP 地址的任何接口上运行服务。

#### 处理来自外部的不可路由 IPv4 地址

即使正确配置了网关来处理你自己网络的过滤和潜在的 NAT，你可能发现自己陷入了这种令人讨厌的境地：需要为别人的配置错误买单。

#### 建立全局规则

一种令人沮丧的常见配置错误是允许带有不可路由地址的流量流向互联网。来自不可路由 IPv4 地址的流量在几种拒绝服务 (DoS) 攻击技术中起着作用，因此考虑阻止来自不可路由地址的流量进入你的网络是值得的。

之前提到的概念（指定一组适用于锚点内所有操作的通用标准）在你的配置大到需要一些结构化辅助手段时非常有吸引。例如，“interface”（接口）可以是特定接口进入流量的有用准则，因为流量通常具有某些相似性。例如，看下文：

```
anchor "dmz" on $dmz_if {
    pass in proto { udp } to $nameserver port domain
    pass in proto tcp to $webservers port { www https }
    pass in proto tcp to $mailerver port smtp
    pass in log (all, to pflog1) in proto tcp from $mailerver \
    to any port smtp
}
```

出站（egress）的独立 `ext` 适用于出站接口组：

```
match out proto tcp to port { https } set queue (qweb, qpri) set pri (5,6)
match out proto tcp { udp } to port domain set queue (qdns, qpri) set pri (6,7)
pass out log icmp set queue (q_dns, qpri) set pri (7,6)
pass in log proto tcp to port smtp set rdr-to 127.0.0.1 port spam dequue-and-spam
pass in log proto tcp from <nospamd> to port smtp
pass in log proto tcp from <spam-white> to port smtp
pass out log proto tcp to port smtp
pass log (all) proto { tcp, udp } to port ssh keep state (max-src-conn 15, \
max-src-conn-rate 7/3, overload <bruteforce> flush global)
}
```

如果根据接口亲和性在锚点分组规则，另一种逻辑优化是合并标签以帮助策略路由决策。一个简单但有效的例子如下：

```
anchor "dmz" on $dmz_if {
    pass in proto { udp } to $nameservers port domain tag GOOD
    pass in proto tcp to $webservers port { www https } tag GOOD
    pass in proto tcp to $mailerver port smtp tag GOOD
    pass in log (all, to pflog1) in proto tcp from $mailerver
    to any port smtp tag GOOD
    block log quick! tagged GOOD
}
```

即使这里的示例在锚点内部包含了一个拦截决策，但基于标签信息的拦截或通过的决策并不非得要在锚点内部发生。

在经历了这一轮将锚点作为结构化工具的“旋风”之后，你可能想将整个规则集转换为基于锚点的结构。如果你尝试这样做，可能会发现一些让内部逻辑更清晰的方法。如果某些规则需要是全局的，位于与通用标准绑定的锚点之外，请不要惊讶。你几乎会发现，在你的环境中证明实用的东西与我在这里展示的场景的灵感来源会有所不同。

#### 你的网络有多复杂？——回顾

在本章的开头，我们提出了两个问题：“你的网络有多复杂？”以及“它需要有多复杂？”在本章的各个章节中，我们介绍了许多工具和技术，它们使得使用 PF 和相关工具构建复杂的基础设施成为可能，并在帮助管理这种复杂性的同时让网络管理员保持理性。

如果你负责一个站点，需要在那里应用在本章提到的所有或大部分技术，我理解你的痛苦。另一方面，如果你负责的是一个多样化的网络，那么后续关于流量整形和资源可用性的章节可能对你也有用。

本书的其余部分涉及针对性能和资源可用性优化你的设置，其中一个章节略有偏离并采用了较轻松的语气。在我们深入探讨如何让你的基础设施对特定群体或个人不可用或难以访问之前，下一章专门负责为那些试图滥用你所维护服务的大众——甚至是组织良好的罪犯——让生活变得更加艰难。

### 扭转局面，采取主动防御

![](img/838f49667801fd8460438797800410dd_118_0.png)

在上一章中，你看到可能需要花费大量的精力和来确保即使在实施严格的数据包过滤的情况下，你想要提供的服务也是可用的。现在，由于你的工作配置已经就绪，你很快会注意到某些服务比其他服务更容易吸引不受欢迎的关注。

这里是这样的场景：你有一个带有数据包过滤的网络以匹配站点需求，其中某些服务需要从其他地方访问。不幸的是，当服务可用时，存在有人想利用它们进行某种恶剧的风险。
你的网络几乎肯定会有通过 SSH（安全外壳）的远程登录，以及运行在网络上的 SMTP 邮件——这两者都是极诱人的目标。在本章中，我们将研究让通过 SSH 获取未经授权访问变得困难的方法，然后转向一些更有效的方法来拒绝垃圾邮件发送者使用你的服务器。

#### 击退粗暴之徒

Secure Shell 安全，通常称为 SSH，对于 Unix 管理员来说是一项相当关键的服务。它经常是机器的主界面，也是脚本小子攻击的最爱目标。

#### SSH 暴力破解攻击

如果你运行了一个可以从互联网访问的 SSH 登录服务，你可能已经在认证日志中见过这些记录：

```
Sep 26 03:12:34 sshd[25771]: Failed password for root from 200.72.41 40992 ssh2
Sep 26 03:12:34 sshd[52799]: Failed password for root from 200.72.41 40992 ssh2
Sep 26 03:12:35 sshd[52793]: Received connection from 200.72.41.31: 11: Bye
Sep 26 03:12:44 sshd[29635]: Invalid user admin from 200.72.41.31
Sep 26 03:12:44 sshd[24703]: userauth_reject: invalid user admin
Sep 26 03:12:44 sshd[24703]: Failed password for invalid admin from 200.72.41.31 port 41484 ssh2
Sep 26 03:12:44 sshd[29635]: Failed password for invalid admin from 200.72.41.31 port 41484 ssh2
Sep 26 03:12:45 sshd[24703]: Connection closed by 200.72.41.31
Sep 26 03:13:10 sshd[76635]: Failed password for root from 200.72.41.31 43344 ssh2
Sep 26 03:13:10 sshd[76635]: Failed password for root from 200.72.41.31 43344 ssh2
Sep 26 03:13:10 sshd[11459]: Received connection from 200.72.41.31: 11: Bye
Sep 26 03:13:15 sshd[31357]: Invalid user admin from 200.72.41.31
Sep 26 03:13:15 sshd[10543]: userauth_reject: invalid user admin
Sep 26 03:13:15 sshd[10543]: Failed password for invalid admin from 200.72.41.31 port 43811 ssh2
Sep 26 03:13:15 sshd[31357]: Failed password for invalid admin from 200.72.41.31 port 43811 ssh2
Sep 26 03:13:15 sshd[10543]: Received connection from 200.72.41.31: 11: Bye
Sep 26 03:13:25 sshd[6526]: Connection closed by 200.72.41.31
```
