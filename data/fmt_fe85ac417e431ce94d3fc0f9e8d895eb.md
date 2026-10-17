
```
# service httpd start
# chkconfig httpd on
```

### 3. 按以下方式为您的站点创建密码：

```
# /usr/lib/mailman/bin/mmsitepass
New site password: ******
Again to confirm password: ******
```

### 4. 编辑 `/usr/lib/mailman/Mailman/mm_cfg.py` 文件并更改 `DEFAULT_URL_HOST` 和 `DEFAULT_EMAIL_HOST` 值。例如，我正在配置邮件列表的计算机的主机名是 `toys.linuxtoys.net`。默认的电子邮件主机是 `linuxtoys.net`。值将显示如下：

```
DEFAULT_EMAIL_HOST = 'toys.linuxtoys.net'
DEFAULT_URL_HOST_DEF = 'linuxtoys.net'
```

您可以将这些值保留为 `$fqdn$`，以简单地使用本地计算机的完全限定域名。

### 5. 编辑 `/etc/httpd/conf.d/mailman.conf` 文件。要使对 mailman 的查询导向 listinfo 页面，请取消该文件底部 RedirectMatch 行的注释，并更改该行以包含您的完全限定域名。例如，当我为 `linuxtoys.net` 邮件列表执行此操作时，该行显示如下：

```
RedirectMatch  ^~/mailman/[\/]*\$ http://www.linuxtoys.net/mailman/listinfo
```

### 6. 要创建一个 mailman 邮件列表，您必须首先创建一个未填充内容的名为 mailman 的邮件列表。与该列表一起，您必须为负责管理该列表的人员分配电子邮件和初始密码。为此，请输入以下内容：

```
# /usr/lib/mailman/bin/newlist mailman
Enter the email of the person running the list:  chris@linuxtoys.net
Initial mailman password:  *********
Hit enter to notify mailman owner...
```

### 7. 按以下方式启动 mailman 服务：

```
# service mailman start
# chkconfig mailman on
```

### 8. 使用 `newlist` 命令创建新的邮件列表，如下所示：

```
# /usr/lib/mailman/bin/newlist
Enter the name of the list:  pro
Enter the email of the person running the list:  chris@linuxtoys.net
Initial pro password:  ****
```

要完成创建邮件列表，您必须通过添加以下行并运行 `newaliases` 程序来编辑 `/etc/aliases`（或等效）文件：

```
## pro mailing list
pro:                  "/usr/lib/mailman/mail/mailman post pro"
pro-admin:            "/usr/lib/mailman/mail/mailman admin pro"
pro-bounces:          "/usr/lib/mailman/mail/mailman bounces pro"
pro-confirm:          "/usr/lib/mailman/mail/mailman confirm pro"
pro-join:             "/usr/lib/mailman/mail/mailman join pro"
pro-leave:            "/usr/lib/mailman/mail/mailman leave pro"
pro-owner:            "/usr/lib/mailman/mail/mailman owner pro"
pro-request:          "/usr/lib/mailman/mail/mailman request pro"
pro-subscribe:        "/usr/lib/mailman/mail/mailman subscribe pro"
pro-unsubscribe:      "/usr/lib/mailman/mail/mailman unsubscribe pro"
```

### 9. 将刚才显示的文字（从 `## pro mailing list` 行开始）复制并粘贴到 `/etc/aliases` 文件的末尾。

### 10. 运行 `newaliases` 命令。此时，您应该能够通过网络浏览器查看新的邮件列表。在本地系统的 Web 浏览器中，在地址栏中输入以下名称：

```
http://localhost/mailman/listinfo
```

### 11. 如果一切看起来正常工作，开始添加更多的邮件列表。在我的例子中，我创建了一个名为 projectlist 的邮件列表。该项目的名称显示在图 19-3 中的列表中。

### 12. 选择该项目名称（点击它）。该项目的信息页面应该会显示出来。

### 13. 滚动到该页面底部并点击项目管理界面链接。

### 14. 当提示时，输入列表管理员密码。现在您可以配置邮件列表的外观、风格和行为。您希望考虑的重要信息包括：

- **隐私选项** — 您希望列表是公开的还是私有的（例如，仅限您所在的组织内部）？您希望谁能够查看您的成员列表？
- **发送过滤器** — 谁可以向列表发布消息？列表是经过审核的还是未经审核的？列表是否可能只单向流动，例如作为联系客户的一种方式？
- **成员管理** — 您的成员可以看到其他成员的信息吗？您的成员添加和移除政策是什么？

### 15. 完成配置选项后，请务必提交您的更改。

此时，您可以允许用户加入列表。鼓励他们探索并设置自己的用户偏好。

如果您在配置 mailman 时遇到问题，请参阅 `/usr/share/doc/mailman-*` 目录中的 `INSTALL`、`REDHAT` 和 `README` 文件。

![](img/fb202c163797a743c3c6cf236316bc96_852_0.png)

图 19-3：在 mailman 中创建多个邮件列表。

## 摘要

Fedora 包含了一整套用于配置和管理邮件服务器的工具。对于邮件传输代理（MTA），Fedora 包含 `sendmail` 和 `Postfix` 软件包。两者都被认为是优秀的、专业级的邮件服务器。

为了允许用户从服务器访问其邮箱，Fedora 包含 `dovecot` 软件包。该软件包实现了 POP3 和 IMAP 协议，以便电子邮件可以被下载或在服务器上操作。您还可以配置 `SquirrelMail`，以允许用户通过基于 Web 的界面访问他们的邮件。

书中包含的信息有助于保护您的邮件服务免受入侵者侵害。特别是，诸如 `SpamAssassin` 的过滤软件和诸如 `Clamav` 的病毒扫描软件对于保护您的邮件服务客户端免受伤害至关重要。

要在 Fedora 中设置邮件列表，可以使用 `mailman` 软件包。除了包含一些非常灵活配置工具外，`mailman` 还提供了简单的基于 Web 的接口来访问邮件列表设置和存档。

# 第 20 章

## 设置 FTP 服务器

### 本章内容

- 理解 FTP 服务器
- 使用 vsFTPd FTP 服务器
- 获取更多关于 FTP 服务器的信息

文件传输协议 `FTP` 多年来一直是互联网上共享文件的标准方法。尽管随着 Web 的普及，使得 Gopher 和 WAIS 等文档数据库服务变得过时，但 FTP 服务器仍然是向公众提供文档和软件目录的最常见方式。

文件共享应用程序，如 `NFS` 和 `Samba`，是在私有网络中共享文件和目录的优秀工具。然而，对于需要在公共网络上共享大量文件的组织来说，FTP 服务器软件提供了更强大的工具来共享文件并保护您的计算机系统。此外，FTP 客户端软件（用于访问 FTP 服务器）适用于任何可以访问网络的计算机。

本章描述了如何使用 Very Secure FTP Server 软件包 `vsFTPd` 来设置和维护 FTP 服务器。

配置您的 FTP 服务器以允许用户上传文件到服务器，比仅允许下载涉及更多的风险。任何人都可能上传恶意文件、覆盖其他文件，或者，取决于配置，将文件放置在非预期的位置。为了帮助缓解这种风险，您可以将服务器设置在一个 `chroot` 环境中，以限制对文件系统的访问。
