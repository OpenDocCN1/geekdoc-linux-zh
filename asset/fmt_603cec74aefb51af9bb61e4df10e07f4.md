
Jul 7 22:33:42 fw:[1] DRP SID2001842 IN=eth0 OUT=eth0 SRC=192.168.10.4 DST=234.50.X LEN=38 TOS=00 PRE=0x00 TTL=62 ID=36070 DF=UDP SPT=16408 PT=53 LEN=18

这次，日志前缀发生了变化。不再是
- `[1] SID2001842`
而是现在
- `[1] DRP SID2001842`

`DRP` 字符串表示 `iptables` 在记录的同时丢弃了 DNS 请求。通过再次在外部防火墙上运行数据包跟踪并发现请求从未通过，确认了这一点。

注意：`snort` 使用 `DRP` 和 `REJ` 是因为 `iptables LOG` 匹配前缀有 29 个字符的限制。你将在第 11 章找到关于 `--ipt-drop` 和 `--ipt-reject` 选项背后运行的更多信息。

## 设置白名单和黑名单

任何基于应用层数据阻止网络通信的软件也应该能够根据白名单从任何阻止操作中排除某些网络或 IP 地址。同时，它应该能够通过黑名单强制丢弃来自某些网络或 IP 地址的所有数据包。

`snort` 支持白名单和黑名单，在 `/etc/fsnort/fsnort.conf` 中有 `WHITELIST` 和 `BLACKLIST` 变量。例如，为了确保 `snort` 永远不对源自或指向 Web 服务器（图 1-2 中的 IP 地址 `192.168.10.3`）的通信采取行动，并丢弃所有来自 IP 地址 `192.168.10.200` 的包，请在 `fswnort.conf` 中包含以下行：

| WHITELIST | 192.168.10.3 |
| BLACKLIST | 192.168.10.200 |

当你使用 `snort` 构建 `fsnort.sh` 脚本时，会添加两个新部分：

```bash
########## Add/network WHITELIST rules ##########

$IPTABLES -A FWSNORT_FORWARD -s 192.168.10.3 -j RETURN

$IPTABLES -A FWSNORT_FORWARD -d 192.168.10.3 -j RETURN

$IPTABLES -A FWSNORT_INPUT -s 192.168.10.3 -j RETURN

$IPTABLES -A FWSNORT_OUTPUT -d 192.168.10.3 -j RETURN

########## Add/network BLACKLIST rules ##########

$IPTABLES -A FWSNORT_FORWARD -s 192.168.10.200 -j DROP

$IPTABLES -A FWSNORT_FORWARD -d 192.168.10.200 -j DROP

$IPTABLES -A FWSNORT_INPUT -s 192.168.10.200 -j DROP

$IPTABLES -A FWSNORT_OUTPUT -d 192.168.10.200 -j DROP
```

在每个 `fsnort` 链中使用 `RETURN` 目标可以尽早地短路特征比较，以尽量减少用于深度数据包检测的 CPU 资源；这些规则已经添加了。同样，黑名单规则的 `DROP` 目标在执行任何额外处理之前在底层匹配数据包。

通过内置的 `FORWARD` 链和 `fsnort` 的数据包流总结见图 10-1。

> 该 IP 地址位于内部网络，但有时某些系统作为内部网络的专用资源运行，不应与外部网络通信。在这种情况下，黑名单规则可以强制与外部网络的零通信。另一个使用黑名单规则有意义的情况是，如果内部系统被入侵，在在修复之前必须严重限制其通信。

![](img/84e6ec42d170b9df6cf29b40151f3d15_213_0.png)

图 10-1：通过 FORWARD 链和 fwsnort 链的路径

# 结语

`Snort` 社区为检测网络攻击的有效语言指明了方向，因此 `fwsnort` 使用 `Snort` 签名集作为其攻击描述的源是合逻辑的。但是，`iptables` 是一个防火墙，而防火墙的核心在于控制。考虑这样一种场景：在您运行在 Linux 系统上的某个任务关键型服务器软件中发现了一个漏洞。在安排维护窗口对该漏洞进行补丁之前，系统将容易受到攻击。通过利用 `Snort` 社区的力量，一旦开发并发布了签名，`fwsnort` 就可以告诉您的 Linux 内核如何在看似利用该漏洞的数据包造成危害之前将其丢弃它们。

尽管 `fwsnort` 可以构建 `iptables` 规则集来丢弃数据包，但这种响应并不能动态地针对恶意 IP 地址实现持久阻塞规则——这需要一个用户态进程。我们将在第 11 章中看到，`fwsnort` 结合 `psad` 可以为应用层攻击构建基于超时阻塞规则。

# 结合 PSAD 和 FWSNORT

到目前为止，我们已经分别涵盖了 `fsnort` 和 `psad` 的操作和理论方面，但尚未将这两个程序结合。尽管 `psad` 提供了检测、告警和自动响应能力，但其检测引擎的有效性从根本上受到 `iptables` 日志格式特征的限制。`fsnort` 提供了更好的攻击检测，包括对应用层攻击的检测。由于 `iptables` 始终处于网络流量的链路上，`fsnort` 可以（可选地）防止恶意数据包到达其目标。

然而，由于源自 `fsnort` 的 `iptables` 策略完全在 Linux 内核中运行，它无法执行通常通过用户态应用程序可以实现的各种告警功能。我们需要一种机制，将 `fsnort` 的签名检测过程与 `psad` 的能力结合，包括主机查询、反向 DNS 查询、发送电子邮件告警、将危险级别与恶意 IP 地址关联以及向 DShield 通信攻击信息。

> ¹ 这假设运行的系统没有从交换机的镜像端口或类似机制接收数据包数据。这通常是一个良好的假设，因为 `iptables` 设计用于针对目标真实系统的实时数据包执行安全策略；对于被动收集的数据包执行策略意义不大。

在本章中，我们将讨论如何通过使用 `psad` 和 `fwsnort` 相互加强来提高两者的有效性。本章最后将讨论如何开发检测 Metasploit 更新的签名，以及如何同时使用 `fwsnort` 和 `psad` 来干扰此类攻击。

# 将 fwsnort 检测关联到 psad 操作

正如第 10 章所述，当 `fwsnort` 检测到攻击时，它会生成一条 `iptables` 日志消息。该消息包含一个日志前缀，告知用户触发日志消息的特定 `Snort` 规则 ID、`fwsnort` 链中的规则编号，以及相应的数据包是否属于已建立的 TCP 会话的一部分。

让我们看看 `fwsnort` 和 `psad` 如何处理针对 MediaWiki 软件的攻击。

# WEB-PHP Setup.php 访问攻击

`Snort` ID `2281` 旨在检测利用 MediaWiki 软件中原始有效漏洞的尝试（该软件最初设计用于为 Wikipedia 服务；参见 http://www.wikipedia.org）。该漏洞由 Bugtra ID `9057` ，并被 `Snort` ID `2281` 标记为 WEB-PHP Setup.php 访问攻击。该漏洞的成功利用可能导致在接收到 HTTP 请求中特殊构造 URI 参数后，在目标系统上执行未经授权的远程代码。我们将模拟一次针对内部 Web 服务器（图 1-2 中的主机 `webserver`）的 WEB-PHP Setup.php 访问漏洞攻击。我们假设默认 `iptables` 策略（由 `iptables` 脚本构建）已部署在 `iptables` 系统上，并且模拟攻击从 `ext_scanner`（IP 地址 `144.202.X.X`）发出。

首先，我们验证可以使用基于的 Web 浏览器通过 `iptables` 防火墙从 `ext_scanner` 系统连接到 `webserver`。（Web 服务器已配置为在接收到 `index.php` 文件的有效请求时显示字符串 "Internal webserver; happy browsing"。）

```
[ext_scanner]$ lynx http://71.157.X.X
Internal webserver: happy browsing
```

在部署 `iptables` 之前演示了连通性后，我们将使用 `fwsnort` 或 `psad` 模拟攻击，以便知道预期返回的结果。首先是 `Snort` 规则 ID `2281`，旨在检测由 Bugtra `9057` 标记的漏洞：

```
alert $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS (msg:"WEB-PHP Setup.php"; flow:to_server,established;uricont==/Setup.php"; nocase; reference:bugtra,9057; classype:web-application-activity; sid:2281; rev:2);
```

> 访问 http://www.securityfocus.com/bid/9057/discuss 获取更多关于此漏洞的信息。

除了字符串 `/Setup.php` 之外，上述规则不关心从 Web 服务器请求的 URI 参数的具体细节（这些可能有所不同）。由于 OCR 此处损坏，无法使用 `/Setup.php` 字符串。（注：此处原文包含大量 OCR 错误和重复，已按要求逻辑处理）。

总体扫描开始：2007年7月19日23:48:18
总邮件告报：2
完整 TCP 范围：[80]
Syslog 主机：iptablesfw
全局统计链：接口 TCP: UDP: ICMP:
FORWARD eth0 2 0

+ [+] TCP 签名：
"WEB-PHP Setup, php access"
目的端口: 80
flags: ACK PSH
content: "/Setup.php"
sid: 2281
chain: FSNORT_FORWARD_ESTAB
packets: 1
classtype: web-application-activity
reference: (bugtraq) http://www.securityfocus.com/bid/9057

上述 `psad` 邮件警报看起来相当正常，包含了所有标准信息，例如时间戳、数据包计数、TCP 标志和端口。然而，此警报中的几条信息值得特别关注。

## TCP 标志

`psad` 报告了生成 `iptables` 日志消息的 TCP 数据包中存在的所有标志位。在 WEB-PHP Setup.php 访问的情况下，触发 `fsnort` 策略生成日志消息的特定 TCP 数据包是一个已建立 TCP 会话的一部分，且 ACK 和 PSH 标志被报告为 ❶。前缀 `[1] SID2281 ESTAB` ❷ 也表示该数据包是由一个使用状态匹配来跟踪已建立 TCP 连接的 `fsnort` 链记录的，因此攻击者无法通过伪造来自任何源地址且包含 `/Setup.php` 字符串的 TCP 数据包来强制 `fsnort` 生成日志消息。

## Report应用层内容

WEB-PHP Setup.php 访问的 `psad` 警报中最感兴趣的部分从上面的 ❶ 开始。这表明 `psad` 注意到了字符串 `[1] SID2281 ESTAB`，并将其映射到相应的 `Snort` 规则。由于 `psad` 在内存中维护了所有 `Snort` 类类型、消息字段和内容字符串的构想，它推断出偏移数据包对应 `web-application-activity` 类中的 WEB-PHP Setup.php 访问，并且必须包含字符串 `/Setup.php`。

`iptables` 本身没有通过 `LOG` 机制报告数据包的实际内容，而且正如第 10 章所述，由于前缀字符串长度限制为 29 个字符，在日志前缀中放置内容字符串通常是不可行的。在 syslog 消息中包含二进制数据包数据也不是一个好主意。

## Snort 规则 ID、消息和引用信息

最后，`psad` 报告了 `Snort` 规则 ID（在此例中为 2281）、所属的类类型（web-application-activity）以及消息字段（WEB-PHP Setup.php access）。还包括一个 Bugtrack，它可以为作为管理员的你提供价值信息，帮助你调查攻击性质，并确定成功的利用对你的网络安全态势意味着什么。这些引用信息包含在原始 `Snort` 规则中，并由 `psad` 缓存用于报告，正如你在 `psad` 邮件警报看到的那样。

## 重新回顾主动响应（Active Response）

在第 8 章和第 10 章中，我们了移除通常限制 `psad` 和 `fsnort` 仅进行被动检测操作的枷锁的影响，并将其重新配置为主动响应攻击。在本节中，我们将继续讨论主动响应，但现在我们将从同时利用 `psad` 和 `fsnort` 响应能力的角度来看这一主题。

## psad 对比 fsnort

尽管在检测到攻击时，`psad` 可以针对攻击者实例化基于超时的 `iptables` 规则，但它本身无法切断连接或阻止匹配应用层签名的初始数据包被转发。相反，`fsnort` 的 `DROP` 或 `REJECT` 目标阻止单个恶意数据包和会话，但 `fsnort` 无法构建可以长时间阻止攻击者的新 `iptables` 规则。

考虑到每个工具的优势，如果能将这两种风格结合起来将非常有益。毕竟，`fsnort` 非常擅长检测并停止包含在 TCP 会话中的特定攻击，但如果没有 `psad` 来管理持久阻塞规则，攻击者就可以自由地对同一目标尝试任何利用方法。检测到第一次尝试可能被认为是相当幸运的；随后的尝试可能完全无法被检测到，因此持久的阻塞规则可能是重要的。如果攻击者拥有针对另一个与第一次攻击无关且没有签名的漏洞的额外利用方法，这一点尤为真实。此外，如果攻击者使用 Tor 匿名网络（http://tor.eff.org）对 TCP 服务发起攻击，拦截单个 IP 地址是无用的，因为每次攻击看起来都来自不同的出口节点（Tor 为每个 TCP 会话随机选择节点）。

虽然第 9 章提到过，但让我在此再次强调：了解主动响应机制的狡猾攻击者可能会试图颠覆它，以使其反过来对付目标网络。此外，如果攻击者控制了多个用于发起攻击的主机（这在地下世界中是常见现象，单个人可以控制许多主机以形成僵尸网络），攻击者可以从尚未用于攻击目标的主机上发起新攻击。网络防御者和攻击者之间始终存在军备竞赛，如果他们能够抵御进攻，应该被认为武装非常精良。

## 限制 psad 响应仅针对 fsnort 检测到的攻击

根据第 194 页“Fsnort 检测到 psad 操作”中包含的信息，我们已经知道 `psad` 可以为 `fsnort` 生成的日志消息发送警报。由此推断，`psad` 可以通过在 `/etc/psad/config` 文件中将 `ENABLE_AUTO_IDS` 设置为 `Y` 来响应 `fsnort` 日志消息设置阻塞规则。

如果 `fsnort` 检测到的攻击使 `psad` 为攻击者分配的等级高于 `AUTO_IDS_DANGER_LEVEL` 设置的值，`psad` 将针对攻击者的 IP 地址启动全局的 `DROP` 规则。然而，`psad` 的危险等级不仅是因为 `fsnort` 记录攻击而分配的；专用端口扫描和后门探测也被分配了危险等级。

正如第 8 章讨论的，对扫描和探测（易于伪造）启用 `psad` 响应是风险行为。理想情况下，我们只想对那些必须涉及已建立的 TCP 连接上的应用层数据的攻击做出响应，而不对其他类型的攻击采取任何行动。

`AUTO_BLOCK_REGEX` 包含一个正则表达式，强制 `psad` 仅在相应的 `iptables` 日志消息匹配该表达式时执行阻塞操作。默认，`AUTO_BLOCK_REGEX` 的值为字符串 `ESTAB`。要启用此功能，必须在 `psad` 配置文件中将 `AUTO_BLOCK_REGEX` 设置为 `Y`。注意：如果你打算允许易伪造的流量，应保持 `AUTO_BLOCK_REGEX` 为空。

## 结合 psad 和 fwsnort

现在我们重新回到 WEB-PHP Setup.php 访问示例，但这次我们使用了 `psad` 和 `fwsnort` 的响应机制。首先，我们配置 `fsnort` 在恶意数据包到达 Web 服务器之前将其丢弃。

```
iptablesfw # tcpdump -l -n 71.157.X.X: 563660994:653660994(0)
13:32:24.839585 142.202.X.59651 71.157.X.X: win 5840 1460 sockOK,timest 323999966 0,nop,wscale 2
13:32:24.84177 71.157.X.X: 142.202.X.59651: 612312505(6) ack 635605995 win 5792 1460 sockOK,timest 2721556999,nop,
wscale 2
13:32:24.868471 142.202.X.59651 71.157.X.X: ack win 1 1460,nop,timest 3239996973 2721556939
13:32:24.892585 142.202.X.59659 71.157.X.X: P 1:229(228) ack win 1 1460,nop,timest 3239996939 2721556939
13:32:25.097233 142.202.X.59651 71.157.X.X: P 1:229(228) ack win 1 1460,nop,timest 3239996939 2721556939
13:32:25.525235 142.202.X.59651 71.157.X.X: P 1:229(228) ack win 1 1460,nop,timest 3239998945 2721556939
13:32:26.464527 142.202.X.59651 71.157.X.X: P 1:229(228) ack win 1 1460,nop,timest 3234000073 2721556939
```

这涵盖了 `fwsnort` 中的 `DROP` 响应，但同时也已传递以实例化一组针对攻击者的阻塞规则。如果我们现在再次尝试从攻击系统上的 Web 服务器获取 `index.html` 页面，面对的是一片死寂：

```
[ext_scanner $#] lynx http://71.157.X.X
```
