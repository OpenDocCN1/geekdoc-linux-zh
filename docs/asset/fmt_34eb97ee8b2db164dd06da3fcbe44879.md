
# 社会因素：DNS 与网络钓鱼

与某些计算机代码中 IP 地址的精确过程不同，人们对域名的使用要不严谨得多。`www.hotmail.com` 这个地址很容易被错打，而包含如 `http://www.rasbank.com-customer-service.gad7n.biz` 这种地址的电子邮件可以有效地用于钓鱼攻击，诱导用户进入恶意网站。

分心焉或缺乏知识的用户可能会将 URL 中的 `rasbank.portion` 误认为是有效的，但真正的顶级域名是 `gad7n.biz`。`customer-service` 子域名往往会让你感到更加困惑。这些用户还可能在警告不可信 SSL 证书的这一非常常见的对话框中点击“确定”，并被完全欺骗去使用他们网上银行网站的完美（但恶意的）副本。

虽然写错名称看起来是无害的，但域名抢注者（typosquatters）会利用这种错误。

# Hacking Exposed Linux: Linux 安全机密与解决方案

DNS 劫持攻击成功的后果至关重要，可能导致所有公共系统的全面沦陷以及敏感信息的广泛泄露。不言说，在注册域名时，应选择一个信誉良好且知名的注册商。

## 技术层面：欺骗、缓存投毒及其他攻击

你已经或多少看到了影响 DNS 基础设施安全的社会方面因素。现在我们来讨论技术方面。

正如你所见到的，在 DNS 事务中，通常会交换两个数据包。将响应与原始查询“粘合”在一起的信息片段是`标识字段（identification field）`。该字段具有 16 位的值，并且每次都应该随机选择该值。在最近的几年里，有几种实现方式没有随机选择该值，这导致了通过欺骗进行会话劫持的可能性。

攻击者可以通过向受害者的客户端发送一系列带有不同 ID 的数据包来猜出正确的 ID，希望其中一个数据包能与客户端查询中的 ID 匹配。当然，猜测 ID 只是过程的一部分，因为攻击者仍然需要猜测匹配的端口号，并在正确的时间小心地注入伪造的响应。

最新的实现方式不容易受到可预测 ID 编号的影响，但如果条件允许，欺骗在理论上总是可能的。当然，在可以进行二层劫持的本地局域网（LAN）上，DNS 欺骗是轻而易举的。

在这种背景下，伪造的响应并不一定需要指向客户端本身。攻击者还可以为受害者 DNS 服务器发出的查询伪造响应，从而投毒其缓存。这种方法的优势在于，如果该 DNS 服务器是一个开放解析器（open resolver），攻击者可以通过请求它解析一个自己的域名，然后伪造该查询的响应来增加成功几率。如果成功，这种攻击将“投毒”受害者 DNS 服务器的缓存，从而辅助恶意意图。

另一种类型的缓存投毒攻击包括向 DNS 响应中注入权威信息。攻击者会向受害者的 DNS 服务器请求（攻击者自己的）区域的解析。DNS 服务器将向攻击者域名的权威服务器请求此类信息，而该服务器由攻击者控制。

被请求域名的区域文件将包含一个额外的部分，其中与请求域名完全无关的条目（例如，`www.google.com` 的虚假 IP 地址），这样请求 DNS 服务器为了性能考虑，即使该条目不是请求的内容，也会缓存该信息。目前，大多数 DNS 服务器实现都配置为拒绝不符合原始查询的额外区域，但旧版系统仍然容易受到此类攻击。

某些协议并不完全依赖 DNS，而是提供了额外的身份验证层。最显著的例子是 TLS-或 SSL 加密连接（如 HTTPS），它们被用于通过受信任的认证机构签名的证书来验证你的端点。即使发生 DNS 劫持，攻击者也无法轻易提供有效的证书。遗憾的是，许多用户倾向于忽略浏览器呈现的 SSL 相关警告，而且应用程序之间的大多数连接也没有按要求强制执行证书验证。

某些协议（如 SSH）会缓存与主机关联的唯一 ID，因此任何 DNS 劫持尝试都会由于 ID 不匹配而引发错误：

```
[keymaker]:/home/epablio:~/.ssh 192.168.1.22

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

@ WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! #

@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@

```

**可能某人正在做某些坏事！** 现在可能有人正在监听你的通信（中间人攻击！）

也可能是 RSA 密钥刚刚被更改。远程主机发送的 RSA 密钥指纹为 ff87:b7:69:dc:f5:ef:8c:39:30:22:44:d2:68:60。

请联系你的系统管理员。将主机密钥添加到 `/home/epablio/.ssh/known_hosts` 以消除此消息。

位于 `/home/epablio/.ssh/known_hosts:25` 的 `192.168.1.22` 的 RSA 主机密钥已更改，且你请求了严格检查。

主机密钥验证失败。 [/example of ssh mismatch]

对于任何身份验证目的，依赖 DNS 以外的其他手段始终是良好的做法，并在你的配置中尽可能使用 IP 地址。

最后，DNS 缓存也可以用于检查你的 DNS 服务器是否一直在查询特定域名。这种技术被称为缓存嗅探（cache snooping）。如果你的 DNS 服务器接受来自任意地址的查询，它将立即提供已解析域的缓存信息，而不是将客户端重定向到顶级 DNS 服务器（如果它允许非递归查询），或者根本不回复查询。成功的缓存嗅探让攻击者能够轻松探测你的网络最近是否在浏览某个特定域名，这可以极地帮助社会工程学攻击。

此示例显示了简单的计时分析如何告诉你你正在查询的 DNS 服务器的用户最近一直在使用 Google 而不是 Excel。除了计时之外，你还可以从缓存的生存时间（TTL）中收集这些信息：在第一情况下，14400 的循环值是新缓存记录的证据，而 Google 的 TTL 138738 显示它已缓存了一段时间（与干净的 DNS 缓存进行简单的交叉检查显示，`www.google.com` 的默认 TTL 时间为 604800）。

```
$ time dig www.excite.com
```

```
; DIG 9.3 <<140.105.134 www.excite.com

;; global options: printcmd

;; Got answer:

;; -HEADER<- opcode: QUERY, status: NOERROR, id: 7685

;; flags: qr rd; QUERY: 1, ANSWER: 1, ADDITIONAL: 2

;; QUESTION SECTION :

;;www.excite.com.                IN      A

;; ANSWER SECTION:

www.excite.com.               14400   IN      A       208.45.133.23

;; AUTHORITY SECTION:

excite.com.                   172799   IN      NS      ns1-156.akam.net.

excite.com.                   172799   IN      NS      dns4.imgfarm.com.

excite.com.                   172799   IN      NS      dns5.imgfarm.com.

;; ADDITIONAL SECTION:

usel.net.                4180    IN      A       63.209.170.136

ns1-156.akam.net.       17866   IN      A       193.108.91.156
```

```
$ time dig www.google.com
```
; DIG 9.3 <<140.105.134 www.google.com
;; global options: printcmd
;; Got answer:
;; -HEADER<- opcode: QUERY, status: NOERROR, id: 37034
;; flags: qr rd; QUERY: 1, ANSWER: 3, AUTHORITY: 6, ADDITIONAL: 0

;; QUESTION SECTION :
;;www.google.com.                IN      A

;; ANSWER SECTION :
www.google.com.               138738 IN CNAME www.l.google.com.
www.l.google.com.               300    IN      A       66.249.85.99
www.l.google.com.               300    IN      A       66.249.85.104

;; AUTHORITY SECTION:
l.google.com.                   77277   IN      NS      a.l.google.com.
l.google.com.                   77277   IN      NS      b.l.google.com.
l.google.com.                   77277   IN      NS      c.l.google.com.
l.google.com.                   77277   IN      NS      d.l.google.com.
l.google.com.                   77277   IN      NS      e.l.google.com.
l.google.com.                   77277   IN      NS      g.l.google.com.

## 软件漏洞

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 10 |
| 风险评分 | 8 |

遗憾的是，ISC 的 BIND 软件在过去几年中经历了大量的严重安全漏洞。因此，采取一些措施来保持 BIND 安装的安全非常重要。

## 保持软件更新

始终积极检查最新的 BIND 告和更新。运行已知的最新安全版本显然至关重要。

## 最小权限原则

你应该以尽可能少的权限运行 BIND。大多数软件包已经以 *named* 用户身份运行它，但你应该仔细检查。如果不是如此，请使用 `-u` 和 `-g` 标志来选择用户。

## 单点故障

| 流行度 | 5 |
| :--- | :--- |
| 简单性 | 5 |
| 影响 | 8 |
| 风险评分 | 6 |

DNS 的关键作用要求其可靠性和容错能力。如果某个特定的网络或域名仅由单一 DNS 服务器提供服务，那么该 DNS 服务器的故障将导致严重的服务中断，因为今天几乎所有的服务都依赖于将域名解析为 IP 地址以及反之的能力。

## 维护备服务器

所有感知 DNS 的软件都允许你在配置中提供备用和可能的三级服务器。此外，区域的 NameServer 记录（通常称为 NS 记录，指定其权威 DNS 服务器）允许多个指定：主服务器是 *master*，而备用服务器是 *slaves*。DNS 不也不应该对它们进行任何区分。

如果未能为你的区域或地址空间提供 DNS 记录（即使是暂时的），可能会导致拒绝服务状况，并产生有利于伪造攻击的场景。因此，你应该始终维护至少一个备用服务器的可靠基础设施。

```
$ dig -t ns google.com
```

```
; <<>> DiG 9.3.0 <<>> -t ns google.com

;; global options: printcmd

;; Got answer:

;; ->HEADER<< opcode: QUERY, status: NOERROR, id: 21063

;; flags: qr da ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 4
```

```
;; QUESTION SECTION:

google.com.
```

```
;; ANSWER SECTION:

google.com. 152248 IN NS ns1.google.com.

google.com. 152248 IN NS ns2.google.com.

google.com. 152248 IN NS ns3.google.com.

google.com. 152248 IN NS ns4.google.com.
```

```
;; ADDITIONAL SECTION:

ns1.google.com. 161231 IN A 216.239.32.10

ns2.google.com. 161231 IN A 216.239.34.10

ns3.google.com. 161231 IN A 216.239.36.10

ns4.google.com. 161231 IN A 216.239.38.10
```

```
;; Query time: 91 msec

;; SERVER: 140.105.134.#53(140.105.134.155)

;; WHEN: Sat Nov 4 16:39:20 2006

;; MSG SIZE rcvd: 164
```

## 通过暴露导致泄露

| 流行度: | 10 |
| :--- | :--- |
| 简单性: | 10 |
| 影响: | 2 |
| 风险评分: | 7 |

与所有网络软件一样，DNS 功能可能会经历不同程度的暴露，允许攻击者对服务器内部有更深入的洞和更好的理解。DNS 服务器带有至少一个网络的描述性信息，如主机名、子域名和 IP 地址。如果攻击者拥有这些信息，他或她可以在攻击之前仔细考虑你的网络。因此，系统管理员必须避免网络 DNS 服务器上的任何信息泄露。

## 安全区域传输

从管理角度来看，主服务器和从服务器的区别在于，存储你域名区域信息的物理文件仅存储在主服务器上。从服务器会根据预定义的间隔自动拉取并缓存主服务器数据库，或者在主服务器发布 NOTIFY 消息（通知其从服务器发生了变化）时拉取。

与通常通过 UDP 通道的普通 DNS 请求不同，区域传输始终通过 TCP 传输。

用于检查主服务器和从服务器之间区域文件一致性的信息是 *序列号*（serial number）。这里我们正在检查 google.com 的区域编号（为 1291839）：

```
<< DIG 9.3.0 >> -t soa www.google.com

; global options: printcmd

; answer:

;; ->HEADER<< opcode: QUERY, status: NOERROR, id: 567261

;; flags: qr ra; QUERY: 1, ANSWER: 1, AUTHORITY: 1, ADDITIONAL: 1
```
*(注：由于 520-521 页原始文本存在严重乱码，后续内容未在此处理)*

## 第 15 章：域名服务

### 487

...

);

这里是上一个示例的输出。你可以看到你现在被指向了一个根服务器而不是

```
$ dig www.google.com
```

```
; DIG 9.3.0 @fuse.inversepath.com www.google.com

;; global options: printcmd

;; Got answer:

;; ->HEADER-- opcode: QUERY, status: NOERROR, id: 34444

;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 13, ADDITIONAL: 13
