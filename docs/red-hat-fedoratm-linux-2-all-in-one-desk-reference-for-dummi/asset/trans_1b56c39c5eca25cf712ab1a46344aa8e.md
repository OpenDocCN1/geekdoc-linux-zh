
数据包含主要名称服务器的名称（在本例中为 @ 或当前域名）、技术联系人的电子邮件地址，以及五个用括号括起来的时间值。

NS 记录指定区域的权威名称服务器。典型的 NS 记录如下所示：

```
.    3600000    IN    NS    A.ROOT-SERVERS.NET.
```

在本例中，该 NS 记录列出了根区域的权威名称服务器（注意第一字段名称为单个点号）。生存时间（Time-To-Live）字段指定该记录在 1000 小时（3600000 秒）内有效。类别为 IN，代表互联网（Internet）；记录类型为 NS。最后一个字段列出名称服务器的名称（A.ROOT-SERVERS.NET.），并以点号结尾。

A 记录指定与某个名称对应的地址。例如，以下 A 记录显示 A.ROOT-SERVERS.NET. 的地址为 198.41.0.4：

```
A.ROOT-SERVERS.NET.    3600000    A    198.41.0.4
```

在本例中，由于该字段是可选的，因此未指定网络类别，其默认值为 IN。

PTR 记录用于反向映射——将地址转换回名称。考虑以下示例：

```
1    IN    PTR    localhost.
```

该记录来自名为 0.0.127.in-addr.arpa 的区域文件。因此，这条记录表示与地址 127.0.0.1 关联的名称是 localhost。

MX 记录指定代表特定域接收邮件的主机名称。例如，这里是一个典型的 MX 记录：

```
naba    IN    MX    10    mailhub.lnbsft.com.
```

这条记录表明，发送给当前域中名为 naba 的主机的邮件将被发送至 mailhub.lnbsft.com（该主机被称为邮件交换器）。数字 10 是优先级值。对于包含不同优先级值的多个 MX 记录，优先级数值较低的记录会优先被尝试。

掌握了关于资源记录的这些信息后，你可以浏览缓存名称服务器的区域文件。

## /var/named/named.ca 文件

关于十三个根名称服务器的信息包含在 `/var/named/named.ca` 文件中，该文件在 `/etc/named.conf` 文件中根区域的区域声明中被指定。以下列表展示了 Fedora Core 系统中 `/var/named/named.ca` 文件的内容：

```
:: This file holds the information on root name servers needed to
:: initialize cache of Internet domain name servers
:: (e.g. reference this file in the "cache . {file}"
:: configuration file of BIND domain name servers).

:: This file is made available by InterNIC
:: under anonymous FTP as
::    file    /domain/named.cache
::    on server    FTP.INTERNIC.NET
::              RS.INTERNIC.NET

:: last update:    Jan 29, 2004
:: related version of root zone:    2004012900

:: formerly NS.INTERNIC.NET

A.ROOT-SERVERS.NET.  3600000 IN  NS  A.ROOT-SERVERS.NET.
                    3600000      A   198.41.0.4

:: formerly NS1.ISI.EDU

B.ROOT-SERVERS.NET.  3600000     NS  B.ROOT-SERVERS.NET.
                    3600000     A   192.228.79.201
:: formerly C.PSI.NET

C.ROOT-SERVERS.NET.  3600000     NS  C.ROOT-SERVERS.NET.
                    3600000     A   192.33.4.12

:: formerly TERP.UMD.EDU

D.ROOT-SERVERS.NET.  3600000     NS  D.ROOT-SERVERS.NET.
                    3600000     A   128.8.10.90

:: formerly NS.NASA.GOV

E.ROOT-SERVERS.NET.  3600000     NS  E.ROOT-SERVERS.NET.
                    3600000     A   192.203.230.10
:: formerly NS.ISC.ORG

F.ROOT-SERVERS.NET.  3600000     NS  F.ROOT-SERVERS.NET.
                    3600000     A   192.5.5.241

:: formerly NS.NIC.DDN.MIL

G.ROOT-SERVERS.NET.  3600000     NS  G.ROOT-SERVERS.NET.
                    3600000     A   192.112.36.4
:: formerly AOS.ARMY.MIL

H.ROOT-SERVERS.NET.  3600000     NS  H.ROOT-SERVERS.NET.
                    3600000     A   128.63.63.53

: formerly NIC.NORDU.NET
:
3600000 NS I.ROOT-SERVERS.NET.
:
I.ROOT-SERVERS.NET. 3600000 A 192.36.148.17
:
: operated by VeriSign, Inc.
:
3600000 NS J.ROOT-SERVERS.NET.
:
J.ROOT-SERVERS.NET. 3600000 A 192.58.128.30
:
: operated by Ripe NCC
:
3600000 NS K.ROOT-SERVERS.NET.
:
K.ROOT-SERVERS.NET. 3600000 A 193.0.14.129
:
: operated by ICANN
:
3600000 NS L.ROOT-SERVERS.NET.
:
L.ROOT-SERVERS.NET. 3600000 A 198.32.64.12
:
: operated by WIDE
:
3600000 NS M.ROOT-SERVERS.NET.
:
M.ROOT-SERVERS.NET. 3600000 A 202.12.27.33
: End of File
```

该文件包含 **NS** 和 **A** 资源记录，它们指定了根区域（由每个 **NS** 记录第一字段中的点号表示）的权威名称服务器名称及其地址。

文件中的注释行以分号开头。这些注释提示了你根名称服务器的位置。互联网有 13 个根名称服务器；大多数根服务器位于美国。对于任何名称服务器来说，此文件都是必需的，因为名称服务器必须能够访问至少一个根名称服务器。

## /var/named/localhost.zone 文件

/etc/named.conf 文件包含针对 localhost 区域的区域声明，该声明将区域文件指定为 *localhost.zone*。该文件位于 Fedora Core 系统的 /var/named 目录中。以下是 /var/named/localhost.zone 文件内容的列表：

```
$TTL	86400
$ORIGIN localhost.
@		1D IN SOA	@ root (
				42			: serial (d. adams)
				3H			: refresh
				15M			: retry
				1W			: expire
				1D )

	1D IN NS		@
	1D IN A		127.0.0.1
```

此区域文件以一个 `$TTL` 指令开始，将为后续未定义 TTL 的记录将默认 TTL 设置为一天（86400 秒）。接下来，`$ORIGIN` 指令将域名设置为 `localhost`。

在这两个指令之后，`/var/named/localhost.zone` 文件包含三个资源记录（RRs）：一个 SOA 记录、一个 NS 记录和一个 A 记录。SOA 和 NS 记录将 `localhost` 指定为该区域的权威主名称服务器。A 记录指定 `localhost` 的地址为 `127.0.0.1`。

## /var/named/named.local 文件

`/etc/named.conf` 文件中的第三个区域声明指定了一个名为 `0.0.127.in-addr.arpa` 的反向映射区域。对于此区域，区域文件是 `/var/named/named.local`，其中包含以下内容：

```
$TTL          86400
@       IN      SOA     localhost. root.localhost. (
                            1997022700        ; Serial
                            28800           ; Refresh
                            14400           ; Retry
                            3600000         ; Expire
                            86400 )         ; Minimum
          IN      NS      localhost.
1       IN      PTR     localhost.
```

SOA 和 NS 记录将 `localhost` 指定为主名称服务器。

![](img/9f89727199836b0f871f1745838aa8b2_717_0.png)

SOA 记录还显示 `root.localhost.` 作为该域的技术联系人的电子邮件地址。请注意，DNS 区域文件对电子邮件地址使用 `user.host.`（注意结尾的点号）格式。在向联系人发送任何电子邮件时，你需要将第一个点号替换为 @ 并移除末尾的点号。

## 缓存名称服务器：启动和测试

既然你已经研究了缓存名称服务器的配置文件，现在可以启动名称服务器并观察其运行情况。要启动名称服务器，请以 `root` 身份登录，并在终端窗口中输入以下命令：

```
service named start
```

此命令启动 `named` — 名称服务器守护进程。

![](img/9f89727199836b0f871f1745838aa8b2_717_1.png)

为了确保每次重启系统时 `named` 服务器都能启动，请以 `root` 身份登录并输入以下命令：

```
chkconfig --level 35 named on
```

## 692 配置 DNS

named 服务器在 /var/log/messages 文件中写入诊断日志消息。启动 named 后，你可以在文本编辑器中打开 /var/log/messages 来检查日志消息。如果没有来自 named 的错误消息，你可以继续测试名称服务器。

+   REMEMBER

在尝试使用缓存名称服务器之前，你必须指定该名称服务器作为你的主要名称服务器。为此，请确保 /etc/resolv.conf 文件的第一行如下所示：

```
nameserver 127.0.0.1
```

现在你可以使用 host 命令来测试名称服务器。例如，若要使用 localhost 上的缓存名称服务器查找 www.gao.gov 的 IP 地址，请输入以下命令：

```
host www.gao.gov localhost
```

以下是 host 命令产生的输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
www.gao.gov. has address 161.203.16.2
```

如输出所示，host 命令使用 localhost 作为 DNS 服务器，并返回了 www.gao.gov 的 IP 地址。如果你得到与此类似的输出，说明缓存名称服务器已启动并正在运行。

## 配置主名称服务器

配置主名称服务器的最佳方法是先配置一个缓存名称服务器（如前几节所述）。然后，为你希望该名称服务器作为主名称服务器的域添加主区域。例如，假设我想为 naba.net 域定义一个主名称服务器。以下是我配置该主名称服务器所经过的步骤（在我以 root 身份登录后）：

- 1. 向 /etc/named.conf 文件添加以下区域声明：

```
zone "naba.net" IN {
type master;
file "naba.zone";
};
zone "0.168.192.in-addr.arpa" IN {
type master;
file "0.168.192.zone";
};
```

