
像 `FEATURE` 和 `MAILER` 这样的 `sendmail` 宏在 `/usr/share/sendmail-cf/README` 文件中有描述。在对 `sendmail.mc` 文件进行修改之前，请查阅该文件以了解更多关于 `sendmail` 宏的信息。

## sendmail.cf 文件语法

`sendmail.cf` 文件的语法设计得易于 `sendmail` 程序解析，因为 `sendmail` 在每次启动时都会读取此文件。在设计文件语法时，人类可读性并不是主要考虑因素。尽管如此，经过一点解释，你就可以理解 `sendmail.cf` 中控制行的含义。

每个 `sendmail` 控制行以一个单字母运算符开头，该运算符定义了其余部分行的含义。以空格或制表符开头的行被视为上一行的延续。空行和以井号 (`#`) 开头的行是注释。

通常，单字母运算符和其后的参数之间没有空格，这使得这些行更难理解。例如，`sendmail.cf` 使用了“类”的概念——本质上是一组短语。你可以定义一个名为 `P` 的类，并用以下控制行向该添加短语 `REDIRECT`：

```
CPREDIRECT
```

由于所有内容混在一起，命令很难辨认。另一方面，要定义一个名为 `Accept` 的类并设置其值为 `OK` 和 `RELAY`，请编写以下内容：

```
C{Accept}OK RELAY
```

这个命令可能更容易理解，因为分隔符（如类名 `Accept`）被包含在花括号中。

其他——更近期的——控制行甚至更容易理解。例如，行 `O HelpFile=/etc/mail/helpfile` 定义选项 `HelpFile` 为文件名 `/etc/mail/helpfile`。该文件包含 `sendmail` 在接收 `HELP` 命令时使用帮助信息。

表 4-1 总结了 `sendmail.cf` 中使用的单字母控制运算符。每个条目还展示了该运算符的一个示例。此表有助于你理解 `sendmail.cf` 中的一些行。

### 表 4-1 sendmail.cf 中使用的控制运算符

| 运算符 | 描述 |
| :--- | :--- |
| `C` | 定义一个类；一个变量（可以视为一个集合），可以包含多个值。例如，`Cwlocalhost` 将名称 `localhost` 添加到类 `w`。 |
| `D` | 定义一个宏，即与单个值关联的名称。例如，`DnMAILER-DAEMON` 将宏 `n` 定义为 `MAILER-DAEMON`。 |
| `F` | 定义一个已从文件读取的类。例如，`Fw/etc/mail/local-host-names` 从文件 `/etc/mail/local-host-names` 读取主机名称并将其添加到类 `w`。 |
| `H` | 定义 `sendmail` 插入消息的头部行的格式。例如，`H??From: < $g >` 定义头部的 `Return-Path` 字段。 |
| `K` | 定义一个映射（键值对数据库）。例如，`Karighth` 将名为 `arith` 的映射定义为同名的内置映射。 |
| `M` | 指定邮件代理。以下行定义了 `procmail` 邮件代理：`Mprocmail, Pa=/usr/bin/procmail, F=DIFGMSPhmu9, S=EnvFromSMTP/HdrFromSMTP, R=EnvToSMTP/HdrFromSMTP, T=DNS/RFC822/X-Unix, A=procmail -Y -m $h $f $u`。 |

## 安装邮件服务器

| 运算符 | 描述 |
| :--- | :--- |
| `O` | 将值分配给选项。例如，`O AliasFile=/etc/aliases` 将 `AliasFile` 选项定义为 `/etc/aliases`，这是 `sendmail` 别名文件的名称。 |
| `P` | 定义优先级字段的值。例如，`Pjunky=-100` 将标记为 `Precedence: junk` 头字段的邮件优先级设置为 -100。 |
| `R` | 定义一条规则。（规则有左侧和右侧；如果输入匹配左侧，则右侧替换它。此规则称为*重写*。）例如，重写规则 `R$* ; $1` 会去除末尾的分号。 |
| `S` | 标记一个规则集，您可以使用后续的 `R` 控制行开始定义它。例如，`S3=canyonify` 将下一个规则集标记为 `canonify` 或 `ruleset 3`。 |
| `T` | 将一个用户名添加到受信任类（class t）中。例如，`Troot` 将 `root` 添加到受信任用户类中。 |
| `V` | 定义配置文件的版本号。例如，`V1.0/Berkeley` 将版本号定义为 1.0。 |

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

您可以忽略以井号或数字符号 (`#`) 开头的行，因为 `sendmail` 将这些行视为注释。其他行是 `sendmail` 控制行，引用 `/etc/mail` 目录中的其他文件。

以下是这些 `sendmail` 文件应包含的内容。（注意，并非所有这些文件都必须存在于 `/etc/mail` 目录中，即使存在，某些文件也可能是空的。）

- `/etc/mail/access`：允许发送邮件的主机名称和/或 IP 地址（有助于阻止垃圾邮件——不需要的电子邮件）
- `/etc/mail/access.db`：由 `/etc/mail/access` 文件生成的访问数据库
- `/etc/mail/helpfile`：SMTP 命令的帮助信息
- `/etc/mail/local-host-names`：本主机已知的名称
- `/etc/mail/mailertable`：用于覆盖邮件路由方式的邮件表（例如，条目 `comcast.net compast:smtp.comcast.net` 告诉 `sendmail` 发给 `comcast.net` 的邮件必须发送到 `smtp.comcast.net`。）
- `/etc/mail/relay-domains`：允许中继的主机
- `/etc/mail/trusted-users`：允许使用其他用户名称发送邮件而不受警告的用户列表
- `/etc/mail/userdb.db`：包含每个用户登录名和真实名称信息的用户数据库文件
- `/etc/mail/virtusertable`：托管在此系统上的具有虚拟域地址的用户数据库

![](img/792720823146d68f19fd50c99ebfce4b_651_0.png)

`/etc/mail` 目录有时还包含其他文件——`/etc/mail/certs` 以及带有 `_pem` 扩展名的文件——旨在通过使用 SMTP 的 STARTTLS 扩展来支持 `sendmail` 中的隐私增强邮件（PEM）。STARTTLS 扩展使用 TLS（更常被称为 SSL——安全套接字层）来验证发件人并加密邮件。RFC 2487 描述了 STARTTLS。（该 RFC 可在 http://ietf.org/rfc/rfc2487.txt 在线获取。）

![](img/792720823146d68f19fd50c99ebfce4b_651_1.png)

如果您编辑 `/etc/mail/mailertable` 文件，必须在更改生效前键入以下命令：

```
makemap hash /etc/mail/mailertable < /etc/mail/mailertable
```
