
# 破解的 Linux：Linux 安全秘密与解决方案

在这个示例中，你可以看到对递归查询的...

## 第 15 章：域名服务

487

...

);

这里是上一个示例的输出。你可以看到你现在被指向了一个根服务器而不是

```
$ dig www.google.com
```

```
;; << DIG 9.3.0 >> @fuse.inversepath.com www.google.com
;; global options: printcmd
;; Got answer:
;; ->HEADER-- opcode: QUERY, status: NOERROR, id: 34444
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 13, ADDITIONAL: 13

;; QUESTION SECTION:
;www.google.com.

;; AUTHORITY SECTION:
| 518398 IN NS M.ROOT-SERVERS.NET |
| 518398 IN NS A.ROOT-SERVERS.NET |
| 518398 IN NS B.ROOT-SERVERS.NET |
| 518398 IN NS C.ROOT-SERVERS.NET |
| 518398 IN NS D.ROOT-SERVERS.NET |
| 518398 IN NS E.ROOT-SERVERS.NET |
| 518398 IN NS F.ROOT-SERVERS.NET |
| 518398 IN NS G.ROOT-SERVERS.NET |
| 518398 IN NS H.ROOT-SERVERS.NET |
| 518398 IN NS I.ROOT-SERVERS.NET |
| 518398 IN NS J.ROOT-SERVERS.NET |
| 518398 IN NS K.ROOT-SERVERS.NET |
| 518398 IN NS L.ROOT-SERVERS.NET |

;; ADDITIONAL SECTION:
| A.ROOT-SERVERS.NET IN A 191.48.1.4 |
| B.ROOT-SERVERS.NET IN A 192.228.79.201 |
| C.ROOT-SERVERS.NET IN A 192.33.14.12 |
| D.ROOT-SERVERS.NET IN A 128.8.10.90 |
| E.ROOT-SERVERS.NET IN A 192.203.230.10 |
| F.ROOT-SERVERS.NET IN A 192.5.2.541 |
| G.ROOT-SERVERS.NET IN A 192.112.36.4 |
| H.ROOT-SERVERS.NET IN A 128.63.2.53 |
| I.ROOT-SERVERS.NET IN A 192.36.148.17 |
| J.ROOT-SERVERS.NET IN A 192.58.128.30 |
| K.ROOT-SERVERS.NET IN A 193.0.14.129 |
| L.ROOT-SERVERS.NET IN A 198.32.64.12 |

Hacking Exposed Linux: Linux 安全秘密与解决方案

M.ROOT-SERVERS.NET. 604798 IN A 202.12.27.33

;; Query time: 187 msec
;; SERVER: 69.60.119.224#53(fuse.inversepath.com)
;; WHEN: Sat Nov 4 17:36:13 2006
;; MSG SIZE rcvd: 451
```

为了实现完全锁定，你可以将递归和非递归查询限制在你的信任访问列表中，当然，你显式允许对自己的区域进行查询：

```
options {
...
allow-transfer { xfer };
allow-recursion { trusted; };
allow-query { trusted; };
...
}
```

```
zone "ourdomain.com" {
type master;
file "ourdomain.com";
allow-query { any; };
}
```

现在的示例查询完全没有返回任何结果：

```
$ dig www.google.com
```

```
;; >> DIG 9.3.0 >> @fuse.inversepath.com www.google.com
;; global options: print: printcmd
;; Got answer:
;; ->HEADER<-- opcode: QUERY, status: REFUSED, id: 31561
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 0
;; QUESTION SECTION:
;;www.google.com.

;; Query time: 189 msec
;; SERVER: 69.60.119.224#53(fuse.inversepath.com)
;; WHEN: Sat Nov 4 17:36:34 2006
;; MSG SIZE rcvd: 32
```

## 第 15 章：域名服务

489

### 隐藏版本

我们无法不提到 BIND 允许你用任意字符串隐藏（并替换）其版本号。虽然我们并不主张通过隐蔽性来维护安全，而且这不应被视为防止版本指纹的可靠方法（可以使用其他手段实现），但隐藏版本号是一个值得提及的小设置。

```
options {
  ...
  version "hidden";
);
```

这里是更改设置后的查询示例：

```
;; >> DIG 9.3.0 >> @140.105.134 version.bind
;; global options: printcmd
;; Got answer:
;; ->HEADER-- opcode: QUERY, status: NOERROR, id: 1929
;; flags: qr ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 0
;; QUESTION SECTION:
version.bind. TXT
;; ANSWER SECTION:
version.bind. 0 TXT "hidden"
;; AUTHORITY SECTION:
version.bind. 0 NS
;; Query time: 86 msec
;; SERVER: 140.105.134#53(140.105.134)
;; WHEN: Sat Nov 4 17:59:10 2006
;; MSG SIZE rcvd: 60
```

### 反向映射

维护所有暴露 IP 地址的反向映射是重要的。即使你不想为你的网络分配名称，也可以像 `pool.domain.com` 这样的标准化名称。

此外，你应该确保名称的直接解析与其 IP 地址的反向解析匹配。这些做法不仅对你的伙伴友好，还能有助于调试并减少反向地址被视为垃圾邮件的检查。

### 视图 (Views)

BIND 允许你在独立的视图中发布不想泄露到外部的区域。建议使用此功能来保护敏感名称并将内部区域限制在你的私有网络。

```
view "internal-in" {
  match-clients { trusted };
  recursion yes;
  ...
}
```

```
view "external-in" in {
  match-clients { any };
  ...
}
```

### DNS 记录伪造

| | 评分 |
| --- | --- |
| 流行度 | 2 |
| 简单性 | 2 |
| 影响 | 10 |
| 风险 | 5 |

整个 DNS 系统大多基于明文包（某些情况下区域信息通过 TCP 传输）。由于 UDP 很容易伪造，DNS 是伪造答案和中间人攻击的眼中。

### DNS 与加密：TSIG 和 DNSSEC

DNS 的最新更新包含了使用 DNS 来解决劫持、投毒和安全区域传输的问题。我们提到过区域传输可以限制在信任的伙伴，由于区域信息的可能敏感性，创建了 Transaction SIG (RFC 2845)。TSIG 允许你使用比简单 IP 地址匹配更强的方法进行验证，允许客户端更新动态数据库。

TSIG 通过使用发送者和接收者之间共享密钥计算的消息摘要来签名 DNS 消息。使用的函数是 128 位 HMAC-MD5。

491

这里是 TSIG 用于保护主从服务器区域传输的示例。我们使用示例名称 `tsigkey-domain.com` 作为密钥：

```
$ dnssec-keygen -a HMAC-MD5 -b 128 -n HOST tsigkey-ourdomain.com.
```

这产生了两个文件：

- `tsigkey-ourdomain.com.157.54730.key`
- `tsigkey-ourdomain.com.157.54730.private`

```
$ cat tsigkey-ourdomain.com.157.54730.key
tsigkey-ourdomain.com. IN KEY 512 3 157 hiY6iDNpPmGtofRww==
```

可以使用 `key` 语句在配置中指定生成的密钥：

```
key tsigkey-ourdomain.com. {
  algorithm hmac-md5;
  secret "hiY6iDNpPmGtofRww=";
}
```

可以使用 `key` 语句强制对特定服务器的所有 DNS 流量签名：

```
server 10.1.7.10 {
  keys { tsigkey-ourdomain.com; };
}
```

最后，在主服务器上，可以将区域传输限制为签名伙伴：

```
zone "ourdomain.com" {
  type master;
  file "ourdomain.com";
  allow-query { any };
  allow-transfer { key tsigkey-ourdomain.com; };
}
```

TSIG 是一种简单的机制，正因如此它有一些缺点。你必须在服务器之间手动分发密钥，这不是一种可扩展的解决方案。此外，没有任何权限级别能像公钥加密那样灵活。为了解决这些问题，提出了 DNSSEC 协议（RFC 4033/4034/4035）。该协议涉及公钥加密对区域文件进行签名。基本上，使用专门的 DNSKEY 记录发布公钥，使用相关的私钥（保留）对记录进行签名。

由于无法对否定查询进行签名，DNSSEC 包含了 Next Secure (NSEC) 记录来显式发布区域中存在哪些记录。换句话说，你得到的不是某个查询的否定回复，而是你的查询范围内的可用记录列表（使用规范排序顺序），这些列表可以与你的请求进行匹配。

在这个示例中，你可以看到一条 NSEC 记录公告 alpha.ourdomain.com 和 delta.ourdomain.com 还有其他域名。如果你询问 beta.ourdomain.com，这将是回复：

```
alpha.ourdomain.com 86400 IN NSEC delta.ourdomain.com 
      MX RRSIG NSEC TYPE1234
```
