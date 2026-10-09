
列出可以在服务器上登录的用户，或者不允许在服务器上登录的用户。必须将`user_list_enable`（第 615 页）选项设置为`YES`，`vsftpd`才会检查此文件中的用户列表。将`user_list_enable`设置为`YES`并将`user_list_deny`（第 515 页）设置为`YES`（或不设置）可以防止用户在服务器上登录。设置`user_list_enable`和`user_list_deny`则仅允许指定的用户在服务器上登录。

```
/etc/vsftpd/chroot_list
```

根据`chroot_list_enable`（第 617 页）和`chroot_local_user`（第 617 页）的设置，此文件列出强制在其家目录进入`chroot`监狱的用户，或者不放置在`chroot`监狱的用户。

```
/var/log/vsftpd.log
```

日志文件。更多信息请参阅第 621 页的日志。

## 章节总结

`FTP`是一种通过网络从另一个系统下载和上传文件的协议。`FTP`既是客户端/服务器协议的名称，也是调用该协议的客户端程序的名称。由于`FTP`不是一种安全协议，它应该只用于下载公共信息。你可以在`avoid jail`的受限环境中运行`vsftpd` `FTP`服务器，这样可以大大降低恶意用户破坏系统的可能性。

许多服务器和客户端实现了`FTP`协议。`ftp`工具是原始的客户端实现；`sftp`是一个安全的实现，它使用`OpenSSH`功能来加密连接。`vsftpd`守护进程是一个安全的`FTP`服务器；它比其他`FTP`服务器更好地保护服务器免受恶意用户攻击。

公共`FTP`服务器允许以匿名或`ftp`身份登录。按照惯例，当你以匿名用户登录时，提供电子邮件地址作为密码。公共服务器在`pub`目录下经常会有有趣的文件。

`FTP`提供了两种文件传输模式：二进制（`binary`）和`ASCII`。使用二进制模式传输所有类型的文件（包括`ASCII`文件）是安全的。如果你使用`ASCII`模式传输二进制文件，传输将失败。

## 练习

- 1. 当你从 Linux 服务器以`ASCII`模式向 Windows 机器下载`ASCII`文件时，`FTP`对该文件做了哪些更改？将文件下载到 Mac 时会发生什么变化？

- 2. 如果以`ASCII`模式传输可执行程序文件会发生什么？

- 3. 在什么情况下`ftp`比`sftp`是更好的选择？

- 4. 你如何防止本地用户使用他们的系统用户名和密码在`vsftpd`服务器上登录？

- 5. `sftp`相比`ftp`有什么优势？

- 6. `ftp`中`cd`和`get`有什么区别？

## 高级练习

- 7. 为什么在`PORT`模式下连接`FTP`服务器可能会遇到问题？

- 8. 为什么在`chroot`监狱中运行`vsftpd`有好处？

- 9. 下载文件后，你发现它与提供的`MD5`校验和不匹配。再次下载文件得到相同的错误校验和。你做错了什么？如何修复它？

- 10. 你如何配置`vsftpd`通过`xinetd`运行，这种方法的主要优势是什么？

## 20. sendmail: 设置邮件客户端、服务器及更多

| 本章内容 | | |
| --- | --- |
| 快速入门 I：在客户端上配置 `sendmail` | 630 |
| 快速入门 II：在服务器上配置 `sendmail` | 631 |
| `sendmail` 如何工作 | 632 |
| 配置 `sendmail` | 635 |
| `SpamAssassin` | 640 |
| 网页邮箱 (Webmail) | 644 |
| 邮件列表 (Mailing Lists) | 646 |
| 设置 `IMAP` 或 `POP3` 服务器 | 647 |
| 设置 `KMail` | 648 |
| 认证中继 (Authenticated Relaying) | 650 |

## `/sbin/service sendmail restart`

```
Shutting down sendmail:      [ OK ]
Shutting down sm-client:    [ OK ]
sendmail:                     [ OK ]
Starting sendmail:
Starting sm-client:           [ OK ]
```

运行`chconfig`以使`SpamAssassin`守护进程在系统进入多用户模式时启动（此配置下通常安装了`SpamAssassin`）：

## `/sbin/chkconfig spamassassin on`

与`sendmail`一样，`SpamAssassin`通常处于运行状态。重新启动它会使`spamd`重新读取其配置文件：

## `/sbin/service spamassassin restart`

```
Stopping spamd:             [ OK ]
Starting spamd:            [ OK ]
```

`IMAP`和`POP`协议被实现为多个守护进程。有关这些守护进程以及如何启动它们的信息，请参见第 647 页。

## Notes

### 防火墙

`SMTP`服务器通常使用 `TCP` 端口 25。如果 `SMTP` 服务器系统正在运行防火墙，您需要打开此端口。使用 Red Hat 图形化工具（第 768 页），从“信任服务”（Trusted Services）框架中选择“邮件 (`SMTP`)”来打开此端口。更多通用信息请参见第 25 章，该章节详细介绍了`iptables`。

### cyrus

本章涵盖了`dovecot`包中包含的`IMAP`和`POP3`服务器。Red Hat Linux 还在`cyrus-imapd`包中提供了`IMAP`和`POP3`服务器。

## 更多信息

### Web

- `sendmail` [www.sendmail.org](http://www.sendmail.org)

- `IMAP` [www.imap.org](http://www.imap.org)

- `IMAP` and `POP3` [www.dovecot.org](http://www.dovecot.org)

- `IMAP` and `POP3` [cyrusimap.www.cmu.edu](http://cyrusimap.www.cmu.edu)

- `SquirrelMail` [www.squirrelmail.org](http://www.squirrelmail.org)

- `Postfix` [www.postfix.org/docs.html](http://www.postfix.org/docs.html)（替代 MTA，第 652 页）

- `Qmail` [gmail.area.com](http://gmail.area.com)

- `Mailman` [www.list.org](http://www.list.org)

- `procmail` [www.procmail.org](http://www.procmail.org)

- `SpamAssassin` [spamassassin.org](http://spamassassin.org)

- Spam database [razor.sourceforge.net](http://razor.sourceforge.net)

## 快速启动 I：在客户端上配置 sendmail

提示：您可能不需要配置`sendmail`来发送邮件

在`sendmail`运行时，请执行第 631 页[测试](#)下方描述的命令。只要`sendmail`能够连接到出站端口 25，您就不需要像本节描述的那样设置`sendmail`使用`SMTP`继器。如果您收到了通过测试发送的邮件，可以跳过本节。

此快速启动配置了一个出站的`sendmail`服务器。该服务器：

- 通过 ISP 中继使用远程`SMTP`服务器将出站邮件发送到其目的地（一个`SMTP`中继）。

- 将源自本地系统的邮件发送到`SMTP`服务器。它不转发来自其他系统的邮件。

- 不处理入站邮件。通常情况下，您需要使用`POP`或`IMAP`来接收邮件。

要设置此服务器，必须编辑`/etc/mail/sendmail.mc`并重启`sendmail`。

### 修改 sendmail.mc

`sendmail.mc`中以下行的`dnl define`表明该行是一条注释：

```
dnl define('SMART_HOST','smtp.your.provider')
```

要指定远程`SMTP`服务器，您必须在编辑器中打开`sendmail.mc`并更改前面的行，删除行开头的`dnl`，并将其替换为您的 ISP `SMTP`服务器的完全限定域名（FDN）（您可以从您的 ISP 获取此名称）。请勿修改该行中的反引号（`）或单引号（'）。如果您的 ISP `SMTP`服务器是`smtp.mysisp.com`，您将把该行改为：

```
define('SMART_HOST','smtp.mysisp.com')
```

**提示：不要修改反引号（`）或单引号（'）**

请勿修改`sendmail.mc`中任何行中的反引号（`）或单引号（'）。这些符号控制`m4`预处理器将`sendmail.mc`转换为`sendmail.cf`的方式；如果不保留这些符号，`sendmail`将无法正常工作。

## 重启 sendmail

当重启它时，`sendmail`会从您编辑的`sendmail.mc`文件重新生成`sendmail.cf`文件：

```
# /sbin/service sendmail restart
```

### 测试

使用以下命令测试`sendmail`：

```
$ echo "my sendmail test" | /usr/sbin/sendmail user@remote.host
```

将`user@remote.host`替换为另一个接收邮件系统的电子邮件地址。您需要向远程系统发送邮件以确保`sendmail`正在转发您的邮件。

## 快速启动 II：在服务器上配置 sendmail

如果您想接收指向您拥有的注册域的邮件，则需要将`sendmail`设置为入站邮件服务器。快速启动介绍了如何设置此类服务器。该服务器：

- 仅接受来自本地系统的出站邮件。

- 将出站邮件递送到接收者系统，而不使用中继。

- 接受来自任何系统的入站邮件。

此服务器不转发来自其他系统的出站邮件。如果您希望本地系统充当继器，请参见第 638 页的“访问：设置中继主机”。要使此配置生效，您必须能够建立出站连接并接收指向端口 25 的入站。

`sendmail.mc`中限制`sendmail`仅接受来自本地系统入站邮件的行只有：

```
DAEMON_OPTIONS(Port=smtp,Addr=127.0.0.1, Name=MTA')dnl
```

要允许`sendmail`接受来自其他系统的入站邮件，请删除上述行的`Addr=127.0.0.1,`：

```
DAEMON_OPTIONS(Port=smtp, Name=MTA')
```

默认情况下，`sendmail`不使用远程`SMTP`服务器中继邮件，无需更改（快速启动 I）。一旦您重启了`sendmail`，它将接受发送给系统的邮件。

## sendmail 如何工作

### 出站邮件

当您发送邮件时，MUA 将邮件传递给`sendmail`，`sendmail`在`/var/spool/mqueue`目录下创建两个文件，用于在`sendmail`处理期间持有邮件。为了为邮件创建唯一文件名，`sendmail`生成一个随机字符串并在文件名中使用该字符串。`sendmail`守护进程将邮件主体存储在名为`df`（数据文件）的文件，后面跟着生成的字符串。将头部和其他信息存储在名为`gof`（队列文件）的文件，后面跟着生成的字符串。

如果发生交付错误，`sendmail`会创建邮件的临时副本并存储在名为`tf`（临时文件）的文件，并将错误记录在`xf`中。一旦邮件成功发送，`sendmail`将删除`/var/spool/mqueue`中属于该邮件的文件。

### 入站邮件

默认情况下，MDA 将入站消息存储在邮件池`/var/spool/mail`中的用户文件中，采用`mbox`格式。在此目录下，每个用户都有一个以用户名命名的文件。邮件保留这些文件中直到被收集（通常由 MUA 执行）。一旦 MUA 从邮件池收集邮件，MUA 将按照用户的指示存储邮件，通常在用户的家目录层次结构中。

### mbox 与 maildir

`mbox`格式将用户的所有邮件存储在一个文件中。为了防止损坏，当进程添加或删除文件中的消息时，必须锁定文件；您无法在 MTA 添加消息的同时删除消息。一种竞争格式`maildir`将每条消息存储在单独的文件中。这种格式不使用锁，允许 MUA 在新邮件交付的同时读取和删除消息。此外，`maildir`格式更适合处理更大的邮箱。`dovecot`包支持`mbox`和`maildir`格式。`Gmail` (852) 作为`sendmail`的替代方案使用`maildir`格式的邮箱。

## 邮件日志

`sendmail`守护进程将日志消息存储在`/var/log/mailog`中。其他邮件服务器（例如`doveimap-login`和`pop3-login`守护进程）也可能向此文件记录信息。以下是一个日志项：

```
/var/log/mailog
```

```
...
Mar 3 16:25:33 sendmail[7225]: i23GPXvm007224:to=user@localhost.localdomain, claddr=root@localhost.localdomain>(0/0), delay=00:00:00, xdelay=00:00:00, mailer-local, pri=30514, dsn=2.0.0, stat=Sent
```

每个日志条目以时间戳、发送邮件的、邮件服务器名称（`sendmail`）和一个唯一标识符开头。收件者地址位于`to`标签之后，发送者地址位于`claddr`之后。附加字段提供了邮件器的名称和发送消息所需的时间。如果消息正确，`stat=`标签标记为`Sent`（已发送）。

当`sendmail`发送消息时，消息会被标记为`Sent`；这并不表示消息已经送达。如果由于后续发生错误导致消息未送达，发送者通常会收到一封邮件告知其未送达并给出原因。

如果你发送和接收大量邮件，`mailog`文件可能会变得很大。`syslog`日志（第 559 页）项设置为经常归档和轮转`mailog`文件。

## 别名与转发

三个文件可以转发邮件：`.forward`（第 634 页）、`aliases`和`virtuertable`（第 640 页）。第 640 页的表 20-1 对了这三个文件。

### 表 20-1 转发技术比较

| | `.forward` | `aliases` | `virtuertable` |
|---|---|---|---|
| 控制者 | 非 `root` 用户 | `root` | `root` |
| 转发至 | 非 `root` 用户 | 本地系统上的任何真实或虚拟用户 | `sendmail` 识别的任何域上的任何真实或虚拟用户 |
| 优先级 | 第三 | 第二 | 第一 |

## `/etc/aliases`

大多数情况下，当你发送邮件时，它会发送给特定个人：收件者，`user@system`，映射到指定系统上的特定真实用户。有时你可能希望将邮件发送给一组用户，而不是特定的收件者。用户示例包括`postmaster`、`webmaster`、`root`和`tech_support`。不同的用户可能在不同的时间收到此邮件，或者邮件可能由一组用户回答。你可以使用`aliases`文件将入站地址映射到本地用户、文件、命令和远程地址。

`aliases`文件中的每行都包含若干个本地伪用户（pseudouser），随后是冒号、空格和由逗号分隔的终点列表。默认安装包含了许多别名，可以将某些某些伪用户的消息重定向到`root`。这些别名的格式如下：

- `system: root`

将消息发送到`root`账户是使它们易于审阅的好方法。但是，由于`root`的邮件很少被检查，你可能想向真实用户发送副本。以下行行将发送到本地系统`abuse`的邮件转发到`root`和`alex`：

- `abuse: root, alex`

你可以使用这种类型的别名创建简单的邮件列表。例如，转发别名会将发送到本地系统`admin`的所有邮件副本发送给几个用户，包括位于不同系统上的 Zach：

- `admin: sam, helen, mark, zach@corp.com`

你可以通过指定绝对路径代替终点地址来将邮件重定向到文件。以下别名在不太负责的系统管理员中非常流行，它们将发送到`complaints`的邮件重定向到`/dev/null`（第 448 页），在那里它们会消失：

- `complaints: /dev/null`

你还可以通过在命令前加上管道符(|) 来将邮件发送到命令的标准输入。这种技术通常用于如`Mailman`（第 646 页）之类的邮件列表软件。对于它维护的每个列表，`Mailman`在`aliases`文件中有条目，例如`mylistist`的条目：

```
mylistist: "/usr/lib/mailman/mailman post mylist"
```

### newaliases

在编辑`/etc/aliases`后，你必须以`root`身份运行`newaliases`或重启`sendmail`以重新创建`sendmail`读取的`aliases.db`文件。

### praliases

你可以使用`praliases`列出`sendmail`目前加载的别名：
