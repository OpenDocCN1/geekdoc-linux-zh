
From:`chris@linuxuxt.net` RELAY

To:`spidermaker.com` RELAY

To:`former-user@linuxuxt.net` ERROR: User no longer works here

在 `Connect:192.168` 行上，网络地址（推测为你局域网使用的 IP 地址的第一部分）被允许中继邮件。这是允许所有从本地局域网机器上发送邮件的人让其邮件被中继的好方法。在下一行（`Connect:linuxuxt.net`）上，邮件被中继。第三行（`spammer-domain.com`）被拒绝。

`From:chris@linuxuxt.net` 行允许特定的发送者。`To:spidermaker.com` 行允许特定的接收者。`To:former-user@linuxuxt.net` 行显示错误消息。

# 第 19 章：设置邮件服务器 811

> 注意：通常情况下，告诉潜在的垃圾邮件发送者某个用户账户并不并不好主意。垃圾邮件发送者经常查询邮件服务器获取此类信息，通常向常用名称发送电子邮件，试图确定服务器上存在哪些真实用户。作为一般原则，尽量对钓鱼你邮件服务器的人提供尽可能少的信息。

最后几行（以 `@example.net` 和 `@example.com` 开头）说明了如何将特定域接收者的邮件重定向到同一个名称。在第一个的情况下，所有发送 `@example.net` 的消息都会进入名为 `example-catchall` 的用户的信箱。最后一行显示了如何将特定域的用户映射到所选域上的相同用户名 `#1`。

一旦你对此文件进行了相应的修改，必须重新构建 `virtualtable` 数据库（`virtualtable.db` 文件） 才能使更改生效。有关此主题的信息，请参阅“Starting sendmail and generating database files”。

# 添加用户账户

最终，你的邮件服务器收到的电子邮件会被放置在用户的邮箱中，用户可以根据自己的意愿提取并阅读。这些用户名中的每一个都必须作为真实用户添加到你的 Fedora 系统中。例如，要将用户 `chris` 添加到你的 Fedora `sendmail` 服务器中，你可以这样操作（以 `root` 身份）：

```
# useradd -s /sbin/nologin chris
```

此操作会在 `/etc/passwd` 中创建一个名为 `chris` 的用户账户，将 `shell` 设置为 `/sbin/nologin`，并在 `/var/spool/mail/chris` 为该用户创建一个信箱。`/sbin/nologin` 防止用户登录到 `shell`（当只想只想使用邮件服务器或 FTP 访问时，这是一个良好的安全实践）。现在，`sendmail` 可以直接将电子邮件发送到该用户的邮箱。

为了让他他以后能从他的 `POP3` 客户端访问其电子邮件，他需要一个用户账户的密码。使用如下密码为该用户设置密码：

```
# password chris
Changing password for user chris
New UNIX password: *****
Retype new UNIX password: *****
passwd: all authentication tokens updated successfully
```

确保用户拥有此用户名和密码，以便将其配置到用户的电子邮件客户端中。

# 启动 sendmail 并生成数据库文件

你刚刚对 `sendmail.mc`、`virtualtable`、`access`、`domaintable` 和 `mailertable` 配置文件所做的任何配置，在它们重新生成为数据库（`.db`）文件之前，都不会生效。你有几种不同的方法可以将你的配置文件加载到数据库文件中：

- 重启 `sendmail` —— 每当你重启电脑或重启 `sendmail` 守护进程（`service sendmail restart`），所有的 `sendmail` 配置文件（包括 `sendmail.mc`）都会被编译成数据库文件，供 `sendmail` 服务器使用。你也可以使用 `sendmail` 启动脚本在不停止 `sendmail` 守护进程的情况下（使用 `/etc/aliases.db` 文件）重新构建数据库。只需简单地重新构建数据库：

```
# /etc/init.d/sendmail reload
```

此命令会重建所有数据库文件，包括 `/etc/aliases` 文件。（如果 `reload` 没有更新，说明未安装 `sendmail-cf` 包：`yum install sendmail-cf`。）

- 制作配置文件 —— 使用 `make` 命令，你可以将部分或全部配置文件转换为数据库文件，这样它们就可以立即被 `sendmail` 守护进程使用。要做到这一点，切换到 `/etc/mail` 目录，并输入 `make all` 或带有你正在创建的目标数据库文件的 `make`：

```
# cd /etc/mail
# make virtualtable.db
```

你可以用 `access.db`、`domaintable.db`、`mailertable.db` 或 `sendmail.db` 替换 `virtualtable.db`（注意你使用的是 `.db` 目标名称 own原始配置文件的名称）。如所述，你也可以使用 `make` 命令重建所有数据库文件。

到此时，你的 `sendmail` 服务器应该已经启动运行。你可以通过向它发送邮件并检查日志文件以查看服务器是否有反应来测试你的服务器。确保你的防火墙允许 TCP 端口 `25` 的请求。输入以下内容检查你的邮件服务器是否正在响应请求：

```
# telnet 127.0.0.1 25
Trying 127.0.0.1...
Connected to localhost.localdomain (127.0.0.1)
Escape character is ''.
220 toys.linux. SMTP Sendmail 81.4/3/81.4/3;
Sun, 16 Nov15 2008 03:34:02 -0500
```

你可以看到 `sendmail` 守护进程正在运行并响应端口号 `25`。尝试输入 `HELO`。（字面上就是 `HELO` 而不是 `HELLO`！）完成后，输入 `QUIT` 退出。

> 注意：有关排查邮件服务器故障的更多信息，请参考 Wiley Publishing 出版的《Linux Troubleshooting Bible》。

# 重定向邮件

有时，你的电子邮件用户可能将邮件重定向到本地服务器邮箱以外的某个。每个用户都可以使用 `.forward` 文件重定向其邮件。在系统范围内，管理员可以设置别名。

# .forward 文件

用户重定向邮件的一种方法是通过 `.forward` 文件。`.forward` 的格式是名称后跟冒号，然后是用逗号分隔的地址或程序列表。常见用途包括：

- 将邮件管道到程序：
  - `user|/usr/bin/mailx` ---发送邮件到另一个账户：
  - `user@other.com`
- 将邮件投递到本地用户：
  - `user2`

`.forward` 文件放置在用户的家目录下。提示：如果你留空 `.forward` 文件，`sendmail` 将不会转发邮件。

# aliases 文件

处理邮件的更灵活的方法是使用 `/etc/aliases` 文件。别名文件包含名称后跟冒号，然后是用户名或别名。Fedora 默认设置了一些别名：

```
bin:root
daemon:root
adm:root
lp:root
```
