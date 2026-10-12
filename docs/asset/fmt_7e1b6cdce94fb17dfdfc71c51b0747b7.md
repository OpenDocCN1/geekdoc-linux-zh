
## siege

**描述** `siege` - 一个 HTTP/HTTPS 压力测试工具。**Siege** 是一个多线程 HTTP 负载测试和基准测试实用。它旨在让 Web 开发人员能够在压力下测量代码的性能。它允许使用配置的并发模拟用户攻击 Web 服务器。这些用户会让 Web 服务器处于“被围攻的状态”。性能指标包括经过时间、总传输数据量、服务器响应时间、事务率、吞吐量、并发数以及返回 OK 的次数。这些指标会在每次运行结束后进行量化并报告。其意义和重要性将在下方讨论。`Siege` 本质上有三种运行模式：回归（当通过轰炸调用时）、互联网模拟和暴力破解。

**用法** `siege [options] siege [options] [url]`

**选项** `http://linux.die.net/man/1/siege`

**示例** `siege -c25 -t1M www.example.com`

**示例** `siege -g www.google.com`

## smurf6

**描述** `thc-ipv6` - THC-IPV6-ATTACK-TOOLKIT - 直接运行不带选项的工具，它们将为你提供帮助并显示命令行选项。

**smurf6** - 使用 icmp echo 响应对目标进行 smurf。echo 请求的目标是未指定的本地所有节点组播地址。

**用法** `smurf6 interface victim-ip [multicast-network-address]`

**示例** 无

**检测提示** 大多数工具可以很容易被 IDS 或专门的检测软件发现。这样做是有意为之，以便更容易检测违规使用。这些工具要么指定了固定的数据包特征，要么通用地嗅探数据包（例如，还会响应发送到不存在的 mac 地址的 icmp6 邻居请求，因此非常容易被检测）。如果你不希望这样，请修改代码。

# t50

描述 `T50` 也是一个多协议数据包注入。

- 特性
- 轰炸
- CIDR 支持
- TCP, UDP, ICMP, IGMPv2, IGMPv3, EGP, DCCP, RSVP, RIPv1, RIPv2, GRE, ESP, AH, EIGR 和 OSPF。
- TCP 选项。
- 高性能。
- 每秒可以发送 1.000.000 个数据包。

用法 `t50 <host> [/CIDR] [options]`

选项 `https://github.com/merces/t50/blob/master/src/usage.c`

选项 `t50 -h`

示例 `t50 VICTIM_IP --flood -S --turbo`

示例 `t50 VICTIM_IP --flood --turbo --dport (80 443) -S --protocol TCP`

## [57] VOIP 压力测试

- `iaxflood`
- `invite flood`

## iaxflood

描述 `IAXFlood` 是一个用于泛洪 Asterisk PBX 使用的 IAX2 协议的工具。

用法 `./iaxflood sourcename destinationname numpackets`

示例 无

## invite flood

描述 SIP INVITE 泛洪 - 上述两种攻击都针对 HTTP；而此这一个是针对 SIP 的 VoIP 泛洪。它利用了 SIP 发起建立过程中正常的时间延迟来使 SIP 服务器过载。由于 SIP 运行在 UDP 之上，来自呼叫者、黑客或僵尸网络的单个数据包就可以在电话开始时启动“拨号”和响铃过程。在日常生活中，我们并不会输入电话号码与听到对方那端的“你好”或语音邮件提示之间的 20 秒延迟感到异样。但当这种延迟在数千个并发连接中相乘时，可能会导致服务器崩溃，并可能为基于 VoIP 的呼叫中心开启更大的混乱之门。此外，预先判断哪些通话是合法的，哪些是 DDoS 的一部分是非常的，特别是如果攻击者足够明足以伪造 UDP 头部中的 IP 地址，或者伪造 SIP 头部使其与相应的 UDP 头部匹配。

用法 无；GUI 工具

选项 无；GUI 工具

示例 无；GUI 工具

## [58] WEB 压力测试

- `thc-ssl-dos`

## thc-ssl-dos

**描述** `thc-ssl-dos` - THC 发布了一个利用 SSL 重协商对给定的 SSL 服务器进行拒绝服务的 DOS 工具。它使用重协商来通过单个 TCP 连接不断地触发（与服务器）新的 SSL 握手。**THC-SSL DOS** 是由一个名为 The Hacker's Choice (THC) 的黑客小组开发的，作为一种概念证明，鼓励厂商修复一个严重的 SSL 漏洞。**THC-SSL-DOS** 与其他“低且慢”攻击一样，仅需少量数据包即可对相当大的服务器造成拒绝服务。它的工作原理是启动常规 SSL 握手，然后立即请求重协商加密密钥，不断重复这种消耗服务器资源的重协商请求，直到所有服务器资源耗尽。

**URL** `www.thc.org/thc-ssl-dos/`

**示例** `/thc-ssl-dos 127.3.133.7 443`

**提示**

平均服务器每秒可以进行 300 次握手。这将需要你笔记本 CPU 的 10-25%

如果使用了 SSL 加速器，请使用多个主机 (SSL-DOS)

要聪明一点

## [59] WLAN 压力测试

- `mdk3`
- `reaver`

## mdk3

**描述** `MDK` 是一个用于无线网络审计的工具。它可以用于对 802.11 网络的各种攻击，包括取消认证、信标攻击和泛洪。

用法 `mdk3 <mode>`

功能：
- 取消认证（将用户从 AP 断开连接）
- 信标攻击（创建伪造 AP）
- 泛洪（用数据包泛洪网络）
- 扫描（发现隐藏网络）
- 破解（破解 WEP/WPA）

选项 `mdk3`

示例 `mdk3`
