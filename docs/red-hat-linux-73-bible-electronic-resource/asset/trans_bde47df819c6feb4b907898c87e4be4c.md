
## 转发电子邮件及阻止垃圾邮件

可以配置 `/etc/mail/virtusertable` 和 `/etc/mail/access` 文件来转发电子邮件以及丢弃来自不受欢迎用户的邮件。virtusertable 文件最常用于接收多个域名的邮件的机器。它允许你重定向传入的消息。以下是 virtusertable 文件中可能包含的一些映射示例：

```
@township.org wilhelm@orgnet.com
videotech@myotherbox.org hadji
sales@very smallcompany.com george@wehavenomoney.com
```

第一行将发送到 `township.org` 的所有邮件投递到 `wilhelm@orgnet.com`。第二行将原本发往 `videotech@myotherbox.org` 的邮件重定向到本地用户账户 `hadji`。第三行将发往 `sales@very smallcompany.com` 的邮件重定向到远程用户 `george@wehavenomoney.com`。

类似地，Access 列表数据库是从 `/etc/mail/access` 创建的。它可以根据消息头中包含的地址、主机名、域名或 IP 地址，选择性地接受、拒绝、中继或丢弃任何消息：

```
ads@freestuff.net DISCARD
junkmail.com REJECT
coupons.junkmail.com OK
spam.junkmail.com 550 Unsolicited bulk email will
be stored and handled for a fee of $500/KB
```

在上述代码块中，第一行丢弃（不返回任何错误消息）来自 `ads@freestuff.net` 的所有邮件。第二行拒绝来自 `junkmail.com` 域内的所有邮件，并向发件人返回一般的投递状态通知消息。然而，第三行通过允许来自 `coupons.junkmail.com` 的邮件来覆盖先前的设置，而第四行则针对特别烦人的 `spam.junkmail.com` 域返回指定的错误代码。

`FR-o` 行标识了一个可以配置为允许邮件中继的文件。`DR` 和 `DH` 行指的是未限定名称的电子邮件和本地电子邮件被发送到的位置：

```
# Hosts for which relaying is permitted ($=R)
FR-o /etc/mail/relay-domains
# who I send unqualified names to (null means deliver locally)
DR
# who gets local email traffic (SR has precedence for unqualified names)
DH
```

在上述代码块中，第一行声明了文件类 R，这是一个主机列表，邮件可以发送到此处的这些主机进行中继，该列表存储在此文件 `/etc/mail/relay-domains` 中。第二行和第三行可用于定义两个宏 R 和 H，其中包含可以中继邮件的机器名称。为了使该功能正常工作，请将主机名添加到 relay-domains 文件中。在 DR 后添加主机名以标识未限定名称的邮件被发送到的主机，并在 DH 后添加主机名以标识所有本地电子邮件被发送到的主机。接下来的几行涉及去引用（dequoting）：

```
# dequoting map
Xdequote dequote
```

Kdequote 行声明了类 dequote 的去引用数据库。这用于从重写规则中的地址中移除引号。接下来的几行涉及用户名和域名如何对外公开：

```
# class E: names that should be exposed as from this host, even if we
masquerade
# class L: names that should be delivered locally, even if we have
a relay
# class M: domains that should be converted to $M
# class N: domains that should not be converted to $M
#CL root
C(E)root
```

上述 class E 行（CE root）表明，即使其他指令指示主机名应伪装成其他名称，来自用户 root 的邮件也应始终具有适当的主机名和域名全称。相关的 class L 可用于列出那些应接收本地主机邮件的用户名，即使其他指令指示所有邮件都应中继到其他位置。class M 可用于指示哪些域应将其主机名伪装（如在下方的 M 宏中设置）。class N 可用于指示不应被伪装的主机名。接下来的几行也涉及伪装：

```
# who I masquerade as (null for no masquerading) (see also S=M)
DM

# my name for error messages
DnMAILER-DAEMON

CPREDIRECT

# Configuration version number
DZ0.11.4
```

上述 DM 行（宏 M）定义了用于替代机器真实主机名的名称。宏 n 定义了用作错误消息发件人的用户名（或别名）。CPREDIRECT 行将文本 REDIRECT 添加到类 P 中，该类在几个代码块之前已定义。这与重定向功能（在 m4 配置文件中启用）配合使用，允许为不再活动的账户创建别名。例如，如果 `/etc/aliases` 文件包含以下行：

```
jeff: jeff@newplace.com.REDIRECT
```

任何发送到本地机器 jeff 的邮件都会导致向原始发件人返回信息消息，指示地址已更改。原始邮件消息不会转发到上述 jeff 示例中列出的地址。DZ8.11.4 行设置宏 Z，其中包含 sendmail 守护程序的完整版本信息。

## sendmail 选项

sendmail.cf 文件包含了一个长选项列表，你可以在 Red Hat Linux 系统中为 sendmail 设置这些选项。选项定义在 Options 块之后开始。以下是 Options 部分开头的示例：

```
##################
#   Options   #
##################

# strip message body to 7 bits on input?
O SevenBitInput=False

# 8-bit data handling
# O EightBitMode=pass8
```

SevenBitInput 选项指示 sendmail 不应从所有邮件消息的每个字节中清除最高位。EightBitMode 规定 sendmail 如何处理未明确标记为 8 位的消息数据。pass8 选项允许任何 8 位数据未经修改即被投递；mimefy 将任何未指定的数据转换为 MIME 编码类型；strict 拒绝任何未标记的 8 位数据。请注意，此选项对指定为 8 位的数据没有影响。接下来的几行涉及别名文件：

```
# wait for alias file rebuild (default units: minutes)
O AliasWait=10

# location of alias file
O AliasFile=/etc/aliases
```

在重建别名数据库之前，sendmail 会执行几项检查，以确保没有其他进程正在尝试执行相同的操作。AliasWait 选项指定 sendmail 在等待和执行检查之间交替切换的分钟数。AliasFile 选项指定包含邮件别名的纯文本文件的位置。接下来的几行涉及 sendmail 如何分配磁盘空间：

```
# minimum number of free blocks on filesystem
O MinFreeBlocks=100

# maximum message size
```

