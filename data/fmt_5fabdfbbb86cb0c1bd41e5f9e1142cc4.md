
通过基于本地 SMTP 的网络连接邮件中枢（Mail Hub）。此功能包含的 `mail.popen.com` 参数是邮件中枢的规范名称。当然，您应该更改此规范名称以反映您的邮件服务器，例如：`FEATURE(`client1`, `my.mailhub.com`)`。

```
undefined(ALIAS,FILE)
```

此此配置选项可以防止 Sendmail 的空版本尝试访问 `/etc/mail/aliases` 和 `/etc/mail/aliases` 文件。在 `.mc` 文件中添加此行后，您就不需要在所有内部邻居客户端 Sendmail 机器上拥有 `aliases` 文件了。只有在邮件中枢服务器上需要用于网络中所有服务器和客户端的别名。

注意：我们指出，在此类配置下，不应定义任何邮件器，也不进行任何别名设置或转发。

## 第 2

既然宏配置文件 `null.mc` 已经创建，我们可以通过以下命令在所有邻居服务器和客户端机器上从这些语句构建 Sendmail 配置文件：

```
[root] deep cp -f /var/tmp/sendmail-version/etc/cf/
[root] deep cp -f m4/m4.mc null.mc >/etc/mail/sendmail.cf
```

## 第 3

邮件将不再被投递到您的本地机器。由于将不再有入站邮件连接，您不再需要在邻居或本地服务器、客户端机器上运行 Sendmail 守护进程。

要停止邻居或本地服务器或客户端机器上的 Sendmail 守护进程，请编辑或创建 `/etc/sysconfig/sendmail` 文件并更改/添加以下行：

```
DAEMON=yes
读取：
DAEMON=no
以及：
QUEUE=1h
```

注意：`/etc/sysconfig/sendmail` 文件下的 `QUEUE=1h` 会导致 Sendmail 每小时处理一次队列。我们保留该行是因为在邮件中枢宕机时，Sendmail 仍需要定期处理队列。

### 第 4

本地机器从不使用别名、访问或其他映射数据库。由于所有的映射文件数据库都位于网络中我们所有本地机器的中央邮件中枢服务器并使用，我们可以安全地从所有本地机器上删除以下命令和手册页。

```
/usr/bin/newaliases
usr/man/man1/newaliases.1
usr/man/man5/newaliases.5
```

- 要从系统中删除这些文件，请使用以下命令：

`[root] client] rm -f /usr/bin/newaliases`

`[root] client] rm -f /usr/man/man1/newaliases.1`

`[root] client] rm -f /usr/man/man5/newaliases.5`

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture ® and OpenDocs Publishing

### 第 5

从整个本地 Sendmail 服务器或客户端中移除不必要的 Procmail 程序。

由于本地机器将所有内部和外部邮件发送到邮件中枢服务器进行后续投递，我们不需要使用像 Procmail 复杂的本地投递程序来完成工作。

相反，我们可以使用默认的 "/bin/mail" 程序。

- 要从系统中移除 Procmail，请使用以下命令：

`[root@client]# rpm -e procmail`

### 中央邮件中枢的 /etc/mail/access 和 access.db 文件

可以创建 "access" 数据库文件来接受或拒绝来自选域的邮件。例如，您可以选择拒绝所有来自已知垃圾邮件发送者的邮件，或接受转发来自您本地网络的所有邮件，因为现在 Sendmail 默认拒绝中（这是一种反垃圾邮件功能）。在 "access" 文件示例中，我们将允许来自 localhost 以及所有以 IP 地址 192.168.1 开头的本地网络地址的继继。"access" 和 "access.db" 文件对于本地或邻居客户端不是必需。只有当您决定设置中央邮件中枢来处理所有用户时才需要。另请注意，使用中央邮件中枢将提高您网络上运行 Sendmail 的其他服务器和客户端的安全性和管理。

## 第 1

创建 `access` 文件（`touch /etc/mail/access`）并添加以下行：

```
# 下面显示的此文件格式说明来自
# Sendmail 源码发行版下的 "ct/README" 文件。
# 表格本身使用电子邮件地址、域名名和网络
# 作为键。例如，
# spammer@aol.com REJECT
# cyberspammer.com REJECT
# 192.168.212 REJECT
# 将拒绝来自 spammer@aol.com 的邮件、来自 cyberspammer.com 的任何用户
#（或 cyberspammer 域内的任何主机），以及位于
# 192.168.212.\* 网络上的任何主机。
# 映射的值部分包含：
# OK 即使运行列表中的其他规则
# 拒绝它，也接受邮件，例如，
# 域名无法解析。
# RELAY 接受投往指定域的或
# 从指定域接收的邮件，以便通过
# 您的 SMTP 服务器继继。RELAY 也作为
# 其他检查的隐式 OK。
# REJECT 用通用消息拒绝发送者或收件者。
# DISCARD 使用 $discard mail 完全
# 丢弃消息。这对于
# 地址有效，即您应该
# 丢弃从接收到的任何内容。
# 此处是 RFC 821 get
# "any text" 是返回的消息。
```

Copyright 1999 - 2000 Gerhard Maurani, Open Network Architecture ® and OpenDocs Publishing

## 第 2

创建 `access.db` 文件：

记住，由于 "/etc/mail/access" 是一个数据库，在按说明创建文本文件后，您必须使用 "makemap" 工具创建数据库映射。

- 创建数据库映射，请使用以下命令：

`[root@deep] makemap hash /etc/mail/access.db < /etc/mail/access`

## 服务器软件（邮件网络服务） | 第5章

中央邮件枢纽所使用的 "etc/mail/virtertable, domainable, mailertable, and virtertable.db, domainable.db, mailertable.db" 文件

所有这些文件都涉及 Sendmail 的功能，系统管理员可以对其进行调整。再次强调，这些功能通常只在中央邮件枢纽服务器上需要。以下是每一项的解释：

### virtertable & mailertable db 文件

`virtertable` 是一个将虚拟域名映射到新地址的数据库。通过此功能，发送到你网络中虚拟域名的邮件可以投递到本地、远程或单个用户地址。

### domainable & domainable db 文件

`domainable` 是一个将旧域名映射到新域名的数据库。通过此功能，你网络上的多个域名名可以从旧域名重写为新域名。

### mailertable & mailertable db 文件

`mailertable` 是一个将“主机域名”名称映射到特殊传输代理（delivery agent）和新域名对的数据库。通过此功能，你网络上的邮件可以通过特定的传输代理投递到新的或远程域名。

- 要使用以下命令在 "etc/mail/virtertable" 中创建 virtertable、domainable、mailertable 以及对应的 ".db" 文件：

```bash
[root@eep # for map in virtertable domainable mailertable
> touch /etc/mail/s($map)
> chmod 044 /etc/mail/s($map)
> makedmap /etc/mail/s($map).db < /etc/mail/s($map)
> chmod 044 /etc/mail/s($map).db
> done
```

## 适用于所有配置 "etc/mail/local-host-names" 文件

读取 "etc/mail/local-host-names" 文件是为了获取本地主机的别名。此类文件的一个用途可能是包含你网络中的主机列表，本地主机在这些主机中作为 MX 接收者。对于这些机器，我们只需要将它（即 mail.opencena.com）处理的机器名称添加到 "etc/mail/local-host-names" 中即可。这是一个示例：

创建 `local-host-names` 文件（`touch /etc/mail/local-host-names`）并添加以下行：
