
## /etc/mail/freebsd.mc

`/etc/mail/freebsd.mc` 文件是 Sendmail 的“主配置”文件。它包含一组特性与选项，用于覆盖标准配置文件中的默认设置，其方式类似于 `/etc/rc.conf` 覆盖 `/etc/defaults/rc.conf`。不过，在使用 `freebsd.mc` 时，设置的格式要怪异得多。命令使用 m4 宏语言编写（该语言在 Sendmail 配置之外几乎无人使用）。随后，`.mc` 文件会与 Sendmail 源代码中位于 `/usr/share/sendmail` 或 `/usr/src/contrib/sendmail` 的默认 `.m4` 文件一起编译，生成 `.cf` 输出文件。之后，您可以将该文件安装为新的 sendmail.cf 文件。

听起来是否令人困惑且不合常理？确实如此。然而，在 FreeBSD 的近期版本中，这一流程已有了显著改进。过去，若要重新生成 sendmail.cf 文件，您必须亲自进入源码目录，找出最符合系统环境的 `.mc` 文件，尽力依据在线文档进行修改，然后找出那个用于生成输出文件的晦涩 m4 编译命令——之后还得手动安装该文件。如今的情况已大大改善，尽管仍然算不上用户友好。

m4 语言的每一行在某个位置都包含字符串 `dnl`；它代表“删除至换行符”（delete through newline），并标记可读行的结束（每行都必须包含一个）。若要注释掉某一行，请将 `dnl` 放在行首。否则，将其放在行尾。

`/etc/mail` 中有一个 Makefile，允许您仅通过输入 `make cf` 即可从 `freebsd.mc` 文件创建新的 `.cf` 文件。然后，使用 `make install` 将此输出文件（`freebsd.cf`）安装到 sendmail.cf 中：

```bash
# make cf
/usr/bin/m4 -D_CF_DIR_=/usr/share/sendmail/cf /usr/share/sendmail/cf/m4/cf.m4
freebsd.mc > freebsd.cf
# make install
install -c -m 444 freebsd.cf /etc/mail/sendmail.cf
```

`/etc/mail/Makefile` 还有多种其他用途，您稍后将会看到。

> **注意**
> *Makefile*（通常命名为 Makefile）是一种特殊文件，位于任何源代码树的顶层；它包含“构建目标”，允许您以预定义的方式编译代码。我们在第 14 章“安装附加软件”中讨论了端口（ports）所使用的 Makefile。在那一章的示例中，您可以使用 make 命令编译端口中的程序，但目标 `install` 会告知 make 命令您希望运行该端口 Makefile 中规定的安装程序。
>
> 在 `/etc/mail` 中，FreeBSD 提供的 Makefile 允许您编译组成 Sendmail 配置的各种数据库，甚至控制 Sendmail 本身。它本身并不是一个配置文件。相反，它是系统的一部分。因此，除非您知道自己在做什么，否则**不要**修改它。

## /etc/mail/aliases

`/var/mail` 中为系统中的每个用户都有一个邮箱；然而，在您机器上拥有电子邮件地址并不意味着该用户必须有账户。您可以随时设置别名，将传入的电子邮件地址映射到其他任何地址，无论是您机器上的另一个账户、互联网上的其他地址，甚至可以是管道到文件或程序。默认的 `/etc/mail/aliases` 包含了所有这些类型的示例。别名行包含别名名称、冒号、空格或制表符，以及目标地址或管道：

```text
tiger: bob@stripes.com
fsmith: frank
pager: "|/usr/local/bin/pageeme"
dump: ">>/home/frank/dump2me"
mylist:include:/home/frank/list.txt
```

最后一个示例是一个“include”别名，它从指定位置的纯文本文件中读取地址列表。这是一种管理邮件列表的简便方法。只需修改被包含的文件，该别名就会始终保持最新状态。

传统上，也是出于“网络礼仪”的考虑，系统拥有多个用于不同目的的管理员别名，它们都是 root 的别名。其中一些“伪账户”包括 abuse（用于报告垃圾邮件或源自您服务器的恶意活动的地址）、postmaster（运行邮件服务器的人）和 webmaster（负责 Web 服务器的人）。其中一些已在默认配置中别名为 root，其他一些您可能需要取消注释以启用它们。

在对 `/etc/mail/aliases` 进行任何更改后，必须重建 `aliases.db` 文件，该文件是别名文件的哈希表版本，提供快速查找（正如我们在第 9 章“用户、组和权限”中讨论的 `/etc/master.passwd`）。您可以使用传统的 `newaliases` 命令来执行此操作，或者为了与其他维护任务保持一致，使用 `make aliases`：

```bash
# make aliases
/usr/sbin/sendmail -bi
/etc/mail/aliases: 25 aliases, longest 10 bytes, 254 bytes total
chmod 0640 /etc/mail/aliases.db
```

如果别名数据库是最新的，此处显示的命令不会返回任何输出。

> **注意**
> 使用全局别名并不是将邮件从一个本地地址重定向到另一个本地地址或外部地址的唯一方法。例如，如果用户希望将其所有传入邮件自动转发到某个外部地址，您可以使用 `/etc/mail/aliases` 来实现，但这需要 root 权限。如果该用户在系统上拥有完整账户，则有更好的方法。

用户只需在其主目录中创建一个 `.forward` 文件，其中包含转发的电子邮件地址，即可将邮件转发到另一个地址。可以使用任何文本编辑器完成此操作，甚至可以使用 `echo` 简单实现：

```bash
# echo "frank@somewhereelse.com" > .forward
```

删除此文件将停止邮件转发。

## /etc/mail/access

访问数据库提供了一种方法，可对单个主机、子网或整个地址组应用特定规则——这是一个优秀的反垃圾邮件措施。适用的规则包括 **OK**、**REJECT**、**RELAY**、**DISCARD** 和 **550 `<message>`**。默认 `/etc/mail/access` 文件的内容展示了地址/主机名字段可以如何格式化：

```text
cyberspammer.com          550 We don't accept mail from spammers
FREE.STEALTH.MAILER®     550 We don't accept mail from spammers
another.source.of.spam   REJECT
okay.cyberspammer.com    OK
128.32                   RELAY
```

左侧的地址可以是完整的主机名或 IP 地址，也可以是部分地址；`cyberspammer.com` 将匹配 `cyberspammer.com` 域中的任何主机名，而 `128.32` 覆盖整个 `128.32.xxx.xxx` B 类网络。右侧包含规则，可以是以下任何一种：

- **OK** 接受来自指定主机的消息，无论该主机是否可能无法通过系统中的其他检查（例如我们稍后将讨论的反中继措施）。
- **REJECT** 拒绝由指定主机发起的连接。
- **DISCARD** 在接受消息后静默丢弃它们，使发送者认为消息已成功投递。
- **RELAY** 为指定主机启用中继，覆盖其他检查（与 **OK** 类似）。
- **550 `<message>`** 指定显示给匹配主机规范的发送者的“拒绝”消息。此消息将在 SMTP 会话期间显示，并包含在发回给发送者的错误电子邮件消息中。

在对 `/etc/mail/access` 进行更改后，必须重新生成 `access.db` 文件。您可以使用 `make maps` 目标来完成此操作，它会重新生成自上次运行 `make maps` 以来已更改的任何功能映射文件。随后使用 `make restart` 重启 Sendmail 主进程以使用新的 `access.db` 文件：

```bash
# make maps
# make restart
Restarting: sendmail sendmail-clientmqueue.
```

## /etc/mail/local-host-names

以前称为 `sendmail.cw`，此文件指定您的服务器声称拥有的所有主机名。如果您托管多个域并为所有这些域提供邮件服务（虚拟主机），这些信息尤为重要。在这种情况下，如果您未将每个相关域名添加到 `local-host-names` 文件，发往您所托管域的传入消息将弹回给发送者，并附带令人恐惧的消息：“MX list for <domain> loops back to myself; local configuration error.”（<domain> 的 MX 列表回环到我自己；本地配置错误）。

```bash
# cat /etc/local-host-names
somewhere.com
www.somewhere.com
boobsmachine.com
```

`local-host-names` 文件格式简单：主机名列表，每行一个。默认安装中不存在该文件，但如果您通过 DNS 为机器添加更多域名或主机名别名，则需要创建它。将名称添加到列表后，运行 `make restart` 以重启服务器：

```bash
# make restart
Restarting: sendmail sendmail-clientmqueue.
```

## /etc/mail/virtusertable

同样关于虚拟主机的话题，`/etc/mail/virtusertable` 提供了一种方法，将您托管的某个域中的地址映射到本地账户、其他地址或错误消息。这在某种程度上是访问数据库和别名文件的混合体。

假设您正在托管一个名为 `mycave.org` 的次要域。您希望 `webmaster@mycave.org` 去往本地用户 `bill`，`info@mycave.org` 去往远程地址 `anne@elsewhere.com`，并拒绝所有其他地址（`@mycave.org`）。这可以通过以下使用制表符分隔的规则实现：

```text
webmaster@mycave.org	bill
info@mycave.org		anne@elsewhere.com
@mycave.org		error:nouser User unknown
```

请注意，这些规则的指定顺序无关紧要；当构建 `virtusertable.db` 哈希表时，每个规则都有自己独立的查找值，且 `virtusertable` 文件中的顺序无关紧要。与访问数据库一样，您需要重建 `virtusertable.db` 并重启服务器。使用 `make maps` 完成此操作最为简便，但请记住，这会重建 `/etc/mail` 中所有已修改的映射数据库：

```bash
# make maps
/usr/sbin/makemap hash virtusertable.db < virtusertable
chmod 0640 virtusertable.db
```

