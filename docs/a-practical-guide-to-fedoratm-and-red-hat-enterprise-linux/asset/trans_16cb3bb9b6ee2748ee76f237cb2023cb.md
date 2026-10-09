

![](img/243613168ac865b539f12460d966088e_816_0.png)

图 20-3 SquirrelMail 正在运行配置测试

## 启动
你不需要启动 SquirrelMail，也不需要为它开放任何端口。但是，你需要配置并启动 sendmail（第 743 页）、IMAP（第 763 页）和 Apache（第 936 页），并为它们开放端口（如果服务器运行在带有防火墙的系统上）。

## 配置
SquirrelMail 文件位于 /usr/share/squirrelmail。创建以下链接以使 SquirrelMail 可通过 Web 访问：

```
# ln -s /usr/share/squirrelmail /var/www/html/mail
```

执行以下命令以配置 SquirrelMail：

```
# cd /usr/share/squirrelmail/config
# ./conf.pl
SquirrelMail Configuration : Read: config_default.php (1.4.0)

Main Menu --
1. Organization Preferences
2. Server Settings
3. Folder Defaults
4. General Options
5. Themes
6. Address Books
7. Message of the Day (MOTD)
8. Plugins
9. Database
10. Languages
D. Set pre-defined settings for specific IMAP servers
C Turn color on
S Save data
Q Quit

Command >>
```

该菜单具有多层级。当你选择一个设置（而非子菜单）时，conf.pl 会显示有助于你决定如何回答其提出的问题 的信息。设置服务器的域名（Server Settings 页面中的数字 1）和你正在使用的 IMAP 服务器名称（主菜单中的 D）。SquirrelMail 提供多种主题；如果你不喜欢 SquirrelMail 的外观，可以从 Themes（数字 5）中选择另一个主题。当你完成更改后，退出 `conf.pl`。每当你想更改 SquirrelMail 的配置时，请运行 `conf.pl`。

![](img/243613168ac865b539f12460d966088e_817_0.png)

图 20-4 SquirrelMail 登录页面

SquirrelMail 提供了一个测试其配置的网页。将服务器上的浏览器指向 `localhost/mail/src/conf/test.php`。将 `localhost` 替换为服务器的 IP 地址或 FQDN，以便从其他系统查看该页面。SquirrelMail 会检查其配置并在此页面上显示结果。图 20-3 显示 SquirrelMail 无法连接到本地系统上的 IMAP 服务器，可能是因为尚未安装 IMAP。

## 登录
将 Web 浏览器指向 `localhost/mail` 或 `localhost/mail/src/login.php` 以显示 SquirrelMail 登录页面（图 20-4）。将 `localhost` 替换为服务器的 IP 地址或 FQDN，以便从其他系统查看该页面。输入在服务器系统上拥有账户的用户的用户名和密码。

# 邮件列表

如果你定期向同一群庞大的收件人发送电子邮件，邮件列表可以成为一个资产。与在电子邮件的 To 或 Cc 字段中列出众多收件人或向多人单独发送相同电子邮件相比，它提供了几项优势：

- 匿名性——电子邮件的收件人无法看到其他收件人的地址。
- 存档——发送到列表的电子邮件存储在一个中心位置，列表管理员指定的列表成员或公众可以浏览这些邮件。
- 访问控制——你可以指定谁可以向列表发送电子邮件。
- 一致性——当你使用 To 或 Cc 向一群人发送电子邮件时，很容易忘记希望加入列表的人，并错误地包括希望退出列表的人。
- 效率——邮件列表应用程序随时间分散电子邮件传输，从而不会使邮件服务器过载。

| 项目 | 描述 |
| :--- | :--- |
| **Mailman** | Mailman，GNU 列表管理器，主要用 Python 编写，管理电子邮件讨论和电子邮件新闻列表。由于与 Web 集成，Mailman 使用户管理其账户和系统管理员管理列表变得更加容易。更多信息，请参见 Mailman 主页 (www.list.org)，以及安装 Mailman 后 /usr/share/doc/mailman* 目录中的文件。 |
| **先决条件** | 安装 **mailman** 软件包和 MTA，如 **sendmail**（第 742 页）。若要使用 Web 界面，你必须安装 Apache（第 935 页）。 |
| **Mailman 站点列表** | 执行以下 **newlist** 命令以创建站点列表，将你的邮件站点名称替换 *painting_class*。你还必须创建一个名为 **mailman** 的站点列表（将 **mailman** 替换 *painting_class*）；否则 Mailman 将无法启动。 |

```
# /usr/lib/mailman/bin/newlist
Enter the name of the list: painting_class
Enter the email of the person running the list: helen@example.com
Initial painting_class password:
```

为了完成创建你的邮件列表，你必须通过添加以下行并可能运行 *newaliases* 程序来编辑你的 /etc/aliases（或等效）文件：

```
## painting_class mailing list
painting_class:	"/usr/lib/mailman/mail/mailman post painting_class"
painting_class-admin:	"/usr/lib/mailman/mail/mailman admin painting_class"
painting_class-bounces:	"/usr/lib/mailman/mail/mailman bounces painting_class"
painting_class-confirm:	"/usr/lib/mailman/mail/mailman confirm painting_class"
painting_class-join:	"/usr/lib/mailman/mail/mailman join painting_class"
painting_class-leave:	"/usr/lib/mailman/mail/mailman leave painting_class"
painting_class-owner:	"/usr/lib/mailman/mail/mailman owner painting_class"
painting_class-request:	"/usr/lib/mailman/mail/mailman request painting_class"
painting_class-subscribe:	"/usr/lib/mailman/mail/mailman subscribe painting_class"
painting_class-unsubscribe:	"/usr/lib/mailman/mail/mailman unsubscribe painting_class"
Hit enter to notify painting_class owner...
```

在列表上的用户能够接收电子邮件之前，你需要将 **newlist** 生成的行（以新的邮件站点名称开头的行）复制到 /etc/aliases（第 746 页）的末尾，并运行 **newaliases**（第 747 页）。

> **提示：** 除了你想设置的站点列表外，你必须使用 **newlist** 实用程序创建一个名为 **mailman** 的站点列表。如果你不创建这个站点列表，你将无法启动 Mailman。

| 项目 | 描述 |
| :--- | :--- |
| **mm_cfg.py** | Mailman 的主配置文件是 /etc/mailman/mm_cfg.py。当你安装 Mailman 时，它在此文件中将 *fqdn* 的值分配给 DEFAULT_EMAIL_HOST（邮件列表的默认域名）和 **DEFAULT_URL_HOST**（Mailman 的默认 Web 服务器）。根据需要更改分配给这些变量的值，确保将值包含在单引号内，并启动或重启 Mailman。以下示例使用 www.example.com 作为默认 Web 服务器，使用 mail.example.com 作为默认邮件服务器： |

```
# grep '^DEFAULT' /etc/mailman/mm_cfg.py
DEFAULT_URL_HOST = 'www.example.com'
DEFAULT_EMAIL_HOST = 'mail.example.com'
```

你可以通过修改名为 `/etc/mailman/sitelist.cfg` 的文件来配置 Mailman 邮件列表的许多方面。更多信息请参见该文件中的注释。

在设置 **mailman** 站点列表和你选择的站点列表后，当系统进入多用户模式时运行 `systemctl` 以启动 **mailman** 服务，然后启动 **mailman** 服务。使用 `systemctl status` 命令确保服务正在运行。

```
# systemctl enable mailman.service
# systemctl start mailman.service
```

修改任何 Mailman 配置文件或添加新的站点列表后，再次执行第二条命令，将 **start** 替换为 **restart** 以使 Mailman 重新读取其配置文件。切记也要根据需要启动 **sendmail** 和 **Apache**。

在 Mailman Web 界面工作之前，你必须修改 `/etc/httpd/conf.d/mailman.conf` 文件的最后一行。删除开头的 **hashmark**（ **#**），并将域名更改为先前在 `mm_cfg.py` 中为 Web 界面主机建立的域名：

```
# tail -1 /etc/httpd/conf.d/mailman.conf
RedirectMatch ^/mailman/.*)$ http://www.example.com/mailman/listinfo
```

重启 **Apache**。假设 Web 界面主机是 `example.com`，任何人都可以将浏览器指向 `example.com/mailman` 以显示可用邮件列表的列表。单击邮件列表的名称，显示一个页面，允许你查看列表存档、发送消息或订阅列表。页面底部有一个链接指向列表的管理界面。

如果 Mailman 指示没有公开宣传的 Mailman 邮件列表，请将以下行添加到 `mm_cfg.py` 并重启 Mailman。

```
VIRTUAL_HOST_OVERVIEW = Off
```

# 设置 IMAP 或 POP3 邮件服务器

**Dovecot** IMAP（Internet Message Access Protocol，互联网消息访问协议）和 POP（Post Office Protocol，邮局协议）允许用户远程获取和管理电子邮件。本节说明如何为这些协议设置服务器。**Dovecot**（www.dovecot.org 和 wiki.dovecot.org）实现了这些协议。安装 **Dovecot** 后，请参见 `/usr/share/doc/dovecot*` 以获取更多信息。

