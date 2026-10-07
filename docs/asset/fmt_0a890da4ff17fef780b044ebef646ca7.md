
ipeye 扫描器（http://ntsecurity.org/toolbox/ipeye）是一款允许用户扫描远程主机的软件。从意义上说，ipeye 类似于 Nmap（尽管功能没有那么丰富），运行在 Windows 系统上。Snort 规则 ID 622 检测网络上何时在使用 ipeye 扫描器：

```
alert tcp $EXTERNAL_NET any $HOME_NET (msg:"SCAN ipeye SYN scan"
flags:S; seq:1958810375; reference:arachnids,236; classype:attempted-recon;
sid:622; psad_id:100197; psad_dl:2);
```

上述 Snort 规则不需要使用任何应用层测试；相反检测 TCP 头部中是否设置了 SYN 标志和特定的 TCP 序列号 1958810375（这些测试如上方所示）。

使用 psad 检测 ipeye 扫描器的实例，必须在 iptables 命令行上启用 `--log-tcp-sequence` 选项，以便数据包命中 LOG 规则时 iptables 在日志中包含序列号。每个包含 SYN 标志和序列号 1958810375（下方加粗处）的 iptables 日志消息都将触发 psad 中的匹配：

```
Jul 11 20:28:21 iptablesfw: DROP IN=eth0 OUT= MAC=00:13:46:3a:41:4b
00:0a:cc:28:54:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=60 TOS=0x10
PREC=0x00 TTL=64 ID=3970 PROTO=TCP SPT=45664 DPT=15324
Seq=1958810375 ACK=0 WINDOW=5840 RES=0x00
SYN URG=0
```

任何包含 SYN 标志和序列号 `1958810375`（下方加粗处）的 iptables 日志消息都会触发 psad 的匹配：

```
Jul 11 20:28:21 iptablesfw: DROP IN=eth0 OUT= MAC=00:13:46:3a:41:4b
00:0a:cc:28:54:08:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=60 TOS=0x10
PREC=0x00 TTL=64 ID=3970 PROTO=TCP SPT=45664 DPT=15324
Seq=1958810375 ACK=0 WINDOW=5840 RES=0x00
SYN URG=0
```

通过 psad，带有以下词的 syslog 消息出现在 `/var/log/messages`，表示 psad 已检测到 ipeye：

```
Jul 11 20:28:21 iptables src: 192.168.10.3 match: "SCAN ipeye SYN scan" (sid:622)
```

## 检测 LAND 攻击

LAND 攻击是一种针对 Windows 系统的拒绝服务攻击，它构造一个源和目标地址相同的数据包。在 Snort 规则集中，检测 LAND 攻击的关键是 SYN 数据包。以下行代表了由 LAND 攻击生成的 iptables 日志，随后是对应的 psad syslog：

```
Jul 11 20:31:33 iptables kernel: DROP IN=eth0 OUT= MAC=00:13:d3:b6:e4:00:13:c:62:40:08 SRC=192.168.10.30 DST=192.168.10.11 LEN=60 TOS=0x10
PREC=0x00 TTL=63 ID=43679 PROTO=TCP SPT=52728 DPT=15324
Seq=1958810375 ACK=0 WINDOW=5840 RES=0x00
SYN URG=0
Jul 11 20:31:38 iptablesfw src: 192.168.10.3 match: "BAD-TRAFFIC SRC/DST" (sid:527)
```

LAND 攻击是一种经典的攻击。由于 SRC 和 DST 字段总是包含在内，因此构建 psad 来检测它不需要特殊的命令行参数。然而，为了减少误报，psad 通过检查 SRC 和 DST 是否相同来引入测试：

```
alert tcp $EXTERNAL_NET any -> $HOME_NET (msg:"BAD-TRAFFIC data in TCP SYN packet"; flags:S; reference:url://www.cert.org/incident_notes/IN-09-07.html; classype:misc-activity; sid:207; _psad_id:100000; _psad_dl:;)
```

## 检测 TCP 端口 0

虽然法的 TCP 连接不通过端口 0 传输，但没有什么阻止目标端口 0 的 TCP 数据包。事实上，Nmap 在 3.50 版本中获得了扫描端口 0 的功能。原始 Snort 规则 ID 524（注意加粗的端口值）检测发送到端口 0 的包，UDP 端口 0 也有类似的规则：

```
alert tcp $EXTERNAL_net <> $HOME_net (msg:"BAD-TRAFFIC port 0 traffic"; classype:misc-activity; sid:524; psad_id:100101; psad_dl:2);
```

包含 DPT 字段中值的 iptables 日志消息将触发 psad 中的此签名，如加粗所示包含 `DPT=0`：

```
Jul 11 22:02:07 iptables kernel: DROP IN=eth0 OUT= MAC=00:13:d3:b6:e4:00:13:c:62:40:08 SRC=192.168.10.30 DST=192.168.10.11 LEN=44 TOS=0x00
PREC=0x00 TTL=41 ID=43679 PROTO=TCP SPT=29211 DPT=0 WINDOW=3072 RES=0x00
SYN URG=
Jul 11 22:01:22 iptables psad src: 192.168.10.31 match: "BAD-TRAFFIC port 0 traffic" (sid:524) tcp port: 0
```

### 检测零 TTL 流量

与 TCP 和 UDP 端口 0 一样，在链路上可能会放置一个 TTL 值为 0 的数据包。虽然路由 IP 数据包的设备不应转发此类数据包，但系统可以向任何通过链路层设备（如交换机或网接器）连接的其它系统发送此类数据包。

Snort 规则 ID 1321 用于检测 TTL 值设置为 `0`（加粗部分）的 IP 数据包，下方会显示相应的 iptables 消息，如下所示：

```
alert $EXTERNAL_NET any -> $HOME_NET any msg="BAD-TRAFFIC 0 ttl"; ttl:0;
reference:url,support.microsoft.com/default.aspx?scid=kb-EN-US;q13268;
reference:url,www.isi.edu/in-notes/rfc1122.txt; classype:masc-activity;
id:13221; psad_id:100104; psad_dl:2;
```

包含 TTL 字段值的 iptables 日志消息将触发此签名，该数据包包含 TTL=0，示下所示：

```
Jul 14 15:33:28 iptables kernel: In=eth1 Out= MAC=00:13:46:3a:41:4b:00:13:46
c20:64:48:00 SRC=192.168.10.1 DST=192.168.10.1 LEN=104 TOS=00 PREC=000
TTL=0 ID=DF PROTO=TCP TYPE=6 CODE=0 SEQ=150142
Jul 14 15:33:31 iptables pfwd src: 192.168.10.3 signature match:
"BAD-TRAFFIC 0 ttl" (id: 1321)
```

### 检测 Naptha 拒绝服务攻击

Naptha 拒绝服务工具旨在向目标 TCP 栈泛洪大量 SYN 数据包，使系统无法合法地处理这些请求。根据 Snort 规则 ID 275，Naptha 工具创建的数据包包含 IP ID 值 413 以及 TCP 序列号 6060842，下文所示：

```
alert $EXTERNAL_NET any <> $HOME_NET msg="NAPHA"; flags=5;
id:413; seq=6060842; reference:bugtraq,2022; reference:cve,2000-1039;
reference:url,razor.bindview.com/publish/advisory/adv_NAPTHA.html;
reference:url,www.cert.org/advisory/CA-2000-21.html;
reference:url,www.microsoft.com/security/bulletin/M005-091.msx;
classtype:attempted-dos; sid:275; psad_id:1001111; psad_dl:2;
```

接下来的 iptables 日志消息触发了通过的 Naptha 规则（注意冒号处的 IP ID 值为 413，冒号处的 TCP 序列号为 6060842，以及冒号处的 SYN 标志已设置）：

```
Jul 20 28:21:28 iptables pfwd kernel: DROP In=eth1 Out= MAC=00:13:46:3a:41:4b:00
a00:c2:64:52:48:00 SRC=192.168.10.3 DST=192.168.10.1 LEN=60 TOS=01
PREC=000 TTL=64 ID=413 DF PROTO=TCP SPT=45664 DST=13504
SEQ=6060842 ACK=0 WINDOW=5480 RES=0x0 SYN URG=0
Jul 14 15:35:26 iptables pfwd src: 192.168.10.3 signature match: "DOS
NAPTHA" (sid: 275) tcp port: 10354
```

### 检测源路由尝试

源路由是 IPv4 协议支持的一种技术，攻击者借此尝试将数据包路由通过原本无法访问的网络。源路由选项包含在 IP 头部选项中，Snort 规则 ID 500 使用 IP 头部测试器检测松散源路由尝试（如下所示）：

```
alert ip $EXTERNAL net -> $HOME any msg:"MISC source route lssr"; ipsr: reference:achninds,a18; reference:bugtraq,646; reference:cue; 1999-0909; classtype:bad-unknown; sid:500;
```

## 使用 p0f 进行被动操作系统指纹识别

由于 psad 倾向于使用被动检测而非主动生成网络流量，因此不使用操作系统指纹识别。我们将从严格被动手段可以实现的角度继续讨论。

最广为人知的成功的被动操作系统实现之一是 p0f，它由 Michal Zalewski（http://lcamt.coredup.com）开发。事实证明，如果你能够拦截 TCP 数据包数据（无论是因为你访问了数据包流经的网络网段，还是因为数据包指向或源自你控制的系统），你就可以收集许多对操作系统指纹识别非常有用的信息。TCP SYN 和 SYN/ACK 数据包包含的信息最多，因为它们定义了 TCP 连接应当遵循的参数，并在与某些端协商这些参数时具有区分度。

在 p0f 的操作系统指纹识别中，通过检查来自系统的 TCP SYN 或 SYN/ACK 数据包的 IP 和 TCP 头部中的几个字段，可以识别远程操作系统。这些字段包括：

- 分片位 (Fragmentation bit)
- 初始 TTL 值
- 最大分段大小 (MSS)
- 整体 SYN 数据包大小
- TCP 选项值和顺序
- TCP 窗口大小

p0f 使用自定义签名格式来存储每个操作系统上述的特定参数。例如，这里是一个运行 2.5 内核的 Linux 系统的指纹（该签名需要更新，因为它实际上指的是稳定的 2.6 内核而非 2.5 开发内核，且指纹中也为 2.4 内核留出了空间）：

```
53:64:1:60M*,S,T,N,W::Linux:2.5 (sometimes 2.4)(1)
```

p0f 签名格式具有由冒号（:）分隔的字段：

- 从左到右读取，第一个字段 `53` 指 TCP 窗口大小。此字段指示 p0f 寻找窗口大小为分段大小 (MSS) 三倍的 TCP SYN 数据包。
- 第二字段 `64` 指 IP 头部中的 TTL；由于 TTL 值在穿越互联网时会减少，此字段指的是初始 TTL 值，p0f 允许数据包中的实际 TTL 值更小。
- 第三字段 `1` 指 IP 头部中的不分片 (DF) 位。因为签名在该字段中的值为 1，它在寻找 DF 位被设置的状态。
- 第四字段 `60` 是整体数据包大小。在这个示例中，签名要求大小为 60 字节。
- 第五字段 `S,T,N,W` 描述 TCP 头部的选项部分。在这个示例中，签名寻找任何 MSS，随后是确认 (S)、时间戳 (T) 和窗口缩放因子 (W)。

关于被动操作系统指纹识别的全面处理可见 Michal Zalewski 的《Silence on the Wire》(2005)。

### 使用 psid 模拟 p0f

为了在包头部上运行指纹算法，p0f 使用 libcap 嗅听线路数据包。相比之下，psid 包含了基于 iptables 消息作为输入来实现操作系统指纹识别的代码。只要使用了 `--tcp-options` 参数来解码，p0f 检查的每个头部值（TCP 窗口大小、TTL 值、选项等）在 iptables 消息中都是可用的。这里显示了一个包含 TCP 头部选项部分的日志消息：

```
Jul 14 22:03 iptables kernel: DROP IN=eth0 OUT= MAC=00:13:32:41:4b:00:00:28:42:5a:08:00 SRC=192.168.1.10 DST=192.168.1.10 LEN=60 TOS=0x10 PRE=0000 TTL=64 ID=37356 PROTO=TCP SPT=5442 DST=23 WINDOW=5840 RES=0x00
```

#### 从 iptables 解码 TCP 选项

使用上述日志消息实现 p0f 指纹识别的唯一技巧是对 OPT 十六进制转储进行解码，以便与签名进行匹配。OPT 字符串代表 TCP 头部选项部分的解码结果，通过逐个检查该字符串并与 TCP 头部中的可能值（http://www.iana.org/assignments/tcp-parameters）进行匹配，SYN 数据包中使用的选项变得清晰。除了每个字节宽的列表结束（End of List）和无操作（NOP）选项外，每个选项都由类型指定，后跟长度，并以值结束。这被称为类型-长度-值（TLV）编码。

例如，上述十六进制的开头 `02040584` 解码为 `02` 最大分段大小，`04` 长度（包含类型字节），`05B4` 1460（十进制值）。对整个十六进制进行类似的分析可得出结论：

- 最大分段大小为 1460
- NOP
- 确认 OK
- 时间戳为 1833790
- 窗口缩放因子为 2

这组选项匹配 `S64:1:60:M*,S,T,N,W::Linux:2.5 (sometimes 2.4)`，这是正确的，因为运行 2.6 内核的机器连接 TCP 端口 23 是开发系列。通过将 SYN 数据包中的 TCP 选项与签名匹配，通常可以识别探测你 iptables 的远程操作系统。然而，此功能仅通过使用 `--tcp-options` 实现，因此强烈建议你在向 iptables 添加 LOG 规则时使用此选项。

## DShield 报告

DShield 分布式入侵检测系统（http://www.dshield.org）是收集和报告安全数据的重要工具。它作为各种软件（包括入侵检测系统、路由器和防火墙）提供的数据中心存储器。许多产品可以通过电子邮件或网络界面向 DShield 提交安全警报。可以向 DShield 提交事件数据的程序完整列表可以在 http://www.dshield.org/howto.php 找到。

DShield 数据库被设计为一个全局仓库；任何人都可以它来了解哪个 IP 地址正在攻击最大数量的目标、哪些协议经常被攻击等。提交到 DShield 的事件数据形状非常重要。防火墙或入侵检测系统记录的某些事件数据不适合包含在 DShield 中，因为它们没有开放互联网上的恶意流量。这些数据可能包括内部网络（RFC 1918 空间）上主机之间的攻击，或刻意的端口扫描（grc.com）。

psad 自动提交数据到 DShield 是支持的。一旦在 DShield 网站注册，psad 会每六小时发送一次数据提交，但这可以通过 `psad.conf` 中的 `ALERT_INTERVAL` 变量进行控制。除非安全策略明确禁止与 DShield 的通信，否则 psad 强烈建议启用它。

### DShield 格式

尽管 DShield 接受来自各种软件的原始输出，但为了减少 DShield 服务器的处理压力，以特定格式提交数据是有帮助的。这种格式要求每个安全事件单独占一行，使用制表符分隔以下字段：

- 作者（DShield 用户 ID，如果你未在 DShield 注册则为 0）
- 计数
- 日期（格式为 YYYY-MM-DD HH:MM:SS，Z 为时区）
- 协议（数字或文本形式，如 TCP）
- 源 IP 地址
- 源端口（或 ICMP 类型）
