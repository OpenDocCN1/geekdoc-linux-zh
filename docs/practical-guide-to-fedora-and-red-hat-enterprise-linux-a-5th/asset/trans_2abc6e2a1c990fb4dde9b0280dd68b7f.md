

如前文所述，SpamAssassin 会重写其评定为垃圾邮件的电子邮件的主题行。配置文件中有一个 `rewrite_subject` 关键字用于控制此行为。该关键字后跟的 1 表示 SpamAssassin 将重写主题行。0（零）则关闭此行为。

SpamAssassin 被设置为重写其评定为垃圾邮件的电子邮件的主题行。配置文件中的 `rewrite_header` 关键字用于控制此行为。关键字后跟随的 Subject 一词告诉 SpamAssassin 重写主题行。

```
rewrite_header Subject [SPAM]
```

`required_hits` 关键字指定了邮件在被 SpamAssassin 视为垃圾邮件前必须达到的最小命中次数。默认值为 5.0。将此关键字的值设置为更高的数字，可以使 SpamAssassin 将更少的邮件标记为垃圾邮件。

`required_score` 关键字指定了邮件在被 SpamAssassin 视为垃圾邮件前必须达到的最低分数。默认值为 5.00。将此关键字的值设置为更高的数字，可以使 SpamAssassin 将更少的邮件标记为垃圾邮件。

```
required_score 5.00
```

当设置为 0（零）时，`report_safe` 关键字会使 SpamAssassin 修改其评定为垃圾邮件的邮件标头。

有时，本应被标记为垃圾邮件的邮件未被标记，或者本不应被标记为垃圾邮件的邮件却被标记了。使用 `whitelist_from` 关键字指定永远不应被标记为垃圾邮件的地址，使用 `blacklist_from` 指定始终应被标记为垃圾邮件的地址：

```
whitelist_from sams@example.com
blacklist_from *@spammer.net
```

你可以在 `whitelist_from` 和 `blacklist_from` 行上指定多个地址，地址之间用空格分隔。每个地址都可以包含通配符。若要白名单化所有从 example.com 域名发送邮件的人，请使用 `whitelist_from` *@example.com。你可以使用多行 `whitelist_from` 和 `blacklist_from` 指令。

## 在邮件服务器上运行 SpamAssassin

本节介绍如何在邮件服务器上设置 SpamAssassin，以便它在将邮件发送到用户之前，先处理所有交付到本地系统的电子邮件。它展示了如何使用 procmail 作为 MDA，并让 procmail 通过 spamc 发送邮件。首先，确保 MTA（sendmail）使用 procmail 作为 MDA。以下 sendmail.mc 中的第一行指定了 procmail 命令、其路径和标志。MAILER 行将 procmail 定义为邮件器。你可能不需要更改这两行中的任何一行。

```
FEATURE(local_procmail,'',''procmail -t -Y -A $h -d $u')dn
MAILER(procmail)dn
```

另外，请确保服务器系统上已安装 `procmail` 软件包。接下来，如果 `/etc/procmailrc` 配置文件不存在，请创建它，使该文件由 `root` 拥有，并具有 644 权限和以下内容。如果它已存在，请从以下文件中追加最后两行：

```
$ cat /etc/procmailrc
DROPPRIVS=yes
:$0 fw
| /usr/bin/spamc
```

该文件的第一行确保 `procmail` 以尽可能少的权限运行。接下来的两行实现了一条规则，将每个用户的传入电子邮件通过 `spamc` 管道传输。`:$0` 告知 `procmail` 后面跟随一条规则。`f` 标志表示过滤器；`w` 标志使 `procmail` 等待过滤器完成并检查退出代码。最后一行指定使用 `/usr/bin/spamc` 实用工具作为过滤器。

配置好此文件后，服务器系统接收的所有用于本地投递的电子邮件都会经过 SpamAssassin 处理，SpamAssassin 会根据全局配置文件中的选项对其进行评级。服务器系统上拥有账户的用户可以在其 `~/.spamassassin/user_prefs` 文件中覆盖全局 SpamAssassin 配置设置。

当你在服务器上运行 SpamAssassin 时，通常希望保守地评估邮件，以便更少的正常邮件被标记为垃圾邮件。将 `required_hits` 设置在 6-10 的范围内通常是合适的。此外，你不想自动删除任何邮件，因为这可能会阻止用户收到非垃圾邮件。当服务器将邮件标记为可能是垃圾邮件时，用户可以手动或自动过滤垃圾邮件，并决定如何处理。

## Web 邮件

传统上，你使用专用的电子邮件客户端（如 KMail）阅读电子邮件。最近，使用 Web 应用程序阅读电子邮件变得更加普遍。如果你有一个商业提供商（如 Gmail、HotMail 或 Yahoo! Mail）的电子邮件账户，你会使用 Web 浏览器阅读电子邮件。以此方式阅读的电子邮件称为 *Web 邮件*。与你在专用客户端上阅读的电子邮件不同，你可以从任何能打开浏览器的地方阅读 Web 邮件：例如，你可以从网吧或朋友的电脑检查你的电子邮件。

SquirrelMail（`squirrelmail` 软件包）提供 Web 邮件服务；SquirrelMail 文件位于 `/usr/share/squirrelmail`。如果你想运行 SquirrelMail，你必须运行 IMAP（第 689 页），因为 SquirrelMail 使用 IMAP 接收和验证电子邮件。你还必须运行 Apache（第 26 章），以便用户可以使用浏览器连接到 SquirrelMail。

SquirrelMail 是模块化的：你可以轻松地使用插件添加功能。有允许你共享日历的插件，还有允许你通过 Web 邮件界面更改密码的插件。有关更多信息，请参阅 SquirrelMail 网站上的插件部分。

创建以下链接以便从 Web 访问 SquirrelMail：

```
# ln -s /usr/share/squirrelmail /var/www/html/mail
```

有了此链接，你可以将 Web 浏览器指向 http://localhost/mail 来显示 SquirrelMail 登录页（图 20-1）。

接下来，使用 /usr/share/squirrelmail/config 中的 `conf.pl` 脚本来配置 SquirrelMail：

```
# cd /usr/share/squirrelmail/config
# ./conf.pl
SquirrelMail Configuration : Read: config_default.php (1.4.0)
----------------------------------------------------------------
Main Menu --
1. Organization Preferences
2. Server Settings
3. Folder Defaults
4. General Options
5. Themes
6. Address Books
7. Message of the Day (MOTD)
8. Plugins
9. Databases
10. Languages

D.  Set pre-defined settings for specific IMAP servers

    C   Turn color on
    S   Save data
    Q   Quit

    Command >>
```

为了使 SquirrelMail 正常工作，你唯一必须设置的项是服务器的域名（来自“服务器设置”页面）。SquirrelMail 提供几种主题；如果你不喜欢 SquirrelMail 的外观，可以从“主题”页面选择另一个主题。

![](img/f28adb66a7398a382f0505e0ba74a872_727_0.png)

**图 20-1** SquirrelMail 登录页

## 邮件列表

如果你定期向同一大组人发送电子邮件，邮件列表可能是一项资产。与在电子邮件的 To 或 Cc 字段中列出众多收件人或将同一电子邮件单独发送给多人相比，邮件列表提供了几个优势：

- **匿名性**——电子邮件的收件人都看不到其他收件人的地址。
- **归档**——发送到列表的电子邮件存储在一个中心位置，列表成员或公众（由列表管理员指定）可以浏览。
- **访问控制**——你可以轻松指定谁可以向列表发送电子邮件。
- **一致性**——当你使用 To 或 Cc 向一群人发送邮件时，很容易遗漏想加入列表的人，并保留想退出列表的人。
- **效率**——邮件列表应用程序在时间上分散电子邮件传输，以免使邮件服务器过载。

Mailman 提供邮件列表支持。Mailman 的主体位于 `/usr/lib/mailman`。配置文件是 `/etc/mailman/mm_cfg.py`，它是 `/usr/lib/mailman/Mailman/mm_cfg.py` 的一个链接。在使用 Mailman 之前，你需要用单引号括起的本地域名替换 `mm_cfg.py` 中以下两行中的 `fqdn`：

```
DEFAULT_URL_HOST = 'fqdn'
DEFAULT_EMAIL_HOST = 'fqdn'
```

进行这些更改后，使用 `newlist` 工具创建一个新的邮件列表：

```
# /usr/lib/mailman/bin/newlist
Enter the name of the list: painting_class
Enter the email of the person running the list: helen@ccorp.com
Initial painting_class password:
```

要完成创建你的邮件列表，你必须通过添加以下行来编辑 /etc/aliases（或等效）文件，并可能运行 'newaliases' 程序：

```
# painting_class mailing list
painting_class:              "/usr/lib/mailman/mail/mailman post painting_class"
painting_class-admin:        "/usr/lib/mailman/mail/mailman admin painting_class"
painting_class-bounces:      "/usr/lib/mailman/mail/mailman bounces painting_class"
painting_class-confirm:      "/usr/lib/mailman/mail/mailman confirm painting_class"
painting_class-join:         "/usr/lib/mailman/mail/mailman join painting_class"
painting_class-leave:        "/usr/lib/mailman/mail/mailman leave painting_class"
painting_class-owner:        "/usr/lib/mailman/mail/mailman owner painting_class"
painting_class-request:      "/usr/lib/mailman/mail/mailman request painting_class"
painting_class-subscribe:    "/usr/lib/mailman/mail/mailman subscribe painting_class"
painting_class-unsubscribe:  "/usr/lib/mailman/mail/mailman unsubscribe painting_class"
```

按回车键通知 painting_class 所有者...

