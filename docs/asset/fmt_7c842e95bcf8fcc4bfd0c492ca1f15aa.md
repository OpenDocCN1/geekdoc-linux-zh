
# 第 14 章 管理 DNS

你还学习了一些解析器无法记忆或使用的内容。例如，你可以从名称推测出来，IBM 的 DNS 管理员已将 DNS 服务委托给了地理位置和网络位置都非常遥远的服务器。你可以看到 IBM 在同一网络上运行了四台服务器——也许是为了平滑地处理负载。我们知道 VSNL（一家大型 ISP）的 DNS 管理员没有想象中那么尽职责，因为他们整个域名只有两台服务器，并且没有正确的反向映射。

DNS 具有无限的魅力，花几个小时玩玩 `dig` 是非常有收获的。通过这种方式，你可以学习到关于 DNS 的一些有趣事情，并熟悉 `dig` 查询和响应，这在调试你的 DNS 设置问题时将证明是非常有用的。

## 属于自己的域名和第三方 DNS

你可以拥有自己的域名并为它提供第三方 DNS 服务，这意味着你不需要为自己配置和管理 DNS 解析器。你甚至可以在没有邮件服务器的情况下为你的域名设置一个邮箱地址。

Fred Atkinson 编写了一份出色的 HOWTO，概述了为你的域名提供第三方 DNS 服务需要遵循的步骤。该文档专为业余无线电操作员（也称为“火腿”）编写，地址为 http://www.mishmash.com/hamdomain/。

以下是为域名提供第三方 DNS 服务涉及的主要任务总结：

- 注册并支付唯一的域名。现在有几家公司提供这些名称的注册，可以货挑选最合理的价格，并在使用之前对该公司进行一些 Google 回溯检查。
- 使用第三方 DNS 提供商提供 DNS 服务。Atkinson 建议使用 ZoneEdit (`www.maximizhout.com`)，我也使用 ZoneEdit，尽管可能还有其他免费提供商，并提供了使用该服务的详细步骤。ZoneEdit 还提供邮件转发服务，发往你@your.domain 的邮件将转发到你的常规 ISP 邮件账户。ZoneEdit 还允许你使用 DynamicDNS，这让你能够在动态分配的 IP（来自电缆或调制拨号提供商）上运行服务器，同时你仍然有 DNS 服务器可以定位。ZoneEdit 还可以为你提供启动页面空间，或将请求转发到已经建立的具有复杂地址页面。
- 返回你的域名注册商，告诉它哪些名称服务器将成为你域名的权威服务器。

一旦你完成了上述任务，信息大约需要三天时间在互联网上生效。有趣的是，大多数使用 Atkinson 网站信息的人并没有像他意图的那样建立无线电呼号域名；尽管如此，他的努力非常受感谢。

## DNS 工具概览

虽然 DNS 工具将在本书的后面详细介绍，但我们在这里提供可用工具的简要概述，供那些不需要深入了解 DNS 奥秘和秘密的读者参考。这些工具存在于 `bind-utils` 软件包中，其日常用途不需要 DNS 管理员级别的技能。如果你想知道哪个域名属于哪个 IP 地址，或者反之，这些就是你追溯该查询的工具。正向查询是将名称映射到 IP 地址；反向查询是将地址映射到名称。

以下是你将用到的工具：

- `dig` (域名信息抓取器)
- `host`
- `nslookup`
- `whois`

接下来的章节将简要描述这些工具并提供它们的使用示例。

## dig

一种命令行工具，Domain Information Groper 会查询 DNS 名称服务器。默认情况下，`dig` 使用 `/etc/resolv.conf` 中列出的名称服务器并执行 NS（名称服务器）查询。反向查询通过 `-x` 参数完成，并执行默认的 A（地址）查询。

下面是一个使用 `dig` 进行正向查询的示例：

```
$ dig www.pearson.com
```

```
; <<>> DIG 9.2.2 <<>> www.pearson.com

;; global options: printcmd

;; Got answer:

;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 59962

;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 2

;; QUESTION SECTION:

www.pearson.com.

               IN      A

;; ANSWER SECTION:

www.pearson.com.      86400  IN      165.193.130.83
```

```
; AUTHORITY SECTION:

pearson.com.      86400 IN NS ns1-p.dns.pipex.net.

pearson.com.      86400 IN NS ns.pearson.com.

pearson.com.      86400 IN NS ns0-p.dns.pipex.net.
```

```
; ADDITIONAL SECTION:

s0-p.dns.pypex.net.  66542 IN A 158.43.129.80

ns1-p.dns.pypex.net. 66542 IN A 158.43.193.80
```

```
; Query time: 294 msec

;; SERVER: 64.83.0.10#53(64.83.0.10)

;; WHEN: Mon Sep 1 16:42:00 2003

;; MSG SIZE rcvd: 151
```

使用 `dig` 进行反向查询：

```
$ dig -x 165.193.130.83
```

```
; <<>> DIG 9.2.2 -x 165.193.130.83

;; global options: printcmd

;; Got answer:

;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 59962

;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 3, ADDITIONAL: 2

;; QUESTION SECTION:

165.193.130.83.in-addr.arpa.

               IN      PTR

;; ANSWER SECTION:

165.193.130.83.in-addr.arpa.      86400  IN PTR www.pearson.com.
```

```
; AUTHORITY SECTION:

pearson.com.      86400 IN NS ns1-p.dns.pipex.net.

pearson.com.      86400 IN NS ns.pearson.com.

pearson.com.      86400 IN NS ns0-p.dns.pipex.net.
```

```
; ADDITIONAL SECTION:

s0-p.dns.pypex.net.  66542 IN A 158.43.129.80

ns1-p.dns.pypex.net. 66542 IN A 158.43.193.80
```

```
; Query time: 294 msec

;; SERVER: 64.83.0.10#53(64.83.0.10)

;; WHEN: Mon Sep 1 16:42:00 2003

;; MSG SIZE rcvd: 151
```
