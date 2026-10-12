
## 受信任用户

你可以允许你信任的用户发送发件人名称与其真实用户名不同的消息。以下行出现在用于设置受信任用户值的 Trusted users 部分：

```
Ft/etc/mail/trusted-users
Troot
Tdaemon
Tuucp
```

这些名称指定了允许使用 sendmail 的 `-f` 标志来设置除运行命令的用户之外的发件人的用户。你可能不想在此处指定任何普通用户帐户。然而，如果你使用邮件列表管理器（见下一节）来指定外出邮件的发件人，你可能希望包含行 `Tmajordomo`。否则，所有发往列表收件人的外出邮件都将包含错误 *X-Authentication-Warning: localhost: majordomo set sender to owner-bigmailinglist using -f in the message header*。如果受信任用户很多，请使用文件类 `t` 来指定包含名称列表的文件。

## 邮件头格式

使用 sendmail 的邮件头的格式在你的 `/etc/sendmail.cf` 文件中设置。以下行出现在该部分开头：

```
H?P?Return-Path: <$g>
HReceived: $S?$from $$S . $?$_(?s$S|from $.$_)    
$.$?(auth_type){authenticated?$auth_ssf} bits=${auth_ssf}$.)  
$.$y $j ($v/SZ)$?r with $r$. id ${tls_version}
(version=${tls_version} cipher=${cipher} bits=${cipher_bits}    
verify=${verify})$.$S$u
for $u; $|;  
$.$b
H?D?Resent-Date: $a
H?D?Date: $a
H?F?Resent-From: $?:x$S <$g>$|$G$.
H?F?From: $?:x$S <$g>$|$G$.
H?x?Full-Name: $x
# HPosted-Date: $a
# H!l?Received-Date: $b
H?M?Resent-Message-Id: <$t.$i@$j>
H?M?Message-Id: <$t.$i@$j>
```

这些行决定了消息头的格式。在将适当的值代入前述变量后，这段文本块会变成 `/var/spool/mqueue` 中的 qf 文件。

## 重写规则

sendmail.cf 文件的重写规则部分包含处理你的 sendmail 服务所需的一组复杂规则。规则涵盖诸如转换地址和处理本地主机名之类的内容。你不应随意更改此部分中的条目。

## 邮件传输代理定义

邮件投递代理（MDAs）在邮件传输代理定义中描述。具体来说，该部分分别定义了使用的 Mlocal 和 Mprog MDAs（procmail 和 smrsh）：

```
Mlocal, P=/usr/bin/procmail, F=lsDFMAw5:|@qSPfhn9, S=EnvFromL/HdrFromL, R=EnvToL/HdrToL, T=DNS/RFC822/X-Unix, A=procmail -Y -a $h -d $u
Mprog, P=/usr/bin/smrsh, F=lsDFMOgoe9, S=EnvFromL/HdrFromL, R=EnvToL/HdrToL, D=$z::/, T=X-Unix/X-Unix/X-Unix, A=smrsh -C $u
```

一般来说，你不需要修改邮件传输代理定义中指定的选项。

然而，前面显示的 Mlocal 和 Mprog 邮件传输代理定义值得注意。Mlocal 定义用于将消息投递到本地帐户。procmail MDA 被使用（而不是旧的 UNIX 标准 /bin/mail）来将邮件放入本地用户的邮箱中。

Mprog 邮件传输代理定义用于消息的收件人实际上是一个程序时（如下一节所述的 majordomo 的情况）。为了将消息定向到程序，sendmail 使用一个名为 smrsh（SendMail 受限 Shell）的程序。从安全角度来看，允许邮件直接管道到程序并不是一个好主意，但 smrsh 使过程更安全一些。为了使程序成功执行，程序的链接必须存在于 /etc/smrsh 目录中。此限制确保只有管理员安装的程序才能直接接收邮件，而其他随机可执行程序将被拒绝。

## 重定向邮件

有时，你可能希望将邮件重定向到本地服务器上收件人邮箱之外的某个位置。每个用户都可以使用 .forward 文件重定向他的邮件。在系统范围内，你可以在 /etc/aliases 文件中设置别名来重定向邮件。

### .forward 文件

用户重定向自己邮件的一种方式是通过使用 .forward 文件，如先前列出的 sendmail.cf 文件中所述。纯文本 .forward 文件的格式是以逗号分隔的邮件收件人列表。.forward 文件的常见用途包括：

- 将邮件管道到程序以过滤邮箱内容：

```
" | /usr/bin/procmail"
```

- 将发往一个用户（例如 jkpat）的邮件发送给另一个用户（例如本例中在不同机器上的 cht09）：

```
cht09@other.mybox.com
```

- 将邮件投递给本地用户（再次为 jkpat）*并*发送给另外两个用户（cht09 和 brannigan）：

```
\jkpat, cht09@other.mybox.com, brannigan
```

### 别名文件

一种更灵活的邮件投递处理方法（系统范围而非特定于单个用户）涉及 /etc/aliases 文件，它也是一个纯文本文件。别名文件（在 sendmail.cf 部分中已描述）包含一个名称后跟冒号，然后是用户名、另一个别名、地址列表、文件或程序，邮件将被投递到那里。冒号左侧的名称（可以是有效用户名或只是别名）然后可以用作本地机器上的电子邮件收件人。使用别名文件进行邮件别名允许对正常的邮件处理行为进行几种扩展：

- 一个帐户可以在多个不同名称下接收邮件：

```
patterson: jkpat
```

这表示任何发往 patterson@mybox.com（只是别名）的邮件都将到达 jkpat（实际用户帐户）的邮箱。

- 邮件可以在不是有效（或合理）用户名的名称下接收：

```
Charlie.Jackson.II@mybox.com: jackson
```

他可能真的不想把 Charlie.Jackson.II 作为用户名输入，但这并不意味着他不能以这种方式接收邮件。

-  intended for one user can be redirected to another account (or to several accounts)：

```
oldemployee: bradford
consultant: bradford, jackson, patterson
users: :include:/root/mail/lists/users
```

这里，任何发往 oldemployee@mybox.com 的消息都将被投递到用户 bradford 的邮箱。此外，用户 bradford、jackson 和 patterson 将收到发往 consultant 的任何邮件。第三行表示“users”别名的收件人指定在文件 /root/mail/lists/users 中。

- 邮件可以发送到本地机器上的文件：

```
acsp-bugs: /dev/null
trouble-ticket: /var/spool/trouble/incoming
```

在第一行，由于虚构的 ACSP 程序已不再在机器上使用，因此无需跟踪其错误，邮件将被有效地忽略。第二行将传入的故障单存储在 /var/spool/trouble/incoming 文件中。记住，如果你启用此功能，任何地方的任何人都可以发送足够大的消息来填满该目录所在的分区。这是一个安全风险，在实施前应仔细评估。

- 传入消息可以直接管道到可执行程序：

```
majordomo: "| /usr/lib/majordomo/wrapper majordomo"
```

> 提示：当解析地址时，sendmail 实际上并不使用 /etc/aliases 文本文件。为了更快访问，文本文件被转换为 Berkeley 数据库文件 /etc/aliases.db，该文件解析别名地址。因此，每次修改 /etc/aliases 文本文件时，都必须运行 newaliases 命令（相当于 sendmail -bi）来重建数据库文件。

## 介绍 Postfix

Postfix 是一个邮件传输代理，你可以用它代替 Sendmail 来处理 Red Hat Linux 系统上的邮件服务。Postfix 旨在更易于管理且更安全。

尽管许多配置文件和其他组件与 Sendmail 不同，但其中一些旨在替换 Sendmail 组件。为了帮助你从 Postfix 过渡到 Sendmail，Red Hat Linux 已配置这两个软件包使用 alternatives 系统。第 10 章描述了如何使用邮件传输代理切换器在两者之间切换。

当你切换到 Postfix 并启动 Postfix 守护进程，如第 10 章所述，Postfix 将接管作为 MTA，用 Postfix 组件替换 Sendmail 组件，并使用一些相同的邮件箱和日志文件位置。Postfix 基于 /etc/postfix 目录中设置的配置文件接管邮件传输。以下是 Postfix 服务使用的默认位置概述：

- **邮件配置** (/etc/postfix/main.cf) — Postfix 的主要配置文件。标识 Postfix 队列、命令和别名的位置，以及定义 Postfix 所服务的的主机和域名。如果你在该文件中未添加完全限定的域名，Postfix 将使用你的本地主机名作为其代表的邮件服务的名称。

- **邮件箱** (/var/spool/mail) — 包含传入邮件文件的目录，每个用户的邮箱由其用户名的文件表示。（这是 Sendmail 使用的相同默认 spool 目录。）

