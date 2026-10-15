
针对客户的域名使用这种方法，在理想情况下将发现一个潜在目标列表。在进行更具侵入性的活动之前，这些目标应该由客户进行确认。事实上，建议在运行像 `Recon-ng` 这样的工具之前，如果客户运行着自己的 DNS 服务器，你应该向客户寻求书面许可，因为这个工具可能具有很强的侵入性。

## 第 5 章 域名系统 101

### 主机

如果你想快速进行查询，可以使用 `host` DNS 查询工具。有时，你得到的将不仅仅是一个 IP 地址。这里有一个示例：

```
host google.co.uk
```

这返回了 IPv4 和 IPv6 地址，以及五个邮件主机及其各自的优先级。（下一章将更详细讨论邮件。）

```
google.co.uk has address 216.58.198.163

google.co.uk has IPv6 address 2a00:1450:4009:803::2003

google.co.uk mail is handled by 20 alt1.aspx1.google.com

google.co.uk mail is handled by 10 aspx1.google.com

google.co.uk mail is handled by 30 alt2.aspx1.google.com

google.co.uk mail is handled by 30 alt3.aspx1.google.com

google.co.uk mail is handled by 50 alt4.aspx1.google.com
```

在为客户工作时，你通常会在获得主机名之前拥有机器的 IP 地址。你只需通过查询 DNS 就能判断出主机的作用（或者在这种情况下进行合理的推测）。在这种情况下，你可以使用 `host` 提供 IP 地址而不是主机名。这里有一个示例：

```
host 9.9.9.9
```

这将告诉你所提供的 IP 地址的主机名，这就是指针 `PTR` 资源记录发挥作用的地方。

```
9.9.9.9-in-addr.arpa domain name pointer dns.quad9.net
```

这看起来可能很奇怪，但 DNS 需要使用像 `9.9.9.9.in-addr.arpa` 这样的域名来获取 IP 地址并将其转换为更熟悉的主机名；它不能简单地查找 IP 地址。这与普通查询一样，会向各种名称服务器请求答案，从根级别 ` . ` 开始，然后是 `arpa`（或区域），然后是 `in-addr.arpa.` 区域，然后是 `9.9.9.in-addr.arpa.` 区域此类此类。最终，在 PTR 记录中存储 `9.9.9.in-addr.arpa` 的名称服务器将提供最终答案，在这种情况下是 `dns.quad9.net`。注意，查询答案中包含了结尾的句号（这是完全有效的），许多其他 DNS 工具有时需要它。

## 使用 Dig 查找 SOA

识别名称服务器的另一种方法是使用 `dig`，它可以请求域的 SOA。记住 SOA 是区域的主要和权威名称服务器。在 `google.co.uk` 的情况下，它看起来如下：

```
dig google.co.uk SOA
```

响应应该类似于此：

```
<<< DIG 9.10.3-P-Debian >>> google.co.uk SOA

;; global options: --cmd

;; Got answer:

;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 50559

;; flags: qr rd ra ; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:

;; EDNS: version: 0, flags; udp: 512

;; QUESTION SECTION:

IN SOA

google.co.uk.

;; ANSWER SECTION:

google.co.uk 59 IN SOA nsl1.google.com.

admin.google.com. 22513951 900 1800 60

;; Query time: 71 msec

;; SERVER: 192.168.40.47(192.168.40.47)

;; WHEN: Wed Dec 12 13:36:51 GMT 2018

;; MSG SIZE rcvd: 101
```

关键在于，在 `ANSWER SECTION` 中，SOA 被列为 `nsl1.google.com`。这是 Google 主要名称服务器的主机名。该服务器的 IP 地址可以通过以下方式获取：

```
dig nsl1.google.com
<<< DIG 9.10.3-P-Debian >>> nsl1.google.com

;; global options: --cmd

;; answer:

;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 64267

;; flags: qr rd ra ; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:

;; EDNS: version: 0, flags; udp: 512

;; QUESTION SECTION:

IN A

nsl1.google.com.

;; ANSWER SECTION:

google.com. 21599 IN A 216.239.32.100

;; Query time: 59 msec

;; SERVER: 192.168.40.47(192.168.40.47)
```

现在你有了 Google 主要名称服务器的 IP 地址。Google 是一个带有名称服务器的示例。你经常会发现属于小型组织的 SOA 实际上并不属于该域名。这是一个示例：

```
dig hacker.house soa
>> DIG 10.3-P-Debian hacker.house soa

;; global options: --cmd

;; answer:

;; >>HEADER<< opcode: QUERY, status: NOERROR, id: 3706

;; flags: qr rd ra ; QUERY: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:

;; EDNS: version: 0, flags; udp: 512

;; QUESTION SECTION:

hacker.house.

IN SOA

;; ANSWER SECTION:

hacker.house. 3599 IN SOA nsl1.livedns.co.uk.

admin.hacker.house. 154265575 10800 3600 64800 3600

;; Query time: 52 msec

;; SERVER: 192.168.40.47(192.168.40.47)

;; WHEN: Wed Dec 12 13:52:31 GMT 2018

;; MSG SIZE rcvd: 100
