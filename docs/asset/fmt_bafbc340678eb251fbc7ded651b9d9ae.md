
## 第 20 章 电子邮件

`Selector` `email`
`Socket` `inet:8891@localhost`
`SignatureAlgorithm` `rsa-sha1`
`Syslog` `Yes`
`UserID` `dkim`
`X-Header` `Yes`
`Mode` `sv`
`InternalHosts` `/etc/mail/dkim-internal-hosts`

`dkim.conf` 中条目的通用格式为：

`parameter value`

井号 (`#`) 用于引入注释。分发版中包含一个注释良好的配置文件 `dkim-filter.conf.sample`，其中包含了变量的描述及其默认值。在 `dkim-filter.conf` 页面可以找到更详细的描述。

如果你正在配置中央邮件枢纽，`Domain` 行应该是你将要签名的全限定域名逗号分隔列表，或者是一个包含此类列表的文件名。

`KeyFile` 参数指定签名消息的私钥位置。假设文件名的第一部分是选择器（此处为 "`email`"）。

`MTA` 行列出了在验证后应始终对其邮件进行签名的 MTA。这类似于 `sendmail_DAEMON_OPTIONS` 配置参数中的 `Name` 部分。

`Socket` 规范指定了 TCP 端口；这里是 `localhost` `8891`。`SignatureAlgorithm` 可以是 `rsa-sha1` 也可以是 `rsa-sha256`；默认值已经足够新，所有 MTA 都能使用它。`X-Header` 参数指定 `dkim-filter` 应该为每条已签名的消息添加一个头行。`Mode` 用于签名 (`s`)、验证 (`v`) 或两者都有 (`sv`)。

`InternalHosts` 参数应指向一个文件，该文件包含一个出站邮件需要签名的主机列表。主机应按全限定域名列出。

若干配置选项可以帮助调试。检查 `MilterDebug`、`LogWhy` 和 `SyslogSuccess`。其中某些选项会产生大量的日志信息，一旦对结果满意后，务必关闭它们。

另一系列选项指定了对无法验证签名的消息的操作：`On-Default`、`On-BadSignature`、`On-DNSError`、`On-Security`、`On-InternalError` 和 `On-NoSignature`。它们各接受 `rejects`、`tempfail`、`accept` 和 `discard`。

该系统高度可配置，`dkim-filter.conf` 页面中描述了更多（80多个）参数。

### amavisd-new 中的 DKIM 配置

在 `amavisd-new` 中使用 DKIM，必须拥有版本 `0.33` 或更高的 Perl 模块 `Mail::DKIM`。如果没有，请从 CPAN 下载。你必须生成密钥对，开启 DKIM 验证和签名，指向你的私钥文件，并设置一些签名选项。

`amavisd` 本身可以为 DKIM 生成密钥：

```
$ amavisd genrsa /etc/mail/dkim/keys/email.key
```

## Exim 中的 DKIM 签名选项

| 选项 | 类型 | 必须 | 内容 |
|---|---|---|---|
| `dkim_domain` | 字符串 | 是 | 用于签名的域名 |
| `dkim_selector` | 字符串 | 是 | 选择器（名称） |
| `dkim_private_key` | 字符串 | 是 | 私钥或放松格式的文件 |
| `dkim_canon` | 字符串 | 否 | 规范化方法：简单 `simple` 或松弛 `relaxed` |
| `dkim_strict` | 字符串 | 否 | 如果为 `true`，签名错误将把邮件退回队列 |
| `dkim_sign_headers` | 字符串 | 否 | 签名包含的头部 |

前三个“选项”是强制性的，必须配置；其余选项是完全可选的。默认情况下，规范化方法（`dkim_canon`）为松弛（`relaxed`），导致签名错误的消息将没有签名（`dkim_strict`），且 Exim 使用 RFC4871 头部列表（`dkim_sign_headers`）。强制性选项非常直观，但如果你有一个拥有多个真实或虚拟域名的复杂站点，那么在定义它们时必须非常巧妙。

### 验证入站的签名消息

入站的 DKIM 签名消息在 `acl_smtp_dkim` ACL 中验证。该 ACL 为每个签名调用一次，并返回以下代码之一：

- `none` – 消息未签名
- `invalid` – 签名无法验证（密钥不可用或无效）
- `fail` – 头部、正文或两者签名验证失败
- `pass` – 签名有效

状态通过 `$dkim_verify_status` 变量返回，失败详情在 `$dkim_verify_reason` 变量标签中，这些标签允许访问签名的各种字段，并允许实现特殊策略（例如：标记来自 `gmail.com` 但没有签名的邮件，或拒绝来自 `paypal.com` 但未通过验证的邮件）。

### 完整示例

密钥选择器命名为 `dyyyyyy`，其中 `d` 代表日期的“d”，`yyyy` 是密钥生成的年份，`mm` 是生成的月份。密钥文件命名为 `rsa.private.selector.domain`，并存储在用宏 `DKKEY_DIR` 定义的密钥目录中。确保该目录可 `exim` 读取，但其他用户无法读取。

```
###### 定义数据库和密钥目录的宏

CONFIG_DIR = path_to_config_dir

DKIM_DIR = path_to_key_dir
```

```
###### 主部分：定义要签名的域名和所需的 DKIM acl

domainlist dkim_domains = cdb:CONFIG_DIR/dk.selector.cdb

ac_smtp_dkim = acl_process_dkim
```

```
###### acl：验证入站邮件的签名，添加头部

acl_process_dkim:

warn dkim_status = none

  add_header = @at_start-X-DKIM-Report: $dkim_verify_status[pass]

  if {($dkim_verify_status[pass]){$dkim_verify_reason} \
  (Signer=$dkim-cur_signer) (Testing-$dkim_key_testing)}
```

```
###### 路由器部分：放在 "dnslookup" 路由器之前，对非本地进行签名

dnslookup_signed:

driver = dnslookup

domains = !local_domains

transport = remote_dkim

condition = ${if match_domain($sender_address_domain) \
  +dkim_domains)}

no_verify
```

这些片段导致出站邮件被签名，且入站邮件的签名通过验证并添加 DKIM 报告头部。以下是该头部的示例：

> `X-DKIM-Report: pass (Sender@gmail.com) (Testing=0)`

如果你打算拒绝或惩罚签名未通过验证的消息，则需要进一步的策略。

路由器部分的 `no_verify` 行并非指 DKIM 验证，而是验证收件人地址；它在此路由器中已关闭，但在后续的 `dnslookup` 路由器中执行。做两次没有意义。

### Postfix 中的 DKIM

Postfix 中 DKIM 的实现是通过第 846 页描述的 `dkim-milter` 软件包实现的。生成你的密钥对并使用 `dkim-test` 进行测试；从发行版的示例构建 `dkim-filter.conf` 文件，然后教 Postfix 使用 `dkim-filter`。在 `main.cf` 中，在任何其他 milter 选项之后，添加以下行：
`smtmpd_milters = inet:localhost:8891`
`non_smtmpd_milters = inet:localhost:8891`
`milter_protocol = 2`
`milter_default_action = accept`

现在你只需要做的是启动 `dkim-filter` 并重启 `postfix`。

## 20.17 集成电子邮件解决方案

有很多集成电子邮件解决方案，从免费的开源产品到昂贵的商业产品不等。它们处理的不仅仅是电子邮件。常见的网关和会议功能包括

- 通讯录和共享联系人列表管理
- 日历和任务管理
- 列表和公告板
- 即时消息
- SSL/TLS 加密
- 存档和自动备份
- 支持移动设备（BlackBerry、iPhone 等）

这些软件包中的大多数包含一个配置 GUI，读者在处理这一巨大的章节时或或少需要它。（也许我们应该把这一节放在章节的开头而不是结尾。）许多产品的目标是替代 Microsoft Exchange。

有几个产品值得特别提及：

- Citadel (`https://citadel.org`) 是开源且免费的。
- Zimbra (`https://zimbra.com`) 是专有的。
- Kerio MailServer (`https://kerio.com`) 按用户授权。
- Communicate Pro (`https://communicate.com`) 是昂贵的。
- Cisco IronPort 是硬件。
- Sophos 和 Clearsw 是内置的。
- Microsoft Exchange 是传统的。

## 20.18 推荐阅读

我们没有将列出的参考文献混在一起，而是按照主题进行了分类。

### 通用垃圾邮件参考文献

CLAYTON, RICHARD. “Good Practice for Combating Unsolicited Bulk Email.” RIPE/Domenet.2000, `ripe.net/docs/206.html`.

FIELD, JULIAN. `MailScanner: A User Guide`. University of Southampton Department of Electronics,2007.

MCDALD, ALISTAIR. *SpamAssassin: A Practical Guide to Configuration, Customization, and Integration.* Packet Publishing,2004.

SCHWARTZ, ALAN. *SpamAssassin*. Sebastopol, CA: O’Reilly Media,2004.

WOLF, PAUL, CHARLIE SCOTT AND MIKE ERWIN. *The Anti-Spam Tool Kit*.erville, CA: Osborne,2004.

### sendmail 参考文献

COSTALES, BRYAN, CLAUS ASSMANN, GEORGE JANSEN, AND GREGORY NEIL SHAPIRO. *sendmail*, 4th Edition. Sebastopol, CA: O’Reilly Media,2007. 这本书是 `sendmail` 配置的权威教程——包含了系统管理员指南以及完整的参考部分。作者包含了两个 `sendmail` 开发人员（Claus 和 Greg），他们确保了技术的准确性并增加了见解。

安装说明和对配置文件的描述包含在 `sendmail Installation and Operation Guide` 中，可以在 `sendmail` 发行版的 `doc/op` 子目录下找到。该文档与 `cf` 目录下的 `README` 文件结合，提供了 `sendmail` 系统的良好视角。

`sendmail.org`, `sendmail.org/~ca`, 以及 `sendmail.org/~shapairo` 所有与 `sendmail` 的文档、HOWTOs 和教程。

### Exim 参考文献

HAZEL, PHILIM. The Exim SMTP Mail Server: Official Guide for Release 4, 2nd Edition. Cambridge, UK: User Interface Technologies,2007.

HAZEL, PHILIM. *Exim: The Mail Transfer Agent*. Sebastopol, CA: O’Reilly Media,2001.

MEERS, JASON. Getting started with EXIM. `emim-new-users.co.uk`,2007.

### 练习题

Exim 规范是 Exim 配置的定义文档。它非常详尽，并随着每个新版本的发布而更新。文本版本包含在发行版的 `doc/spec.txt` 文件中，也可以从 `exim.org` 获取 PDF 版本。该网站上还有几份操作指南文档。

### Postfix 参考文献

BLUM, RICHARD. Postfix. Saim Publishing, 2001.

DENT, KYLE D. Postfix: The Definitive Guide. Sebastopol, CA: O'Reilly Media, 2003.

HILDEBRAND, RALF, AND PATRICK KOETTER. The Book of Postfix: State of the Art Message Transport. San Francisco, CA: No Starch Press, 2005.

这本书是最好的；它会引导你完成 Postfix 配置的所有细节细节，即使对于复杂的环境也是如此。作者在 Postfix 社区中非常活跃，并定期在 `postfix-users` 邮件列表中参与。遗憾的是，这本书已经绝版了，但很容易买到二手副本。

`postfix.org/SOHO_README.html` 是一个关于如何在家庭或小型办公室环境中使用 Postfix 的指南。

### RFC

RFC 5321 和 5322 是 RFC 821 和 822 的当前版本。它们定义了 SMTP 协议以及互联网电子邮件的消息格式和地址格式。RFC 5335 和 5336 涵盖了国际化邮件地址的扩展。目前有近 90 份与邮件相关的 RFC，无法在此全部列出。更多信息请访问 `rfc-editor.org` 的通用 RFC 搜索引擎。

## 第 20 章

### 电子邮箱

#### 20.19 练习题

- E20.1 简要说明用户代理 (`MUA`)、投递代理 (`DA`) 和访问代理 (`AA`) 之间的区别。然后解释邮件传输代理 (`MTA`) 和邮件提交代理 (`MSA`) 之间的区别。

- E20.2 检查你本地服务器上的邮件队列。目录中是否存在残留文件（crust）？是否存在没有控制文件的消息，或者有控制文件没有消息？队列中最旧的邮件是什么？（需要 root 权限）。

- E20.3 解释什么是 MX 记录。为什么 MX 记录对邮件投递很重要？请举一个 MX 记录配置错误导致邮件无法投递的例子。

- E20.4 确定你站点邮件服务的设计，并按照第 754 页附图 B 的风格画图。入站邮件在哪里进行垃圾邮件或病毒扫描？出站邮件又是哪里？

- E20.5 比较使用 `/etc/mail/aliases` 与使用 LDAP 服务器或 MySQL 数据库存储邮件别名的区别。它们各自的优缺点是什么？

- E20.6 为以下邮件头写写简短描述。邮件经过了什么路径？它是发给谁的，又是投递给了谁？它在传输过程中花费了多久？

```
Delivered-To: sailingengi@gmail.com

Received: 10.231.143.81 with SMTP dt t7cs175323bibu;

Mon, 28 Dec 2009 20:15:20 (-0800)

Received: 10.231.157.131 with SMTP id

b3mr2134004bx.19.12620119841;

Mon, 28 Dec 2009 20:15:19 (-0800)

Return-Path: <garth@grsweb.com

Received: from mail-relay.astrust.com (mail-relay.astrust.com

[63.173.189.2]) by google.com with ESMTP id

12si19022498wn.27.dec.2009.12.28.20:15:19;

Mon, 28 Dec 2009 20:19 (-0800)

Received-SPF: neutral (google.com: 63.173.189.2 is not permitted nor denied by best guess record for domain of garth@grsweb.com) client-ip=63.173.189.2;

Authentication-Results: mx.com; spf=neutral (google.com:

63.173.189.2 is not permitted nor denied by best guess record for domain of garth@grsweb.com)smtp.mail=garth@grsweb

Received: from mout.perfora.net (mout.perfora.net [74.208.194.1]) by mail-relay.astrust.com, (8.12.11/8.12.11) with ESMTP id nBT4fi9r017821 from <eviat@astrust.com>; Mon, 28 Dec 2009 21:25:19 -0700

Received: from grsweb.com (wolverine.dreammost.com [75.119.201.185]) by ESMTP (node-emrus1) id MaORD-

1KGSS22TY-00uEuN; Mon, 28 Dec 2009 20:15:13 -0700
```
