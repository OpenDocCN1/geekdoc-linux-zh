

为了避免在不同发行版（如 Fedora Core 和 SUSE）中反复提及不同的文件和目录名称，以下讨论中我将使用 Fedora Core 的文件和目录名称。一般性讨论适用于所有 Linux 发行版中的 **sendmail**，但你必须将文件和目录名称替换为你特定发行版中对应的名称。

通过在位于 **/usr/share/sendmail-cf** 目录中的文件里定义自己的一组高级宏，**sendmail** 实际上创建了自己的宏语言。**sendmail** 的宏文件使用 **_mc** 扩展名。你需要配置的主要 **sendmail** 宏文件是位于 **/etc/mail** 目录中的 **sendmail.mc**。

与 **/etc/mail/sendmail.cf** 文件相比，**/etc/mail/sendmail.mc** 文件更短，更容易操作。以下是随 Fedora Core 提供的 **/etc/mail/sendmail.mc** 文件中的部分内容：

```
dnl(1)dnl
dnl # This is the sendmail macro config file for m4. If you make changes to
dnl # /etc/mail/sendmail.mc, you will need to regenerate the
dnl # /etc/mail/sendmail.cf file by confirming that the sendmail-cf package is
dnl # installed and then performing a
dnl #
dnl # make -C /etc/mail
dnl #
include(`/usr/share/sendmail-cf/m4/cf.m4'dnl
VERSIONID(`setup for Red Hat Linux')dnl
OSTYPE(`linux')dnl
dnl #
dnl # default logging level is 9, you might want to set it higher to
dnl # debug the configuration
dnl define(`confLOG_LEVEL', `9')dnl
dnl #
dnl # Uncomment and edit the following line if your outgoing mail needs to
dnl # be sent out through an external mail server:
dnl #
dnl define(`SMART_HOST', smtp.comcast.net')
....lines deleted ...
dnl #
dnl MASQUERADE_AS('mydomain.com')dnl
dnl #
dnl # masquerade not just the headers, but the envelope as well
dnl FEATURE(masquerade_envelope)dnl
dnl #
dnl # masquerade not just @mydomainalias.com, but @*.mydomainalias.com as well
dnl #
dnl FEATURE(masquerade_entire_domain)dnl
dnl MASQUERADE_DOMAIN(localhost.localdomain)dnl
dnl MASQUERADE_DOMAIN(mydomainalias.com)dnl
dnl MASQUERADE_DOMAIN(mydomain.lan)dnl
MAILER(smtp)dnl
MAILER(procmail)dnl
dnl MAILER(cyrusv2)dnl
```

如果你修改了 /etc/mail/sendmail.mc 文件，你必须通过运行 m4 宏处理器处理 sendmail.mc 文件来生成 /etc/mail/sendmail.cf 文件，命令如下。（你必须以 **root** 身份登录。）

```
m4 /etc/mail/sendmail.mc > /etc/mail/sendmail.cf
```

注释还告诉你，你需要 **sendmail-cf** 包来处理此文件。

从上一部分对 m4 宏的描述中，你可以看到 **sendmail.mc** 文件使用 **define** 来创建新的宏。你还可以看到大量使用 dnl 来避免在输出中插入过多的空行。

其他大写的单词（如 **OSTYPE**、**FEATURE** 和 **MAILER**）是 sendmail 宏。这些宏定义在 /usr/share/sendmail-cf 目录子目录中的 .m4 文件中，并通过以下 *include* 宏合并到 sendmail.mc 文件中：

```
include(`/usr/share/sendmail-cf/m4/cf.m4') dnl
```

反过来，/usr/share/sendmail-cf/m4/cf.m4 文件又包含 cfdhead.m4 文件，该文件又包含其他 m4 文件，等等。净效果是，当 m4 宏处理器处理 sendmail.mc 文件时，宏处理器会从 /usr/share/sendmail-cf 的各个子目录中合并许多 m4 文件。

关于 /etc/mail/sendmail.mc 文件，以下是需要注意的一些要点：

- **VERSIONID**(`setup for Red Hat Linux') 宏将引号内的版本信息插入到输出中。
- **OSTYPE**(`linux') 指定操作系统为 Linux。你必须尽早指定此宏以确保正确的配置。通常将置此宏于 **VERSIONID** 宏之后是惯例。
- **MAILER**(smtp) 描述邮件代理。根据 /usr/share/sendmail-cf/README 文件中的说明，**MAILER** 声明总是放置在 sendmail.mc 文件的末尾，并且 **MAILER**(smtp) 总是先于 **MAILER**(procmail)。邮件代理 **smtp** 指的是 SMTP 邮件代理。
- **FEATURE** 宏请求各种特殊功能。例如，FEATURE(`blacklist_recipients') 开启阻止特定用户名、主机或地址的传入邮件的功能。指定允许或拒绝哪些邮件的规格放在访问数据库中（存储在 /etc/mail/access.db 文件中）。你还需要 FEATURE(`access_db') 宏来开启访问数据库。
- **MASQUERADE_AS**(`mydomain.com') 使 sendmail 将 outgoing 邮件标记为来自主机 mydomain.com（替换为你的域名）。其理念是一个大型组织设置一个单一的 sendmail 服务器，处理许多子域的邮件，并使所有邮件看起来都来自一个单一域名。（例如，大学中许多部门的邮件看起来都来自大学的主域名。）
- **MASQUERADE_DOMAIN**(subdomain.mydomain.com) 指示 sendmail 将来自 user@subdomain.mydomain.com 等地址的邮件视为起源于由 MASQUERADE_AS 宏指定的域名上的相同用户名。

像 FEATURE 和 MAILER 这样的 sendmail 宏在 /usr/share/sendmail-cf/README 文件中有描述。在对 sendmail.mc 文件进行修改之前，请查阅该文件以了解更多关于 sendmail 宏的信息。

## sendmail.cf 文件语法

sendmail.cf 文件的语法设计得易于 sendmail 程序解析，因为 sendmail 在每次启动时都会读取此文件。在设计文件语法时，人类可读性并不是主要考虑因素。尽管如此，经过一点解释，你就可以理解 sendmail.cf 中控制行的含义。

每个 sendmail 控制行以一个单字母运算符开头，该运算符定义了其余部分行的含义。以空格或制表符开头的行被视为上一行的延续。空行和以井号 (#) 开头的行是注释。

通常，单字母运算符和其后的参数之间没有空格，这使得这些行更难理解。例如，sendmail.cf 使用了“类”的概念——本质上是一组短语。你可以定义一个名为 P 的类，并用以下控制行向该添加短语 REDIRECT：

```
CPREDIRECT
```

由于所有内容混在一起，命令很难辨认。另一方面，要定义一个名为 `Accept` 的类并设置其值为 `OK` 和 `RELAY`，请编写以下内容：

```
C{Accept}OK RELAY
```

这个命令可能更容易理解，因为分隔符（如类名 `Accept`）被包含在花括号中。

其他——更近期的——控制行甚至更容易理解。例如，行 `O HelpFile=/etc/mail/helpfile` 定义选项 `HelpFile` 为文件名 `/etc/mail/helpfile`。该文件包含 sendmail 在接收 `HELP` 命令时使用帮助信息。

表 4-1 总结了 sendmail.cf 中使用的单字母控制运算符。每个条目还展示了该运算符的一个示例。此表有助于你理解 sendmail.cf 中的一些行。

### 表 4-1 sendmail.cf 中使用的控制运算符

| 运算符 | 描述 |
| :--- | :--- |
| C | 定义一个类；一个变量（可以视为一个集合），可以包含多个值。例如，`Cwlocalhost` 将名称 `localhost` 添加到类 `w`。 |
| D | 定义一个宏，即与单个值关联的名称。例如，`DnMAILER-DAEMON` 将宏 `n` 定义为 `MAILER-DAEMON`。 |
| F | 定义一个已从文件读取的类。例如，`Fw/etc/mail/local-host-names` 从文件 `/etc/mail/local-host-names` 读取主机名称并将其添加到类 `w`。 |
| H | 定义 sendmail 插入消息的头部行的格式。例如，`H??From: < $g >` 定义头部的 `Return-Path` 字段。 |
| K | 定义一个映射（键值对数据库）。例如，`Karighth` 将名为 `arith` 的映射定义为同名的内置映射。 |
| M | 指定邮件代理。以下行定义了 `procmail` 邮件代理：`Mprocmail, Pa=/usr/bin/procmail, F=DIFGMSPhmu9, S=EnvFromSMTP/HdrFromSMTP, R=EnvToSMTP/HdrFromSMTP, T=DNS/RFC822/X-Unix, A=procmail -Y -m $h $f $u`。 |

