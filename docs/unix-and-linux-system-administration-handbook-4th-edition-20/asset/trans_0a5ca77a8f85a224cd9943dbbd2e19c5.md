

## 第 20 章：电子邮箱

## 20.18 推荐阅读

我们没有将此处列出的参考文献杂乱在一起，而是按照 MTA（邮件传输代理）和主题对其进行了分类。

### 通用垃圾邮件参考文献

- CLAYTON, RICHARD. 《对抗未经请求的批量邮件的良好实践》。RIPE/Demon Internet. 2000, ripe.net/docs/ripe-2006.html.
  该文档面向 ISP（互联网服务提供商）。它包含了大量的策略信息以及一些指向技术主题的优良链接。

- FIELD, JULIAN. 《MailScanner：用户指南与训练手册》。南安普顿大学电子工程部门，2007。

- MCDALD, ALISTAIR. 《SpamAssassin：配置、定制与集成实战指南》。Packet Publishing, 2004。

- SCHWARTZ, AL. 《SpamAssassin》。Sebastopol, CA: O’Reilly Media, 2004。

- WOLFE, PAUL, CHARLIE SCOTT, AND MIKE ERWIN. 《反垃圾邮件工具箱》。Emeryville, CA: 2004。

### sendmail 参考文献

- COSTALES, BRYAN, CLAUS ASSMANN, GEORGE JANSEN, AND GREGORY NEIL SHAPI. 《sendmail，第 4 版》。Sebastopol, CA: O’Reilly Media, 2007。
  这本书是 sendmail 配置的权威著作——多达 1300 页。它包含了系统管理员指南以及完整的参考章节。同时也提供电子版。作者包含了两位 sendmail 开发人员（Claus 和 Greg），他们负责确保技术正确性并注入了深度见解。

  安装说明和对配置文件的良好描述可以在《Sendmail 安装与操作指南》中，该指南可以在 sendmail 分发版的 `doc/sub` 目录下找到。该文档是完整的，结合 `cf` 目录下的 `README` 文件，可以让你对 sendmail 系统有一个深入细致的了解。

  sendmail.org、sendmail.org/~ca 和 sendmail.org/~gashapiro 均包含与 sendmail 相关的文档、HOWTO 和教程。

### Exim 参考文献

- HAZEL, PHILIP. 《Exim SMTP 邮件服务器：第 4 版官方指南，第 2 版》。Cambridge, UK: User Interface Technologies, Ltd., 2007。

- HAZEL, PHILIP. 《Exim：邮件传输代理》。Sebastopol, CA: O’Reilly Media, 2001。

- MEERS, JASON. 《入门 EXIM》。exim-new-users.co.uk, 2007。

### 练习

Exim 规范是 Exim 配置的定义文档。它非常完整，并随着每个新发行版的发布而更新。文本版本包含在发行版的 `doc/spec.txt` 文件，PDF 版本可从 exim.org 获取。网站上还有几个 how-to 文档。

### Postfix 参考文献

- BLUM, RICHARD. 《Postfix》。Sams Publishing, 2001。

- DENT, KYLE D. 《Postfix：权威指南》。Sebastopol, CA: O'Reilly Media, 2003。

- HILDEBRANDT, RALF, AND PATRICK KOETTER. 《Postfix 之书：消息传输状态》。San Francisco, CA: No Starch Press, 2005。
  这本书是最好的；它指导你完成复杂环境下的 Postfix 配置的所有细节。作者在 Postfix 社区非常活跃，并定期在 postfix-users 邮件列表中参与。遗憾的是，这本书已经绝版了，但很容易买到二手书。

  postfix.org/SOHO_README.html 是一个关于在家庭或小型办公室环境中使用 Postfix 的指南。

### RFC

RFC 5321 和 5322 是 RFC 821 和 822 的当前版本。它们定义了 SMTP 协议以及互联网邮件的消息和地址格式。RFC 5335 和 5336 涵盖了国际化电子邮件地址的扩展。目前有近 90 个与邮件相关的 RFC，无法在此全部列出。更多信息请参见 rfc-editor.org 的通用 RFC 搜索引擎。

## 20.19 练习

- E20.1 简要说明用户代理（MUA）和接入代理（AA）之间的区别。然后解释邮件传输代理（MTA）和邮件提交代理（MSA）之间的区别。
- E20.2 检查你本地邮件服务器上的邮件队列。是否存在没有控制文件的消息，或者有控制文件没有消息？队列中最旧的邮件是什么？（需要 root 权限）
- E20.3 解释什么是 MX 记录。为什么 MX 记录对邮件投递很重要？举例说明配置错误的 MX 记录可能导致邮件无法投递的情况。
- E20.4 确定你站点邮件服务的设计，并按照第 754 页附图 B 的风格绘图。入站邮件在哪里进行垃圾邮件或病毒扫描？出站邮件呢？

![](img/579efec8c67772f31ecf34844bbb71a2_903_0.png)

- E20.5 比较使用 `/etc/mail/aliases` 与使用 LDAP 或 MySQL 数据库存储邮件别名的区别。各自的优缺点是什么？
- E20.6 为以下邮件头部写一段简要描述。这封邮件经过了什么路径？发给谁的，又是投递给了谁的？在传输过程中花费了多久？
（此处为复杂的邮件头部示例，根据翻译要求保留其代码格式且不翻译内部内容）
```
