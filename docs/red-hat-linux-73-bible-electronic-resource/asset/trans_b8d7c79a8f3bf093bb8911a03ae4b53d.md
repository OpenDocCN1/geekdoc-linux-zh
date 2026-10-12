
## 初始化 Tripwire 数据库

Tripwire 可以运行的四种模式中的第一种是数据库初始化模式。此模式会为系统中的文件创建一个新的校验和数据库。以 root 身份登录时，输入以下命令：

```
# tripwire --init
```

系统将提示你输入站点密码短语，之后将构建校验和数据库。数据库将写入文件 /var/lib/tripwire/host.twd，其中 host 将被替换为你的计算机主机名。

Tripwire 通过检查其策略文件来选择要校验的文件和目录。Tripwire 自带一个适用于大多数新安装的 Red Hat Linux 系统的策略文件，但可能会尝试查找你系统中不存在的几个文件。如果发生这种情况，你将看到类似以下内容的错误消息：

```
### Warning: File system error.
### Filename: /usr/bin/dos
### No such file or directory
### Continuing...
```

这些错误消息不会影响校验和数据库的创建，但可能使识别真正的错误消息变得困难。要消除它们，你必须修改策略文件。

## 重建策略文件

Tripwire 策略文件用于描述系统和数据文件的预期行为。Tripwire 使用策略文件信息创建文件系统的快照。稍后，此快照（称为基线）将与运行中的系统进行比较，以检查你的系统是否被试图入侵的人修改过。

要修改 Tripwire 的策略文件，你必须首先编辑文本配置文件 /etc/tripwire/twpol.txt。在编辑器中打开该文件，注释掉提及那些导致错误消息的缺失文件的行。例如，如果你想消除缺失文件 /usr/bin/dos 的错误消息，请在策略文本文件中查找以下行：

```
/usr/bin/dos      -> $(SEC_SUID)  ;
```

在行的开头放置 # 字符以注释掉该行。它现在应如下所示：

```
#  /usr/bin/dos      -> $(SEC_SUID)  ;
```

现在你必须处理策略文本文件并创建 Tripwire 在创建或检查校验和数据库时实际使用的加密和数字签名策略文件。输入 tripwire 命令，并将 --update-policy 参数和策略文本文件的名称传递给它：

```
# tripwire --update-policy /etc/tripwire/twpol.txt
```

系统将提示你输入站点和本地密码短语。之后，将构建新的策略。然后你可以使用 `tripwire --init` 命令重建校验和数据库。这次“没有此文件”错误消息不应再出现。

## 检查文件完整性

在构建校验和数据库后，你应该定期运行 Tripwire 的完整性检查模式。完整性检查模式将重新计算每个文件的校验和，并将其与数据库中存储的校验和进行检查，为任何已更改的文件打印警告消息。使用 `--check` 参数来执行此操作：

```
# tripwire --check
```

通常情况下，不会报告错误消息。但是，如果某个文件已被修改，你可能会收到一条消息，表明黑客已进入你的系统并修改了一些操作系统文件，例如 `telnetd` 程序。`telnetd` 程序可能被替换为包含通过后门绕过你安全设置的版本。你至关重要的是，要用 Linux 安装 CD 或有效 Linux 发行版 FTP 站点上的原始版本替换任何已更改的程序。此外，在执行彻底的安全日志审计并关闭任何发现的安全漏洞时，请将你的系统从互联网中断开。

Tripwire 可能会报告并非由入侵引起的文件更改。这通常发生在你升级操作系统或安装软件补丁时。你最好的策略是在安装任何升级或补丁之前运行一次 Tripwire 检查。假设没有错误，继续执行升级或补丁，然后使用 `tripwire` 命令更新校验和数据库。没有必要完全重建数据库；你可以运行 Tripwire 的更新模式，仅重建那些已更改文件的校验和。

## 更新数据库

要在更新模式下运行 Tripwire，请使用 `--update` 参数调用它。

```
# tripwire --update
```

这将重新计算自上次更新以来任何已更改文件的校验和，并将这些更改保存到数据库。这与使用 `tripwire --init` 命令完全重建校验和数据库相比，耗时少得多。

> **提示：** 你可以通过从只读媒体（如 CD-ROM）运行 Tripwire，或至少从仅在运行 Tripwire 时才挂载的媒体运行，来大大提高 Tripwire 的安全性。此外，将校验和数据库存储在仅在需要时挂载的可移动媒体上是提高 Tripwire 安全性的另一种方式。

我将我的 Tripwire 可执行文件和数据库存储在 CD-R 可写 CD-ROM 驱动器上。当然，在运行 `tripwire` 命令时，你需要指定不同的文件路径。可以使用 `-d` 参数来更改校验和数据库的位置。在我的 Linux 系统 ratbert 上，我通过加载我的 Tripwire CD 并输入以下内容来运行 `tripwire` 命令：

```
# /mnt/cdrom/tss/bin/tripwire --check -d /mnt/cdrom/tss/db/ratbert.db
```

如果我升级操作系统，我必须生成一个新数据库并将其烧录到一张新的 CD 上，但这是确保我的 Tripwire 数据库未被破坏所需支付的一点小小代价。

## 防御拒绝服务攻击

入侵并非你的系统可能面临的唯一安全风险。你的计算机可能遭受拒绝服务攻击。这是一种试图让你的计算机崩溃或至少将其性能降低到不可用水平的攻击。有各种各样的拒绝服务利用方法。大多数都集中在过载某些系统资源，例如可用的磁盘空间或互联网连接。最常见的攻击及其防御方法在以下章节中讨论。

## 邮件轰炸

*邮件轰炸* 是向特定用户或系统发送如此多的电子邮件以至于计算机硬盘被填满的做法。有几种方法可以保护你自己免受邮件轰炸。你可以安装电子邮件过滤工具（如 Procmail）或配置你的 sendmail 守护进程。

> **交叉引用：** 参见第 19 章，以获取有关 sendmail 的更完整描述。

### 使用 Procmail 阻止邮件

Procmail 电子邮件过滤工具默认随 Red Hat Linux 安装，并与 sendmail 电子邮件守护进程紧密集成，因此可用于选择性阻止或过滤特定类型的电子邮件。你可以在 Procmail 网站 www.procmail.org 上了解更多关于 Procmail 的信息。

要为你的用户帐户启用 Procmail，请在你的主目录中创建一个 `.procmailrc` 文件。该文件的模式应为 0600（你可读，但其他人不可读）。输入以下内容，将 *evilmailer* 替换为正在对你进行邮件轰炸的实际电子邮件地址。

```
# Delete mail from evilmailer
:0
* ^From.*evilmailer
/dev/null
```

Procmail 的在线手册页更详细地解释了其功能。在命令提示符处输入 `man procmail` 以查看它。`procmailrc` 和 `procmallex` 手册页将告诉你更多关于 `.procmailrc` 文件的信息，并提供如何选择性处理不同类型邮件的众多示例。你还应该查看位于 www.wasasa.fi/~ts/info/proctips.html 的网页“Timo's procmail tips and recipes”。

### 使用 sendmail 阻止邮件

当只有一个用户受到邮件轰炸时，Procmail 电子邮件工具工作得相当好。但是，如果邮件轰炸影响了多个用户，你可能应该配置你的 sendmail 守护进程以阻止来自邮件轰炸者的所有电子邮件。你可以通过将邮件轰炸者的电子邮件地址或系统名称添加到位于 /etc/mail 目录中的访问文件中来实现此目的。

访问文件中的每一行都包含一个电子邮件地址、主机名、域名或 IP 地址，后跟一个制表符，然后是一个关键字，指定当该实体向你发送消息时采取的操作。有效关键字包括 OK、RELAY、REJECT、DISCARD 和 ERROR。使用 REJECT 关键字将导致发送者的电子邮件被退回并附带错误消息。关键字 DISCARD 将导致消息被静默丢弃，而不发送错误返回。你甚至可以使用 ERROR 关键字返回自定义错误消息。

因此，一个 /etc/mail/access 文件的示例可能看起来像这样：

```
# Check the /usr/share/doc/sendmail/README.cf file
# for a description of the format of this file. (search for
# access_db in that file) The
# /usr/share/doc/sendmail/README.cf is part of the
# sendmail-doc package.
#
# by default we allow relaying from localhost...
localhost.localdomain	RELAY
localhost	RELAY
127.0.0.1	RELAY
#
# Senders we want to Block
#
evilmailer@yahoo.com	REJECT
stumpy.glaci.com	REJECT
cyberpromo.com	DISCARD
199.170.176.99	ERROR:"550 Die Spammer Scum!"
199.170.177	ERROR:"550 Email Refused"
```

与大多数 Linux 配置文件一样，以 # 磅号开头的行是注释。我们阻止的垃圾邮件发送者列表位于此示例文件的末尾。注意，要阻止的地址可以是完整的电子邮件地址、完整的主机名、仅域名、IP 地址或子网。

要阻止特定的电子邮件地址或主机对你进行邮件轰炸，请以 root 身份登录到你的系统，编辑 /etc/mail/access 文件，并添加一行以 DISCARD 来自冒犯发送者的邮件。保存文件并退出编辑器后，你必须使用 makemap 命令将访问文本文件转换为 sendmail 守护进程使用的数据库格式。要将拒绝文件转换为名为 access.db 的哈希索引数据库，请键入以下内容：
