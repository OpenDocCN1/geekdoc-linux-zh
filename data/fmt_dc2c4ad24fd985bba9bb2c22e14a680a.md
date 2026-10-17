
此示例显示，你的 `sendmail` 服务器接收的所有目标为 `example.com` 的消息将转发到名为 `mxl.linuxtoys.net` 的服务器。`smtp` 表示该服务器支持简单邮件传输协议。

## 配置虚拟用户

进入你的 `sendmail` 服务器的邮件将引导至你的机器，请求交付特定域名的特定个人。对于 `sendmail` 服务器支持的每个域名，你可以指定如何处理发送给该域邮件接收者的电子邮件。

使用 `sendmail`，你在 `/etc/mail/virtusertable` 文件中设置虚拟用户定义。本质上，你是在告诉 `sendmail` 根据你设置的定义来重定向指向特定用户名或域名的邮件。

如果你的服务器处理多个域名，则配置 `virtusertable` 文件尤为重要。这是因为默认情况下，相同的用户名（无论域名名如何）将存储在同一个邮箱箱中。例如，如果你的服务器处理 `example.com` 和 `linuxtoys.net` 的邮件，发给 `chris@example.com` 和 `chris@linuxtoys.net` 的邮件将重定向到 `/var/spool/mail/chris` 邮箱箱。通过 `virtusertable` 文件，你可以以许多方式更改这种行为。

`virtusertable` 文件默认是空的。以下是一些示例，说明了如何根据 `virtusertable` 定义以不同方式引导传入的邮件。

```
chris@linuxtoys.net chris

cnegu@linuxtoys.net chris

francois@linuxtoys.net francois@spidermaker.com

info@linuxtoys.net info-list

bogus@linuxtoys.net error:nouser No such user here

@example.net error-catchall

@example.com #1@linuxtoys.net
```

在前两行中，发往 `linuxtoys.net` 的 `chris` 或 `cnegu` 的传入邮件被重定向到名为本地服务器用户 `chris` 的邮箱箱。在下一行中，发往同一域名内 `francois` 的任何电子邮件都将去 `francois@spidermaker.com`。之后，发送给 `info` 用户名的电子邮件将保存到本地 `info-list` 邮件帐户。

以 `bogus@linuxtoys.net` 开头的行行说明了一个错误情况。在这里，发往用户 `bogus` 的邮件将被拒绝，并带有“No such user here”错误消息定向回发送者。除了创建自定义错误消息外，你还可以使用任何符合 RFC 1893 的增强邮件系统状态代码。

> 注意：通常情况下，告诉潜在垃圾邮件发送者用户账户不存在并不是好主意。垃圾邮件发送者经常查询邮件服务器寻找此类信息，通常向常用名称发送电子邮件，以试图确定服务器上存在哪些真实用户。作为一个一般原则，尽可能向钓鱼你邮件服务器的人提供尽可能的信息。

最后几行（以 `@example.net` 和 `@example.com` 开头）说明了如何将发往给定域所有接收者的邮件定向到同一个地方。在第一情况下，是 `-catchall`。在第二情况下，是 `#1@linuxtoys.net`。一旦你根据需要调整了此文件，就必须重新构建访问数据库（`access.db` 文件）以使更改生效。

## 添加用户

以 `@example.net` 和 `@example.com` 开头的最后几行说明了发往给定域所有接收者的邮件可以定向到同一个地方。在第一情况下，是 `catchall`。在第二情况下，是 `#1@linuxtoys.net`。一旦你根据需要调整了此文件，就必须重新构建访问数据库（`access.db` 文件）以使更改生效。有关此主题的信息，请参阅“启动 `sendmail` 并生成数据库文件”。

## 启动 sendmail 并生成数据库文件

此时，你的 `sendmail` 服务器应该已经运行。你可以通过向它发送邮件来测试服务器，并查看日志文件了解其反应。确保你的防火墙允许 TCP 25 的请求。通过输入以下内容检查邮件服务器是否有响应：

```
# telnet 127.0.0.1 25

Trying 127.0.0.1...

Connected to localhost.localdomain (127.0.0.1).

Escape character is '^'.

220 toys.linuxtoys.net SMTP Sendmail 8.14.1/8.14.1;

Sun, 15 Jun 2008 03:34:02 -0500
```

你可以看到 `sendmail` 进程正在运行并响应端口 25。尝试输入 `HELO`。（真的是 `HELO` 而不是 `HELLO`！）完成后，输入 `QUIT` 退出。

你有几种不同的方法可以加载你的配置文件：

- **重启 `sendmail`** —— 每当你重启计算机或重启 `sendmail` 守护进程（`service sendmail reload`）时，所有配置（包括 `sendmail.mc`）都会编译成数据库文件。如果要在不停止 `sendmail` 的情况下重新构建数据库，请使用 `sendmail` 启动脚本：

```
# /etc/init.d/sendmail reload
```

- **制作配置文件** —— 使用 `make` 命令，你可以将部分或所有配置文件制作成数据库文件，以便 `sendmail` 进程立即使用。要进行更改，请使用 `/etc/mail` 目录，并输入 `make all` 或带有你要创建的目标数据库文件。例如：

```
# cd /etc/mail

# make virtusertable.db
```

你可以用 `access.db`、`domtable.db`、`mailtert.db` 或 `sendmail.db` 替换 `virtuosable.db`。（注意你使用的是 `.db` 目标名称和原始配置文件的名称）。如前所述，你也可以使用 `make all` 命令重新构建所有数据库文件。

## 第 19 章：设置邮件服务器 813

## 重定向邮件

有时，您的电子邮件用户可能会将邮件重定向到本地服务器邮箱箱以外的地方。每个用户可以使用 `.forward` 文件来重定向其邮件。在系统范围内，管理员可以在 `/etc/aliases` 文件中设置别名来重定向邮件。

### .forward 文件

用户重定向自己的邮件的一种方法是使用 `.forward` 文件，用户可以将其放置在自己的家目录中（例如 `/home/jkpat/.forward`）。纯文本格式的 `.forward` 文件格式是用逗号分隔的邮件收件者列表。`.forward` 文件的常见用途包括：

- 将邮件通过管道交给程序以过滤邮箱箱内容：
  `| /usr/bin/procmail`
- 设置一个用户的默认邮件邮件（例如 `jkpat`）到另一个用户（例如不同机器上的 `cht09`）：
  `cht09@other.mybox.com`
- 将邮件递送到本地用户（`jkpat`）并发送给其他人（`cht09` 和 `brannigan`）：
  `jkpat, cht09@other.mybox.com, brannigan`

> **提示：** 不允许在所有用户都可以读取的目录中拥有 `.forward` 文件。如果您对 `.forward` 文件留有权限，`sendmail` 将忽略该文件而不按您的意愿进行转发。要允许 `sendmail` 使用开启权限的 `.forward` 文件，可以删除 `sendmail.mc` 文件中的 `CONDF_SENDMAIL` 行。

### aliases 文件

另一种更灵活的邮件处理方法（系统范围而非特定用户）涉及 `/etc/aliases` 文件，它也是一个纯文本文件。`aliases` 文件包含一个名称，后面跟着一个冒号，然后是用户名、另一个别名、地址列表或递送邮件的程序。冒号左侧的名称（可以是有效用户名或别名）可以作为本地机器或远程机器的邮件收件者。

`/etc/aliases` 中默认设置了一些别名（例如 Fedora 中的 `bin`、`adm`、`lp` 等），而不是为每个设置独立的邮箱箱，这些邮件都指向 `root` 用户，如下：

```
bin     root

adm: root

lp: root
```
