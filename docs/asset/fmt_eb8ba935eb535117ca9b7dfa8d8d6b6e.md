
文件需要三个部分：

- Server 部分——定义名称服务器 (`localhost`) 以及与其通信时使用的密钥 (`rndc`)
- Options 部分——设置合理的默认值，因为文件必须列出服务器
- Key 部分——包含我们已经创建的密钥 `/etc/rndc.key`

如果你需要它，`rndc(8)` 和 `rndc.conf(5)` 手册页包含更多信息。

# named.conf

我们从类似这样的文件开始：

``` 
options {

    # 区域文件存放的位置。

    directory "/var/named";

};
```

``` 
# 允许 localhost 运行 rndc 的命令。

controls { inet 127.0.0.1 allow { localhost; } keys { all }; };
```

`options` 部分指定了 `named` 查找文件的目录。此信息决定了最初查询哪个服务器。虽然 `hints` 文件可以通过 FTP 获取，但保持同步的 {友好方法是使用 `dig`。我们询问根服务器（无论哪一个）并直接使用 `dig` 输出：

``` 
# dig @root-servers.net > /var/named/root.hints

# cat /var/named/root.hints

DIG 8.2 @root-servers.net .

;; 1 server found.

;; options: recursion

;; got answer:

;; ->HEADER opcode: QUERY, status: NOERROR, id: 6

;; flags: qr aa; QUERY: 1, AUTHORITY: 0, ADDITIONAL: 13

;; QUERY SECTION: { , type = NS, class = IN
```

``` 
; ANSWER SECTION

IN NS      ROOT-SERVERS.NET.

IN NS      C.ROOT-SERVERS.NET.

IN NS      G.ROOT-SERVERS.NET.
```

``` 
IN NS      F-SERVERS.NET.

IN NS      B-SERVERS.NET.

IN NS      J-SERVERS.NET.

IN NS      K-SERVERS.NET.

IN NS      L-SERVERS.NET.

IN NS      M-SERVERS.NET.

IN NS      I-SERVERS.NET.

IN NS      E-SERVERS.NET.

IN NS      A-SERVERS.NET.
```

;; ADDITIONAL SECTION:
H.ROOT-SERVERS.NET A 128.63.2.53
C.ROOT-SERVERS.NET A 192.33.4.12
G.ROOT-SERVERS.NET A 192.11.36.4
F.ROOT-SERVERS.NET A 192.5.54.21
B.ROOT-SERVERS.NET A 128.9.0.10
J.ROOT-SERVERS.NET A 198.41.0.10
K.ROOT-SERVERS.NET A 193.0.14.129
L.ROOT-SERVERS.NET A 198.32.64.12
M.ROOT-SERVERS.NET A 202.12.27.33
I.ROOT-SERVERS.NET A 192.36.148.17
E.ROOT-SERVERS.NET A 192.203.230.10
D.ROOT-SERVERS.NET A 128.8.10.90
A.ROOT-SERVERS.NET A 198.1.0.4

;; Total query time: 4489 msec
;; lustre to SERVER: j.root-servers.net 198.41.0.10
;; WHEN: Mon Sep 10 04:18:26 2001
;; MSG SIZE sent: 177 recd: 436

# 区域文件

`0.0.127-in-addr.arpa` 区域表示我们是该区域的主服务器，区域数据在 `127.0.0` 文件中。在检查第一个真实的区域文件细节之前，请查看资源记录规范的通用格式：

`name TTL class type data`

这里

`img/c4a0ea5ab3561ff33a8da88887702720_756_0.png`

`TTL`（生存时间）字段是一个数字，指定了记录可以缓存的时间。在下一节对 `SOA` 记录的讨论中，将对其进行更详细的解释。如果省略了此字段，则假设该区域使用默认 `TTL`。`TTL` 值通常以秒为单位，你可以后接 `m` 表示分钟、`h` 表示小时或 `d` 表示天。

`BIND` 支持记录类，但对于所有实际用途而言，唯一重要的类是 `IN`（互联网）。如果未指定类，则假设默认值为 `IN`；为了少写一些字符，在我们编写的任何区域文件中不要提及该类。

数据字段（或多个字段）包含特定于此类类型记录的数据。在我们检查每个 `RR`（资源记录）的使用时，将介绍适当的语法。

以下是 `0.0.127.in-addr.arpa` 区域的区域文件：

| TTL 2D | |
| --- | --- |
| @ SOA | localhost.hostmaster.example.com. (
| 2001090101 ; Serial |
| 24h ; Refresh |
| 2h ; Retry |
| 3600000 ; Expire (1000h) |
| 1h) ; Minimum TTL |
| NS localhost. |
| PTR localhost.| |

每个区域文件都应该包含的 `TTL` 指令将该区域的默认最小生存时间设置为两天。这将在下一节中进一步讨论。

## 区域文件的 SOA 记录

区域文件的第二行使用了你之前看到的特殊名称 `@`。在这里，它代表 `0.0.127.in-addr.arpa`，即 `SOA`（起始起始标记）记录所属的区域。其余的字段（一直到结束括号为止）包含 `SOA` 特有的数据。

`SOA` 记录中的第一个数据字段是该域主服务器的完全限定域名。第二个字段是该区域联系人的电子邮件地址。它通过将 `@` 符号替换为 `.` 来写成 `DNS` {；例如，`foo@example.com` 将被写为 `foo@example.com.`（注意末尾的点号）。

不要使用像 `a.b@example.com` 这样的地址，因为它会被写成 `a.b.example.com`，稍后会被误解为 `a@b.example.com`。

## 使用 BIND 为真实域名提供 DNS

确保发送到 `SOA` 字段中指定的联系邮箱地址的邮件被频繁阅读是非常，因为它被用于报告 `DNS` 设置问题和其他潜在有用信息。

接下来的几个数值字段指定了该区域的各种特性。这些值必须正确配置，为了做到这一点，你必须理解每个字段。如注释所示（注意区域重载文件的注释与 `named` 的注释语法不同），这些字段分别是序列号、刷新间隔、重试时间、过期期和最小 `TTL`。

序列号是 32 位数值，可以存储 0 到 4,294,967,295 ($2^{32}-1$) 之间的值。每当区域数据发生变化时，都必须增加序列号。此更改作为发送给从服务器的信号，告知它们需要传输区域数据的内容。惯例是使用 `YYYYMMDD` 格式分配序列号；即日期和两位数的修订号（例如，`2001090101`）。对于同一天内进行的更改，仅修改修订号。这合理地假设你一天对一个区域的修改不超过 99 次。对于第二天的更改，更改日期且修订号从 01 开始。

刷新间隔指定了从服务器应如何检查主数据是否已更新。它被设置为 24 小时，但如果区域经常变化，应该降低该值。如果从服务器和主服务器都支持 `DNS NOTIFY` 机制（`DNS` 软件支持），从服务器可以更早地重新加载主数据。

重试时间仅当从服务器在刷新时间结束后未能连接主服务器时有效。它指定了在尝试尝试之前应该等待多久（这里设置为两小时）。如果从服务器在过期期范围内无法连接主服务器（通常是因为灾难性故障），它将丢弃已有的区域数据并停止回答该区域的查询。因此，过期期应该足够长以便主名称服务器恢复。已反复证明，一或两周的值太短了。一千小时（约六周）被认为是良好的默认值。

如前所述，每个 `RR` 都有一个 `TTL` 字段，指定了它可以缓存多久。如果 `RR` 没有显式指定 `TTL` 值，则使用默认 `TTL`（由 `SOA` 指令设置）。这允许单个 `RR` 覆盖默认 `TTL`。`SOA TTL` 是 `SOA` 记录中的最后一个字段，用于确定负面响应（`NXDOMAIN`）应该缓存多久。也就是说，如果查询导致 `NXDOMAIN` 响应，它将按照 `SOA TTL` 指定的时间进行缓存。旧版本的 `BIND` 使用 `SOA` 最小 `TTL` 来设置默认 `TTL`，但 `BIND 9` 不再这样做。为了缓存的友好性，建议默认 `TTL` 为两天，`SOA TTL` 为一小时。
