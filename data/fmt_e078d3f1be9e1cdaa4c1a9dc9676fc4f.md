
设置 PPP 客户端需要一个现代电话线、某个电话号码处的 PPP 服务器，以及编译到内核中的 PPP 支持。检查 `dmsg` 命令以查看 PPP 支持是否已编译到内核中。你也可以检查 `/lib/modules/` 目录下的 `ppp.o`，查看它是否被编译为模块。如果支持没有编译进内核，请重新编译内核并使用新内核重启。

验证 PPP 连接的快速方法是执行类似于以下的操作：

```
pppd connect 'chat -v "*" ATDTphone CONNECT " login: login word: \
/dev/cual 38400 debug crtscts modem defaultroute
```

电话、线路和密码由提供 PPP 账户的人分配给你。此外，将 `/dev/cual` 修改为你的解调器位置。记住 Linux 下的 `/dev/cual` 等同于 DOS 和 Windows 下的 COM2。`chat` 命令用于拨打解调器并提供登录和密码信息。一旦 `chat` 返回成功（即建立了连接），PPP 将接管线路并启动连接。服务器和客户端会协商诸如最大传输单元（MTU）、压缩等其他设置。这需要几秒钟，但完成后，你应该能够使用 `/sbin/ifconfig` 命令检查网络连接。

如果你看到列表中有一个 `ppp0`，说明你已经就绪了。

要使用 DNS，请检查 `/etc/resolv.conf` 文件。

## 6.2 INETD

```
name 42/upd      nameserver
whois 43/tcp     nickname # 通常指向 sri-nic
domain 53/tcp
domain 53/udp
mtmp 57/tcp      # 已弃用
bootps 67/udp    # bootp 服务器
bootpc 68/udp    # bootp 客户端
tftp 69/udp
gopher 70/tcp    # gopher 服务器
```

行的第一项是 `name`。其后是端口号（通常是 TCP 或 UDP），随后是任何别名。如你上方所示，接收邮件的端口被称为 `smtp` 端口，它位于 25 端口。它的别名是 `mail`，因此你可以运行类似下面的命令：

```
[markk@way ~$] telnet localhost smtp
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
220 wayga.ratatosok.org ESMTP Sendmail 8.8.5/8.8.5; Mon, 1 Sep 1997
18:54-30
```

`telnet` 命令会将你连接到 TCP/IP 端口 25（`sendmail` 目前正在运行的地方）。

## /etc/inetd.conf

`/etc/inetd.conf` 文件获取来自 `/etc/services` 文件的端口信息，并告诉 `inetd` 需要监控哪些端口。这里是一个示例 `inetd.conf` 文件的部分：

```
# 这些是标准服务。
#
ftp stream tcp nowait /usr/sbin/tcpd.ftpd -1 -a
telnet stream tcp nowait /usr/sbin/tcpd in.inetd
gopher stream tcp nowait /usr/sbin/tcpd gn
```

```
# 除非你*真的*知道自己在做什么，否则不要取消注释 stream。
# smtp 现在由 sendmail 守护进程处理，而不是 smtpd。它**没有**
# 从这里运行，而是在启动时从 /etc/cd/rc#.d 启动。
# smtp stream tcp nowait /usr/bin/smtpd
nntp stream tcp nowait /usr/sbin/tcpd in.nntpd
```

该文件中的条目如下：

- 来自 `/etc/services` 的条目，指定监控哪个端口。
- `stream` 或 `dgram`（`tcp` 是 `stream`，`udp` 是 `dgram`）。
- 协议（`tcp` 或 `udp`）。
- 选项（`wait` 或 `nowait`）。`wait` 表示等待程序结束或在返回监控端口之前完成。`nowait` 选项表示不等待并直接返回监控端口。如果选择了 `nowait`，程序一次只会运行一个实例。
- 运行的用户——这通常是 `root`。
- 程序名称以及你想要添加的任何选项。

在 `/etc/services` 的示例中，我们连接到了 `mail` 端口，但 `inetd.conf` 的示例显示 `smtp` 并没有被监控。发生了什么？对于某些高吞吐量程序（`http` 和 `sendmail` 是主要的范例），你不希望程序不断重启，因为程序初始启动需要大量时间。但是，对于一个已经在运行的程序来派生（fork）或产生新进程，开销要小得多。因此，对于这类程序，让它们持续运行并自己处理连接会更好。

像 `telnetd` 和 `ftp` 这样的程序不需要大量的启动时间，因此 `inetd` 会根据需要启动新的副本。

## 6.3 网络应用程序

既然网络已经建立好了，你打算用它做什么呢？大多数标准主题（Web、FTP、电子邮件）已经涵盖过了，但本章的其余部分将涵盖对大家都有利的跨网络应用程序。DNS（名称服务器）和 NFS（网络文件服务器）就是此类应用程序。

### DNS

名称服务器是将 IP 地址（208.197.103.125）与到主机名（wayga.net）匹配的程序。它也提供反向匹配，通知你某台地址为 208.197.103.125 的机器名为 wayga.net。由于名称服务器的工作之一是查找并缓存来自客户端的 DNS 请求，它可以被用于慢链路的一端（也许在两个办公室之间），并减少跨越链路的 DNS 流量。它还提供了从一个地址转发邮件到另一个地址的规定，并在特定情况下提供备份，以防某个 Web 服务器忙而另一个空闲。

在任何连接到 TCP/IP 网络的实例，你都希望使用 DNS 主机名解析。通过在你的 `/etc/resolv.conf` 文件中放入几行即可轻松完成设置：

```
domain mayga.net
nameserver 192.33.4.10
```

将 `mayga.net` 修改为你的域名，并将 IP 地址更改为你的 ISP 提供的名称服务器 IP。如果你不知道本地名称服务器，这个 IP 地址在紧急情况下可以应急，让你运行起来。你也可以在这里放置多个 `nameserver` 条目，它将按顺序搜索，直到连接到 DNS 服务器为止。

如果你计划在本地运行 `named`（DNS 服务器软件），你应该将 IP 地址更改为 `127.0.0.1`。确保在里面保留几个其他 IP 地址，以防 `name` 宕机。

### 你应该成为 DNS 服务器吗？

你只有在以下情况下才使用 DNS 服务器：

1. 你拥有一个域名并想对一个慢链路进行控制。
2. 你在慢链路上运行一个大型网络。
3. 你没有连接互联网。

对于第 1 点，许多 ISP 会提议为你提供 DNS 服务，但如果你处于机器频繁变化的环境中，自己处理可能比等待 ISP 更新他们的表要容易得多。对于第 2 点，`named` 可以作为缓存来存储频繁使用的主机，这将减少部分流量。对于第 3 点……嗯，如果你的网络上没有其他 DNS 主机，应该有人来做，而且可能你来最合适。如果你不符合这三点中的任何一点，你可能不需要运行 DNS 服务器。

> 7 是的，如果你正在使用 NIS。

注意，第一个 DNS 会停止。如果没有找到第一个 DNS，搜索将停止。如果你期望成为世界的辅助或辅助 DNS（即互联网），你必须设置你的机器。`named.boot` 文件包含了在 `named` 启动时给它的信息。`named.boot` 告诉 `named` 三件事：

1. 哪个目录
- 哪些主服务
2. 提供了什么

在这种情况下，`named` 做了三件事：

1. 哪个目录
- 哪些主服务
2. 哪些反向服务

`named.boot` 告诉 `named` 三件事：

1. 哪个目录
- 哪些主服务
2. 哪些反向服务

`named.ca` 告诉 `named` 三件事。第二个语句说明缓存文件保留在 `wayga.net` 中。第三个语句表示任何对 `127.0.0.1`（也称为回环设备）的请求都应通过查看 `named.local` 文件完成。`named.ca` 包含了关于根名称服务器的信息。如果本地 `named` 没有该主机名，它将开始在根服务器中查找。这里是 `wayga.net` `named.ca` 的部分：
