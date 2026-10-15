

从发行版中的示例复制 dkim-filter.conf 文件，然后教 Postfix 使用 dkim-filter。在 main.cf 中，在其他任何 milter 选项之后，添加以下行

```
smtp_milters = inet:localhost:8891
non_smtpd_milters = inet:localhost:8891
milter_protocol = 2
milter_default_action = accept
```

现在你所需要做的就是启动 dkim-filter 并重启 postfix。

## 20.17 集成式邮件解决方案

有大量集成式邮件解决方案可供选择，从免费的开源产品到昂贵的商业产品不等。它们处理的不仅仅是电子邮件。常见的群件和会议功能包括

- 地址簿和共享联系人列表管理
- 日历和任务管理
- 邮件列表和公告板
- 即时消息
- SSL/TLS 加密
- 归档和自动备份
- 对移动设备的支持（BlackBerry、iPhone 等）

大多数这些大型软件包都包含一个配置 GUI，基本上取代了阅读本庞大章节的需要。（也许我们应该把本节放在章节开头而不是结尾。）其中许多产品被定位为 Microsoft Exchange 的替代品。

有几个产品值得特别提及：

- Citadel（citadel.org）是一个开源的邮件和群件软件包，可提供支持合同。
- Zimbra（zimbra.com）在开源和专有系统之间架起了桥梁。其功能齐全的版本是专有的且需要付费，但一个仅受轻微限制的版本是开源且免费的。
- Kerio MailServer（kerio.com）是一个专有系统，像 Zimbra 一样按用户许可。 对于大型组织来说，这些选项可能会变得昂贵。
- Communicate Pro（communicate.com）将语音和视频融入到常规的邮件/群件套件中，并提供传统的无限许可或基于使用的许可。

你也可以考虑邮件设备，即通常基于经过加固、精简的 FreeBSD UNIX 或 Linux 版本构建的硬件盒子。该领域的三个选择是 Cisco 的 IronPort 系列以及 Sophos 和 Clearswift 的型号。这些产品通常执行防病毒和反垃圾邮件过滤，然后将消息交给 Microsoft Exchange 进行投递。

## 20.18 推荐阅读

与其把这里列出的参考资料混在一起，我们已按 MTA 和主题进行了分类。

### 通用垃圾邮件参考资料

CLAYTON, RICHARD. "Good Practice for Combating Unsolicited Bulk Email." RIPE/Demon Internet. 2000. ripe.net/ripe/docs/ripe-206.html.

本文档面向 ISP。它包含大量政策信息以及一些指向技术主题的良好链接。

FIELD, JULIAN. MailScanner: A User Guide and Training Manual. University of Southampton Department of Electronics, 2007.

McDONALD, ALISTAIR. SpamAssassin: A Practical Guide to Configuration, Customization, and Integration. Packt Publishing, 2004.

SCHWARTZ, ALAN. SpamAssassin. Sebastopol, CA: O'Reilly Media, 2004.

WOLFE, PAUL, CHARLIE SCOTT, AND MIKE ERWIN. The Anti-Spam Tool Kit. Emeryville, CA: Osborne, 2004.

### sendmail 参考资料

COSTALES, BRYAN, CLAUS ASSMANN, GEORGE JANSEN, AND GREGORY NEIL SHAPIRO. sendmail, 4th Edition. Sebastopol, CA: O'Reilly Media, 2007.

这本书是 sendmail 配置的权威巨著——共 1,300 页。它包括系统管理员指南以及完整的参考部分。也有电子版可供使用。作者阵容包括两位关键的 sendmail 开发者（Claus 和 Greg），他们确保了技术上的正确性并增添了见解。

安装说明和配置文件的好描述包含在 Sendmail Installation and Operation Guide 中，该文档可在 sendmail 发行版的 doc/op 子目录中找到。该文档相当完整，结合 cf 目录中的 README 文件，可以很好地了解 sendmail 系统的实际运作。

sendmail.org、sendmail.org/~ca 和 sendmail.org/~gshapiro 都包含与 sendmail 相关的文档、HOWTO 和教程。

### Exim 参考资料

HAZEL, PHILIP. The Exim SMTP Mail Server: Official Guide for Release 4, 2nd Edition. Cambridge, UK: User Interface Technologies, Ltd., 2007.

HAZEL, PHILIP. Exim: The Mail Transfer Agent. Sebastopol, CA: O'Reilly Media, 2001.

MEERS, JASON. Getting started with EXIM. exim-new-users.co.uk, 2007.

