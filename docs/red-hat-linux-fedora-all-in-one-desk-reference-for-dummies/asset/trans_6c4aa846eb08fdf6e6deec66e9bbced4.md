
## /var/named/named.ca 文件

关于根域名服务器的信息位于 /var/named/named.ca 文件中，如 /etc/named.conf 文件中根区域的区域语句所指定。以下列表显示了来自 Red Hat Linux 系统的 /var/named/named.ca 文件：

```
: This file holds the information on root name servers needed to
: initialize cache of Internet domain name servers
: (e.g. reference this file in the "cache . <file>*"
: configuration file of BIND domain name servers).
:
: This file is made available by InterNIC
: under anonymous FTP as
: file /domain/named.cache
: on server FTP.INTERNIC.NET
:
: last update: Nov 5, 2002
: related version of root zone: 2002110501
:
:
: formerly NS.INTERNIC.NET
:
A.ROOT-SERVERS.NET. 3600000 IN NS A.ROOT-SERVERS.NET.
3600000 IN A 198.41.0.4
: formerly NS1.ISI.EDU
:
B.ROOT-SERVERS.NET. 3600000 IN NS B.ROOT-SERVERS.NET.
3600000 IN A 128.9.0.107
: formerly C.PSI.NET
:
C.ROOT-SERVERS.NET. 3600000 IN NS C.ROOT-SERVERS.NET.
3600000 IN A 192.33.4.12
: formerly TERP.UMD.EDU
:
D.ROOT-SERVERS.NET. 3600000 IN NS D.ROOT-SERVERS.NET.
3600000 IN A 128.8.10.90
: formerly NS.NASA.GOV
:
E.ROOT-SERVERS.NET. 3600000 IN NS E.ROOT-SERVERS.NET.
3600000 IN A 192.203.230.10
: formerly NS.ISC.ORG
:
F.ROOT-SERVERS.NET. 3600000 IN NS F.ROOT-SERVERS.NET.
3600000 IN A 192.5.5.241
: formerly NS.NIC.DDN.MIL
:
G.ROOT-SERVERS.NET. 3600000 IN NS G.ROOT-SERVERS.NET.
3600000 IN A 192.112.36.4
: formerly AOS.ARL.ARMY.MIL
:
H.ROOT-SERVERS.NET. 3600000 IN NS H.ROOT-SERVERS.NET.
3600000 IN A 128.63.2.53
```
```
: formerly NIC.NOROU.NET
:
I.ROOT-SERVERS.NET. 3600000 IN NS I.ROOT-SERVERS.NET.
3600000 IN A 192.36.148.17
: operated by VeriSign, Inc.
:
J.ROOT-SERVERS.NET. 3600000 IN NS J.ROOT-SERVERS.NET.
3600000 IN A 192.58.128.30
: housed in LINX, operated by RIPE NCC
:
K.ROOT-SERVERS.NET. 3600000 IN NS K.ROOT-SERVERS.NET.
3600000 IN A 193.0.14.129
: operated by IANA
:
L.ROOT-SERVERS.NET. 3600000 IN NS L.ROOT-SERVERS.NET.
3600000 IN A 198.32.64.12
: housed in Japan, operated by WIDE
:
M.ROOT-SERVERS.NET. 3600000 IN NS M.ROOT-SERVERS.NET.
3600000 IN A 202.12.27.33
: End of File
```

此文件包含 NS 和 A 资源记录，指定根区域（由每个 NS 记录第一字段中的“.”表示）的授权名称服务器的名称及其地址。

文件中的注释行以分号开头。这些注释为您提供了有关根名称服务器位置的提示。互联网有 13 个根名称服务器；大多数根服务器位于美国。任何名称服务器都需要此文件，因为名称服务器必须能够访问至少一个根名称服务器。

## /var/named/localhost.zone 文件

/etc/named.conf 文件包含一个用于 localhost 区域的区域语句，该语句指定区域文件为 localhost.zone。该文件位于您的 Red Hat Linux 系统的 /var/named 目录中。以下是 /var/named/localhost.zone 文件包含的内容列表：

```
$TTL 86400
$ORIGIN localhost.
@ 1D IN SOA @ root (
42 ; serial (d. adams)
3H ; refresh
15M ; retry
1W ; expiry
1D ) ; minimum

1D IN NS @
1D IN A 127.0.0.1
```

此区域文件以 $TTL 指令开头，将后续未定义 TTL 的记录的默认 TTL 设置为一天（86,400 秒）。接下来，$ORIGIN 指令将域名设置为 localhost。

在这两个指令之后，/var/named/localhost.zone 文件包含三个资源记录（RR）：一个 SOA 记录、一个 NS 记录和一个 A 记录。SOA 和 NS 记录指定 localhost 为该区域的主要授权名称服务器。A 记录指定 localhost 的地址为 127.0.0.1。

## /var/named/named.local 文件

/etc/named.conf 文件中的第三个区域语句指定了一个名为 0.0.127.in-addr.arpa 的反向映射区域。对于此区域，区域文件为 /var/named/named.local，其中包含以下内容：

```
$TTL      86400
@         IN      SOA     localhost.  root.localhost.  (
                                 1997022700  : Serial
                                 28800      : Refresh
                                 14400      : Retry
                                 3600000    : Expire
                                 86400 )    : Minimum
          IN      NS      localhost.
1         IN      PTR     localhost.
```

SOA 和 NS 记录指定 localhost 为主要名称服务器。

SOA 记录还显示 root.localhost. 作为域的技术联系人的电子邮件地址。请注意，DNS 区域文件使用 user.host.（注意末尾的句点）格式作为电子邮件地址。在向联系人发送任何电子邮件时，您必须将第一个点替换为 @ 并删除最后的点。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_712_0.png)

## 缓存名称服务器：启动和测试

现在您已经研究了缓存名称服务器的配置文件，您可以启动名称服务器并查看其运行情况。要启动名称服务器，请以 root 身份登录并在终端窗口中输入以下命令：

```
service named start
```

此命令启动 named — 名称服务器守护进程。

为确保每次重新启动系统时 named 服务器都会启动，请以 root 身份登录时输入以下命令：

```
chkconfig --level 35 named on
```

![](img/a7eec43a54473e95dc5ea333fecf1bd7_712_1.png)

![](img/a7eec43a54473e95dc5ea333fecf1bd7_713_0.png)

named 服务器在 /var/log/messages 文件中写入诊断日志消息。启动 named 后，您可以通过在文本编辑器中打开 /var/log/messages 来检查日志消息。如果 named 没有错误消息，您可以继续测试名称服务器。

在尝试缓存名称服务器之前，您必须将其指定为您的主要名称服务器。为此，请确保 /etc/resolv.conf 文件中的第一行如下：

```
nameserver 127.0.0.1
```

现在您可以使用 host 来测试名称服务器。例如，要使用 localhost 上的缓存名称服务器查找 www.gao.gov 的 IP 地址，请输入以下命令：

```
host www.gao.gov localhost
```

以下是 host 命令的输出结果：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
www.gao.gov. has address 161.203.16.2
```

如输出所示，host 命令使用 localhost 作为 DNS 服务器并返回 www.gao.gov 的 IP 地址。如果您得到类似的输出，则缓存名称服务器已启动并运行。

## 配置主名称服务器

配置主名称服务器的最佳方法是先配置缓存名称服务器（如前几节所述）。然后，为您希望其成为主名称服务器的域添加主区域。例如，假设我想为 naba.net 域定义一个主名称服务器。以下是我在以 root 身份登录后配置该主名称服务器的步骤：

- 1. 向 /etc/named.conf 文件添加以下区域语句：
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
- 2. 创建区域文件 /var/named/naba.zone，其中包含以下行：
```
$TTL 86400
$ORIGIN naba.net.
@		IN SOA	@ root.naba.net (
		100		; serial
		3H		; refresh
		15M		; retry
		1W		; expiry
		1D )		; minimum

		IN NS	@
		IN A	192.168.0.7

wxp	IN	A	192.168.0.2
```
- 3. 创建区域文件 /var/named/0.168.192.zone，其中包含以下行：
```
$TTL 86400
; Remember zone name is: 0.168.192.in-addr.arpa
@		IN	SOA	naba.net. root.naba.net (
		1		; Serial
		28800	; Refresh
		14400	; Retry
		3600000	; Expire
		86400 ); Minimum

		IN	NS	naba.net.

7		IN	PTR	naba.net.
2		IN	PTR	wxp.naba.net.
```
- 4. 要测试新配置，请使用以下命令重新启动 named 服务器：
```
service named restart
```
- 5. 使用 dig 或 host 查询 DNS 服务器。

例如，以下是我如何使用 host 检查在 localhost 上运行的 DNS 服务器上主机 wxp.naba.net 的地址：

```
host wxp.naba.net localhost
```

此命令产生以下输出：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:

wxp.naba.net has address 192.168.0.2
```

如果您想使用 dig 检查 DNS 服务器，请输入以下命令：

```
dig @localhost wxp.naba.net
```

该 @localhost 部分指定 dig 应联系的 DNS 服务器。
