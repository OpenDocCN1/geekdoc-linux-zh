
`m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf`

![](img/7605650e62fab537998f2b973dbf5a26_504_0.png)

# 安装邮件服务器

注释还告诉你是，你你需要 `sendmail-cf` 包来处理此文件。

根据前一节对 `m4` 宏的描述，你可以看到 `sendmail.mc` 文件使用 `define` 来创建新宏。你还可以看到大量使用 `dnl` 以避免在输出中插入过多的行。

其他大写写单词（如 `OTYPE`、`FEATURE` 和 `MAILER`）是 `sendmail` 宏。这些宏定义在 `/usr/share/sendmail-cf` 目录下子目录中的 `m4` 文件，并通过以下 `include` 宏整合到 `sendmail.mc` 文件中：

```
include(`/usr/share/sendmail-cf/m4/cf.m4`) dnl
```

`/usr/share/sendmail-cf/m4/cf.m4` 文件反过来包含了 `cfhead.m4` 文件，该文件又包含了其他 `m4` 文件，以此此类推。最终效果如下：当 `m4` 宏处理 `sendmail.mc` 文件时，宏处理器会将来自 `/usr/share/sendmail-cf` 各个子目录的许多 `m4` 文件合并。

以下是 `/etc/sendmail.mc` 文件需要注意的一些关键点：

- `VERSIONID('setup for linux')` 宏会将引号内的版本信息插入到输出中。
- `OTYPE('linux')` 将 Linux 指定为操作系统。你必须尽早指定此宏以确保配置正确。
- `MAILER(smtp)` 描述了邮件发送程序。根据 `/usr/share/sendmail-cf/README` 文件中的说明，`MAILER` 声明始终放在 `sendmail.mc` 文件的末尾，且 `MAILER(smtp)` 总是优于 `MAILER(promail)`。邮件器 `smtp` 指的是 SMTP 邮件发送程序。
- `FEATURE` 宏请求各种特殊功能。例如，`FEATURE('blacklist-recipients')` 开启了阻止某些用户、主机或地址的邮件的功能。允许或拒绝哪些邮件的规范存放在访问数据库中（存储在 `/etc/access.db` 文件中）。你还需要 `FEATURE('access_db')` 宏来开启访问数据库。
- `MASQUERADE_AS(`mydomain.com`)` 导致 `sendmail` 让外发邮件看起来是来自主机 `mydomain.com`（将我的域名替换为你的域名）。这种设计思路是让一个大型组织

![](img/7605650e62fab537998f2b973dbf5a26_505_0.png)

设置单一的 `sendmail` 服务器来处理许多子域名的邮件，并让一切看起来都来自同一个域名（例如，来自大学许多部门的邮件看起来都来自某个用户）。

# 其他邮件服务器文件

`/etc/mail` 目录包含了 `sendmail` 使用的其他文件。这些文件被引用在 `sendmail` 配置文件中，即 Fedora 中的 `/etc/mail/sendmail.cf` 和 SUSE 中的 `/etc/sendmail.cf`。例如，这里是你可以如何在 Fedora 中搜索 `/etc/mail` 字符串：

```
grep "\etc/mail" /etc/mail/sendmail.cf
```

以下是命令在典型 Fedora 系统上显示的结果：

## 484 安装邮件服务器

- * `/etc/mail/access`: 允许发送邮件的主机名称、`IP` 地址或两者兼有（用于停止垃圾邮件——即不想要的电子邮件）。
- * `/etc/mail/access.db`: 根据 `/etc/mail/access` 文件生成的访问数据库。
- * `/etc/mail/helpfile`: SMTP 命令的帮助信息。
- * `/etc/mail/local-host-names`: 此主机被识别的名称。
- `mailertable`: 用于覆盖邮件路由方式的邮件表。（例如，项目 `comcast.net smtp:smtp.comcast.net` 告诉 `send` 发送给 `comcast.net` 的邮件必须发送到 `smtp.comcast.net`）。
- * `/etc/mail/relay-domains`: 允许中继的主机。
- * `/etc/mail/trusted-users`: 允许在无警告的情况下使用其他用户身份发送邮件的用户列表。
- * `/etc/mail/usertdb.db`: 包含每个用户登录名和真实名的用户数据库。
- `/etc/mail/virtuertable`: 在此系统上托管的具有虚拟域地址用户的数据库。

`/etc/mail/` 目录有时包含其他文件——`/etc/mail/certs` 以及带有 `.pem` 扩展的文件——这些用于通过使用 SMTP 的 STARTTLS 扩展来支持 `sendmail` 中的增强邮件 (`PEM`)。STARTTLS 扩展使用 TLS（通常称为 SSL——安全套接层）来验证发送者身份并加密邮件。RFC 2487 描述了 STARTTLS（该 RFC 可以在 `http://ietf.org/rfc/rfc2487.txt` 在线获取）。

如果你编辑了 `/etc/mail/mailertable` 文件，必须在更改生效前执行以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

这里有一种更简单的方法，可以确保在进行任何更改后都重新构建所有内容——只需在 `root` 用户下输入以下命令：

```
cd /etc/mail
make
```

第一条命令将当前目录更改为 `/etc/mail`，第二条命令运行 `make` 命令，该命令会读取 `/etc/mail` 中名为 `Makefile` 的文件以执行重建所有内容所需的步骤。（要了解更多关于 `make` 和 `Makefile` 的信息，请参阅第 VIII 卷第 1 章。）

![](img/7605650e62fab537998f2b973dbf5a26_509_0.png)

## forward 文件

用户可以通过在其家目录下放置一个 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，包含用逗号分隔的邮件地址列表。任何发送给该用户的邮件将转发到这些地址。如果 `.forward` 文件包含单个地址，则该用户的所有邮件将重定向到该单一电子邮件地址。例如，假设家目录下放置了一个包含以下行的 `.forward` 文件：

`ashley`

此行会导致 `sendmail` 自动将所有发送给 `emily` 的电子邮件发送到同一系统上的用户名 `ashley`。用户 `emily` 将不会接收任何邮件。

你可以通过列出完整的电子邮件地址将邮件重定向到另一个系统。例如，你可以添加一个包含以下行的 `.forward` 文件，将消息发送到用户名 `wilbur` 的邮件地址

`wilbur@somewhereelse.net`

为了在原始系统中保留消息的副本，除了转发到前述指定的地址外，请在 `.forward` 文件中添加以下行：

只需添加用户名并在行尾加上反斜杠 (`\`)。行末尾的反斜杠会阻止 `sendmail` 重复转发消息。

## sendmail 别名文件

除了 `sendmail.cf` 文件外，`sendmail` 还会咨询名为 `/etc/aliases` 的别名文件将名称转换为地址。别名的位置出现在 `sendmail` 配置文件中。

每个别名都是电子邮件地址的短名称。系统管理员使用 `sendmail` 别名文件转发邮件、创建邮件列表（标识多个用户的单一别名），或通过多个不同的名称引用用户。例如，这里是一些典型的别名：

`gebrown: glbrown`
`all: jessica, isaac, alex, caleb, glbrown`

## 486 安装 INN 服务器

在 `/etc/aliases` 文件中定义任何新别名后，你必须以 `root` 登录并输入以下命令使新别名生效：

```
sendmail -bi
```

安装

N 服务器

本 服务器

如何配置 InterNetNews (`INN`)，这是一个基于 TCP/IP 的新闻服务器。首先，你必须安装 `INN`。

在 Debian、Ubuntu 和 Xandros 中，使用 `dpkg -l inn` 查看是否安装了 `inn`。对于 Fedora 和 SUSE，使用 `rpm -q` 查看是否安装了 `inn` 软件包。
