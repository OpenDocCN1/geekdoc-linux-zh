
## 在防火墙上开放邮件端口

在你的防火墙上打开端口 `110`，允许其他电脑请求你邮件服务器上的 POP3 服务。如果你在使用带有 SSL 支持的 POP3，则应开启端口 `995`（或者对于通过 SSL 运行 IMAPv4 开启端口 `993`）。开启端口的一种简单方法是通过“安全级别和防火墙”窗口（选择系统 → 管理 → 安全级别和防火墙）。选择“其他端口”并点击添加按钮，将 `110` 设置为端口，TCP 和 UDP 设置为协议。

邮件服务器上所有账户的用户默认都配置为接收电子邮件。例如，如果名为 `jsmith` 的用户的电子邮件发送到 `mail.hansonhistory.com` 服务器，该消息将复制到服务器上的 `/var/spool/mail/jsmith` 文件。继续该示例，用户 `jsmith` 可以按如下方式设置他的邮件阅读器：

- **邮件服务器：** `mail.hansonhistory.com`
- **用户名：** `jsmith`
- **密码：** `userspassword`
- **协议：** `POP3`

配置邮件阅读器后，`jsmith` 在他的邮件阅读器中点击“发送并接收”，`/var/spool/mail/jsmith` 文件中的所有电子邮件消息都将下载到他的本地邮件阅读器中。随后消息将从服务器上删除。

> **注意：** 请记住，POP3 和 IMAPv4 服务使用明文协议在网络上传输用户名和密码。根据你的网络环境，这可能会构成安全威胁。

## 使用 SquirrelMail 从浏览器获取邮件

一旦你的邮件服务器运行，你就可以配置 SquirrelMail，允许你的邮件服务器的用户从他们的 Web 浏览器获取邮件。要使用 SquirrelMail，你必须从书中附带的 Fedora 安装光盘中安装 `squirrelmail` 包（或输入 `install squirrelmail`）。此外，要使用 SquirrelMail，你还需要配置并启动以下组件：

- 邮件服务器 (`sendmail` 或 `postfix`)
- IMAPv4 服务器 (`dovecot`)
- Web 服务器 (`httpd`)
- 将通过 SquirrelMail 读取邮件的用户账户

SquirrelMail 拥有非常直观的、基于菜单的管理界面。该界面包含了多种可以添加到 SquirrelMail 的插件，用以使用诸如拼写检查、日历、更改密码和从 POP3 服务器获取邮件等功能。你也可以从 `squirrelmail.org` 获取更多插件。

要配置 SquirrelMail，请在终端窗口中以 `root` 用户身份输入以下内容：

```bash
# /usr/share/squirrelmail/config/conf.pl
```

### 第 19 章：设置邮件服务器 823

你可能想要考虑：
- 组织偏好（例如组织名称）
- 主题（有二十多个可选）
- 插件（恰好可用）

此外，默认情况下，邮件只能从 `localhost` 访问，因此你可能希望更改“服务器设置”。用户要使用 `squirrelmail` 获取邮件，他们只需要在浏览器中输入以下地址：

```
http://server/webmail
```

## 使用 mailman 管理邮件列表

Mailman 是一个用于管理电子邮件的流行开源软件包。除了提供设置和管理列表的灵活界面外，它还有基于 Web 的界面，方便人们加入列表、访问讨论列表存档以及调整自己的偏好。

如果你需要关于配置 `mailman` 的更多信息，有很多地方可以参考。查看 `mailman` 网站 `www.gnu.org/software/mailman/mailman.html`。也可以查看 `/usr/share/doc/mailman`。

> 如果你在早期版本的 Fedora 或 Red Hat Linux 中未使用 `mailman`，请注意 `mailman` 安装目录已从 `/var/mailman` 移动到 `/usr/lib/mailman`。如果你对 `/var/mailman` 目录中的文件进行了任何更改，在升级 `mailman` 软件包后，你需要将这些文件移动到 `/var/lib/mailman` 目录。

以下使用 `mailman` 配置讨论列表的简要步骤：

- 1. 从 Fedora 安装 `mailman` RPM 或输入 `yum install mailman`。
- 2. 按如下启动你的 Web 服务器（如果尚未运行）：

```bash
# service httpd start
# chkconfig httpd on
```

- 3. 按如下方式为你的用户创建密码：

```
/usr/lib/mailman/bin/msitepass
```

新密码：*****
再次确认密码：*****

- 4. 编辑 `/usr/lib/mailman/Mailman/mm_cfg.py` 文件并更改 `DEFAULT_URL_HOST` 和 `DEFAULT_EMAIL_HOST` 值。例如，我配置邮件列表的计算机主机名是 `toys.luxtoys.net`。这些值所示：

```python
DEFAULT_EMAIL_HOST = 'toys.luxtoys.net'
DEFAULT_URL_HOST_DEF = 'luxtoys.net'
```

### 第 19 章：设置邮件服务器 825

你可以将这些值保留为 `faqdn`，以便直接使用本地计算机的完全限定域名。

编辑 `/etc/httpd/conf.d/mailman.conf` 文件。为了让对 `mailman` 的查询跳转到列表页面，请取消文件底部 `RedirectMatch` 行的注释，并将该行更改为包含你的完全限定域名。例如，当我为 `listuxtoys.net` 邮件列表执行此操作时，该行显示如下所示：

```
RedirectMatch "/mailman/]* http://www.listuxtoys.net/mailman/listinfo
```

创建邮件列表之前，你必须先创建一个名为 `mailman` 的空邮件列表。在创建列表的同时，为维护列表的人员分配电子邮件地址和初始密码。要执行此操作，请输入以下命令：

```
# /usr/lib/mailman/bin/newlist mailman
Enter the email of the person running the list: chris@listuxtoys.net
Initial mailman password: ********
Hit enter to notify mailman owner...
```

按照如下方式启动 `mailman` 服务：

```
# service mailman start
# chkconfig mailman on
```

使用 `newlist` 命令创建一个新的邮件列表：

```
# /usr/lib/mailman/bin/newlist
Enter the name of the list: pro
Enter the email of the person running the list: chris@listuxtoys.net
Initial pro password: ******
```

要完成邮件列表的创建，你必须编辑 `/etc/aliases`（或等效文件），添加以下行，然后运行 `aliases` 程序：

```
# pro mailing list
pro: "/usr/lib/mailman/mail/mailman post pro"
pro-admin: "/usr/lib/mailman/mail/mailman admin pro"
pro-bounces: "/usr/lib/mailman/mail/mailman bounces pro"
pro-confirm: "/usr/lib/mailman/mail/mailman confirm pro"
pro-join: "/usr/lib/mailman/mail/mailman join pro"
pro-leave: "/usr/lib/mailman/mail/mailman leave pro"
pro-owner: "/usr/lib/mailman/mail/mailman owner pro"
pro-request: "/usr/lib/mailman/mail/mailman request pro"
pro-subscribe: "/usr/lib/mailman/mail/mailman subscribe pro"
pro-unsubscribe: "|/usr/lib/mailman/mail/mailman unsubscribe pro"
```
