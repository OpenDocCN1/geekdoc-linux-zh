
SMTP 协议只能传输 ASCII 文本。它不支持字体、颜色、图形或附件。如果你想发送这些项目，则需要在使用 SMTP 时配合 MIME（多用途互联网邮件扩展）协议。

# 第 4 章

SMTP 有一个主要缺点，它假设发送和接收的 MTA 始终连接到互联网。这一缺点通过 POP3 克服。

让我们学习 POP3。

## POP3

开发 POP3 是为了解决 SMTP 面临的问题。POP3 运行在连接到网络的服务器上，该服务器持续发送和接收邮件。POP3 服务器存储它收到的任何消息，直到接收者请求它们。如果你想读取邮件，你需要 POP3 来检索在你未连接到互联网（离线）时到达 MTA 的消息。POP3 使用 MTA 的存储空间来保存消息直到它们被请求。你可以通过连接到服务器来检索服务器存储的消息。（注：原文此处有大量重复句子，翻译已按逻辑去重或保留核心含义）。IMAP4 允许用户在服务器上访问并管理邮件。与 POP3 通常将消息下载到本地设备并从服务器删除不同，IMAP4 允许用户在服务器上...

IMAP 的关键功能包括：

- 文件夹管理：用户可以在服务器上组织邮件。
- 服务器端搜索：服务器可以根据各种标准搜索邮件。
- 部分获取：用户可以只下载头部或邮件的特定部分。
- 多设备同步：在服务器上进行的更改（如标记为读或删除）会反映在所有设备上。

## 配置 Sendmail

各种传输代理在 Linux 中均可用。Sendmail 是最广泛使用的之一。在配置 sendmail 之前，你需要了解它的角色。它作为 MTA（邮件传输代理）。

你可以通过两种方式启动 sendmail 服务：

- `service sendmail start`
- 你也可以使用 telnet 连接到本地端口 25。使用以下命令：

```bash
# telnet localhost 25
Trying 127.0.0.1.
Connected to localhost.
Escape character is '^'.
220 vadmin ESMTP 8.14.3/8.14.3; Mon, 4 Jun 2012 02:23:59 -0400
QUIT
221 2.0.0 vadmin closing connection
Connection by foreign host.
```

如果你看到上述输出，说明 sendmail 正在运行。输入 `QUIT` 退出会话。

一旦你安装并运行了 sendmail，你就可以配置它。你可能需要编辑 `/etc/sendmail.cf`（sendmail 配置文件）。定位配置文件中以大写字母 DS 开头的行，如下所示：

```
# "Smart" relay host (may be null)
DS
```

修改该行以定义邮件中继主机名称，例如在我们的案例中，我们指定名为 `mailmessage.example.com` 的主机作为邮件中继主机。邮件中继主机是您网络上发送和接收邮件的计算机名称。在 DS 和主机名之间不要留任何空格。

```
# "智能" relay中继主机（可能为空）
DSmail.example.com
```

如果您的系统中尚未安装 `sendmail-cf` 软件包，请安装它，因为它包含了使用 m4 方法配置 sendmail 所需的 m4 宏文件（下一节描述）。

让我们讨论一下邮件队列。

## 邮件队列

当电子邮件没有被即时送达时，它将留在 MTA 的输出邮件队列中。这背后可能有许多原因。无论原因何，用户都可以继续使用他们的 UA 编写电子邮件。当他们发送消息时，sendmail 会将消息放入邮件队列并在设定一段时间后尝试重发。你可以通过检查启动 sendmail 的初始化脚本来查找这些间隔。`/etc/sysconfig/sendmail` 文件中的以下行描述了这些信息：

```
DAEMON=yes
QUEUE=1h
```

以 `QUEUE` 开头的行定义重试间隔为一小时。你可以以小时 (`h`)、分钟或秒 (`s`) 设置间隔。

让我们讨论一下别名。

## 邮件别名

邮件别名功能用于创建分发列表并使用户访问更方便。例如，如果你在拼写某人的名字时遇到困难，可以设置别名；即使你拼错了名字，邮件仍然到达目标收件者。你还可以将一个不存在的用户别名指向真实的用户。别名文件为 `/etc/aliases`，如下所示：

```
# 基本系统别名 -- 这些必须存在
mailer-daemon: root
postmaster: root
```

```
# 伪账户通用重定向
daemon: root
lp: root
sync: root
shutdown: root
usetup: news
ftpade: ftp
ftpadmin: ftp
ftp-adm: ftp
ftp-admin: ftp
```

```
# trap decode 以捕获安全攻击
decode: root
```

```
# 应该接收 root 邮件的人
#root: marc
# 用户 bob: marc
```

在上面的文件中，你可以看到 mailer-daemon 和 postmaster 的系统别名，指向伪账户的重定向（root 使用得最多），以及用户别名，例如 bob，它将所有发给 bob 的邮件重定向到真实用户 marc。

要在别名文件中创建条目，输入用户名后跟冒号，然后是某种空格，最后是别名。在冒号左侧可以指定多个用户名以创建分发列表。运行 `new` 命令使更改生效，因为你的别名文本文件会更新二进制文件。这一步是必要的，因为 sendmail 查看二进制文件 `/etc/aliases.db` 来读取别名信息。

让我们学习一些 sendmail 的命令。

## Sendmail 文件

Sendmail 使用以下文件和目录：

- `/usr/sbin/sendmail`: 它是 sendmail 守护进程的可执行镜像
- `mail`: 它显示邮件队列的内容
- `/var/spool/mqueue`: 存放邮件队列的目录
- `/var/spool/mail`: 存放用户邮件池的目录。例如：

```
ls -l /var/spool/mail/
-rw-rw---- 1 mail 2012-04-08 12:45 /var/spool/mail/bill1
-rw-rw---- 1 mail 2012-04-08 12:43 /var/spool/mail/ram
-rw-rw---- 1 root 2012-06-02 00:46 /var/spool/mail/root
```

- `/etc/access`: 列出了不允许向您的系统发送邮件的用户名、电子邮件地址、域名名和 IP 地址
- `/etc/mail-domains`: 列出了允许通过您的系统接收电子邮件的主机
- `/etc/local-host-names`: 列出了系统的其他名称
- `/etc/virtertable`: 将电子邮件地址映射到系统上的用户名

现在，让我们学习使用 postfix 邮件服务器。

## 使用 Postfix 邮件服务器

Postfix 被广泛使用，每天处理数千条消息。Postfix 兼容命令行级。Postfix 的开发是为了 sendmail 的高性能、更易用的替代品。在上一节中，你学习了邮件中继主机的语法：

```
d5relay.example.com
```

Postfix 的语法写法如下：

```
relayhost = relay.example.com
```

让我们了解更多关于 Postfix。

默认情况下，Fedora 使用 Sendmail。你必须停止 sendmail 以启动 postfix。使用以下行停止 sendmail：

```
# service sendmail stop
```

首先，确保您的系统中已安装了 postfix。输入以下命令检查：

```
# rpmquery postfix
postfix-2.5.6-3.fc11.1586
```

它返回了系统中安装的 postfix 版本。在继续之前，如果尚未安装，请安装 Postfix。

`/etc/postfix/main.cf` 是 postfix 的主配置文件。Postfix 支持大量的配置变量。以下是应当配置的变量。检查或编辑它们来配置 postfix：

- `mydomain` 变量指定您的域名：`mydomain = example.com`
