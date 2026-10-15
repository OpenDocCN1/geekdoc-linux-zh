
配置 `virtualuser table` 文件如果你的服务器正在处理多个域名的邮件则特别重要。这是因为，默认情况下，相同用户名的邮件（无论域名如何）都会存储在同一信箱中。例如，如果你的服务器处理 `example.com` 和 `linuxtoys.net` 域的邮件，那么发往 `chris@example.com` 和 `chris@linuxtoys.net` 的邮件都将指向 `/var/spool/mail/chris` 信箱。使用 `virtualuser table` 文件，你可以用许多方式改变这种行为。

默认情况下，`virtualuser table` 文件是空的。以下是一些示例，说明了传入消息如何根据 `virtualuser table` 定义以不同方式定向。

| 虚拟用户 | 目标 |
| --- | --- |
| chris@linuxtoys.net | chris |
| cnegus@linuxtoys.net | chris |
| francois@linuxtoys.net | francois@spidermaker.com |
| info@linuxtoys.net | info-list |
| bogus@linuxtoys.net | error:nouser No such user here |
| @example.net | example-catchall |
| @example.com | %1@linuxtoys.net |

在前两行中，发往 `chris` 或 `cnegus@linuxtoys.net` 的传入邮件被指向本地邮件服务器用户名为 `chris` 的信箱。在下一行中，同一域名中发往 `francois` 的任何电子邮件都发往 `francois@spidermaker.com`。之后，发往 info 用户名的邮件保存到本地 `info-list` 邮件账户中。

## 添加用户账户

最终，您的邮件服务器接收到的电子邮件会被放入用户的邮箱中，用户可以随时查看和阅读。这些用户名中的每一个都必须作为 Fedora 系统上的真实用户添加。例如，要将用户 `chris` 添加到您的 Fedora sendmail 服务器，您可以尝试（作为 root 用户）：

```
# useradd -s /sbin/nologin chris
```

此操作会在 `/etc/passwd` 文件中创建一个名为 `chris` 的用户账户，将 shell 设置为 `/sbin/nologin`，并在 `/var/spool/mail/chris` 中为该用户创建一个邮箱。`/sbin/nologin` shell 可以防止用户登录到 shell（例如，当您只希望用户拥有邮件或 FTP 访问权限时，这是一种良好的安全实践）。现在，sendmail 可以将电子邮件定向到该用户的邮箱。

为了让该用户之后能够通过其 POP3 客户端访问邮件，他需要为其用户账户设置一个密码。使用 `passwd` 命令为该用户设置密码，如下所示：

```
# passwd chris
Changing password for user chris
New UNIX password:  ********
Retype new UNIX password:  ********
passwd: all authentication tokens updated successfully
```

请确保用户拥有此用户名和密码，以便将其配置到用户的电子邮件客户端中。

## 启动 sendmail 并生成数据库文件

您刚才对 `sendmail.mc`、`virtusertable`、`access`、`domaintable` 和 `mailerstable` 配置文件所做的任何配置，只有在重新生成为 `database (.db)` 文件后才会生效。将配置文件加载到数据库文件有几种不同的方法：

- **重启 sendmail** — 每次您重新启动计算机或重启 sendmail 守护进程（`service sendmail restart`）时，所有 sendmail 配置文件（包括 `sendmail.mc`）都会被编译成可供 sendmail 服务器使用的数据库文件。您也可以在不停止 sendmail 守护进程的情况下，使用 sendmail 启动脚本来重建数据库（包括 `/etc/aliases.db` 文件）。若要仅重建数据库，请输入：

```
# /etc/init.d/sendmail reload
```

此命令会重建所有数据库文件，包括 `/etc/aliases` 文件。（如果 reload 未更新您的 `sendmail.cf` 文件，请确保已安装 `sendmail-cf` 软件包：`yum install sendmail-cf`。）

- **制作配置文件** — 使用 `make` 命令，您可以将部分或所有配置文件制作成数据库文件，从而使 sendmail 守护进程可以立即使用它们。要做到这一点，请切换到 `/etc/mail` 目录，然后输入 `make all` 或带有您正在创建的数据库文件目标的 `make`。例如：

```
# cd /etc/mail
# make virtusertable.db
```

您可以将 `virtusertable.db` 替换为 `access.db`、`domaintable.db`、`mailerstable.db` 或 `sendmail.db`。（注意，您使用的是 `.db` 目标名称，而不是原始配置文件的名称。）如前所述，您还可以使用 `make all` 命令重建所有数据库文件。

此时，您的 sendmail 服务器应该已经启动并运行。您可以通过向服务器发送邮件并检查日志文件来测试服务器，以查看服务器的反应。请确保您的防火墙允许 TCP 端口 25 上的请求。然后输入以下内容以检查您的邮件服务器是否正在响应请求：

```
# telnet 127.0.0.1 25
Trying 127.0.0.1...
Connected to localhost.localdomain (127.0.0.1).
Escape character is '^]'.
220 toys.linuxtoys.net ESMTP Sendmail 8.14.1/8.14.1;
Sun, 15 Oct 2007 03:34:02 -0500
```

您可以看到 sendmail 守护进程正在运行并响应端口号 25。尝试输入 `HELO`。（这是字面上的 `HELO`，而不是 `HELLO`。）完成后，输入 `QUIT` 退出。

> **注意：** 有关故障排除邮件服务器的更多信息，请参阅 Wiley Publishing 出版的 *《Linux 故障排除圣经》*（*Linux Troubleshooting Bible*）。

## 重定向邮件

有时，您的电子邮件用户可能希望将邮件重定向到本地服务器上的其他位置，而不是他们自己的邮箱。每个用户都可以使用 `.forward` 文件来重定向他们自己的邮件。在整个系统范围内，您作为管理员可以在 `/etc/aliases` 文件中设置别名以重定向邮件。

### .forward 文件

用户重定向自己邮件的一种方法是使用 `.forward` 文件，用户可以将该文件放置在自己的主目录中（例如，`/home/jkpat/.forward`）。纯文本 `.forward` 文件的格式是电子邮件接收者的逗号分隔列表。`.forward` 文件的常见用法包括：

- 将邮件通过管道传递给程序以过滤邮箱内容：

```
"| /usr/bin/procmail"
```

- 将原本发给一个用户（例如 jkpat）的邮件发送给另一个用户（例如 cht09，在这种情况下是在另一台机器上）：

```
cht09@other.mybox.com
```

- 将邮件交付给本地用户（再次是 jkpat）*并且* 同时发送给另外两个人（cht09 和 brannigan）：

```
\jkpat, cht09@other.mybox.com, \brannigan
```

> **提示：** 不允许在可以被所有用户读取的目录中存在 `.forward` 文件。如果您在 `.forward` 文件中保持开放的权限，sendmail 将忽略该文件并且不会按您的意愿转发邮件。要允许 sendmail 使用具有开放权限的 `.forward` 文件，您可以从 `sendmail.mc` 文件中的 `confDONT_BLAME_SENDMAIL` 行中移除 `dn1`。

### aliases 文件

处理邮件交付的更灵活方法（系统范围的，而不是针对特定用户）涉及 `/etc/aliases` 文件，这也是一个纯文本文件。别名文件包含一个名称，后跟冒号，然后是用户名、另一个别名、地址列表、文件或将被投递邮件的程序。冒号左侧的名称（可以是有效的用户名或仅仅是别名）随后可以用作本地机器或远程机器上的电子邮件接收者。
