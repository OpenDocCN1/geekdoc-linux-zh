

4. 在防火墙中开放 110 端口，以允许其他计算机向您的邮件服务器请求 POP3 服务。如果您使用的是支持 SSL 的 POP3，则应改为开放 995 端口（或者用于 SSL 下的 IMAP 的 993 端口）。通过“安全级别和防火墙”窗口（选择 **系统** \rightarrow **管理** \rightarrow **安全级别和防火墙**）开放端口是一个简便的方法。选择 *其他* 端口并单击 *添加* 按钮，将 110 作为端口添加，并将 TCP 和 UDP 作为协议添加。

默认情况下，在您的邮件服务器上拥有用户账户的所有用户都被配置为接受电子邮件。例如，如果有电子邮件发送到 `mail.handsonhistory.com` 服务器并指向名为 `jsmith` 的用户，该邮件将被复制到服务器上的 `/var/spool/mail/jsmith` 文件中。继续这个例子，名为 `jsmith` 的用户可以如下设置其邮件阅读器：

- **邮件服务器**: mail.handsonhistory.com
- **用户名**: jsmith
- **密码**: *theuserpassword*
- **协议**: POP3

配置好邮件阅读器后，当 `jsmith` 从他的邮件阅读器中点击 **发送和接收** 时，`/var/spool/mail/jsmith` 文件中的所有电子邮件消息都会下载到他的本地邮件阅读器中。随后，这些消息将从服务器上删除。

> **注意：** 请记住，普通的 POP3 和 IMAP 服务使用明文协议在网络上传输用户名和密码。根据您的网络环境，这可能会带来安全风险。

## 使用 SquirrelMail 从浏览器获取邮件

一旦您的邮件服务器启动并运行，您可以配置 SquirrelMail，使邮件服务器的用户能够从其 Web 浏览器中获取邮件。要使用 SquirrelMail，您必须从随附本书的 Fedora 安装 DVD 上安装 squirrelmail 软件包（或者输入 `yum install squirrelmail`）。此外，要使用 SquirrelMail，您需要配置并启动以下组件：

- 邮件服务器（sendmail 或 postfix）
- IMAP 服务器（dovecot）
- Web 服务器（httpd）
- 将通过 SquirrelMail 读取邮件的用户账户

SquirrelMail 具有一个非常直观的基于菜单的管理界面。该界面包括一系列您可以添加到 SquirrelMail 的插件，用于使用拼写检查、日历、密码更改以及从 POP3 服务器获取邮件等功能。您还可以从 `squirrelmail.org` 获取更多插件。

要配置 SquirrelMail，请在终端窗口中作为 root 用户输入以下命令：

```
# /usr/share/squirrelmail/config/conf.pl
```

您可能想要考虑调整的功能包括：组织首选项（例如，放入 SquirrelMail 界面的组织名称和徽标）、主题（提供二十多种可选主题）和插件（只需检查是否有可安装的感兴趣插件即可）。

此外，默认情况下，邮件只能从本地主机上的浏览器访问，因此您可能希望更改服务器设置。例如，将域名更改为您将允许用户访问其邮件的域名名称。

用户若要使用 squirrelmail 获取邮件，只需在其 Web 浏览器的地址栏中输入以下地址（如果这是在 localhost 之外运行，请将 *server* 替换为 localhost 或计算机名称）：

```
http://server/webmail
```

图 19-1 展示了 webmail 浏览器界面的示例，其中的 webmail 徽标已被替换为我所在组织的徽标（在此情况下为 LinuxToys.net）。

![](img/fb202c163797a743c3c6cf236316bc96_848_0.png)

图 19-1: 为 SquirrelMail 添加徽标，并让用户从 Web 登录获取邮件。

输入您的用户名和密码。您的邮箱应该会显示出来，如图 19-2 所示。

![](img/fb202c163797a743c3c6cf236316bc96_849_0.png)

## 使用 mailman 管理邮件列表

Mailman 是一个流行的开源软件包，用于管理电子邮件讨论列表。除了提供灵活的管理接口来设置和管理列表外，它还具有基于 Web 的界面，使人们可以轻松加入列表、访问讨论列表存档以及调整自己的偏好设置。

如果您需要更多关于配置 mailman 的信息，有很多地方可以查找。请访问 www.gnu.org/software/mailman/mailman.html 上的 mailman 网站。此外，请查看 /usr/share/doc/mailman-* 中的 README 文件。

> 注意：如果您在早期版本的 Fedora 或 Red Hat Linux 中曾经使用过 mailman，请注意 mailman 安装目录已从 /var/mailman 移至 /usr/lib/mailman。如果您对 /var/mailman 目录中的文件进行了任何更改，需要在升级 mailman 软件包后，将这些文件移至 /var/lib/mailman 目录。

以下是使用 mailman 配置讨论列表的简要步骤：

1. 从 Fedora DVD 安装 mailman RPM。
2. 启动您的 Web 服务器（如果尚未运行），如下所示：
   ```
   # service httpd start
   # chkconfig httpd on
   ```
3. 按以下方式为您的站点创建密码：
   ```
   # /usr/lib/mailman/bin/mmsitepass
   New site password: ******
   Again to confirm password: ******
   ```
4. 编辑 `/usr/lib/mailman/Mailman/mm_cfg.py` 文件并更改 `DEFAULT_URL_HOST` 和 `DEFAULT_EMAIL_HOST` 值。例如，我正在配置邮件列表的计算机的主机名是 `toys.linuxtoys.net`。默认的电子邮件主机是 `linuxtoys.net`。值将显示如下：
   ```
   DEFAULT_EMAIL_HOST = 'toys.linuxtoys.net'
   DEFAULT_URL_HOST_DEF = 'linuxtoys.net'
   ```
   您可以将这些值保留为 $fqdn$，以简单地使用本地计算机的完全限定域名。
5. 编辑 `/etc/httpd/conf.d/mailman.conf` 文件。要使对 mailman 的查询导向 listinfo 页面，请取消该文件底部 RedirectMatch 行的注释，并更改该行以包含您的完全限定域名。例如，当我为 `linuxtoys.net` 邮件列表执行此操作时，该行显示如下：
   ```
   RedirectMatch  ^~/mailman/[\/]*\$ http://www.linuxtoys.net/mailman/listinfo
   ```
6. 要创建一个 mailman 邮件列表，您必须首先创建一个未填充内容的名为 mailman 的邮件列表。与该列表一起，您必须为负责管理该列表的人员分配电子邮件和初始密码。为此，请输入以下内容：
   ```
   # /usr/lib/mailman/bin/newlist mailman
   Enter the email of the person running the list:  chris@linuxtoys.net
   Initial mailman password:  *********
   Hit enter to notify mailman owner...
   ```
7. 按以下方式启动 mailman 服务：
   ```
   # service mailman start
   # chkconfig mailman on
   ```
8. 使用 newlist 命令创建新的邮件列表，如下所示：
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
9. 将刚才显示的文字（从 `## pro mailing list` 行开始）复制并粘贴到 `/etc/aliases` 文件的末尾。
10. 运行 `newaliases` 命令。此时，您应该能够通过网络浏览器查看新的邮件列表。在本地系统的 Web 浏览器中，在地址栏中输入以下名称：
    ```
    http://localhost/mailman/listinfo
    ```
11. 如果一切看起来正常工作，开始添加更多的邮件列表。在我的例子中，我创建了一个名为 projectlist 的邮件列表。该项目的名称显示在图 19-3 中的列表中。
12. 选择该项目名称（点击它）。该项目的信息页面应该会显示出来。
13. 滚动到该页面底部并点击项目管理界面链接。
14. 当提示时，输入列表管理员密码。现在您可以配置邮件列表的外观、风格和行为。您希望考虑的重要信息包括：
    - **隐私选项** — 您希望列表是公开的还是私有的（例如，仅限您所在的组织内部）？您希望谁能够查看您的成员列表？
    - **发送过滤器** — 谁可以向列表发布消息？列表是经过审核的还是未经审核的？列表是否可能只单向流动，例如作为联系客户的一种方式？
    - **成员管理** — 您的成员可以看到其他成员的信息吗？您的成员添加和移除政策是什么？
15. 完成配置选项后，请务必提交您的更改。
    此时，您可以允许用户加入列表。鼓励他们探索并设置自己的用户偏好。

如果您在配置 mailman 时遇到问题，请参阅 `/usr/share/doc/mailman-*` 目录中的 `INSTALL`、`REDHAT` 和 `README` 文件。

