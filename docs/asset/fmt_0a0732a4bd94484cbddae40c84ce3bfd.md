
In the first part of this series on using LDAP with the Cyrus IMAP mail delivery server (`LJ`, November 2003), we got as far as installing and setting up Cyrus IMAP and Cyrus SASL. In this article, we add some users to Cyrus IMAP and configure Postfix to deliver mail to the Cyrus IMAP server.

在本系列关于使用 LDAP 与 Cyrus IMAP 邮件投递服务器的文章的第一部分（`LJ`，2003 年 11 月），我们进行到了安装和设置 Cyrus IMAP 和 Cyrus SASL。在本文中，我们向 Cyrus IMAP 添加一些用户并配置 Postfix 将邮件投递到 Cyrus IMAP 服务器。

### Cyrus IMAP Documentation

### Cyrus IMAP 文档

Before we dive back in to Cyrus IMAP configuration and administration, a note about documentation. Cyrus IMAP comes with an administrator’s manual in HTML format. In the SuSE distribution, the manual is in `/usr/share/doc/packages/cyrus-imapd/doc`, and in Simon Matter’s Red Hat SRPM distribution (see Part I of this article) it’s in `/usr/share/doc/cyrus-imapd-2.1.12`. The link misleadingly labeled `Installation` actually leads not only to Cyrus installation instructions but to configuration and administration instructions as well. Besides this documentation, several man pages also are included with Cyrus IMAP, most notably `imapd.conf(5)`, `imapd(8)` and `cyradm(1)`.

在重新深入 Cyrus IMAP 配置和管理的之前，先说一下文档。Cyrus IMAP 附带一份 HTML 格式的管理员手册。在 SuSE 发行版中，手册位于 `/usr/share/doc/packages/cyrus-imapd/doc`，而在 Simon Matter 的 Red Hat SRPM 发行版中（参见本文第一部分）它位于 `/usr/share/doc/cyrus-imapd-2.1.12`。错误标记为 `Installation` 的链接不仅通向 Cyrus 安装说明，还通向配置和管理的说明。除此之外，Cyrus IMAP 还包含多个手册页，其中最值得注意的是 `imapd.conf(5)`、`imapd(8)` 和 `cyradm(1)`。

In addition to Cyrus IMAP’s included documentation, I recommend the book `Managing IMAP` by Dianna and Kevin Mullet (O’Reilly & Associates, 2000). As far as I know, it’s the only book dedicated to IMAP. Although its coverage of Cyrus IMAP doesn’t extend to LDAP, it’s a well-written book that clearly explains IMAP concepts and Cyrus IMAP administration; it also covers UW-IMAP in some detail.

除了 Cyrus IMAP 自带的文档外，我推荐 Dianna 和 Kevin Mullet 所著的《`Managing IMAP`》（O’Reilly & Associates，2000）。据我所知，这是唯一一本专门介绍 IMAP 的书籍。尽管它对 Cyrus IMAP 的覆盖范围不包括 LDAP，但这是一本写得很好的书籍，清晰地解释了 IMAP 概念和 Cyrus IMAP 管理；它还详细介绍了 UW-IMAP。

### Using cyradm

### 使用 cyradm

Cyrus IMAP comes with a Perl script, `cyradm`, that provides the most convenient way to create and manage user mailboxes. You should understand several things before using `cyradm`. First, you should run `cyradm` from any account with which you also read e-mail. In other words,

Cyrus IMAP 附带一个 Perl 脚本 `cyradm`，它提供了创建和管理用户邮箱最方便的方式。在使用 `cyradm` 之前，你应该了解几件事。首先，你应该从你也用来阅读电子邮件的任何账户运行 `cyradm`。换句话说，

you never should use an IMAP administrative account as an e-mail account. Due to unusual write-access permissions, using such accounts to read or send e-mail can have strange negative effects on your server. As we learned last time, Cyrus administrative accounts are named according to the variable `admins` in `/etc/imapd.conf`.

你永远不应该将 IMAP 管理账户用作电子邮件账户。由于不寻常的写访问权限，使用此类账户阅读或发送电子邮件可能会对服务器产生奇怪的负面影响。正如我们上次所学，Cyrus 管理账户的名称根据 `/etc/imapd.conf` 中的变量 `admins` 命名。

Second, `cyradm` uses the same authentication method as does the rest of Cyrus IMAP. In my previous column, we determined this by setting `/etc/imapd.conf`’s variable `sasl_pwcheck_method` to `saslauthd` and by editing `/etc/sysconfig/saslauthd` to use either LDAP or, in the case of SuSE, to use PAM. PAM itself can be configured to use LDAP for IMAP transactions in the files `/etc/pam.d/imap` and `/etc/openldap/ldap.conf`. In short, `cyradm` identifies and authenticates administrative users with LDAP, assuming you’ve correctly configured LDAP support in Cyrus IMAP, as described last time.

其次，`cyradm` 使用与 Cyrus IMAP 其余部分相同的身份验证方法。在我之前的专栏中，我们通过将 `/etc/imapd.conf` 的变量 `sasl_pwcheck_method` 设置为 `saslauthd` 并编辑 `/etc/sysconfig/saslauthd` 以使用 LDAP 或在 SuSE 的情况下使用 PAM 来确定这一点。PAM 本身可以在文件 `/etc/pam.d/imap` 和 `/etc/openldap/ldap.conf` 中配置为对 IMAP 事务使用 LDAP。简而言之，`cyradm` 使用 LDAP 来识别和验证管理员用户，前提是你已正确配置 Cyrus IMAP 中的 LDAP 支持，如上次所述。
