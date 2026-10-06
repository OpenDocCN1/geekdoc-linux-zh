
尽管灰名单（greylisting）是完全透明且在理论上无害的，但总的来说是一种糟糕的做法：首先，它减慢了所有 SMTP 流量（包括合法流量），延迟从几分钟到几小时不等。此外，延迟灰名单对于每个邮件网关来说都是队列的噩梦。邮件列表和繁忙的网关在保留所有灰名单邮件所需的资源方面将受得尤为严重。

尽管缓存只拒绝每个三元组的第一条消息，但某些服务器接收的 SMTP 流量巨大，而且在某些情况下三元组非常容易变化，这使其有效性降低。在最坏的情况下，重试可能来自不同的 IP 地址组合或不同的信封发件人（某些服务器采用动态信封发件人，特别是邮件列表），然后合法邮件将不断重发直到其在队列中过期。

如果你实施了灰名单，请注意它可能引起的问题，并意识到它对其他服务器队列并不友好。

## 分布式和值 (Distributed Checksum)

许多反垃圾邮件系统使用分布式和值来检测并最终过滤垃圾邮件。其想法是，垃圾邮件可能会发送给互联网上的大量接收者；维护一个包含通过 MTA 服务器的单条消息和值的中心数据库，允许你比较并检查它们是否重复了足够次数，以便将其分类为垃圾邮件。

和值通常不是针对整个消息计算的，而是每次使用模糊（fuzzing）和/或算法针对不同部分，因为垃圾邮件对于每个接收者可能略有不同，例如每封收到的邮件的第一行问候中的名称不同。实现分布式和值求和过滤器的 MTA 将连接到指定的服务器，发送和值，获取响应并评估结果。

分布式和值需要对由于某些原因发送给大量接收者的合法流量进行仔细的白名单处理，最典型的邮件流量（特别是大型公告列表上的）。它还增加了你端的网络流量，因为每封收到的邮件都需要在中心服务器上查询。

可以使用实现这种想法的过滤器，最著名的 `DCC`、`Razor` 和 `Pyzor`。

## 挑战响应 (Challenge-Response)

某些垃圾邮件过滤系统涉及挑战响应架构，该架构会向发送者发回邮件以确认所发送的消息。确认可以是回复挑战邮件、访问消息中的 URL 或提供其他确认手段。将这类系统想象成用户级的灰名单；所有消息都必须由用户手动确认。理论是，垃圾邮件发送者绝不会确认消息。

出于许多原因，必须不惜代价避免这种垃圾邮件预防方法。首先，任何由人类自动发送的邮件都是无法确认的；确认是一个需要人工干预的操作，而自动邮件显然预料到了这类过滤器（自动消息的回复通常石沉大海）。如今许多重要且合法的流量都是自动化的。考虑登录表单配置、在线购物邮件、通讯报等等；清单是无尽的。

此外，你真的无法期望发送者对发送给你的邮件执行进一步的操作，考虑到挑战消息讽刺地被大多数过滤器标记为垃圾邮件。在响应邮件列表时，挑战消息也特别令人厌恼，对所有对挑战机制反应良好的流量进行白名单是一项艰巨的任务。

尽管你极切渴望这种过滤，也请务必遵循 `http://www.templtons.com/brad/spam/challengerespace.html` 特有的最佳实践。

## 初始阶段

`HELO`/`EHLO` 命令用于每个 SMTP 连接的初始阶段，用于向 MTA 介绍连接客户端。`HELO` 命令是原始命令，而 `EHLO` 命令是扩展版本，除了介绍客户端外，还用于请求 SMTP 服务扩展。此命令用于将客户端识别为域名。

即使不支持 SMTP 扩展，所有服务器都应该支持 `EHLO`。`HELO` 命令始终优于旧的 `HELO` 命令（后者作为向后兼容的备选）。

在下面的示例中，我们展示了一个空问候，表示某些不是域名被拒绝了。客户端域名有效，发送虚假域名也是接受的（正如我们在“邮件路由”中提到的）。

```
Verbatim listing 10>
# telnet mail.example.org 25
Trying 192.168.1.1...
Connected to mail.example.org.
Escape character is '^'
220 box.example.org ESMTP mail.example.org ; Mon, 9 Oct 2006 15:42:23 GMT
HELO
```

501 5.0.0 HELO requires domain address

HELO !@@#

501 5.0.0 Invalid domain name

HELO test

```
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
250 testclient.example.org
250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you
```<Verbatim listing 11>

# telnet mail.example.org 25

Trying 192.168.1.1...

Connected to mail.example.org.

Escape character is '^'

220 box.example.org ESMTP mail.example.org ; Mon, 9 Oct 2006 15:42:23 GMT

HELO

testtestclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

250 mail.example.org HELO testclient.example.org [10.1.7.2], pleased to meet you

250 testclient.example.org

mail from: attacker@evil.com

503 5.0.0 Polite people say HELO

```

```>

rcpt to: admin

503 5.0.0 Need MAIL before RCPT

</Verbatim listing>

在 Sendmail 中，你可以通过在隐私设置中添加 `needhello` 来要求问候

```
define(`confPRIV_FLAGS`','`noexpn,novry,needhello`')
```

在 Postfix 中，你可以使用 `greet_pause` 功能来指定延迟（你也可以按 `access_db` 设置）：

```
FEATURE('greet_pause','5000') # 延迟为毫秒，5 秒
```

在 Postfix 上，你可以通过以下配置实现相同效果

```
smtpd_client_restrictions =
sleep 1, reject_unauth_pipelining
smtpd_delay_reject = no
```

## 钓鱼

| 流行程度 | 10 |
| 简单性 | 6 |
| 影响 | 7 |
| 风险评分 | 8 |

钓鱼是一种电子邮件欺诈形式，欺骗用户将敏感信息提交给攻击者控制的资源（通常是网站）。大多数时候，寻求的信息是在线银行凭据和信用卡号。

欺骗用户提交信息的这种技术是提供一个看起来与目标受害者在线银行系统或其他受信资源完全相同的界面。通常这种尝试是盲目的，因此接收与你自己的银行不同的银行的钓鱼邮件非常常见。当然，大数法则适用于这里：当攻击者可以很容易找到百万封钓鱼邮件时，成功破解相当数量受害者的概率是巨大的。

模仿现有且知名在线银行网站的 HTML 内容和图像位于邮件内容或 Web 服务器上

## 第 14 章：邮件服务

被欺骗连接。这种恶意重定向的常用策略是使用与合法 URL 视觉相似的 URL（例如使用 `www.bank-one.com` 而不是 `www.bankone.com`），希望受害者不会注意到。另一种广泛使用的技术是显示原始银行的网页，但重定向到攻击者的网站，例如，`<a href="http://www.owned.site.com">http://www.YourBank.com</a>`。这种技术通常能被带有邮件模块的现代反病毒引擎检测到。

<逐字列表列表 12>

[钓鱼示例]

```
From - May 26 2008 18:55:34 2008
X-Account-Key: account
X-UIDL: 5820481d7009c2ae
X-Mozilla-Status: 0001
X-Mozilla-Status2: 00000000
X-Mozilla-Keys:
Return-Path: <akstaltierimndsgs@xxxxx.org>
Delivered-To: pete@isecom.org
Envelope-To: pete@isecom.org
Received: (gmail 31506 invoked by uid 3048); 26 May 2008 16:48:05 -0000
Delivered-To: isecom.org:pete@isecom.org
Received: (gmail 31502 invoked from network); 26 May 2008 16:48:05 -0000
Received: from mail4.pair.com (66.39.2.4)
by kunatri.pair with SMTP: 26 May 2008 16:48:05 -0000
Received: from localhost (localhost) [127.0.0.1]
by mail4.pair.com (Postfix) with SMTPD 03AEC933A
26 May 2008 12:48:04 -0400 (EDT)
for <pete@isecom.org>; 26 May 2008 12:48:04 -0400 (EDT)
Received: from rosapalooza (host-le32-38-dynamic-01-10-r.mail.spamalat.it
[10.0.38.122]
by mail4.pair.com (Postfix) with ESMTP 33CB29B33
for <pete@isecom.org>; 26 May 2008 12:48:03 -0400 (EDT)
Received: from [10.0.38.122] by mail.xxxxxxx.org, 26 May 2008 17:48:03 +0100
Date: Mon, 26 May 2008 17:48:03 +0100
From: support@intl.paypal.com
X-Mailer: The Bat (v2.10) Educational
Reply-To: akstaltierimndsgs@xxxxxxxx
X-Priority: 3 (Normal)
Message-ID: <919322082.337290297297921@xxxxxxxxxxxxxx>
To: pete@isecom.org
Subject: PayPal Account Suspension
MIME-Version: 1.0
Content-Type: text/html;
```

http://freepdf-books.com

charset=Windows-1252

Content-Transfer-Encoding: 7bit
