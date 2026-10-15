
在前两行中，发往 `chris` 或 `cnegus@linuxtoys.net` 的入站邮件被定向到名为 `chris` 的本地邮件服务器邮箱。在下一行中，发往同一域内 `francois` 的任何电子邮件都去 `francois@spidermaker.com`。之后，发送给 `info` 用户名的邮件将去本地的 `info-list` 邮件账户。

# 第 19 章：设置邮件服务器 803

以 `bogus@linuxtoys.net` 开头的行说明了一种错误情况。在这里，发往名为 `bogus` 的用户的邮件将被带有“No user here”的消息拒绝，并重定向回发送者。除了创建自定义错误消息外，你还可以使用符合 RFC 1893 的增强邮件状态代码（Enhanced Mail Status codes）。

> 注意：通常情况下，告诉潜在的垃圾邮件发送者用户账户不存在并不是一个好主意。垃圾邮件发送者经常查询邮件服务器以寻找信息，通常向常用名称发送邮件，以试图确定服务器上存在哪些真实用户。作为一般原则，尽量给在你的邮件服务器上钓鱼的人提供尽可能少的信息。

最后两行（以 `@example.net` 和 `@example.com` 开头）说明了如何将发往给定域所有接收者的邮件定向到同一个地方。在第一情况下，`example.net` 的消息将进入名为 `example-catchall` 的用户的邮箱。最后一行显示了如何将来自特定域的用户映射到所选域名上的相同名称 `#`。

一旦你对该文件进行了适合你配置的更改，就必须重新构建 `virtusertable` 数据库（`virtusertable.db` 文件），更改才能生效。有关此主题的信息，请参见“启动 sendmail 并生成数据库文件”。

## 添加用户账户

最终，你的邮件收到的邮件被放置在用户的邮箱中，用户可以随心意地提取并阅读。这些用户名中的每一个必须作为真实用户添加到你的 Fedora 系统中。例如，若要向你的 Fedora sendmail 服务器添加用户 `chris`，你可以输入（作为 root 用户）：

```
# useradd -s /sbin/nologin chris
```

此操作在 `/etc/passwd` 文件中创建了一个名为 `chris` 的用户账户，将 shell 设置为 `/sbin/nologin`，并在 `/var/spool/mail/chris` 为该用户创建一个邮箱。`/sbin/nologin` shell 防止用户登录 shell（当他们只想拥有邮件或 FTP 访问时，这是一个良好的安全实践）。Sendmail 可以将电子邮件定向到该用户的邮箱。

为了让该用户以后从其 POP3 客户端访问其邮件，他需要其用户账户的密码。使用 `passwd` 命令如下为该用户设置密码：

```
# passwd chris
```

```
Changing password for user chris

New UNIX password: ********

Retype new UNIX password: ********

passwd: all authentication tokens updated successfully
```

确保该用户拥有此用户名和密码，以便将其配置到用户的邮件客户端中。

## 启动 sendmail 并生成数据库文件

在你对 `sendmail.mc`、`virtusertable`、`access`、`domaintable` 和 `mailertable` 配置文件所做的任何更改在它们重新生成为数据库 `.db` 文件之前都不会生效。你有几种不同的方法可以将配置文件加载到数据库文件中：

- 重启 sendmail —— 每当你重启电脑或重启 sendmail 守护进程（`service sendmail restart`），所有的 sendmail 配置文件（包括 `sendmail.mc`）都会编译成数据库文件，供 sendmail 服务器使用。你可以使用 sendmail 启动脚本在不停止 sendmail 守护进程的情况下重新构建数据库（包括 `/etc/aliases.db` 文件）。若只需重新构建数据库，输入：`# /etc/init.d/sendmail reload`

```
# /etc/init.d/sendmail reload
```

此命令重新构建所有数据库文件和 `/etc/aliases` 文件。如果 `reload` 没有更新你的 `sendmail.cf` 文件，请确保已安装 `sendmail-cf` 软件包：`yum install sendmail-cf`。

- 生成配置文件 —— 使用命令，你可以将部分或所有配置文件转换为数据库文件，使其立即被 sendmail 守护进程使用。要这样做，更改 `/etc/mail` 目录，并输入 `make all` 或 `make`：

```
cd /etc/mail
make all
```

你可以将 `virtusertable.db` 替换为 `access.db`、`domaintable.db`、`mailertable.db` 或 `virtusertable.db`（注意你使用的是 `access.db`）。如所述，你可以使用 `make` 重新构建所有内容。此时，sendmail 应该已经在运行。你可以通过向以下地址发送邮件来测试你的服务器：

```
telnet 127.0.0.1 25
```

Trying 127.0.0.1...
220 localhost ESMTP
HELO localhost
250 Hello localhost
MAIL FROM:<test@example.com>
250 OK
RCP TO:<test@example.com>
250 OK
DATA
354 End data with <CR>.<CR>
test
.
250 2.0.0 accepted for delivery
QUIT
221 Bye

# 第 19 章：设置邮件服务器 805

注意：关于故障服务器的更多信息，请参考 Troubleshooting。

## 重定向邮件

有时，你的邮件用户可能希望将邮件重定向到邮箱以外的地方。每个用户可以使用 `.forward` 文件重定向他的邮件。在范围内，管理员可以在 `/etc/aliases` 文件中设置别名。

## .forward 文件

重定向自己的邮件的一种方法是使用 `.forward` 文件，用户可以将其放置在主目录中（例如 `/home/jkpat/.forward`）。纯文本 `.forward` 文件的格式是逗号分隔的邮件接收者列表。`.forward` 文件的常见用途包括：

- 管道到程序以过滤邮箱：`| /usr/bin/procmail`
- 将发往一个用户（例如 `jkpat`）的邮件发送到另一个（在本例中为不同机器上的 `cht09@other.mybox.com`
- 将邮件递送给本地用户（再次为 `jkpat`）并发送给另外两个（`cht09` 和 `brannigan`）：`\jkpat, cht09@other.mybox.com, \brannigan`

提示：你不可以在所有用户读取的目录下拥有 `.forward` 文件。如果你为 `.forward` 文件留了权限，sendmail 将忽略它且不会按你的预期转发邮件。要允许 sendmail 使用开放权限的 `.forward` 文件，你可以从 `sendmail.mc` 文件中的 `CONF_BLAME_SENDMAIL` 行中删除 `dnl`。

## 别名文件

处理邮件递送的更灵活的方法（全局而非针对特定用户）涉及 `/etc/aliases` 文件，它也是一个纯文本文件。别名文件包含一个名称，后跟冒号，然后是另一个用户名、另一个、地址列表、文件或一个将递送的程序。冒号左侧的名称（可以是有效的用户名或仅为别名）随后可以作为本地机器或远程机器上的邮件接收者。

`/etc/aliases` 中默认已经设置了一些某些别名。例如，因为 Fedora 中定义了许多管理员用户（`bin`、`adm`、`lp` 等），与其让

# 第四部分：Fedora 和 RHEL 网络与服务器设置

为每个用户设置独立的邮箱，所有消息都将重定向到 `root` 用户的邮箱，如下所示：

```
nbin: root
daemon: root
adm: root
lp: root
```
