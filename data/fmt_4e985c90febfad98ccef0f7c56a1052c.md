
`config ppp0`

你应该会得到像列表 8-16 所示的内容（当然，我更改了我的 IP 地址）。

# 列表 8-16：你的动态 IP 地址

```
ppp0 Link encap:Point-Point Protocol

inet addr:192.168.15.10 P-t P:101 Mask:255.255.255.0

UP POINTTOPOINT RUNNING MTU:1500 Metric:1

RX packets:1757 errors:0 dropped:0 overflows:0

TX packets:2080 errors:0 dropped:0 overflows:0
```

你想使用内部地址并让外部世界看到你，所以，请记住它。输入初始的全局拒绝命令：

```
/sbin/ipfwadm -I -p deny

/sbin/ipfwadm -O -p deny

/sbin/ipfwadm -F -p deny
```

清理掉可能从上次设置中留下的任何规则是一个良好的习惯。即使这是第一次设置防火墙规则，也请通过输入以下命令刷新所有三条规则：

```
ipfwadm -I -f

ipfwadm -O -f

ipfwadm -F -f
```

接下来，你需要添加规则来防止 IP 欺骗。这种做法是指某试图通过伪造他们的 IP 数据包以包含你的网络地址（默认地址）来获取你系统的访问。早期，路由器没有考虑这种可能性，很容易被欺骗认为这些数据包是它们网络的一部分。这是一个巨大的安全漏洞，并允许访问所谓的受保护网络。输入以下命令（注意，`192.168.1.0/24` 语法是 `192.168.1.0/255.255.255.0` 的简写）：

```bash
ipwaf -I a deny -V 192.168.15.10 -S 192.168.1.0/24 -D 0.0.0.0/0

ipwaf -I a deny -V 192.168.15.10 -S 192.168.15.10 -D 0.0.0.0/0
```

这些命令指定了任何通过外部 PPP 接口发出的、带有你的本地网络地址或通用地址（`0.0.0.0`）的 IP 数据包都应被直接拒绝。注意，如果在这里使用拒绝规则，攻击者将收到 ICMP 数据包，告知他们遇到了某些情况。
现在，设置允许你的本地网络无限内部使用的规则：

```bash
ipwaf -I a accept -V 192.168.1.1 -S 0.0.0.0/0 -D 0.0.0.0/0

ipwaf -0 a accept -V 192.168.1.1 -S 0.0.0.0/0 -D 0.0.0.0/0
```

配置你的防火墙允许你的本地网络访问互联网：

```bash
ipwaf -0 a accept -P tcp -S 192.168.15.10 -D 0.0.0.0/0 smtp pop-3 telnet www ftp

ipwaf -I a accept -P tcp -k -S 0.0.0.0/0 smtp pop-3 telnet www ftp -D 192.168.15.10

ipwaf -0 a accept -P tcp -S 192.168.15.10 -D 0.0.0.0/0 ftp-data

ipwaf -I a accept -P tcp -S 0.0.0.0/0 ftp-data

ip92.168.15.10

10 -D 0.0.0/0 domain

ipwaf -I a accept -P udp -S 0.0.0/0 domain -192.168.15.10/24
```

前两条命令设置了发出的 TCP 数据包，用于 `smtp`（电子邮件）、`telnet`、`FTP` 和 `www`。接下来的四条命令用于发出的 TCP 和 UDP 数据包。前两条允许返回的 TCP 数据包用于 `smtp`、`pop3`（电子邮件）、`telnet` 和 `www`。后两条用于第二个通道（数据）域名查找（`DNS`）。其他服务如 `gopher` 可以包含——可以通过 `man` 页、`HOWTO` 文档以及 `/etc/services` 文件获取更多信息。

注意，TCP 连接的入站 (`-k`) 规则设置了标志位。此选项允许带有 `ACK` 标志的 TCP 数据包。基本上，它只允许你发起的 TCP 数据包。例如，当你启动 `Telnet` 会话时，你发送的第一个包带有 `SYN` 标志，而 `Telnet` 服务器返回 `ACK` 作为响应。

好了，就这样。你有一个防火墙了！你的系统是安全的，你拥有大量的互联网访问。在接下来的两个章节中，我将向你展示如何在此基础上进行构建。你构建的 `Linux` 服务器是更复杂强大的系统的基础。看看你刚刚用 `ipfwadm` 函数设置的规则。

> 我喜欢定义一些别名来简化防火墙定义过程。
你可能会发现以下列表有用（我确定你会发现更多）：

```bash
alias ip='ipfwadm'

alias ippi='ipfwadm -I'

alias ip0='ipfwadm -0'

alias ipf='ipfwadm -F'

alias ip1='ipfwadm -1'

alias ipp='ipfwadm -h |more|'
```

# 第 8 章：连接互联网

为了完成此过程，请将你交互式执行的所有命令输入一个脚本文件。将其命名为类似 `fire.rules` 之类的名称，并确保将模式更改为仅限 `root` 可执行，因为你希望对这种关键系统保持严格的控制。如果你有分帧中继（`frame relay`）或静态路由 `PPP` 网络连接，你可以在启动时设置防火墙规则。在这种情况下，请在 `/etc/rc.d/rc.local` 脚本文件中添加以下行，这样规则在每次启动时都会执行：

```
if [ -f /etc/rc.d/init.d/fire.rules ]; then
/etc/rc.d/init.d/fire.rules
```
