

## 安装邮件服务器

| 运算符 | 描述 |
| :--- | :--- |
| O | 将值分配给选项。例如，`O AliasFile=/etc/aliases` 将 `AliasFile` 选项定义为 `/etc/aliases`，这是 `sendmail` 别名文件的名称。 |
| P | 定义优先级字段的值。例如，`Pjunky=-100` 将标记为 `Precedence: junk` 头字段的邮件优先级设置为 -100。 |
| R | 定义一条规则。（规则有左侧和右侧；如果输入匹配左侧，则右侧替换它。此规则称为*重写*。）例如，重写规则 `R$* ; $1` 会去除末尾的分号。 |
| S | 标记一个规则集，您可以使用后续的 R 控制行开始定义它。例如，`S3=canyonify` 将下一个规则集标记为 `canonify` 或 `ruleset 3`。 |
| T | 将一个用户名添加到受信任类（class t）中。例如，`Troot` 将 `root` 添加到受信任用户类中。 |
| V | 定义配置文件的版本号。例如，`V1.0/Berkeley` 将版本号定义为 1.0。 |

### 其他 sendmail 文件

`/etc/mail` 目录包含 `sendmail` 使用的其他文件。这些文件在 `sendmail` 配置文件中被引用，在 `Fedora Core` 中为 `/etc/mail/sendmail.cf`，在 `SUSE` 中为 `/etc/sendmail.cf`。例如，这是如何在 `Fedora Core` 的 `/etc/mail/sendmail.cf` 文件中搜索 `/etc/mail` 字符串：

```
grep "*/etc/mail*" /etc/mail/sendmail.cf
```

在我的 `Fedora Core` 系统上，`grep` 命令搜索结果显示如下：

```
Fw /etc/mail/local-host-names
PR-o /etc/mail/relay-domains
Kmailer table hash -o /etc/mail/mailertable.db
Kvirtuser hash -o /etc/mail/virtuser table.db
Kaccess hash -Tc<"MDF"> -o /etc/mail/access.db
#0 ErrorHeader=/etc/mail/error-header
0 HelpFile=/etc/mail/helpfile
O UserDatabaseSpec=/etc/mail/userdb.db
#0 ServiceSwitchFile=/etc/mail/service.switch
#0 DefaultAuthInfo=/etc/mail/default-auth-info
Pt /etc/mail/trusted-users
```

**卷七**
**第四章**

管理邮件和新闻服务器

您可以忽略以井号或数字符号（#）开头的行，因为 sendmail 将这些行视为注释。其他行是 sendmail 控制行，引用 `/etc/mail` 目录中的其他文件。

以下是这些 sendmail 文件应包含的内容。（注意，并非所有这些文件都必须存在于 `/etc/mail` 目录中，即使存在，某些文件也可能是空的。）

- `/etc/mail/access`：允许发送邮件的主机名称和/或 IP 地址（有助于阻止垃圾邮件——不需要的电子邮件）
- `/etc/mail/access.db`：由 `/etc/mail/access` 文件生成的访问数据库
- `/etc/mail/helpfile`：SMTP 命令的帮助信息
- `/etc/mail/local-host-names`：本主机已知的名称
- `/etc/mail/mailertable`：用于覆盖邮件路由方式的邮件表（例如，条目 `comcast.net compast:smtp.comcast.net` 告诉 sendmail 发给 `comcast.net` 的邮件必须发送到 `smtp.comcast.net`。）
- `/etc/mail/relay-domains`：允许中继的主机
- `/etc/mail/trusted-users`：允许使用其他用户名称发送邮件而不受警告的用户列表
- `/etc/mail/userdb.db`：包含每个用户登录名和真实名称信息的用户数据库文件
- `/etc/mail/virtusertable`：托管在此系统上的具有虚拟域地址的用户数据库

![](img/792720823146d68f19fd50c99ebfce4b_651_0.png)

`/etc/mail` 目录有时还包含其他文件——`/etc/mail/certs` 以及带有 `_pem` 扩展名的文件——旨在通过使用 SMTP 的 STARTTLS 扩展来支持 sendmail 中的隐私增强邮件（PEM）。STARTTLS 扩展使用 TLS（更常被称为 SSL——安全套接字层）来验证发件人并加密邮件。RFC 2487 描述了 STARTTLS。（该 RFC 可在 http://ietf.org/rfc/rfc2487.txt 在线获取。）

![](img/792720823146d68f19fd50c99ebfce4b_651_1.png)

如果您编辑 `/etc/mail/mailertable` 文件，必须在更改生效前键入以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```

一种更简单的方法来确保在做出任何更改后重建所有必要内容——只需以 root 身份登录并键入以下命令：

```
cd /etc/mail
make
```

第一条命令将当前目录更改为 `/etc/mail`，第二条命令运行 `make` 命令，该命令读取 `/etc/mail` 中名为 Makefile 的文件以执行重建所有内容的必要步骤。（要了解有关 make 和 Makefile 的更多信息，请参见卷八，第一章。）

### .forward 文件

用户可以通过在其主目录中放置 `.forward` 文件来重定向自己的邮件。`.forward` 文件是一个纯文本文件，包含逗号分隔的邮件地址列表。任何发送给该用户的邮件都会转发到这些地址。如果 `.forward` 文件包含单个地址，则该用户的所有电子邮件都会重定向到该单一电子邮件地址。例如，假设在一个名为 emily 的用户的主目录中放置了一个包含以下行的 `.forward` 文件：

```
ashley
```

此行导致 sendmail 自动将所有发送给 emily 的电子邮件发送到同一系统上的用户名 ashley。用户 emily 完全不会收到邮件。

还可以通过列出完整的电子邮件地址将邮件转发到另一系统上的用户名。例如，我添加了一个 `.forward` 文件，其中包含以下行，以将我的消息（发给我的用户名 naba）转发到邮件地址 naba@comcast.net：

```
naba@comcast.net
```

现在假设我想在原始系统上保留一份消息副本，同时转发到地址 naba@comcast.net。我可以通过在 `.forward` 文件中添加以下行来实现：

```
naba@comcast.net, naba\
```

我只需追加我的用户名并在行尾添加反斜杠。行末的反斜杠（\）阻止 sendmail 反复转发消息（因为当副本发送到系统上我的用户名时，sendmail 通常会再次处理我的 `.forward` 文件）。反斜杠告诉 sendmail 不要反复转发消息。

### sendmail 别名文件

除了 *sendmail.cf* 文件外，*sendmail* 还会参考名为 `/etc/aliases` 的别名文件，将名称转换为地址。别名文件的位置出现在 *sendmail* 配置文件中。

每个*别名*通常是电子邮件地址的较短名称。系统管理员使用 *sendmail* 文件转发*邮件*，创建邮件列表（标识多个用户的单一别名），或通过多个不同名称引用用户。例如，以下是一些典型的别名：

- barkakati: naba
- naba: naba@lnbsoft
- all: naba, leha, ivy, emily, ashley

第一行表示发送给 *barkakati* 的邮件将交付给本地系统上名为 *naba* 的用户。第二行表明发送给 *naba* 的邮件实际上发送到了 *lnbsoft* 系统上的用户名 *naba*。最后一行将 *all* 定义为五个用户 *naba*、*leha*、*ivy*、*emily* 和 *ashley* 的别名。这意味着发送给 *all* 的邮件将发送到这五个用户。

在 `/etc/aliases` 文件中定义任何新别名后，必须以 *root* 身份登录，并通过键入以下命令使新别名生效：

```
sendmail -bi
```

## 安装 INN 服务器

在本节中，我描述了如何配置基于 TCP/IP 的新闻服务器 InterNetNews（INN）。首先，您必须安装 INN。

在 Debian、MEPIS、Ubuntu 和 Xandros 中，键入 `dpkg -l inn*` 以查看是否安装了 *inn*。在 Fedora Core 和 SUSE 中，键入 `rpm -q inn` 并查看是否安装了 *inn* 包。

在 Debian、MEPIS 和 Ubuntu 中，键入 `apt-get install inn` 以安装 INN 服务器。在 Fedora Core 中，以 *root* 身份登录，挂载 DVD，并键入 `cd /media/cdrom/Fedora/RPMS` 后跟 `rpm -vh inn*`。在 SUSE 中，点击 YaST 控制中心软件类别中的“软件管理”。然后使用 YaST 的搜索功能查找 *inn*，从搜索结果中选择相关的包并安装它们。在 Xandros 中，首先运行 Xandros Networks，选择 编辑>设置应用程序源，并点击 Debian Unsuppored Site 链接作为源。然后键入 `apt-get install inn` 以安装 INN 服务器。

