
Arrival-Date: Mon, 5 Mar 2007 04:57:32 -0300

Final-Recipient: RFC8282; info@phycs.unju.edu

Action: failed

Status: 5.1.1

Remote-MIA: DNS; mail.phycs.unju.edu

Diagnostic-Code: SMTP; 550 <info@phycs.unju.edu>... User unknown

Last-Attempt-Date: Mon, 5 Mar 2007 11:18:27 -0300

-- Attachment #3 --

```

```

<-- Type: text/plain, Encoding: 7bit, Size: 0.5K -->

Date: Mon, 5 Mar 2007 11:18:28 -0300

From: Mail Delivery Subsystem <MAIL-DAEMON@huayraint.unju.edu>

To: security@disecom.org

Subject: Returned mail: see transcript for details

...

```

# 第14 章：邮件服务

```
250 2.1.5 <mike@mail.somewhereelse.com>
expn sales
250 2.1.5 "/usr/bin/llmm-receive -L /var/lists/example.org/sales/"
vrfy joe
250 2.1.5 <joe@mail.example.org>
vrfy notauser
550 5.1.1 notauser... User unknown
```

```
</Verbatim 列表>
```

从列表中，你可以快速地发现该信箱至少有两个管理员（拥有本地信箱的 `joe` 和使用 `llmm` 软件的 `mike`）。在同一个 SMTP 会话中，通过一个列出的邮件列表，你还可以验证 `<joe@mail.example.org>` 确实存在，而 `<fred@example.org>` 并不存在。

你可以在 MTA 上禁用这两个命令。在 Sendmail 中，向你的隐私标志中添加 `noexpn` 和 `vrfy`：

```
define('confPRIVACY_FLAGS',`noexpn, vrfy') dnl
```

Postfix 没有 `EXPN` 服务，并且可以在 `main.cf` 中禁用 `VRFY`：

```
disable_vrfy_command = yes
```

在 Sendmail 中禁用 `VRFY` 会禁用 `VERB` 命令，该命令会将连接设置为详细模式（verbose mode），可能会导致敏感信息泄露。由于这两个命令被认为与恶意活动有关，它们往往会在你的服务器日志中产生噪音；这里是 Sendmail 响应的一个示例：

```
<Verbatim 列表 15>
Oct 9 15:40:26 sendmail[2885]: k99FosFvu02885: tc.example.org
[10.1.7.2]: VRFY root
Oct 9 15:40:28 sendmail[30666]: k99FdjD6030666: tc.example.org
[10.1.7.2]: expn root
Oct 9 15:40:28 sendmail[30666]: k99FdjD6030666: tc.example.org
[10.1.7.2]: expn sales
Oct 9 15:40:28 sendmail[30666]: k99FdjD6030666: tc.example.org
[10.1.7.2]: expn admin
Oct 9 15:40:28 sendmail[30666]: k99FdjD6030666: tc.example.org
[10.1.7.2]: possible SMTP attack: command=EXPN, count=6
</Verbatim 列表>
```

即使禁用了 `EXPN` 和 `VRFY`，你仍然可以通过投递消息并检查信封目标地址（envelope destination address）是否返回错误来执行枚举（enumeration）。大多数 MTA 会在 SMTP 连接上立即返回错误以节省带宽；其中一些（最值得注意的是）具有对垃圾邮件友好的行为，即接受所有地址的邮件，稍后如果地址无效则发送退信邮件（bounce email）。

在同一个 SMTP 连接上可以指定多个信封地址，事实有助于垃圾邮件的发送：

```
<Verbatim 列表 16>
# telnet mail.example.org 25
Trying 192.168.1.1...
Connected to mail.example.org.
Escape character is '\'.
220 box.example.org EM mail.example.org ; Mon, 9 Oct 2006 15:42:23 GMT
HELO testclient.example.org
250 mail.example.org Hello testclient.example.org [10.1.7.2], pleased to meet you
mail from:evil@testclient.example.org
250 2.1.0 evil@testclient.example... Sender ok
rcpt toadmin
250 2.1.5 admin... Receiver ok
rcpt toroot
250 2.1.5 root... Receiver ok
rcpt tosales
250 2.1.5 sales... Receiver ok
rcpt tobob
550 5.1.1 bob... User unknown
rcpt tojoe
550 5.1.1 joe... User unknown
rcpt tomike
250 2.1.5 mike... Receiver ok
</Verbatim 列表>
```

防止大规模用户枚举的一种技术是限制在同一个 SMTP 会话中允许的接收者数量。Sendmail 提供了 `BadrcptThrottle` 变量：

```
define(`confBAD_RCPT_THROTTLE`, `100`)
```

Postfix 提供了 `smtpd_recipient_limit` 变量：

```
smtpd_recipient_limit = 100
```

# 开放中继 (Open Relays)

| 流行度 | 7 |
| :--- | :--- |
| 简单性 | 7 |
| 影响 | 5 |
| 风险评分 | 6 |

开放中继是垃圾邮件发送者的天堂，必须不惜一切代价地避免它们。开放中继是一个配置错误的邮件服务器，它允许任何客户端向任何邮件域发送消息（而不仅仅是逻辑上要求的本地和/或被接受的域名）。

垃圾邮件发送者不断在互联网地址空间寻找开放中继，一旦发现，就会利用它们以极高的速率发送垃圾邮件。直接从邮件代理（没有队列概念）或垃圾邮件发送者的 MTA 发送数百万条消息的原因是，在同一个 SMTP 连接上可以指定多个信封地址，这有助于垃圾邮件的过程：

```
<Verbatim 列表 7>
# telnet mail.example.org 25
Trying 192.168.1.1...
Connected to mail.example.org.
Escape character is '\'.
220 box.example.org EM mail.example.org ; Mon, 9 Oct 2006 15:42:23 GMT
HELO testclient.example.org
250 mail.example.org Hello testclient.example.org [10.1.7.2], pleased to meet you
mail from:evil@testclient.example.org
250 2.1.0 evil@testclient.example... Sender ok
rcpt toadmin
250 2.1.5 admin... Receiver ok
rcpt toroot
250 2.1.5 root... Receiver ok
rcpt tosales
250 2.1.5 sales... Receiver ok
rcpt tobob
550 5.1.1 bob... User unknown
rcpt tojoe
550 5.1.1 joe... User unknown
rcpt tomike
250 2.1.5 mike... Receiver ok
</Verbatim 列表>
