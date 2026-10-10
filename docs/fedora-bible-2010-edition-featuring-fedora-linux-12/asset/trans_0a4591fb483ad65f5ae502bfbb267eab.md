
国家名称（2 位代码 [XX]）：

打开 `/etc/dovecot.conf` 文件。然后启用至少一种您允许的安全协议，并修改标识包含您刚刚创建的可信证书和私钥的文件的行。通过此示例，请确保证书和密钥都使用同一个文件：

`protocols = imaps pop3s`
`ssl_cert_file = /etc/pki/tls/certs/dovecot.pem`
`ssl_key_file = /etc/pki/tls/certs/dovecot.pem`

输入以下内容重新加载或重启 dovecot 服务（作为 root 用户）：

`# service dovecot reload`

如果您已按照 `dovecot.conf` 文件中描述的设置协议，用户现在应该能够使用 imaps 或 pop3s 协议连接到您的 dovecot 服务。当他们尝试获取邮件时，将向其显示您创建的证书，并且他们需要接受该证书才能继续。

## 通过浏览器使用 SquirrelMail 获取邮件

一旦您的邮件服务器启动并运行，您可以配置 SquirrelMail，允许您的邮件服务器的用户通过 Web 浏览器获取他们的邮件。要使用 SquirrelMail，您必须通过运行 `yum install squirrelmail` 从 Fedora 存储库安装 squirrelmail 软件包。此外，要使用 SquirrelMail，您需要配置并启动以下组件：

- 邮件服务器 (sendmail 或 postfix)
- IMAPv4 服务器 (dovecot)
- Web 服务器 (httpd)
- SSL 模块 (mod_ssl)
- 将通过 SquirrelMail 读取邮件的用户账户

**注意：** Fedora 包含了另一个流行的 webmail 客户端，Roundcube。要了解有关 Roundcube 的更多信息，请访问 www.roundcube.net。

SquirrelMail 有一个非常直观的基于菜单的管理接口。该接口包括一系列您可以添加到 SquirrelMail 的插件，以使用拼写检查、日历、更改密码和从 POP3 服务器获取邮件等功能。您还可以从 http://squirrelmail.org 获取更多插件。

要配置 SquirrelMail，请在终端窗口中作为 root 用户输入以下内容：

```
# /usr/share/squirrelmail/config/conf.pl
```

您可能需要调整的功能包括：组织首选项（如要在 SquirrelMail 界面中放入的组织名称和徽标）、主题（有二十多种可用）和插件（只需查看那些可供安装的插件中是否有感兴趣的即可）。

此外，默认情况下，只能从本地主机上的浏览器访问邮件，因此您可能希望更改服务器设置。例如，将域名更改为您将允许用户访问其邮件的域名名称。

要使用 squirrelmail，用户只需将以下地址输入到 Web 浏览器的地址栏中（如果您在 localhost 之外运行，则用 `localhost` 或计算机名称替换 `server`）：

```
http://server/webmail
```

图 18-1 展示了 webmail 浏览器界面的示例，其中 webmail 徽标已被替换为我所在组织的徽标（在本例中为 LinuxToys.net）。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_769_0.png)

**图 18-1：** 为 SquirrelMail 添加徽标，让用户可以通过 Web 登录以获取邮件。

输入您的用户名和密码。您的邮箱应该会出现，如图 18-2 所示。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_770_0.png)

## 使用 mailman 管理邮件列表

Mailman 是一个用于管理电子邮件讨论列表的流行开源软件包。除了提供灵活的设置和管理列表的管理接口外，它还有基于 Web 的接口，使人们可以轻松加入列表、访问讨论列表存档并调整自己的偏好设置。

如果您需要更多有关配置 mailman 的信息，有很多地方可以查阅。请查看位于 www.gnu.org/software/mailman/mailman.html 的 mailman 网站。另外，请查看 /usr/share/doc/mailman-* 中的 README 文件。

**注意：** 如果您在之前的 Fedora 版本中曾使用过 mailman，请注意 mailman 安装目录已从 /var/mailman 移至 /usr/lib/mailman。如果您对 /var/mailman 目录中的文件进行了任何更改，在升级 mailman 软件包后，您需要将这些文件移动到 /usr/lib/mailman 目录。

以下是使用 mailman 配置讨论列表的简要步骤：

1. 通过运行 `yum install mailman` 安装 mailman RPM。

2. 启动您的 Web 服务器（如果尚未运行），如下所示：

   ```bash
   # service httpd start
   # chkconfig httpd on
   ```

3. 如下创建您网站的密码：

   ```bash
   # /usr/lib/mailman/bin/mmsitepass
   新站点密码: *****
   再次输入以确认密码: *****
   ```

4. 编辑 `/usr/lib/mailman/Mailman/mm_cfg.py` 文件并更改 `DEFAULT_URL_HOST` 和 `DEFAULT_EMAIL_HOST` 的值。例如，我正在配置邮件列表的计算机的主机名是 `toys.linuxtoys.net`。默认的电子邮件主机是 `linuxtoys.net`。这些值可能如下所示：

   ```
   DEFAULT_EMAIL_HOST    = 'toys.linuxtoys.net'
   DEFAULT_URL_HOST      = 'linuxtoys.net'
   ```

   您可以将这些值保留为 `fqdn`，以仅使用本地计算机的完全限定域名。

5. 编辑 `/etc/httpd/conf.d/mailman.conf` 文件。为了使对 mailman 的查询转到 listinfo 页面，请取消文件底部 `RedirectMatch` 行的注释，并修改该行以包含您的完全限定域名。例如，当我为 `linuxtoys.net` 邮件列表执行此操作时，该行如下所示：

   ```
   RedirectMatch ^~/mailman/\1\*$ http://www.linuxtoys.net/mailman/listinfo
   ```

6. 要创建 mailman 邮件列表，您必须首先创建一个未填充内容的名为 `mailman` 的邮件列表。与该列表一起，您必须为负责管理列表的人员分配电子邮件和初始密码。要这样做，输入以下内容：

   ```
   # /usr/lib/mailman/bin/newlist mailman
   输入管理该列表的人员的电子邮件: chris@linuxtoys.net
   初始 mailman 密码: *******
   按回车键通知 mailman 所有者...
   ```

7. 重启 Web (`httpd`) 服务并启动 mailman 服务，如下所示：

   ```
   # service httpd restart
   # service mailman start
   # chkconfig mailman on
   ```

8. 使用 `newlist` 命令创建新的邮件列表，如下所示：

   ```
   # /usr/lib/mailman/bin/newlist
   输入列表的名称: pro
   输入管理该列表的人员的电子邮件: chris@linuxtoys.net
   初始 pro 密码: ****
   要完成创建您的邮件列表，您必须通过添加以下行并运行 'newaliases' 程序来编辑 '/etc/aliases'（或等效）文件：
   ```

   ```
   ## pro mailing list
   pro:                     "/usr/lib/mailman/mail/mailman post pro"
   pro-admin:               "/usr/lib/mailman/mail/mailman admin pro"
   pro-bounces:             "/usr/lib/mailman/mail/mailman bounces pro"
   pro-confirm:             "/usr/lib/mailman/mail/mailman confirm pro"
   pro-join:                "/usr/lib/mailman/mail/mailman join pro"
   pro-leave:              "/usr/lib/mailman/mail/mailman leave pro"
   pro-owner:               "/usr/lib/mailman/mail/mailman owner pro"
   ```

9. 将刚刚显示的文本（从 `## pro_mailing_list` 行开始）复制并粘贴到您的 `/etc/aliases` 文件末尾。

10. 运行 `newaliases` 命令。此时，您应该能够通过 Web 浏览器查看新的邮件列表。在本地系统的 Web 浏览器中，在地址栏输入以下名称：

    ```
    http://localhost/mailman/pro
    ```

11. 如果一切正常，开始添加更多邮件列表。为了从主要的 list info 页面 `http://localhost/mailman/listinfo` 查看邮件列表，您需要登录或使列表公开。在我的示例中，我创建了一个名为 Pro 的邮件列表。该项目的名称显示在图 18-3 所示的列表中。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_772_0.png)

12. 选择该项目名称（点击它）。项目的 Info 页面应该会显示出来。

13. 滚动到该页面底部并点击项目管理信息链接。

14. 当提示时，输入列表管理员密码。现在您可以配置您的邮件列表的外观、感觉和行为。您想要考虑的重要信息包括：

    - **隐私选项** — 您希望列表是公开的还是私有的（例如，仅在您的组织内部）？您希望允许谁查看您的成员列表？

