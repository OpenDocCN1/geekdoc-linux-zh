
## 安装邮件服务器

为了避免针对 Fedora Core 和 SUSE 等不同发行版反复提及不同的文件和目录名称，我在以下讨论中使用 Fedora Core 的文件和目录名称。这些通用讨论适用于所有 Linux 发行版中的 sendmail，但你必须将这些文件和目录名称替换为你特定发行版的对应项。

通过在位于 `/usr/share/sendmail-cf` 目录下的文件中定义自己的一组高级宏，sendmail 本质上创建了自己的宏语言。`sendmail` 宏文件使用 `.mc` 扩展名。你配置的主要 sendmail 宏文件是 `sendmail.mc`，它位于 `/etc/mail` 目录中。

与 `/etc/mail/sendmail.cf` 文件相比，`/etc/mail/sendmail.mc` 文件更短，且更易于操作。以下是随 Fedora Core 附带的 `/etc/mail/sendmail.mc` 文件中的几行代码：

```
dnl divert(-1)dnl
dnl #
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf package is
dnl # installed and then performing a
dnl #
dnl # make -C /etc/mail
dnl #
include `/usr/share/sendmail-cf/m4/cf/'dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
dnl #
dnl # default logging level is 9, you might want to set it higher to
dnl # debug the configuration
dnl #
dnl define(`confLOG_LEVEL', `9')dnl
dnl #
dnl # Uncomment and edit the following line if your outgoing mail needs to
dnl # be sent out through an external mail server:
dnl #
dnl define(`SMART_HOST', `smtp.comcast.net')
...lines deleted ...
dnl #
dnl MASQUERADE_AS('mydomain.com')dnl
dnl #
dnl # masquerade not just the headers, but the envelope as well
dnl #
dnl FEATURE(masquerade_envelope)dnl
dnl #
dnl # masquerade not just @mydomainalias.com, but *.mydomainalias.com as well
dnl #
dnl FEATURE(masquerade_entire_domain)dnl
dnl MASQUERADE_DOMAIN(localhost.localdomain)dnl
dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
dnl MASQUERADE_DOMAIN(mydomain.lan)dnl
```

MAILER(smtp)dnl
MAILER(procmail)dnl
dnl MAILER(cyrusv2)dnl

> 如果你修改了 `/etc/mail/sendmail.mc` 文件，你必须通过以下命令将 `sendmail.mc` 文件通过 `m4` 宏处理器生成 `/etc/mail/sendmail.cf` 文件。（你需要以 **root** 身份登录。）

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

注释还告诉你，你需要 `sendmail-cf` 包来处理此文件。

根据前一节对 `m4` 宏的描述，你可以看到 `sendmail.mc` 文件使用 `define` 来创建新宏。你还可以看到大量使用 `dnl` 来避免在输出中插入过多的空行。

其他大写单词（如 `OSTYPE`、`FEATURE` 和 `MAILER`）是 `sendmail` 宏。这些宏定义在位于 `/usr/share/sendmail-cf` 目录子目录中的 `.m4` 文件中，并通过以下 `include` 宏整合到 `sendmail.mc` 文件中：

```
include(`/usr/share/sendmail-cf/m4/cf.m4')dnl
```

反过来，`/usr/share/sendmail-cf/m4/cf.m4` 文件包含 `cfeead.m4` 文件，后者又包含其他 `m4` 文件，依此类推。最终结果是，当 `m4` 宏处理器处理 `sendmail.mc` 文件时，宏处理器会整合来自 `/usr/share/sendmail-cf` 各个子目录中的许多 `m4` 文件。

以下是关于 `/etc/mail/sendmail.mc` 文件的一些要点：

- **VERSIONID**(`setup for Red Hat Linux') 宏将引号内的版本信息插入到输出中。
- **OSTYPE**(`linux') 指定操作系统为 Linux。你必须尽早指定此宏以确保正确的配置。习惯上将此宏放在 **VERSIONID** 宏之后。
- **MAILER**(smtp) 描述邮件服务器。根据 `/usr/share/sendmail-cf/README` 文件中的说明，**MAILER** 声明始终放置在 `sendmail.mc` 文件的末尾，并且 **MAILER**(smtp) 始终位于 **MAILER**(procmail) 之前。邮件服务器 **smtp** 指的是 SMTP 邮件服务器。
- **FEATURE** 宏请求各种特殊功能。例如，FEATURE(`blacklist_recipients') 开启了对特定用户名、主机或地址的传入邮件进行拦截的能力。关于允许或拒绝哪些邮件的规范被放置在访问数据库中（存储于 `/etc/mail/access_db` 文件）。你还需要 FEATURE(`access_db') 宏来开启访问数据库。
- **MASQUERADE_AS**(`mydomain.com`) 使 sendmail 将外发邮件标记为来自主机 `mydomain.com`（替换为你的域名）。其想法是大型组织设置单一的 sendmail 服务器来处理许多子域的邮件，并让所有内容看起来都来自同一个域。（例如，大学内许多部门的邮件看起来都来自大学的主域名。）
- **MASQUERADE_DOMAIN**(subdomain.mydomain.com) 指示 sendmail 将来自如 `user@subdomain.mydomain.com` 这样的地址的邮件，标记为起源于由 **MASQUERADE_AS** 宏指定的域中的相同用户名。

FEATURE 和 MAILER 等 sendmail 宏在 `/usr/share/sendmail-cf/README` 文件中有描述。在修改 `sendmail.mc` 文件之前，请查阅该文件以了解有关 sendmail 宏的更多信息。

## sendmail.cf 文件语法

`sendmail.cf` 文件的语法设计旨在易于 sendmail 程序解析，因为 sendmail 在每次启动时都会读取此文件。设计该文件语法时，人类可读性并非主要考虑因素。尽管如此，稍加解释，你就能理解 `sendmail.cf` 中控制行的含义。

每个 sendmail 控制行都以一个单字母运算符开头，该运算符定义了该行其余部分的含义。以空格或制表符开头的行被视为上一行的延续。空行和以井号（#）开头的行是注释。

通常，单字母运算符和其后的参数之间没有空格，这使得这些行更难理解。例如，`sendmail.cf` 使用了类的概念——本质上是一个短语集合。你可以定义一个名为 P 的类，并使用以下控制行将该类中添加短语 REDIRECT：

```
CPREDIRECT
```

由于所有字符都挤在一起，该命令很难解读。另一方面，若要定义一个名为 Accept 的类并将其值设置为 OK 和 RELAY，请编写以下内容：

```
C(Accept)OK RELAY
```

这个命令可能更容易理解，因为分隔符（如类名 Accept）被花括号包围。

其他——较新的——控制行甚至更容易理解。例如，该行：

```
O HelpFile=/etc/mail/helpfile
```

定义了选项 HelpFile 为文件名 `/etc/mail/helpfile`。该文件包含 sendmail 在接收到 HELP 命令时使用的帮助信息。

表 4-1 总结了 *sendmail.cf* 中使用的单字母控制运算符。每个条目还显示了该运算符的示例。此表有助于你理解 *sendmail.cf* 中的一些行。

| 运算符 | 描述 |
| :--- | :--- |
| C | 定义一个类；一个变量（可视为一个集合），可以包含多个值。例如，`Cwlocalhost` 将名称 `localhost` 添加到类 `w` 中。 |
| D | 定义一个宏，即与单个值关联的名称。例如，`Dtm` 或 `DtMAILER-DAEMON` 将宏 `m` 定义为 `MAILER-DAEMON`。 |
| F | 定义从文件读取的类。例如，`Fw/etc/mail/local-host-names` 从文件 `/etc/mail/local-host-names` 读取主机名称并将其添加到类 `w` 中。 |
| H | 定义 sendmail 插入到消息中的头部行的格式。例如，`HP??Return-Path: <$g>` 定义了头部的 `Return-Path:` 字段。 |
| K | 定义一个映射（键值对数据库）。例如，`Karith arith` 将名为 `arith` 的映射定义为同名内置映射。 |
| M | 指定一个邮件服务器。以下行定义了 procmail 邮件服务器：`Mp=procmail`, `Pe=/usr/bin/procmail`, `F=DFGSPhnu9`, `S=EnvFromSMTP/HdrFromSMTP`, `R=EnvToSMTP/HdrFromSMTP`, `T=DNS/RFC822/X-Unix`, `A=procmail -Y -m $h $f $u`。 |

