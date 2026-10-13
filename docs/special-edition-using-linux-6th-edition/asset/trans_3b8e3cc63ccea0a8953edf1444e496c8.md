
在你的本地子目录中构建 hosts.allow 文件时，你决定先把简单的行放在前面。前两行使任何地方的任何人都能访问 pop3 和 ftp：

```text
ipop3d: ALL: ALLOW
in.ftpd: ALL: ALLOW
```

对于 imap 守护进程，你只想允许 localhost。这包括 127.0.0.1，但你打算将其开放给整个 127 IP 段，因为只有 localhost 的 IP 会以 127 开头。你还会按名称 bar.void.org 及相应 IP 192.168.0.2 启用本地系统。你要拒绝所有其他用户，并让 root 知道连接尝试：

```text
imapd: LOCALHOST, 127., bar.void.org, 192.168.0.2: ALLOW
imapd: ALL : (/usr/sbin/safe_finger -l %h | /usr/bin/mail root) & : DENY
```

对于 telnet 守护进程，你决定将其开放给本地网络，但你还希望在任何人打开 telnet 时显示警告横幅：

```text
in.telnetd: LOCAL, 127., 192.168.0., .void.org: banners /etc/banners : ALLOW
```

然后，你创建一个名为 /etc/banners/in.telnetd 的文件，内容如下：

```text
WARNING: Unauthorized entry into this system for any reason is a criminal
act and will be prosecuted to the fullest extent of the law.
```

接下来，你允许本地网络访问 swat：

```text
swat: LOCAL, .void.org, 192.168.0., 127.: ALLOW
```

最后，你拒绝所有其他服务（以防万一有遗漏）：

```text
ALL : ALL : DENY
```

为了确保新的 hosts.allow 文件没有问题，运行 tcpdchk 并查找带有 warning 的行：

```text
tcpdchk -vd
```

```text
Using network configuration file: /etc/inetd.conf

>>> Rule hosts.allow line 1:
daemons:  ipop3d
clients: ALL
option:  ALLOW
access: granted

>>> Rule hosts.allow line 2:
daemons:  in.ftpd
clients: ALL
option:  ALLOW
access: granted

>>> Rule hosts.allow line 3:
daemons: imapd
clients: LOCALHOST bar.void.org 192.168.0.2 127.
option:  ALLOW
access: granted

>>> Rule hosts.allow line 4:
daemons: imapd
clients: ALL
option:  spawn (/usr/sbin/safe_finger -l @client_hostname | /usr/bin/mail root) &
option:  DENY
access:  denied

>>> Rule hosts.allow line 5:
daemons: in.telnetd
clients: LOCAL 192.168.0. 127. .void.org
option:  banners /etc/banners
option:  ALLOW
access:  granted

>>> Rule hosts.allow line 6:
daemons: swat
clients: LOCAL .void.org 192.168.0. 127.
option:  ALLOW
access:  granted

>>> Rule hosts.allow line 7:
daemons: ALL
clients: ALL
option:  DENY
access:  denied
```

使用 tcpdmatch 测试几个客户端，你会得到所期望的响应：

```text
tcpdmatch -d ipop3d locutus2.calderasystems.com

client:  hostname locutus2.calderasystems.com
client:  address 207.179.18.140
server:  process ipop3d
matched: hosts.allow line 1
option:  ALLOW
access:  granted
```

in.ftpd 的结果类似，现在来看看只想让本地主机访问的 imap 守护进程：

```text
tcpdmatch -d imapd foo

warning: foo: hostname alias
warning: (official name: foo.void.org)
client:  hostname foo.void.org
client:  address 192.168.0.1
server:  process imapd
matched: hosts.allow line 4
option:  spawn (/usr/sbin/safe_finger -l @foo.void.org | /usr/bin/mail root) &
option:  DENY
access:  denied
```

测试 telnet 服务器会显示以下内容：

```text
warning: foo: hostname alias
warning: (official name: foo.void.org)
client:  hostname foo.void.org
client:  address 192.168.0.1
server:  process in.telnetd
matched: hosts.allow line 5
option:  banners /etc/banners
WARNING: Unauthorized entry into this system for any reason is
a criminal act and will be prosecuted to the fullest extent of the law.

option:  ALLOW
access:  granted
```

测试一个非本地客户端的 telnet 访问时，你会收到以下内容：

```text
client:   hostname locutus2.calderasystems.com
client:   address   207.179.18.140
server:   process in.telnetd
matched:  hosts.allow line 7
option:   DENY
access:   denied
```

再创建几个假设性匹配后，会发现你创建的规则达到了预期效果。请记住，只有由 inetd 管理的那些 TCP 服务才会以这种方式受到保护。其他不由 inetd 运行的服务或 UDP 服务必须通过其他方式加以保护，例如 netfilter。

## IP 伪装

### 本章内容

- IP 伪装、网络地址转换与端口转发 — 684
- 所需内核组件 — 686
- 设置 — 687
- SNAT — 689
- DNAT — 689
- 项目：构建 NAT 系统 — 690

### IP 伪装、网络地址转换与端口转发

从标题来看，本章意在讨论 IP 伪装。事实上也的确如此。如果你参与任何 Linux 邮件列表，无疑会看到这个术语的出现。但随着新的 Linux 2.4.x 系列内核以及处理 IP 地址重写和改写的框架软件的出现，IP 伪装本身已经改变了其地位。

Linux 现在通过称为 iptables 的用户态接口使用 netfilter 软件来执行有状态的包过滤，你可以在第 36 章“IP 防火墙”中读到相关内容。它使用相同的用户态接口来执行网络地址转换（NAT）、伪装和端口转发。

如果你不熟悉 NAT 的概念，它基本上能让你在数据包穿过防火墙时重写数据包头。这些报头可以在离开防火墙时（路由后）被重写，并涉及将源地址从发起连接的系统更改为防火墙的外部地址。于是，Internet 上的服务器会看到一个来自防火墙或 NAT 系统的连接。因为更改的是源地址，netfilter 将其称为源 NAT（SNAT）。你可以利用这一点来隐藏一个使用公共 IP 的网络。IP 伪装是 SNAT 的一种特殊形式，常用于允许具有私有 IP（Internet 不可路由的 IP）的网络访问 Internet。两者所做的基本事情相同，并且都可与私有 IP 一起使用。不过，IP 伪装现在通常保留给具有动态 IP 的拨号账户。如果你在连接到 ISP 时不知道自己被分配了什么 IP，那么很可能就是这种情况，因此你将需要伪装目标而不是 SNAT 目标。更多相关内容将在后面的文字中介绍。

netfilter 允许的另一种 NAT（或数据包改写）类型称为目标 NAT（DNAT）。这种地址改写形式在路由前执行，用于将初始连接接入 NAT 系统并重定向到内部系统。在某些圈子中，这被称为*端口转发*，因为转发通常基于初始连接端口进行。这将使你能够在受信任网络上使用不同的系统来处理 HTTP、FTP、邮件、DNS 等，但在外部世界看来，好像 NAT 盒子在做所有事情。这种特殊的地址改写形式要求你拥有可路由的 IP。如果必须使用伪装，那么你将无法使用 DNAT。

最常见的是，包过滤防火墙软件用于隐藏内部公共网络，并只允许特定流量进入。图 35.1 描绘了这种类型的网络。

**图 35.1** 具有一个 IP 地址块的网络。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_704_0.png)

还有一种不遵循这种方式的网络方案。那就是家庭和小型企业网络，其中大多数没有合法的 IP 地址块可用，而且大多数只能通过拨号方式访问其他 TCP/IP 网络，尤其是 Internet（见图 35.2）。每次连接时，它们都会从可用 IP 池中分配到一个 IP。

**图 35.2** 具有一个公共 IP 地址并使用 IP 伪装的网络。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_704_1.png)

通过 IP 伪装，家庭或小型企业网络可以使用单台服务器上的单个 IP 地址，为所有连接的机器提供访问外部网络（如 Internet）的能力。所有发往 Internet 的网络数据包都会被伪装成似乎来自运行 IP 伪装的服务器。服务器维护必要的信息，以便将返回的网络数据包路由回应该接收它们的机器。头脑灵活的人可能会说：“但每个连接既是 SNAT 又是 DNAT，这取决于数据包的流动方向。”不过，决定我们正在做哪种转换的是初始连接数据包，即 SYN 数据包（仅设置了 SYN 位的数据包）。之后，连接跟踪允许返回数据包回到发起系统。连接跟踪使 netfilter 变为有状态的，这是一个被过度使用的营销流行语，意思是它能识别连接的状态（新建、已建立和关联）。它还使 netfilter 运行得更快。因为关联、已建立的连接不会运行整套规则，netfilter 会记住与该连接相关的规则，使用这些规则并跳过其余规则。
