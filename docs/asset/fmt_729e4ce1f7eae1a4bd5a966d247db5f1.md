
当你连接到一个站点时，你可以使用`queue`命令排队命令，设置要执行的 FTP 操作列表。有了此功能，你可以向站点排队多个下载操作。可以重新排序队列并删除条目（如果需要）。你还可以连接到多个站点并为每个站点设置队列。`mirror`命令让你维护镜像站点的本地版本。你可以下载整个站点或仅更新较新的文件，以及删除不再存在于镜像上的文件。

你可以用`.lftprc`文件中的选项来自定义`lftp`。系统范围的设置放在`/etc/lftp.conf`文件中。在这里，你可以设置诸如使用的提示符和匿名密码等功能。`.lftp`目录保存命令历史、日志、书签和启动命令的支持文件。`lftp`还支持`.netrc`文件，检查其中的登录信息。

# CHAPTER 网络工具

你可以使用各种网络工具执行诸如获取有关网络上其他系统的信息、访问其他系统以及直接与其他用户通信等任务。可以使用`ping`、`finger`、`traceroute`和`host`等实用程序获取网络信息。Talk、ICQ 和 IRC 客户端使你能够直接与网络上的其他用户通信。`telnet`对你可能在网络上连接的另一系统上的帐户执行远程登录。一些工具具有相应的 K Desktop 或 GNOME 版本。此外，你的网络可能使用网络远程访问命令。这些对于较小的网络很有用，使你能够直接访问远程系统以复制文件或执行命令。

## 网络信息：`ping`、`finger`、`traceroute`和`host`

你可以使用`ping`、`finger`、`traceroute`和`host`命令查找有关网络上系统和用户的状态信息。`ping`用于检查远程系统是否处于运行状态。你使用`finger`查找有关网络上其他用户的信息，查看他们是否已登录或是否收到邮件。`host`显示网络上系统地址信息，为你提供系统的 IP 和域名地址。`traceroute`可用于跟踪你的消息在到达你之前经过的计算机网络和系统的序列。表 15-1 列出了各种网络信息工具。

虽然未随 Red Hat 一起提供，但对于 GNOME 桌面，GNOME Workstation Command Center 实用程序提供了用于输入`ping`、`traceroute`和`host`命令等功能的 GNOME 接口。在 K Desktop 上，你可以使用 KDE 网络实用程序发出`ping`、`finger`、`traceroute`和`host`命令。

## `ping`

`ping`命令检测系统是否处于运行状态。`ping`以你想要检查的系统名称作为参数。如果要检查的系统已关闭，`ping`会发出超时消息，指示无法建立连接。下一个示例检查 www.redhat.com 是否已启动并连接到网络：

```
$ ping www.redhat.com
PING www.portal.redhat.com (206.132.41.231): 56 data bytes
64 bytes from 206.132.41.231: icmp_seq=0 ttl=248 time=24.0 ms
64 bytes from 206.132.41.231: icmp_seq=1 ttl=248 time=124.5 ms
64 bytes from 206.132.41.231: icmp_seq=2 ttl=248 time=77.9 ms
64 bytes from 206.132.41.231: icmp_seq=3 ttl=248 time=220.1 ms
64 bytes from 206.132.41.231: icmp_seq=4 ttl=248 time=14.9 ms

--- www.portal.redhat.com ping statistics ---
6 packets transmitted, 5 packets received, 16% packet loss
round-trip min/avg/max = 14.9/92.2/220.1 ms
```

你也可以使用`ping`并使用 IP 地址而不是域名。使用 IP 地址时，`ping`可以直接尝试检测远程系统，而无需通过域名服务器将域名翻译成 IP 地址。这对于网络的域名服务器可能暂时宕机，而你想检查网络上某个特定远程主机是否已连接的情况非常有帮助。在下一个示例中，用户使用其 IP 地址检查 Red Hat 网站：

```
$ ping 206.132.41.231
PING 206.132.41.231 (206.132.41.231): 56 data bytes
64 bytes from 206.132.41.231: icmp_seq=0 ttl=248 time=16.6 ms
64 bytes from 206.132.41.231: icmp_seq=1 ttl=248 time=65.1 ms
64 bytes from 206.132.41.231: icmp_seq=2 ttl=248 time=70.1 ms
64 bytes from 206.132.41.231: icmp_seq=3 ttl=248 time=336.6 ms
64 bytes from 206.132.41.231: icmp_seq=4 ttl=248 time=53.6 ms
64 bytes from 206.132.41.231: icmp_seq=5 ttl=248 time=42.1 ms

--- 206.132.41.231 ping statistics ---
6 packets transmitted, 6 packets received, 0% packet loss
round-trip min/avg/max = 16.6/97.3/336.6 ms
```

> 注意`ping`操作也可能失败，如果网络的防火墙拒绝了`ping`访问。有关更多详细信息，请参阅第 19 章。

## `finger`和`who`

你可以使用`finger`命令获取有关网络上其他用户的信息，并使用`who`命令查看当前系统上有哪些用户在线。`who`和`w`命令列出当前连接的所有用户，以及他们何时、多久以及从何处登录。`w`命令提供更详细的信息。它有几个选项可指定详细程度。`who`旨在在本地系统或网络上运行。`finger`可以在大型网络上运行，包括互联网，尽管大多数系统出于安全原因会阻止它。

> 注意 Etherial 是一个协议分析器，可以捕获网络数据包并显示有关它们的详细信息。你可以检测网络上传输了什么类型的信息以及其来源和目的地。Etherial 主要用于网络和服务器管理。Etherial 在第 38 章中有详细讨论。

## `host`

使用`host`命令，你可以查找连接到你的网络的远程系统的网络地址信息。此信息通常由系统的 IP 地址、域名地址、域名昵称和邮件服务器组成。此信息是从你的网络的域名服务器获取的。对于互联网，这包括你可以通过互联网连接的所有系统。

`host`命令是确定远程站点的 IP 地址或 URL 的有效方法。如果你只有站点的 IP 地址，你可以使用`host`查找其域名。对于网络管理，IP 地址对于在你的`/etc/host`文件中创建自己的域名条目非常有帮助。这样，你就不必依赖远程域名服务器（DNS）来定位站点。

```
$ host www.gnome.org
www.gnome.org is a nickname for gnome.labs.redhat.com
gnome.labs.redhat.com has address 199.183.24.235
gnome.labs.redhat.com mail is handled (pri=10) by mail.redhat.com
```

```
$ host 199.183.24.235
235.24.183.199.IN-ADDR.ARPA domain name pointer
gnome.labs.redhat.com
```

Gwhois 程序是一个基于 GNOME 的客户端，用于显示从 NIC 网络服务获取的主机信息。Gwhois 提供了一个 X Window System 接口，其中包含可供选择的 NIC 服务器列表。gHostLookup 是一个简单的 GNOME 应用程序，当你提供主机名时，它会返回机器的 IP 地址。

## `traceroute`

互联网连接是通过各种路由建立的，途经一系列互连的网关主机。从一个系统到另一个系统的路径可能采用不同的路由，其中一些可能比其他路由更快。对于缓慢的连接，你可以使用`traceroute`检查连接到主机的路由，监控速度以及路由经过的中间网关连接数量。`traceroute`命令以你想要检查路由的系统的主机名或 IP 地址作为参数。可用选项可指定参数，如服务类型（`-t`）或源主机（`-s`）。`traceroute`命令将返回路由经过的主机列表，以及发送到每个网关的三个探测的时间。大于五秒的时间将以星号`*`显示。

```
traceroute rabbit.mytrek.com
```

你也可以使用`mtr`或`xmtr`工具同时执行`ping`和跟踪（系统工具菜单上的 Traceroute）。Red Hat 还包括 Xtraceroute（更多系统工具菜单）。
