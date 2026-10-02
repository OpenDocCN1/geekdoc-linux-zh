
An MX 记录指定了代表特定域接收邮件的主机名称。以下是一个典型的 MX 记录：

```
Server7 IN MX 10 mailhub.lnbsoft.com.
```

该记录表示发往当前域中名为 server7 的主机的邮件会被发送到 mailhub.lnbsoft.com。（该主机称为邮件交换器。）数字 10 是优先级值。在具有不同优先级值的多个 MX 记录列表中，优先级值较低的记录会先尝试。

掌握了关于 RR 的这点信息后，你可以浏览缓存名称服务器的区域文件。

## 根区域文件

互联网有 13 个根名称服务器，其中大多数位于美国。关于这 13 个根名称服务器的信息位于 /etc/named.conf 文件中根区域的区域语句所引用的区域文件中。（根区域文件在 Fedora 中为 /var/named/named.ca，在 Debian 和 Ubuntu 中为 /etc/bind/db.root，在 SUSE 中为 /var/lib/named/root.hint。）以下列表显示了根区域文件：

```
; This file holds the information on root name servers needed to
; initialize cache of Internet domain name servers
; (e.g. reference this file in the "cache . <file>"
; configuration file of BIND domain name servers).
;
; This file is made available by InterNIC
; under anonymous FTP as
; file /domain/named.cache
; on server FTP.INTERNIC.NET
; -OR- RS.INTERNIC.NET
;
; last update: Jan 29, 2018
; related version of root zone: 2018012900
;
;
; formerly NS.INTERNIC.NET
;
. 3600000 IN NS A.ROOT-SERVERS.NET.
A.ROOT-SERVERS.NET. 3600000 A 198.41.0.4
;
; formerly NS1.ISI.EDU
;
. 3600000 NS B.ROOT-SERVERS.NET.
B.ROOT-SERVERS.NET. 3600000 A 192.228.79.201
;
; formerly C.PSI.NET
;
. 3600000 NS C.ROOT-SERVERS.NET.
C.ROOT-SERVERS.NET. 3600000 A 192.33.4.12
;
; formerly TERP.UMD.EDU
;
. 3600000 NS D.ROOT-SERVERS.NET.
D.ROOT-SERVERS.NET. 3600000 A 128.8.10.90
;
; formerly NS.NASA.GOV
;
. 3600000 NS E.ROOT-SERVERS.NET.
E.ROOT-SERVERS.NET. 3600000 A 192.203.230.10
;
; formerly NS.ISC.ORG
;
. 3600000 NS F.ROOT-SERVERS.NET.
F.ROOT-SERVERS.NET. 3600000 A 192.5.5.241
;
; formerly NS.NIC.DDN.MIL
;
. 3600000 NS G.ROOT-SERVERS.NET.
G.ROOT-SERVERS.NET. 3600000 A 192.112.36.4
;
; formerly AOS.ARL.ARMY.MIL
;
. 3600000 NS H.ROOT-SERVERS.NET.
H.ROOT-SERVERS.NET. 3600000 A 128.63.2.53
;
; formerly NIC.NORDU.NET
;
. 3600000 NS I.ROOT-SERVERS.NET.
I.ROOT-SERVERS.NET. 3600000 A 192.36.148.17
;
; operated by VeriSign, Inc.
;
. 3600000 NS J.ROOT-SERVERS.NET.
J.ROOT-SERVERS.NET. 3600000 A 192.58.128.30
;
; operated by RIPE NCC
;
. 3600000 NS K.ROOT-SERVERS.NET.
K.ROOT-SERVERS.NET. 3600000 A 193.0.14.129
;
; operated by ICANN
;
. 3600000 NS L.ROOT-SERVERS.NET.
L.ROOT-SERVERS.NET. 3600000 A 198.32.64.12
;
; operated by WIDE
;
. 3600000 NS M.ROOT-SERVERS.NET.
M.ROOT-SERVERS.NET. 3600000 A 202.12.27.33
; End of File
```

该文件包含 NS 和 A RR，用于指定根区域（由每个 NS 记录第一字段中的 . 表示）的授权名称服务器的名称及其地址。

文件中的注释行以分号开头。这些注释为你提供了关于 13 个根名称服务器位置的提示。任何名称服务器都需要此文件，因为名称服务器必须能够访问到至少一个根名称服务器。

## localhost.zone 文件

/etc/named.conf 文件包含一个针对 localhost 区域的区域语句，指定区域文件为 localhost.zone。该文件在 Fedora 中位于 /var/named 目录，在 SUSE 中位于 /var/local/named 目录，在 Debian 中位于 /etc/bind/db.local。以下是 localhost.zone 文件的内容：

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

该区域文件以 $TTL 指令开头，将后续未定义 TTL 的记录的默认 TTL 设置为一天（86400 秒）。接下来，$ORIGIN 指令将域名设置为 localhost。

在这两个指令之后，localhost.zone 文件包含三个 RR：一个 SOA 记录、一个 NS 记录和一个 A 记录。SOA 和 NS 记录指定 localhost 为该区域的主要授权名称服务器。A 记录将 localhost 的地址指定为 127.0.0.1。

## 127.0.0.1 的反向映射区域文件

/etc/named.conf 文件中的第三个区域语句指定了一个名为 0.0.127.in-addr.arpa 的反向映射区域。对于该区域，区域文件在 Fedora 中为 /var/named/named.localhost，在 SUSE 中为 /var/lib/named/127.0.0.zone，在 Debian 和 Ubuntu 中为 /etc/bind/db.127。该区域文件包含以下内容：

```
$TTL 86400
@ IN SOA localhost. root.localhost. (
1997022700 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
IN NS localhost.
1 IN PTR localhost.
```

SOA 和 NS 记录指定 localhost 为主要名称服务器。PTR 记录指定 localhost 为对应地址 127.0.0.1 的名称。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_293_0.png)

SOA 记录还显示 root.localhost. 作为域的技术联系人的电子邮件地址。DNS 区域文件使用 user.host.（注意末尾的句点）格式作为电子邮件地址。在向联系人发送任何电子邮件时，你必须将第一个句点替换为 @ 并删除最后的句点。

## 缓存名称服务器：启动和测试

在研究完缓存名称服务器的配置文件后，你可以启动名称服务器并观察其运行情况。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_293_1.png)

要启动名称服务器，请以 root 身份登录并在 Fedora 和 SUSE 中输入 /etc/init.d/named start。为了确保每次重新启动系统时 named 服务器都会启动，请在 Fedora 和 SUSE 中输入 chkconfig --level 35 named on。在 Debian 和 Ubuntu 中，输入 /etc/init.d/bind9 start 来启动 named 服务器。

named 服务器在 /var/log/messages 文件中写入诊断日志消息。启动 named 后，你可以通过在文本编辑器中打开 /var/log/messages 来检查日志消息。如果 named 没有错误消息，你就可以继续测试名称服务器。

![](img/322157d1fa7d965f05bcd68ed0ffc36b_293_2.png)

在尝试缓存名称服务器之前，你必须将其指定为你的主要名称服务器。为此，请确保 /etc/resolv.conf 文件中的第一行如下：

```
nameserver 127.0.0.1
```

现在你可以使用 host 来测试名称服务器。要使用 localhost 上的缓存名称服务器查找 www.gao.gov 的 IP 地址，请输入以下命令：

```
host www.gao.gov localhost
```

以下是 host 命令的输出结果：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
www.gao.gov. has address 161.203.16.77
```

如输出所示，host 命令使用 localhost 作为 DNS 服务器并返回 www.gao.gov 的 IP 地址。如果得到类似的输出，则表示缓存名称服务器已启动并运行。

## 配置主名称服务器

配置主名称服务器的最佳方法是先配置缓存名称服务器（如前几节所述）。然后为你希望该名称服务器成为主名称服务器的域添加主区域。假设你想为 server7.net 域定义一个主名称服务器。以下是你在 Fedora 系统上（以 root 身份登录后）配置该主名称服务器的步骤：

- 1. 在 /etc/named.conf 文件中添加以下区域语句：
- 2. 创建区域文件 /var/named/server7.zone 并在其中写入以下行：

```
zone "server7.net" IN {
type master;
file "server7.zone";
};
zone "0.168.192.in-addr.arpa" IN {
type master;
file "0.168.192.zone";
};
```

```
$TTL 86400
$ORIGIN server7.net.
@ 1D IN SOA @ root.server7.net (
100 ; serial
3H ; refresh
15M ; retry
1W ; expiry
1D ) ; minimum
1D IN NS @
1D IN A 192.168.0.7
wxp IN A 192.168.0.2
```

- 3. 创建区域文件 /var/named/0.168.192.zone 并在其中写入以下行：

```
$TTL 86400
; Remember zone name is: 0.168.192.in-addr.arpa
@ IN SOA server7.net. root.server7.net (
1 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
IN NS server7.net.
7 IN PTR server7.net.
2 IN PTR wxp.server7.net.
```

- 4. 要测试新配置，请使用以下命令重新启动 named 服务器：

```
sudo systemctl restart named
```

- 5. 使用 dig 或 host 查询 DNS 服务器。

以下是如何使用 host 检查在 localhost 上运行的 DNS 服务器上主机 wxp.server7.net 的地址：

```
host wxp.server7.net localhost
```

该命令的输出结果如下：

```
Using domain server:
Name: localhost
Address: 127.0.0.1#53
Aliases:
wxp.server7.net has address 192.168.0.2
```

如果你想使用 dig 检查 DNS 服务器，请输入以下命令：

```
dig @localhost wxp.server7.net
```

该 @localhost 部分指定了 dig 联系的 DNS 服务器。
