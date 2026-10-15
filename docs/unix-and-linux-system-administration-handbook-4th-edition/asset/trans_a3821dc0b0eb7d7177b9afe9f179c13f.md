

expn.com 已经在队列中排队超过 1,280 分钟。本示例中的所有目标都暗示消息可能是由度假脚本在响应垃圾邮件时发送的。

qshape 还可以通过 -s 标志按发件人域进行汇总。

## Soft-bouncing

如果将 soft_bounce 设置为 yes，Postfix 在原本会发送永久性错误消息（如 “user unknown” 或 “relaying denied”）的情况下，会发送临时错误消息。这是一个很好的测试功能；它让你在配置更改后监控邮件的处理情况，而不会冒永久丢失合法邮件的风险。你拒绝的任何邮件最终都会再次尝试投递。测试完成后不要忘记关闭此功能，否则你将不得不一遍又一遍地处理每封被拒绝的邮件。

## Testing access control

测试访问控制限制最简单的方法是尝试从外部主机发送邮件，看看会发生什么。这是一个很好的基本测试，但它并不能涵盖特殊情况，例如来自你没有登录的域的邮件。

Postfix 2.1 引入了 SMTP 协议的一个扩展，称为 XCLIENT，用于模拟来自其他地方的提交。此功能默认处于禁用状态，但通过在 main.cf 中添加以下配置行，你可以为源自 localhost 的连接启用它：

```
smtpd_authorized_xclient_hosts = localhost
```

一个测试会话可能看起来像这样：

```
$ telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
220 tardis.ee.ethz.ch ESMTP Postfix
XCLIENT NAME=mail.cs.colorado.edu ADDR=192.168.1.1
250 Ok
HELO mail.cs.colorado.edu
250 tardis.ee.ethz.ch
MAIL FROM:<evi@colorado.edu>
250 Ok
RCPT TO:<david@colorado.edu>
554 <david@colorado.edu>: Relay access denied
```

## 20.16 DKIM CONFIGURATION

我们的 DKIM 覆盖范围有点分散。介绍性材料在 DNS 章节中（第 591 页）和本章第 768 页。这里我们集中讨论通过外部工具 amavisd 使用 DKIM 的电子邮件相关细节，以及直接与 sendmail、Exim 和 Postfix 结合使用。sendmail 和 Postfix 使用

milters 来实现 DKIM；Exim 则原生支持。Exim 的实现是新的（2009 年底）并且仍然有点粗糙。

## DKIM: DomainKeys Identified Mail

DKIM 是积极识别发件人组织的新的希望。如果广泛部署，它将遏制垃圾邮件发送者和网络钓鱼者伪造发件人域的能力。来自你银行的邮件确实来自你的银行——或者至少不会被归类为网络钓鱼或垃圾邮件。

DKIM 取代了早期的 DomainKeys 系统。DKIM 使用公钥加密（密钥存储在 DNS 中）让接收方验证邮件的来源和完整性。这些保证在我们互联的世界中变得至关重要，因为如此多的业务都是通过电子方式进行的。DKIM 还防止发件人否认自己发送了邮件，这一特性被称为不可否认性。

DKIM 实现分为两部分：一部分在邮件离开你的站点时对发出的邮件进行签名，另一部分在邮件到达时验证入站邮件的签名。第一个操作应在邮件离开你的站点之前由你的出站邮件枢纽执行（在完成任何内部重写和内容扫描之后）。第二个部分，验证，应在消息接收后立即执行，在其他扫描工具添加或更改其标头之前执行。

sendmail.org 有几个方便的工具是通用的，可以与任何实现 DKIM 的软件一起使用。第一个是 ADSP 助手，它接受一个域名并生成你必须添加到 DNS 以实现 DKIM 的相应 ADSP TXT 记录。[^21] 第二个工具是验证器，你可以在一切准备就绪后使用它来检查你的设置。

DKIM 和 ADSP 资源记录的细节在第 591 页有介绍。它们目前仍然是 TXT 记录，但未来可能会获得自己的 DNS 资源记录类型。OpenSSL 和 **amavisd** 都包含用于生成 DKIM 密钥的代码。各种 DKIM milter 包也包含生成密钥的脚本。

一旦你配置了 MTA 生成 DKIM 签名，你可以向 sa-test@sendmail.net 发送邮件以验证一切是否正常工作。服务器会通过电子邮件回复你，告诉你收到了哪些安全功能。

如果你有一个 Gmail 账户，另一种测试方法是向自己发送一封邮件。点击“显示详情”链接应该会显示一个 signed-by 字段。你也可以在下拉菜单中要求 Gmail“显示原始邮件”——此命令会显示包含所有标头的原始邮件，包括 DKIM 签名。

## DKIM miltering

用于实现 DKIM 的软件最初由 Sendmail, Inc. 开发，用于作为 milter 与 **sendmail** MTA 接口。现在有两个版本

> 21. 在出站邮件签名设置并正常工作之前，不要发布你的 ADSP 记录，否则其他站点可能会开始拒绝你的邮件。

