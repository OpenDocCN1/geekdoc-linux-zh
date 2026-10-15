
```
$ dig @ns3.vsn1.com. 66.109.200.203.in-addr.arpa PTR +norec

; <<>> DiG 9.2.1 <<>> @ns3.vsn1.com. 66.109.200.203.in-addr.arpa PTR +norec
; global options: printcmd
; Got answer:
; ->>HEADER<- opcode: QUERY, status: NXDOMAIN, id: 37848
; flags: qr aa ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 0

; QUESTION SECTION:
;66.109.200.203.in-addr.arpa.    IN    PTR

; AUTHORITY SECTION:
200.203.in-addr.arpa.    86400   IN      SOA     dns.vsn1.net.in.
helpdesk.giagmbm01.vsn1.net.in. 200001059 86400 7200 2592000 345600

; Query time: 259 msec
; SERVER: 203.197.12.42#53(ns3.vsn1.com.)
; WHEN: Wed Sep  4 21:19:16 2002
; MSG SIZE  rcvd: 114
```

## 这里发生了什么？

在之前的响应中，状态始终是 `NOERROR`，但这次响应的状态是 `NXDOMAIN`（域名不存在），并且标志部分包含 `aa`（权威应答）标志。这意味着我们查找的名称已知不存在。相比之下，来自根名称服务器的响应没有设置 `aa` 标志，而是说“我们不知道这个名称。去问别人吧。”来自 `ns3.vsn1.com` 的权威应答表示“我知道这个名称不存在，你可以停止查找了。”

`vsn1.net.in` 的管理员显然没有费心为他们拨号 IP 地址池设置 PTR 记录。如果他们设置了，响应将看起来像我们之前看到的那些，并且会包含一条 PTR 记录。事实上，响应列出了该区域的 SOA 记录，其中包含域联系人的电子邮件地址 `helpdesk@giagmbm01.vsn1.net.in`，如果我们想要抱怨反向解析故障，可以联系他们。

## 解析器学到了什么？

根据我们目前为止所做的工作，我们拥有了 `com` 顶级域（TLD）权威名称服务器的名称和地址列表。未来，如果我们被要求解析，比如说 `www.samspublishing.com`，我们可以直接从一开始将查询定向到 `gld-servers.net`，而不是在根服务器上浪费一次查询。然而，NS 记录有一个过期时间（也称为生存时间，或 `TTL`，你可以在本章稍后的“区域文件”中了解它），为 `2d`，这意味着信息仅在两天内保证准确。这种更新滞后时间就是你看到通告称 DNS 更改可能需要几天时间才能在整个互联网上传播的原因。

同样，我们知道 `ibm.com` 的权威名称服务器，用于接下来两天内涉及 `ibm.com` 的查询。例如，当用户在 IBM 网页上点击链接时，Web 浏览器可能会请求 `commerce.ibm.com` 的 IP 地址。我们可以再次询问 `NS.WATSON.ibm.com` 来节省两次查询。当然，我们的缓存中还有 `www.ibm.com` 的四个 A 记录，如果浏览器再次请求解析该名称，我们可以返回其中一个。

所有这些信息（包括从反向解析过程中获取的信息）都可以由你的计算机缓存直至过期，并用于加快后续查询。

你还学到了一些解析器无法记忆或使用的信息。例如，从名称可以猜测，IBM 的 DNS 管理员按照建议，将其 DNS 服务委托给了在地理位置和网络上都较远服务器。你可以看到 IBM 在同一网络上运行四个 Web 服务器——或许是为了优雅地处理负载。我们知道 VSNL（一家大型 ISP）的 DNS 管理员并不像他们所能做到的那样尽责，因为他们整个域只有两个名称服务器，并且没有正确的反向映射。

DNS 令人无尽着迷，花几个小时玩弄 `dig` 会得到很好的回报。通过这样做，你可以学到一些关于 DNS 的有趣知识，并熟悉 `dig` 的查询和响应，这将非常有助于调试你自己的 DNS 配置问题。

## 使用 DNS 工具

Fedora 包含许多允许你操作 DNS 的标准工具。这些工具位于 `bind-utils` 和 `whois` 软件包中，具有不需要 DNS 管理员技能的日常用途。如果你想知道哪个域名属于某个 IP 地址，或者反过来，这些工具就是用来追踪这些信息的地方。正向查找是将名称映射到 IP 地址；反向查找是将地址映射到名称。

以下是你将使用的工具：

- `dig`（域名信息抓取器）
- `host`
- `nslookup`
- `whois`

以下各节简要描述这些工具并提供使用示例。

### dig

`dig`（Domain Information Groper，域名信息抓取器）是一个命令行实用程序，用于向 DNS 名称服务器发出查询。默认情况下，`dig` 使用 `/etc/resolv.conf` 中列出的名称服务器，并执行 `NS`（名称服务器）查询。反向查找通过 `-x` 参数完成，默认执行 `A`（地址）查询。

以下是使用 `dig` 进行正向查找的示例：

```
$ dig www.pearson.com

; <<>> DiG 9.2.2 <<>> www.pearson.com
;; global options: printcmd
;; Got answer:
;; ->HEADER<- opcode: QUERY, status: NOERROR, id: 59962
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 2
```

;; 问题部分：

;www.pearson.com. IN A

;; 回答部分：

www.pearson.com. 86400 IN A 165.193.130.83

;; 授权部分：

pearson.com. 86400 IN NS ns1-p.dns.pipex.net.

pearson.com. 86400 IN NS ns.pearson.com.

pearson.com. 86400 IN NS ns0-p.dns.pipex.net.

;; 附加部分：

ns0-p.dns.pipex.net. 66542 IN A 158.43.129.80

ns1-p.dns.pipex.net. 66542 IN A 158.43.193.80

;; 查询时间：294 毫秒

;; 服务器：64.83.0.10#53(64.83.0.10)

;; 时间：2003 年 9 月 1 日 星期一 16:42:00

;; 接收消息大小：151

使用 `dig` 进行反向查找：

```
$ dig -x 165.193.130.83

;; DiG 9.2.2 <<>> -x 165.193.130.83

;; 全局选项：printcmd

;; 获取答案：

;; ->>HEADER<<- 操作码：QUERY，状态：NOERROR，ID：63402

;; 标志：qr rd ra；查询：1，回答：1，授权：2，附加：0

;; 问题部分：

;83.130.193.165.in-addr.arpa. IN PTR

;; 回答部分：

83.130.193.165.in-addr.arpa. 43200 IN PTR prs-sun-106-nyeh-peshr-hme0-4.digisle.net.

;; 授权部分：

130.193.165.in-addr.arpa. 43200 IN NS ns.digisle.net.

130.193.165.in-addr.arpa. 43200 IN NS ns1.digisle.net.

;; 查询时间：41 毫秒

;; 服务器：64.83.0.10#53(64.83.0.10)

;; 时间：2003 年 9 月 1 日 星期一 16:42:21

;; 接收消息大小：135
```

## host

`host` 是一个命令行工具，它通过查询 DNS 名称服务器来执行正向和反向查找，功能与 `dig` 类似。

以下是使用 `host` 进行正向查找的示例：

```
$ host www.pearson.com

www.pearson.com has address 165.193.130.83
```

以下是使用 `host` 进行反向查找的示例：

```
$ host 165.193.130.83

83.130.193.165.in-addr.arpa domain name pointer

prs-sun-106-nyeh-peshr-hme0-4.digisle.net.
```

## nslookup

`nslookup` 是一个命令行工具，可以用于以交互或非交互方式查询 DNS 名称服务器。请注意，`nslookup` 已经过时，建议改用 `dig`。

以下是使用 `nslookup` 进行正向查找的示例：
