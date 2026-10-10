
![](img/c27875544958897d817484d558c208c8_577_3.png)

你还可以使用网络中的路由器上的路由协议来自动将路由添加到路由表中。两种常见的路由协议是路由信息协议（`RIP`）和开放最短路径优先（`OSPF`）。如果你安装 `quagga` 软件包，就可以使用 `zebra` 命令配置 `RIP` 和 `OSPF` 路由协议。

由于像互联网这样的大型网络的路由列表太大，无法存储在路由器的路由表中，因此大多数路由器都配置了默认网关。任何发往路由表中未列出的目的地的数据包都会被发送到默认网关，默认网关是一个可以将数据包转发到相应网络或到其自身默认网关的路由器，依此类推，直到数据包到达目的地。

如果你网络上的计算机无法连接到远程网络上的其他计算机，问题很可能与路由有关。用于排查路由问题的常用实用工具是 `traceroute` 命令；它会显示当前计算机与远程计算机之间的所有路由器。要追踪从本地计算机到 IP 地址为 `3.4.5.6` 的计算机的路径，你可以使用以下命令：

```
[ root@server1 ~]$ traceroute 3.4.5.6
traceroute to 3.4.5.6 (3.4.5.6), 30 hops max, 38 byte packets
1 linksys (192.168.0.1) 2.048 ms 0.560 ms 0.489 ms
2 apban.pso.com (7.43.111.2) 2.560 ms 0.660 ms 0.429 ms
3 tts.ishtcid.net (3.0.0.1) 3.521 ms 0.513 ms 0.499 ms
4 sr1.lala.com (3.4.5.6) 5.028 ms 0.710 ms 0.554 ms
[ root@server1 ~]$
```

![](img/c27875544958897d817484d558c208c8_578_0.png)

`traceroute` 命令的一个常见替代项是 `tracepath` 命令。

![](img/c27875544958897d817484d558c208c8_578_1.png)

要追踪 `IPv6` 路由，你可以使用 `traceroute6` 或 `tracepath6` 命令。

## 网络服务

回顾第 1 章，`Linux` 提供种类繁多可供用户跨网络使用的服务。在能够配置适当的网络服务以满足你组织的需求之前，你必须首先识别网络服务的类型和功能。

网络服务是在你的计算机上运行的进程，为网络上的客户端计算机提供某种有价值的服务。它们通常由一系列守护进程表示，这些守护进程监听网络上的特定请求。守护进程使用唯一标识每个网络服务的端口号来识别它们应响应哪些数据包。不同的守护进程监听不同的端口号。端口号类似于公寓编号，用于邮件投递。`IP` 地址的网络 `ID` 确保数据包被投递到正确的街道（网络）；主机 `ID` 确保数据包被投递到正确的建筑物（主机）；而传输层协议和端口号则确保数据包被投递到正确的公寓（服务）。

端口及其关联协议在 `/etc/services` 文件中定义。要查看 `telnet` 守护进程监听哪个端口，你可以使用以下命令：

```
[root@server1 ~]# grep telnet /etc/services
telnet      23/tcp
telnet      23/udp
telnet      107/tcp     # Remote Telnet
rtelnet     107/udp
telnets     992/tcp
telnets     992/udp
skytelnet   1618/tcp    # skytelnet
skytelnet   1618/udp    # skytelnet
hp-3000-telnet      2564/tcp    # HP 3000 NS/VT block mode telnet
hp-3000-telnet      2564/udp    # HP 3000 NS/VT block mode telnet
tll1-telnet         3083/tcp    # TLL1-TELNET
tll1-telnet         3083/udp    # TLL1-TELNET
telnetcpd           3696/tcp    # Telnet Com Port Control
telnetcpd           3696/udp    # Telnet Com Port Control
scpi-telnet         5024/tcp    # SCPI-TELNET
scpi-telnet         5024/udp    # SCPI-TELNET
ktelnet             6623/tcp    # Kerberos VS Telnet
ktelnet             6623/udp    # Kerberos VS Telnet
[root@server1 ~]# _
```

上述输出表明，`telnet` 守护进程同时使用 `TCP/IP` 和 `UDP/IP` 监听端口 23。

![](img/c27875544958897d817484d558c208c8_579_0.png)

> 用户数据报协议/互联网协议（`UDP/IP`）是 `TCP/IP` 的一个更快的版本，因此可靠性较低。

端口编号范围从 0 到 65534。0–1023 端口被称为**知名端口**，因为它们代表常用的服务。表 12-2 提供了一份常见知名端口的列表。

![](img/c27875544958897d817484d558c208c8_579_1.png)

> 许多协议都有一个使用加密通信的安全版本。例如，安全 `HTTP` 被称为 `HTTPS`，并因此使用不同的端口号。

网络实用程序可以直接连接到提供网络服务的守护进程；这些守护进程被称为独立守护进程。或者，网络实用程序可以通过互联网超级守护进程（`inetd`）或扩展互联网超级守护进程（`xinetd`）连接到网络服务，后者会在需要时启动适当的守护进程以提供网络服务。这种结构如图 12-8 所示。

`inetd` 或 `xinetd` 守护进程通常用于启动和管理较小的网络守护进程（如 `telnet` 和 `rlogin`）的连接。`Ubuntu Server 14.04` 默认安装了 `inetd` 守护进程，但你可以通过软件仓库选择安装 `xinetd` 守护进程。`Fedora`

表 12-2 常见知名端口

| 服务 | 端口 |
| :--- | :--- |
| `FTP` | `TCP 20, 21` |
| 安全 `Shell` (`SSH`) | `TCP 22` |
| `Telnet` | `TCP 23` |
| `SMTP` | `TCP 25` |
| `HTTP` / `HTTPS` | `TCP 80` / `TCP 443` |
| `rlogin` | `TCP 513` |
| `DNS` | `TCP 53, UDP 53` |
| 简单 `FTP` (`TFTP`) | `UDP 69` |
| `POP3` / `POP3S` | `TCP 110` / `TCP 995` |
| `NNTP` / `NNTPS` | `TCP 119` / `TCP 563` |
| `IMAP4` / `IMAP4S` | `TCP 143` / `TCP 993` |

![](img/c27875544958897d817484d558c208c8_580_0.png)

大多数系统默认不包含 `inetd` 或 `xinetd` 守护进程，但你可以通过软件仓库安装 `xinetd`。

`inetd` 守护进程通过编辑 `/etc/inetd.conf` 文件进行配置。例如，如果你安装了 `telnet` 守护进程，可以在 `/etc/inetd.conf` 中配置以下行，以确保它能被 `inetd` 启动：

```
[root@server1 ~]# grep telnet /etc/inetd.conf
	telnet stream tcp nowait root /usr/sbin/tcpd /usr/sbin/in.telnetd
[root@server1 ~]#
```

上述输出显示了 `telnet` 守护进程的完整路径（`/usr/sbin/in.telnetd`）。

`xinetd` 守护进程通过 `/etc/xinetd.conf` 文件中的条目进行配置。通常，此文件还整合了 `/etc/xinetd.d` 目录中的所有文件。大多数由 `xinetd` 管理的守护进程都通过位于 `/etc/xinetd.d` 目录下、以守护进程命名的文件进行配置。例如，如果你安装了 `telnet` 守护进程，可以通过 `/etc/xinetd.d/telnet` 文件配置其被 `xinetd` 启动，如下所示的输出：

```
[root@server1 ~]# cat /etc/xinetd.d/telnet
service telnet
{
    flags           = REUSE
    socket_type     = stream
    wait            = no
    user            = root
    server          = /usr/sbin/in.telnetd
    log_on_failure  += USERID
    disable         = no
}
[root@server1 ~]#
```

大型网络守护进程很少由 `inetd` 或 `xinetd` 启动。相反，它们是在启动时由 `rc` 脚本作为 `UNIX SysV` 或 `Systemd` 系统初始化过程的一部分启动的独立守护进程。

许多独立守护进程和由 `inetd`/`xinetd` 管理的守护进程也有配置文件，用于控制其操作方式并指示守护进程使用的其他重要文件的路径。为简化起见，许多此类守护进程仅在一个包含注释的配置文件中存储所有信息，这些注释指明了每一行的语法和用途。因此，这些配置文件可能非常大；`Apache` Web 服务器使用的配置文件通常长达数百行。除此之外，大多数独立网络守护进程不使用系统日志守护进程（`syslogd`）或 `Systemd` 日志守护进程（`journald`）来记录与其操作相关的信息。相反，它们自行将这些信息记录到 `/var/log` 目录下与其同名的子目录中。例如，`Samba` 守护进程的日志文件位于 `/var/log/samba` 目录中。

表 12-3 列出了在参与网络环境的 `Linux` 计算机上常见的网络服务名称和功能。你将在本章以及第 13 章中学习如何配置这些网络服务中的许多服务。

表 12-3 常见网络服务

| 网络服务 | 类型 | 端口 | 描述 |
| :--- | :--- | :--- | :--- |
| `Apache` Web 服务器 (`httpd`) | 独立 | `TCP 80`<br>`TCP 443` | 使用 `HTTP`/`HTTPS` 向网络上拥有 Web 浏览器的其他计算机提供 Web 页面<br>配置文件：`/etc/httpd/conf/httpd.conf` 或<br>`/etc/apache2/apache2.conf` |
| `BIND` / `DNS` 服务器 (`named`) | 独立 | `TCP 53`<br>`UDP 53` | 为互联网上的特定命名空间将完全限定域名解析为 `IP` 地址<br>配置文件：`/etc/named.conf` |
| `DHCP` 服务器 (`dhcpd`) | 独立 | `UDP 67`<br>`UDP 68` | 为网络上的计算机提供 `IP` 配置<br>配置文件：`/etc/dhcp/dhcpd.conf` |
| 华盛顿大学 `FTP` 服务器 (`in.ftpd`) | `inetd`/`xinetd` | `TCP 20`<br>`TCP 21`<br>`UDP 69` | 使用 `FTP` 实用工具将文件传输到网络上的其他计算机并从中接收文件<br>配置文件：`/etc/ftpaccess`<br>被拒绝 `FTP` 访问的主机：`/etc/ftphosts`<br>被拒绝 `FTP` 访问的用户：`/etc/ftpusers`<br>`FTP` 数据转换 `/etc/ftpconversions` |
| 非常安全的 `FTP` 服务器 (`vsftpd`) | 独立 | `TCP 20`<br>`TCP 21`<br>`UDP 69` | 使用 `FTP` 实用工具将文件传输到网络上的其他计算机并从中接收文件。配置文件：`/etc/vsftpd/vsftpd.conf`<br>被拒绝 `FTP` 访问的用户：`/etc/vsftpd/ftpusers` 和 `/etc/vsftpd.user_list` |
| 网间新闻服务器 (`innd`) | 独立 | `TCP 119`<br>`TCP 563` | 接收和管理新闻组帖子，并将其传输到其他新闻服务器<br>配置文件：`/etc/news/innd.conf` |
| `NFS` 服务器 (`rpc.nfsd`) | 独立 | `TCP 2049` | 向网络上拥有 `NFS` 客户端实用工具的其他计算机共享文件<br>配置文件：`/etc/exports` |
| `NIS` 服务器 (`ypserv` & `ypbind`) | 独立 | `TCP 111` | 向属于 `NIS` 域的 `NIS` 客户端共享配置信息<br>配置文件：`/etc/ypserv.conf` |
| `POP3` 服务器 (`pop3d`) | 独立 | `TCP 110`<br>`TCP 995` | 允许拥有电子邮件阅读器的用户使用邮局协议版本 3 (`POP3`) 从服务器获取电子邮件 |
| `IMAP4` 服务器 (`imapd`) | 独立 | `TCP 143`<br>`TCP 993` | 允许拥有电子邮件阅读器的用户使用互联网消息访问协议 (`IMAP`) 从服务器获取电子邮件 |
| `Sendmail` 邮件服务器 (`sendmail`) | 独立 | `TCP 25` | 使用简单邮件传输协议 (`SMTP`) 接收和发送电子邮件给用户或互联网上的其他邮件服务器<br>配置文件：`/etc/sendmail.cf` |
| `Postfix` 邮件服务器 (`postfix`) | 独立 | `TCP 25` | 使用简单邮件传输协议 (`SMTP`) 接收和发送电子邮件给用户或互联网上的其他邮件服务器<br>配置文件：`/etc/postfix/main.cf` |
| `rlogin` 守护进程 (`in.rlogind`) | `inetd`/`xinetd` | `TCP 513` | 允许使用 `rlogin` 和 `rcp` 实用工具的用户复制文件并在网络上的其他计算机上获取 shell |
| `rsh` 守护进程 (`in.rshd`) | `inetd`/`xinetd` | `TCP 514` | 允许使用 `rsh` 实用工具的用户在网络上的其他计算机上运行命令 |
| `Samba` 服务器 (`smbd` & `nmbd`) | 独立 | `TCP 137`<br>`TCP 138`<br>`TCP 139`<br>`TCP 445` | 允许 `Windows` 用户查看 `Linux` 服务器上的共享文件和打印机<br>配置文件：`/etc/samba/smb.conf` |
| 安全 `Shell` 守护进程 (`sshd`) | 独立 | `TCP 22` | 通过使用加密通信提供 `telnet`、`rlogin` 和 `rsh` 实用工具的安全替代方案<br>配置文件：`/etc/ssh/sshd_config` |
| `Squid` 代理服务器 (`squid`) | 独立 | `TCP 3128` | 允许网络上的计算机共享一个到互联网的连接。它也被称为代理服务器<br>配置文件：`/etc/squid/squid.conf` |
| `telnet` 守护进程 (`in.telnetd`) | `inetd`/`xinetd` | `TCP 23` | 允许拥有 `telnet` 实用工具的用户跨网络登录系统并获取 shell |

## 远程管理

正如我们在第 6 章中讨论的那样，`Linux` 服务器通常安装在机架式服务器系统中，该系统位于服务器机房的机架上，并远程进行管理。有几种方法可以执行远程 `Linux` 服务器的命令行和图形化管理，包括 `telnet`、远程命令、安全 `Shell` (`SSH`) 和虚拟网络计算 (`VNC`)。

### Telnet

在远程 `Linux` 计算机上进行管理的最简单方式是通过命令行界面。`telnet` 命令传统上用于获取运行 `telnet` 服务器守护进程的远程 `UNIX` 和 `Linux` 服务器上的命令行 shell，这些服务器通过网络连接。几乎所有 `Macintosh`、`Linux` 和 `UNIX` 系统都附带 `telnet` 命令。对于 `Windows` 系统，你可以从 `www.chiark.greenend.org.uk/~sgtatham/putty/` 下载免费的 `Putty` 程序，以启动到另一台计算机的 `telnet` 会话。

大多数现代 `Linux` 发行版默认不安装 `telnet` 服务器守护进程，但可以轻松从软件仓库安装。在使用 `Systemd` 系统初始化过程的系统中，如 `Fedora 20`，`telnet` 服务器守护进程直接由 `Systemd` 作为独立守护进程管理。在其他系统中，如 `Ubuntu Server 14.04`，`telnet` 服务器守护进程由 `inetd` 或 `xinetd` 管理。

![](img/c27875544958897d817484d558c208c8_583_0.png)

> 默认情况下，由于 `/etc/security` 文件中的条目，你被阻止以 `root` 用户身份登录并获取某些网络服务（如 `telnet`）的 shell。删除或重命名此文件允许 `root` 用户通过 `telnet` 命令跨网络登录并接收 shell。

一旦配置好 `telnet` 守护进程，你就可以从远程计算机连接到它。只需将目标计算机的主机名或 `IP` 地址指定给 `telnet` 命令，并使用相应的用户名和密码登录。`telnet` 会话期间获取的 shell 运行在伪终端（一个不从计算机键盘直接获取输入的终端）上，而不是本地终端，其工作方式与正常 shell 非常相似：你可以执行命令，并使用 `exit` 命令终止 `BASH` shell 并结束会话。以下输出显示了一个使用主机名为 `server1` 的计算机的示例 `telnet` 会话：
