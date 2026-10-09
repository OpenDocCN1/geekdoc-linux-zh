
毫秒（ms）。往返时间（RTT）告诉你数据包从你的机器到路由器再返回所花费的时间。这是两台机器之间的延迟。

有时 RTT 可能会显示为星号 (*)，这表明远程机器正在运行但未响应。这是许多远程设备的正常反应。

如果某行中唯一的指示是一排星号，则表示无法到达远程系统。（具体来说，这意味着数据包没有返回到你的系统。）这可能表明存在问题，也可能是数据包被防火墙阻止了。

输出内容还可能包含多个消息符号，例如 !H 或 !N。这些符号的简要说明如下：

- !H 主机不可达。路由器没有通往目标系统的路由。
- !N 网络不可达。
- !P 协议不可达。
- !S 源路由失败。
- !F 需要分片。通常表示路由器配置错误。
- !X 通信在管理上被禁止。

从不同位置进行 traceroute 可能很有用。这可以提供关于网络流量路径和连接类型的更多信息。如果你想要从互联网上的不同位置进行 traceroute，请访问网站 www.traceroute.org。

```
% /usr/local/bin/traceroute www.yahoo.com
traceroute to www.yahoo.akadns.net (66.218.71.94): 1-30 hops, 38 byte packets
1 palexq4.hpl.external.hp.com (192.6.19.2) 0.976 ms 0.0 ms 0.976 ms
2 palgwb01-vbblpa.americas.hp.net (15.243.170.49) 0.977 ms 0.976 ms 1.95 ms
3 * * *
4 svi-edge-15.inet.qwest.net (65.115.64.25) 1.95 ms 1.95 ms 1.95 ms
5 svi-core-02.inet.qwest.net (205.171.14.150) 0.976 ms (ttl=250!) 1.95 ms
(ttl=250!) 1.95 ms (ttl=250!)
6 sjp-brdr-01.inet.qwest.net (205.171.214.46) 2.93 ms 2.93 ms 2.92 ms
7 so-2-0-0.edge1.SanJose1.Level3.net (209.245.146.229) 61.5 ms (ttl=247!)
61.5 ms (ttl=247!) 61.5 ms (ttl=247!)
8 so-5-0-0.gar2.SanJose1.Level3.net (209.244.3.141) 61.5 ms 60.5 ms 61.5 ms
9 ge-10-2.ipcolo3.SanJose1.Level3.net (64.159.2.169) 61.5 ms (ttl=248!)
61.5 ms (ttl=248!) 61.5 ms (ttl=248!)
10 unknown.Level3.net (64.152.69.30) 70.3 ms (ttl=244!) 69.3 ms (ttl=244!)
69.3 ms (ttl=244!)
11 w15.www.scd.yahoo.com (66.218.71.94) 72.2 ms (ttl=53!) 73.2 ms (ttl=53!)
72.2 ms (ttl=53!)
```

### telnet
telnet 实用程序是一个用于 TCP/IP 网络的终端仿真程序。客户端机器运行 telnet 程序，种类繁多。服务器运行 telnet 服务，允许客户端连接并通过 telnet 程序输入命令。从 telnet 会话中运行的命令与从控制台运行的命令效果相同。这允许你从远程位置控制服务器。

telnet 是一个不安全的程序，它以明文形式发送信息。当你连接到服务器时，会被提示输入用户名和密码，任何在网络上窃听的人都可以截取这些信息。因此，不推荐使用 telnet。建议考虑使用 SSH。

从 OSI 模型的角度来看，如果成功建立 telnet 会话，则意味着模型的所有七层都已 traversed（遍历）。这表明系统运行正常。

图 13-10 显示了一个名为 Styx 的计算机到一台名为 pythia 的计算机的 SSH 会话。在 Linux 操作系统中使用 SSH 的命令是 `ssh <远程计算机名称或IP地址>`。然后会被要求输入密码，该密码将以加密形式发送。在首次连接时，将为两个系统之间的连接生成一个 RSA 密钥。

![](img/37f079cee226b270f2e09b37a2e4a05d_377_0.png)

### nslookup
nslookup 实用程序用于查询域名服务器。请注意以下命令结果，nslookup 已被弃用。还有两个其他命令可用，dig 和 host。

```
# nslookup 216.109.118.70
Note: nslookup is deprecated and may be removed from future releases.
Consider using the 'dig' or 'host' programs instead. Run nslookup with
the '-silent' option to prevent this message from appearing.
Server:     130.160.46.26
Address:    130.160.46.26#53
Non-authoritative answer:
70.118.109.216.in-addr.arpa    name = p7.www.dcn.yahoo.com.
Authoritative answers can be found from:
```

### dig
dig（域名信息获取器）实用程序用于 DNS 查找。它用于排查名称服务器问题，是 nslookup 程序的替代方案。

dig 会查询你的默认系统解析器，或者你可以在命令行中列出特定服务器来查询它。例如，要使用 192.168.0.20 上的 DNS 来查找关于 yahoo.com 的信息，请使用以下命令：

`dig @192.168.0.20 www.yahoo.com`

dig 命令的结果包含大量信息：

- 在结果顶部，列出了 dig 的版本以及输入的命令选项。
- 接下来是状态信息。此列表显示 NOERROR 状态，表明在检索名称时没有发生错误。
- 接下来是 QUESTION（问题）和 ANSWER（答案）部分。QUESTION 部分显示了执行的查询。在以下列表中，查找了 A 记录（默认类型）。你可以指定 NS、PTR、MX 等作为域名查询类型（参见 RFC 1035）。
- 接下来是 AUTHORITY（权威）和 ADDITIONAL（附加）部分（未显示）。AUTHORITY 部分列出了该域名的主名称服务器和辅助名称服务器。ADDITIONAL 部分提供了这些名称服务器的 IP 地址。
- 最后一个部分显示有关查询的信息，例如查询执行时间、使用的服务器和端口以及返回的消息大小。

```
# dig www.yahoo.com

;; <<>> DiG 9.2.1 <<>> www.yahoo.com
;; global options: printcmd
;; Got answer:
;; ->>HEADER<- opcode: QUERY, status: NOERROR, id: 36344
;; flags: qr rd ra; QUERY: 1, ANSWER: 9, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.yahoo.com.                IN      A

;; ANSWER SECTION:
www.yahoo.com.      1799    IN  CNAME   www.yahoo.akadns.net.
www.yahoo.akadns.net. 29        IN  A       216.109.118.70
www.yahoo.akadns.net. 29        IN  A       216.109.118.68
www.yahoo.akadns.net. 29        IN  A       216.109.118.78
www.yahoo.akadns.net. 29        IN  A       216.109.118.65
www.yahoo.akadns.net. 29        IN  A       216.109.118.69
www.yahoo.akadns.net. 29        IN  A       216.109.118.77
www.yahoo.akadns.net. 29        IN  A       216.109.118.71
www.yahoo.akadns.net. 29        IN  A       216.109.118.74

;; Query time: 73 msec
;; SERVER: 192.168.0.20#53(192.168.0.20)
;; WHEN: Fri Nov 21 10:22:46 2003
;; MSG SIZE  rcvd: 193
```

### host
host 实用程序在给定主机名时返回 IP 地址或地址。其最简单的形式仅返回 IP 地址。

```
# host yahoo.com
yahoo.com has address 66.218.71.198
```

使用 `-t ns` 选项列出域名的权威名称服务器。

```
# host -t ns yahoo.com
yahoo.com name server ns1.yahoo.com.
yahoo.com name server ns2.yahoo.com.
yahoo.com name server ns3.yahoo.com.
yahoo.com name server ns4.yahoo.com.
yahoo.com name server ns5.yahoo.com.
```

使用 `-t mx` 选项列出域名的邮件服务器。对 yahoo.com 的此查询返回了三个 MX 记录。返回的优先级号表明 mx1 和 mx2 是首选邮件服务器，如果前两者不可用，则使用 mx4。

```
# host -t mx yahoo.com
yahoo.com mail is handled by 1 mx1.mail.yahoo.com.
yahoo.com mail is handled by 1 mx2.mail.yahoo.com.
yahoo.com mail is handled by 5 mx4.mail.yahoo.com.
```

`-a` 选项返回主机所有可用的字段。使用带有此选项的 host 命令针对你自己的服务器，以确保其提供所需的所有信息。

```
# host -a yahoo.com
Trying "yahoo.com"
; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 22067
; flags: qr aa; QUERY: 1, ANSWER: 12, AUTHORITY: 5, ADDITIONAL: 7

; QUESTION SECTION:
yahoo.com.			IN ANY

; ANSWER SECTION:
yahoo.com.		1800 IN A 66.218.71.198
yahoo.com.		7200 IN MX 1 mx1.mail.yahoo.com.
yahoo.com.		7200 IN MX 1 mx2.mail.yahoo.com.
yahoo.com.		7200 IN MX 5 mx4.mail.yahoo.com.
yahoo.com.		1800 IN LOC 37 23 30.900 N 121 59 19.000 W 7.00m 100m 100m 2m
yahoo.com.		1800 IN RP hostmaster.yahoo-inc.com.
contact.yahoo.com.
yahoo.com.		172800 IN NS ns1.yahoo.com.
yahoo.com.		172800 IN NS ns2.yahoo.com.
yahoo.com.		172800 IN NS ns3.yahoo.com.
yahoo.com.		172800 IN NS ns4.yahoo.com.
yahoo.com.		172800 IN NS ns5.yahoo.com.
yahoo.com.		1800 IN SOA hidden-master.yahoo.com.
 hostmaster.yahoo-inc.com. 2003112104 900 300 604800 600

; AUTHORITY SECTION:
yahoo.com.		172800 IN NS ns1.yahoo.com.
yahoo.com.		172800 IN NS ns2.yahoo.com.
yahoo.com.		172800 IN NS ns3.yahoo.com.
yahoo.com.		172800 IN NS ns4.yahoo.com.
yahoo.com.		172800 IN NS ns5.yahoo.com.

; ADDITIONAL SECTION:
mx1.mail.yahoo.com. 1800 IN A 64.156.215.5
mx1.mail.yahoo.com. 1800 IN A 64.156.215.6
mx1.mail.yahoo.com. 1800 IN A 64.157.4.78
mx1.mail.yahoo.com. 1800 IN A 64.157.4.79
mx1.mail.yahoo.com. 1800 IN A 64.156.215.7
ns1.yahoo.com.		172800 IN A 66.218.71.63
ns2.yahoo.com.		172800 IN A 66.163.169.170

Received 503 bytes from 130.160.46.26#53 in 49 ms
```

### netstat
netstat 命令打印有关 Linux 网络系统的信息。显示的信息由第一个命令行参数控制。可用参数如下所示：

- **（无）** 无参数时，显示开放套接字的列表。
- **--route** 显示内核路由表。
- **--groups** 显示多播组成员信息。
- **--interface[=iface]** 显示所有网络接口或指定接口的表格。
- **--masquerade** 显示伪装连接的列表。
- **--statistics** 显示每个协议的摘要统计信息。

