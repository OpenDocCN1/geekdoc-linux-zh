
该文件的第一行确保`procmail`以最小权限运行。接下来的两行实现了一个规则，将每个用户的入站邮件通过`spam`过滤器。`:0`告诉`procmail`后面有一个规则。`f`标识一个过滤器；`procmail`等待过滤器完成并检查退出码。最后一行指定将使用`/usr/bin/spam`工具。

有了这个文件，服务器接收的所有本地递送邮件都会通过SpamAssassin，它根据全局配置文件中的选项进行评分。在服务器系统中拥有账户的用户可以在`~/.spamassassin/user_prefs`文件中覆盖SpamAssassin配置设置。

在服务器上运行SpamAssassin时，你通常希望保守地对邮件评分，以便标记较少的邮件为垃圾邮件。将`required_hits`设置在6-10之间是合适的。另外，不要自动删除，因为这可能会阻止用户收到非垃圾邮件。当服务器将邮件标记为可能是垃圾邮件时，用户可以手动过滤垃圾邮件并决定如何处理它。

## 额外的邮件工具

本节涵盖了Web邮箱（Webmail）和邮件列表。此外，还讨论了如何设置IMAP和POP3服务器。

## Web邮箱 (WEBMAIL)

传统上，你使用`Evolution`等专用邮件客户端读取邮件。最近，使用Web应用程序读取邮件变得越来越普遍。如果你拥有`Gmail`、`HotMail`或`Yahoo Mail`等商业提供者的邮件账户，你会使用Web浏览器读取邮件。这种方式读取邮件被称为Web邮箱。与你在专用客户端上读取的邮件不同，你可以在此后识别或阻止类似的不受欢迎的邮件。参见第1段：热带1周
我们要去哪里！那里有大量的女性、酒精、等等！
这是享乐岛屿上每个男人的梦想。 [...]
内容分析: (24.5分)
`MSGID_DSBL` (4.3分) 邮件由垃圾邮件工具生成（零变体）
`INVALID_DATE_TZ_ABSURD` (4.3分) 邮件头部：`Date`未由时间生成
`MSGID_OF_SPAM_420ZERO` (3.5分) 正文：假期优惠
`VACATION_SUM` (1.9分) 主题：包含 "remove"
`MSGID_OUTLOOK_TIME` (4.4分) `Message-Id`是伪造的（`Outlook`格式）
`DATE_IN_FUTURE_06_12` (1.3分) 日期在接收时间6到12小时后
`RCVD_IN_NJABL` (9.4分) `RBL`：通过`dsnjabl.org`的中继接收
`RCVD_IN_DSBL` (9.9分) 于`94.99.200.dsbl.org`中发现
`RCVD_IN_UNCONFIRMED_DSBL` (0.5分) `RBL`：通过未确认的`.dsbl.org`接收
`XBL_NJABL_OPEN_PROXY` (0.5分) `RBL`：发送者是代理/中继/hotmail/垃圾邮件发送者
`XBL_OPEN` (2.6分) `RBL`：通过`list.dsbl.org`接收（发现`211.157.63.200.list.dsbl.org`）
`X-Spam-Flag`: test
`Subject`: [SPAM] 未收到

## 配置 SPAMASSASSIN

SpamAssassin在多个位置查找配置文件；详细信息请参阅`assassin`手册。最容易处理的配置文件是`/etc/mail/spamassassin/local.cf`。你可以编辑此文件来全局配置SpamAssassin。你可以在`~/.spamassassin/user_prefs`文件中覆盖这些全局选项并添加自己的选项。你可以将本节讨论的选项放在这两个任何一个文件中。

例如，你可以配置SpamAssassin重写它评定为垃圾邮件的邮件的主题。配置文件中的`rewrite_header`关键字控制此行为。该关键字后的单词`Subject`告诉SpamAssassin重写主题行。删除下面一行的`#`符号即可开启此行为：

```
# rewrite_header Subject *****SPAM******
```

`required_score`指定了邮件在被SpamAssassin认为是垃圾邮件之前必须接收的最低分数。默认值为5.00。将此关键字的值设置为更高的数字可以使SpamAssassin标记更少的邮件为垃圾邮件。

```
required_score 5.00
```

有时，应该被标记为垃圾邮件的地址邮件没有被标记，而不应该标记为垃圾邮件的地址邮件被标记了。使用`whitelist_from`关键字指定永远不要被标记为垃圾邮件的地址，使用`blacklist_from`指定应该始终被标记为垃圾邮件的地址：

```
whitelist_from sams@example.com

blacklist_from *@spammer.net
```

你可以在`whitelist_from`和`blacklist_from`行上用空格分隔指定多个地址。每个地址都可以包含通配符。要将所有从`example.com`域名发送邮件的人加入白名单，请使用`whitelist_from *@example.com`。

## 在邮件服务器上运行 SPAMASSIN

本节解释了如何在邮件服务器上设置SpamAssassin，以便在将邮件发送给用户之前处理所有递送到本地系统的邮件。它展示了如何使用`procmail`作为MDA，让`procmail`通过垃圾过滤器发送邮件。

首先确保服务器上安装了`procmail`软件包。如果`/etc/procmail`配置文件不存在，请创建它并确保其所有者为`root`且权限为`644`，并将以下内容追加到其中：如果它已存在，

```
$ cat /etc/procmail
DROP=yes:0| /usr/bin/spam
```

该文件的第一行确保`procmail`以最小权限运行。接下来的两行实现了一个规则，将每个用户的入站邮件通过`spam`过滤器。`:0`告诉`procmail`后面有一个规则。`f`标识一个过滤器；`procmail`等待过滤器完成并检查退出码。最后一行指定将使用`/usr/bin/spam`工具。

有了这个文件，服务器接收的所有本地递送邮件都会通过SpamAssassin，它根据全局配置文件中的选项进行评分。在服务器系统中拥有账户的用户可以在`~/.spamassassin/user_prefs`文件中覆盖SpamAssassin配置设置。

在服务器上运行SpamAssassin时，你通常希望保守地对邮件评分，以便标记较少的邮件为垃圾邮件。将`required_hits`设置在6-10之间是合适的。另外，不要自动删除，因为这可能会阻止用户收到非垃圾邮件。当服务器将邮件标记为可能是垃圾邮件时，用户可以手动过滤垃圾邮件并决定如何处理它。

## 额外的邮件工具

本节涵盖了Web邮箱（Webmail）和邮件列表。此外，还讨论了如何设置IMAP和POP3服务器。

## Web邮箱 (WEBMAIL)

传统上，你使用`Evolution`等专用邮件客户端读取邮件。最近，使用Web应用程序读取邮件变得越来越普遍。如果你拥有`Gmail`、`HotMail`或`Yahoo Mail`等商业提供者的邮件账户，你会使用Web浏览器读取邮件。这种方式读取邮件被称为Web邮箱。与你在专用客户端上读取的邮件不同，你可以在此后识别或阻止类似的不受欢迎的邮件。参见第1段：热带1周
我们要去哪里！那里有大量的女性、酒精、等等！
这是享乐岛屿上每个男人的梦想。 [...]
内容分析: (24.5分)
`MSGID_DSBL` (4.3分) 邮件由垃圾邮件工具生成（零变体）
`INVALID_DATE_TZ_ABSURD` (4.3分) 邮件头部：`Date`未由时间生成
`MSGID_OF_SPAM_420ZERO` (3.5分) 正文：假期优惠
`VACATION_SUM` (1.9分) 主题：包含 "remove"
`MSGID_OUTLOOK_TIME` (4.4分) `Message-Id`是伪造的（`Outlook`格式）
`DATE_IN_FUTURE_06_12` (1.3分) 日期在接收时间6到12小时后
`RCVD_IN_NJABL` (9.4分) `RBL`：通过`dsnjabl.org`的中继接收
`RCVD_IN_DSBL` (9.9分) 于`94.99.200.dsbl.org`中发现
`RCVD_IN_UNCONFIRMED_DSBL` (0.5分) `RBL`：通过未确认的`.dsbl.org`接收
`XBL_NJABL_OPEN_PROXY` (0.5分) `RBL`：发送者是代理/中继/hotmail/垃圾邮件发送者
`XBL_OPEN` (2.6分) `RBL`：通过`list.dsbl.org`接收（发现`211.157.63.200.list.dsbl.org`）
`X-Spam-Flag`: test
`Subject`: [SPAM] 未收到

## 第 20 章：设置邮件服务器、客户端及更多

安装以下软件包：

- `squirrelmail`
- `apache2` (page 858; 安装`​squirrelmail`时依赖)
- `exim4` (page 678) 或`sendmail`
- `dovecot-imapd` (page 699) 或另一个IMAP服务器

启动你不需要启动`Squirrelmail`，也不需要为其开启任何端口。但是，如果服务器运行在带有防火墙的系统上，你需要配置、启动`exim4` (page 682)、IMAP (page 699) 和`Apache` (page 859)。

配置`SquirrelMail`文件位于`/usr/share/squirrelmail`。创建以下链接以便Web访问：

```
$ sudo ln -s /usr/share/squirrelmail /var/www/mail
```

使用以下命令配置`SquirrelMail`：

```
$ squirrelmail-configure : 读取: config.php (1.4.0)

主菜单 --
1. 组织设置
2. 服务器设置
3. 文件夹默认
4. 普通选项
5. 主题
6. 地址簿
7. 今日主题 (MOTD)
8. 插件
9. 数据库
10. 语言

D. 为特定的 IMAP 服务器设置预定义设置
```

此菜单有多个层次。当你选择一个设置（而不是子菜单）时，`squirrelmail-configure`会显示帮助你决定如何回答问题的。设置服务器域名（`Server Settings`页面上的第1项）和你正在使用的IMAP服务器名称（主菜单上的`D`项）。`SquirrelMail`提供多个主题；如果你不喜欢`SquirrelMail`的外观，请从主题（第5项）中选择另一个主题。完成更改后，退出`squirrelmail-configure`。每当你想要更改`SquirrelMail`配置时，运行`squirrelmail-configure`。

`SquirrelMail`提供了一个测试其配置的页面。将服务器上的浏览器指向`localhost/mail/src/configtest.php`。将`localhost`替换为IP地址或另一个系统查看页面的服务器完全限定域名(`FQDN`)。`SquirrelMail`会检查其配置并在页面上显示结果。图20-2显示`SquirrelMail`无法连接到本地系统的IMAP服务器，因为尚未安装IMAP。

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_748_0.png)

图20-2 正在运行配置测试的`SquirrelMail`

在`localhost/mail`或`localhost/mail/src/login.php`登录浏览器以显示`SquirrelMail`登录页面（图20-3）。将`localhost`替换为服务器的IP地址或`FQDN`，以便从另一个系统查看该页面。使用在服务器系统中拥有账户的用户用户名和密码。

![](img/7decc2e43bc591b4d8cc4d0cd9fb2ae8_748_1.png)

图20-3 `SquirrelMail`登录页面

## 邮件列表

如果你定期向同一组大群人员发送电子邮件，邮件列表可能是一项资产。与在邮件的收件人或抄送字段中列出大量收件者，或向许多人逐个发送相同的邮件相比，它具有以下几个优势：

- 匿名性——邮件的收件者之一可以看到其他收件者的地址。
- 存档——发送到列表的邮件被存储在中央位置，列表管理员可以指定的列表成员或公众可以对其进行浏览。
- 访问控制——当你使用收件人或抄送向一组人发送邮件时，很容易忘记想要加入列表的人，并错误地包含了想要离开列表的人。
- 效率——邮件列表应用程序会随时间分散邮件传输，从而不会导致邮件服务器过载。

`Mailman`是GNU列表管理器，主要用`Python`编写，用于管理邮件讨论和时通讯列表。由于它与Web集成，`Mailman`使用户方便管理账户，管理员方便管理列表。更多信息请参阅`Mailman`主页(`www.list.org`)和`/usr/share/doc/mailman`目录下的文件。

安装`mailman`包和如`exim4`之类的`MTA`（第679页）。要使用Web界面，你必须安装`Apache`（第858页）。

当你安装`mailman`包时，`dpkg postinst`脚本会显示一个伪图形界面，要求你指定`Mailman`显示的语言，并告诉你必须创建一个站点列表。执行以下`newList`命令来创建一个站点，将`painting_class`替换为你的站点名称：

```
$ sudo newList painting_class
```

输入运行列表的人员的邮箱：`helen@example.com`

要完成邮件列表的创建，你必须通过编辑`/etc/aliases`（或等效文件）来添加以下行，并可能需要运行`'newaliases'`程序：

```
## painting_class 邮件列表

painting_class: "/var/lib/mailman/mailman post painting_class"

painting_class-admin: "/var/lib/mailman/mailman admin painting_class"

painting_class-bounces: "/var/lib/mailman/mailman bounces painting_class"

painting_class-confirm: "/var/lib/mailman/mailman confirm painting_class"

painting_class-join: "/var/lib/mailman/mailman join painting_class"

painting_class-leave: "/var/lib/mailman/mailman leave painting_class"

painting_class-owner: "/var/lib/mailman/mailman owner painting_class"

painting_class-request: "/var/lib/mailman/mailman request painting_class"

painting_class-subscribe: "/var/lib/mailman/mailman subscribe painting_class"

painting_class-unsubscribe: "/var/lib/mailman/mailman unsubscribe painting_class"
```

按回车键通知`painting_class` owner...

> 在列表上的用户接收邮件之前，你需要将`newlist`生成的带有邮件列表名称的行复制到`/etc/aliases`（第686页）并运行`newaliases`。

在启动`Mailman`之前，必须创建一个名为`mailman`的站点列表。将其复制到`aliases`文件并运行`newaliases`。

## 额外的邮件工具

`mailman init`脚本在设置好`mailman`站点列表站点列表后，使用以下命令启动`Mailman`守护进程：

```
$ sudo /etc/init.d/mailman start
* Starting Mailman master
```

在修改任何`Mailman`配置文件或添加新站点列表后，执行相同的命令，但将`start`替换为`reload`，以便`Mailman`重新读取配置文件。

`mm_cfg.py`是`Mailman`的主配置文件是`/etc/mailman/mm_cfg.py`。当你安装`Mailman`时，它会自动为`DEFAULT_EMAIL_HOST`（邮件列表的默认域名）和`DEFAULT_URL_HOST`（`Mailman`的默认Web服务器）赋值。根据需要更改这些变量并重启`Mailman`。

```
$ cat /etc/mailman/mm_cfg.py

# 新创建 ML 邮箱地址的默认域名

DEFAULT_EMAIL_HOST = 'example.com'

# 新创建 ML 接口的默认主机

DEFAULT_URL_HOST = 'example.com'
```

另一个系统查看页面的服务器`FQDN`。`SquirrelMail`会检查其配置并在页面上显示结果。图20-2显示`SquirrelMail`无法连接到本地系统的IMAP服务器，因为尚未安装IMAP。

在`localhost/mail`或`localhost/mail/src/login.php`登录浏览器以显示`SquirrelMail`登录页面（图20-3）。将`localhost`替换为服务器的IP地址或`FQDN`，以便从另一个系统查看该页面。使用在服务器系统中拥有账户的用户用户名和密码。

`mailman init`脚本在设置好`mailman`站点列表站点列表后，使用以下命令启动`Mailman`守护进程：

```
$ sudo /etc/init.d/mailman start
```
