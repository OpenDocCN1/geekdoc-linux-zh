
options 部分用于指定 named 查找区域文件的目录（在文件的其他部分中指定的目录）。您将在本章后续的示例中了解如何使用的其他选项。

接下来，我们指示 named 接受来自经过身份验证的 rndc 的命令。我们包含密钥文件 /etc/rndc.key 以及 controls 部分，其中说明 rndc 从 localhost 连接并使用指定的密钥。（您可以在 allow 列表中指定多个 IP 地址，或使用如本章后面“管理 DNS 安全性”一节中所述的访问控制列表。）

. 区域告诉 named 有关根名称服务器的信息，其名称和地址位于 root.hints 文件中。该信息决定了最初查询哪个根名称服务器，尽管基于服务器的响应时间，这一决定通常会被修正。虽然可以通过 FTP 获取 hints 文件，但推荐的、对网络友好的保持同步方法是使用 dig。我们向一个根名称服务器（任何一个都行）请求 . 的 NS 记录，并直接使用 dig 的输出：

```
# dig @j.root-servers.net. ns > /var/named/root.hints
# cat /var/named/root.hints
;; <<> Dig 8.2 <<> @j.root-servers.net . ns
;; (1 server found)
;; res options: init recurs defnam dnsrch
;; got answer:
;; ->>HEADER<< opcode: QUERY, status: NOERROR, id: 6
;; flags: qr aa rd; QUERY: 1, ANSWER: 13, AUTHORITY: 0, ADDITIONAL: 13
;;
; QUERY SECTION:
;; , type = NS, class = IN
;
;
; ANSWER SECTION:
.			6d IN NS	H.ROOT-SERVERS.NET.
.			6d IN NS	C.ROOT-SERVERS.NET.
.			6d IN NS	G.ROOT-SERVERS.NET.
.			6d IN NS	F.ROOT-SERVERS.NET.
.			6d IN NS	B.ROOT-SERVERS.NET.
.			6d IN NS	J.ROOT-SERVERS.NET.
.			6d IN NS	K.ROOT-SERVERS.NET.
.			6d IN NS	L.ROOT-SERVERS.NET.
.			6d IN NS	M.ROOT-SERVERS.NET.
.			6d IN NS	I.ROOT-SERVERS.NET.
.			6d IN NS	E.ROOT-SERVERS.NET.
.			6d IN NS	D.ROOT-SERVERS.NET.
.			6d IN NS	A.ROOT-SERVERS.NET.
;
;; ADDITIONAL SECTION:
H.ROOT-SERVERS.NET.		5w6d16h IN A	128.63.2.53
C.ROOT-SERVERS.NET.		5w6d16h IN A	192.33.4.12
G.ROOT-SERVERS.NET.		5w6d16h IN A	192.112.36.4
F.ROOT-SERVERS.NET.      5w6d16h IN A    192.5.5.241
B.ROOT-SERVERS.NET.      5w6d16h IN A    128.9.0.107
J.ROOT-SERVERS.NET.      5w6d16h IN A    198.41.0.10
K.ROOT-SERVERS.NET.      193.0.14.129
L.ROOT-SERVERS.NET.      198.32.64.12
M.ROOT-SERVERS.NET.      202.12.27.33
I.ROOT-SERVERS.NET.      192.36.148.17
E.ROOT-SERVERS.NET.      192.203.230.10
D.ROOT-SERVERS.NET.      128.8.10.90
A.ROOT-SERVERS.NET.      198.41.0.4
;
;; Total query time: 4489 msec
;; FROM: lustre to SERVER: j.root-servers.net 198.41.0.10
;; WHEN: Mon Sep 10 04:18:26 2001
;; MSG SIZE  sent: 17  rcvd: 436
```

## 区域文件

named.conf 中的区域 0.0.127.in-addr.arpa 部分说明我们是该区域的主名称服务器，并且区域数据位于文件 127.0.0.中。在详细查看第一个真正的区域文件之前，先看一下 RR（资源记录）规格的一般格式：

```
name TTL class type data
```

这里，name 是与该记录关联的 DNS 名称。在区域文件中，以 . 结尾的名称是完全限定名称，而其他的名称是相对于区域名称的。在区域 example.com 中，foo 指的是完全限定名称 foo.example.com。特殊名称 @ 是区域本身名称的缩写形式。如果省略名称，则再次使用最后指定的名称。

TTL（生存时间）字段是一个数字，指定记录可以被缓存的时间。这在下一节关于 SOA 记录的讨论中会详细解释。如果省略此字段，则假设使用区域的默认 TTL。TTL 值通常以秒为单位，但您可以添加 m 表示分钟，h 表示小时，或 d 表示天。

BIND 支持不同的记录类，但就实际目的而言，唯一重要的类是 IN，代表互联网。如果没有明确指定类，则假设默认值为 IN；为了少打几个字，我们在编写的任何区域文件中都不提及类。

type 字段是强制性的，它指定了正在使用的 RR，例如 A、NS、MX 或 SOA。（这里我们只使用了现有的少数几种 RR。请查阅 DNS 标准以获取完整列表。）

data 字段（或字段）包含特定于此类型记录的数据。适当的语法将在我们依次检查每个 RR 的使用时介绍。

以下是 `0.0.127.in-addr.arpa` 区域的区域文件：

```
$TTL	2D
@	SOA	localhost. hostmaster.example.com. (
		2001090101	; Serial
		24h		; Refresh
		2h		; Retry
		3600000	; Expire (1000h)
		1h)		; Minimum TTL
	NS	localhost.
1	PTR	localhost.
```

应该开始每个区域文件的 $TTL 指令将该区域的默认最小生存时间设置为两天。这在下一节中将进一步讨论。

### 区域文件的 SOA 记录

区域文件中的第二行使用了您之前看到的特殊 @ 名称。在这里，它代表 `0.0.127.in-addr.arpa`，SOA（*Authority 的起点*）记录属于它。其余的字段（持续到右括号）包含 SOA 特定的数据。

SOA 记录中的第一个数据字段是域的主名称服务器的完全限定名称。第二个字段是区域联系人的电子邮件地址。用 . 替换 @ 符号可以将其写为 DNS 名称；foo@example.com 将写为 `foo.example.com`（注意末尾的 .）。

不要使用诸如 a.b@example.com 这样的地址，因为它写成 `a.b.example.com`，后来会被错误解释为 `a@b.example.com`。

![](img/34e72348d53ca54c2a1d9c871316691b_559_0.png)

接下来的几个数字字段指定该区域的各个特征。这些值必须正确配置，为此，您必须理解每个字段。如注释中所示（请注意，区域文件注释的语法与 `named.conf` 注释的相同语法不同），这些字段是序列号、刷新间隔、重试时间、过期期和最小 TTL。

序列号是 32 位量，可以保存 0 到 4,294,967,295（2^32 − 1）之间的值。每次更改区域文件时，必须递增序列号。此更改作为信号告知从服务器它们需要再次传输区域内容。惯例是以 `YYYYMMDDnn` 格式分配序列号，即变更日期和一个两位数的修订号（例如，2007060101）。对于同一天内的更改，只递增修订号。这合理假设您在一对内一个区域进行不超过 99 次更改。对于第二天的更改，日期变更，修订号从 01 重新开始。

刷新间隔指定从服务器应检查主数据是否更新的频率。这里设置为 24 小时，但如果区域经常更改，该值应更低。如果从服务器和主服务器都支持 DNS NOTIFY 机制，从服务器可以更快重新加载区域，大多数 DNS 软件都支持此机制。

重试时间仅在刷新时间过去后从服务器无法联系到主服务器时才相关。它指定在再次尝试之前应等待多长时间。（这里设置为两小时。）如果从服务器在过期期长度内持续无法联系到主服务器（通常是由于某种灾难性故障），它会丢弃已有的区域数据并停止回答该区域的查询。因此，过期期应足够长，以便主名称服务器能够恢复。已反复表明，一两周的值太短。一千小时（约六周）被认为是良好的默认值。

正如您前面阅读的，每个 RR 都有一个 TTL 字段，指定在必须再次咨询数据来源之前可以缓存该记录的时间。如果 RR 定义没有明确指定 TTL 值，则使用默认 TTL（由 $TTL 指令设置）代替。这使得单个 RR 可以根据需要覆盖默认 TTL 值。

SOA TTL，SOA 记录中的最后一个数字字段，用于确定负面响应（NXDOMAIN）应被缓存多长时间。（也就是说，如果查询导致 NXDOMAIN 响应，则缓存该事实的时间由 SOA TTL 指示。）旧版本的 BIND 使用 SOA 最小 TTL 来设置默认 TTL，但 BIND 9 不再这样做。推荐缓存友好的默认 TTL 为 2（两天）和 SOA TTL 为 1（一小时）。

之前使用的值对于不常更改的区域是良好的默认值。对于具有不同需求的区域，您可能需要稍作调整。在这种情况下，建议阅读网站 http://www.ripe.net/docs/ripe-203.html。

### 区域文件的其他记录

区域文件中的下一两行创建 NS 和 PTR 记录。NS 记录没有指定显式名称，因此使用最后的一个，即 SOA 记录的 @。因此，0.0.127.in-addr.arpa 的名称服务器被定义为 localhost。

PTR 记录的名称是 1，它变成 1.0.0.127.in-addr.arpa（这是将地址 127.0.0.1 写为 DNS 名称的方式）。当限定后，PTR 记录名称 1 变成 localhost。（稍后，当我们配置我们的名称服务器以成为真实域的权威服务器时，您会看到其他许多 RR 类型。）
