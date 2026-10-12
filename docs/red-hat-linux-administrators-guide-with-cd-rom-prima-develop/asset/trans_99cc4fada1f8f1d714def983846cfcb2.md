

此功能允许使用受限 shell 来运行本地邮件代理（例如 procmail）。该选项使 sendmail 更加安全，因为本地邮件代理将仅对其他程序拥有受限的访问权限。

FEATURE('virtusertable',`hash -o /etc/mail/virtusertable`)

此功能允许服务器托管虚拟域。表达式的第二部分说明了数据库格式以及包含虚拟域的文件路径。

虚拟域是指与你的服务器名称不关联但托管在你机器上的域。通过此设置，你还可以设置邮件别名，并允许发往这些虚拟域的电子邮件路由到有效的电子邮件地址。

FEATURE(redirect)

此命令拒绝任何要求重定向的邮件。除非你希望支持未经请求的电子邮件——垃圾邮件——以及那些滥用无辜邮件服务器的人，否则请使用此选项。你应该保留此选项。

FEATURE(always_add_domain)

始终为你的未限定地址添加域名。如果你想伪装 FROM 地址在发送时的样子，你需要设置此选项。此伪装选项不同于 chains 伪装选项；相反，它会更改 outgoing 电子邮件以反映你系统的域名。

FEATURE(use_cw_file)

此行告诉 sendmail 读取 sendmail.cw 文件以获取主机的备用名称。此文件包含可能托管在你系统上的其他虚拟域的名称。

define(`PROCMAIL_MAILER_PATH', `/usr/bin/procmail`)

如果你希望使用 procmail 对你的本地邮件进行分类、过滤和传递，请在此处设置其路径。procmail 程序是一个有用的实用工具，用于将电子邮件路由到不同的账户和用户。

FEATURE(local_procmail)

此功能允许 procmail 传递你的本地邮件。你可以不让你的默认邮件程序处理传入电子邮件，而是将 procmail 定义为默认邮件处理器。与大多数 Linux 系统中安装的常规邮件代理相比，procmail 具有几个优势，即更容易定义规则将特定电子邮件路由到不同的用户，并处理不需要的电子邮件。

MAILER (procmail)

使用 procmail 的接口。

MAILER (smtp)

使用标准的 SMTP 邮件代理（sendmail）处理 outgoing 邮件。它驻留在 25 端口，并定义在 `/etc/services` 文件中。

FEATURE('access_db')

使用位于 `/etc/mail/access` 的 access 数据库，允许或拒绝来自特定域的邮件。此数据库也被称为垃圾邮件压制工具，因为你可以丢弃来自特定主机的电子邮件，或允许其他主机通过你的服务器中继。每次编辑 access 文件时，你都必须*重新哈希*或重建数据库。为此，请输入命令 `makemap -r hash access.db < access`。在 Red Hat Linux 下，此重新哈希选项已经为 sendmail RPM 包启用，默认带有 makefile。要重新哈希默认 access 文件，只需在 `/etc/mail` 目录中输入 `make` 即可。

FEATURE('blacklist_recipients')

此命令启用使用 access.db 屏蔽特定用户/主机名的功能。

DOMAIN('generic')

如果你希望使用 sendmail.cw 文件，请在 *.mc 文件中保留此行。

FEATURE (masquerade_envelope)

伪装你的邮件的头部和信封。信封包含外部邮件传递子系统将向其传递错误报告和警告的电子邮件地址。

FEATURE(genericstable,'hash -o /etc/mail/genericstable')

此行指定 sendmail 使用带有伪装信息的哈希表。未哈希的文件看起来像这样：

```
me kerry@myisp.net
root kerry@myisp.net
nobody kerry@myisp.net
```

此文件告诉 sendmail 重写你的邮件的 FROM 地址，这样你就可以通过你的 ISP 的邮件服务器中继所有邮件。第一列包含本地地址，第二列是 sendmail 应替代使用的地址。为了让 sendmail 读取此文件，你必须使用此命令对其进行哈希处理：`makemap -r hash genericstable.db < genericstable`。再次说明，如果此文件在你的默认 RPM sendmail 安装中已定义，你可以使用位于 /etc/mail 中的 make 命令重新哈希该文件。

GENERICS_DOMAIN_FILE('/etc/mail/genericsdomain')

你需要将你的本地域名添加到这个文件中，以便 sendmail 知道哪些邮件是本地的，哪些需要进行伪装。要设置你的本地域，请使用命令 hostname。将此名称放置在 /etc/mail/genericsdomain 文件中。

define('SMART_HOST', 'mail.myisp.net')

sendmail 程序使用此“智能”主机来中继你所有 outgoing 邮件。如果你的机器使用外部邮件服务器，请在此处插入你的 ISP 的邮件服务器名称。

FEATURE('accept_unresolvable_domains')

此行告诉 sendmail 接受所有由邮件头部定义的域，即使它们无法解析，这是因为你的服务器不在线或未连接到互联网，或者是由于名称服务器没有响应。如果你的计算机每周七天、每天 24 小时运行，请勿使用此行。允许任何没有有效域的电子邮件形式，都是对垃圾邮件发送者进行主机中继的邀请。

FEATURE('relay_based_on_MX')

此命令告诉 sendmail 仅从你的 MX 或邮件域中的计算机进行中继。如果你不明白这行的含义，请不要使用它。

define('conEDIAL_DELAY', '50s')

sendmail 程序将 outgoing 邮件的传递延迟一定时间。如果你拥有拨号连接，并希望 sendmail 每当有 outgoing 邮件时都连接到互联网，请使用此行。（你还需要安装 diald 以定期自动拨号连接你的 ISP。）

如果你希望每次上网时都发送 outgoing 邮件，请使用以下行代替拨号延迟：

```
define(`confCON_EXPENSIVE',`True')
define(`SMTP_MAILER_FLAGS',`e')
FEATURE(`noceanonly')
```

第一行和第二行告诉 sendmail 将“昂贵”邮件代理的邮件放入队列，而不是立即发送，然后将 outgoing 邮件代理标记为“昂贵”。最后一行告诉 sendmail 不要将邮件地址转换或规范化为 FQDN（完全限定域名），因为这包括 DNS 查找，而这只能在线完成。

如果你希望仅在上网时发送邮件，你还必须告诉 sendmail 不要在指定分钟数后处理队列。每次启动或重启时，你可能需要使用命令 **sendmail -bd** 而不是 **sendmail -bd -q30m** 来启动 sendmail。

因为 sendmail 在启动时由 init 启动，你还必须修改 */etc/sysconfig/sendmail* 文件或在 Red Hat 下重新定义 */etc/rc.d/init.d/sendmail* 文件，以避免每隔几分钟检查一次队列。将前者文件更改为以下内容：

```
DAEMON=yes
QUEUE=
```

最后，将命令 */usr/sbin/sendmail -q* 添加到 */etc/ppp/ip-up.local* 中（在非 Red Hat 机器上也可能是 */etc/ppp/ip-up*），以便在你上网时发送所有邮件。

## 复制新的配置文件

前一段中所示的通用 *.mc* 文件的细节可以应用于源代码，或根据你特定的服务器进行定制。一旦你在 generic-linux.mc 或基于现有 generic-linux.mc 文件创建的新文件中添加了必要的行，你就可以运行 *m4* 预处理器程序来解析你的宏并创建编译后的 sendmail.cf 文件。

如果你使用的是随 Red Hat 发行版提供的默认 *.mc* 文件，并且这正是你刚才编辑的文件，请使用以下命令：

```
m4 /etc/sendmail.mc > /etc/sendmail.cf
```

但是，如果你希望使用推荐的源代码，请使用以下命令。首先确保你在正确的目录中。以下示例从当前位置调用 *.mc* 文件，然后将其解析到发出命令的同一目录：

```
m4 /usr/local/gnu/sendmail-8.11.0/cf/cf/kerry-linux.mc > kerry.cf
```

这给我生成了我自己的 kerry.cf 文件，它将重命名为 sendmail.cf。请务必将发行版版本的 /etc/sendmail.cf 备份，给它加上 .dist 扩展名或附加你希望的任何内容。通过先将你的 sendmail.cf 命名为其他名称，你可以随意编辑配置文件，而不会损害新文件。

在执行下一步之前，备份你当前的 /etc/sendmail.cf 文件：

```
cp /usr/local/gnu/sendmail-8.11.0/cf/cf/kerry.cf /etc/sendmail.cf
```

一旦这个新文件覆盖了旧的 sendmail.cf 文件，你就可以手动编辑它了。sendmail.cf 文件中需要为本地定制而处理的唯一部分是位于重写规则之前的那些部分。文件的第一个部分允许你更改最大电子邮件大小及类似变量。然而，重写规则需要比本章所能提供的对 sendmail 语法有更深入的了解。

## 安装二进制文件

既然新的 sendmail.cf 文件已就位，你就可以复制你在运行 .Build 序列时创建的 sendmail 二进制文件。在目录 /usr/local/gnu/sendmail-8.11.0/obj.Linux.2.2.16.i586/sendmail/sendmail 中定位二进制文件。它应该位于由 sendmail 创建的对象目录中，并由 Linux 标题、内核号和处理器类型标识。

首先，备份发行版的 sendmail 二进制文件，以防新文件不起作用。备份文件始终是一个重要的预防措施，以防出现问题。

将 sendmail 二进制文件复制到 /usr/lib 目录。通常，文件 /usr/lib/sendmail 是到 /usr/sbin/sendmail 的符号链接。在复制时请注意这一点。

