
```
# /etc/tripwire/twninstall.sh
Creating key files...

(When selecting a passphrase, keep in mind good passphrases typically have upper and lower case letters, digits, punctuation marks, and are at least 8 characters in length.)

Enter the site keyfile passphrase: ******
Verify the site keyfile passphrase: ******
Enter the local keyfile passphrase: ******
Verify the local keyfile passphrase: ******
```

根据提示，您需要选择本地和站点口令。`口令`是用于对 Tripwire 创建和使用的各种文件进行数字签名的特殊密码。数字签名用于验证文件的来源和完整性。它是防止攻击者篡改 Tripwire 软件包的一种保护机制。安装脚本首先会提示您输入站点口令。当您输入口令时，它不会显示，因此会被要求再次输入以验证第一次是否输入正确。您在选择此口令时应像在选取登录密码一样小心。基本上，避免使用字典单词、专有名词以及其他容易猜到的密码。（脚本建议使用至少 8 个字符，并包含大小写字母、数字和标点符号的组合。）

接下来创建 Tripwire 配置文件。系统会提示您输入站点口令。它用于对该文件进行数字签名。

```
Signing configuration file...
Please enter your site passphrase:
```

接下来，创建策略文件。再次，您将被要求提供站点口令，以便用它对策略文件进行数字签名。

```
Signing policy file...
Please enter your site passphrase:
```

Tripwire 软件现在已安装在您的系统上并准备就绪。Tripwire 策略文件的文本版本被复制到 `/etc/tripwire/tw.pol` 文件。主 `tripwire` 命令有四种运行模式。

## 初始化 Tripwire 数据库

Tripwire 可以运行的四种模式中的第一种是数据库初始化模式。此模式会为系统中的文件创建一个新的校验和数据库。以 root 身份登录时，输入以下命令：

```
# tripwire --init
```

系统将提示你输入站点密码短语，之后将构建校验和数据库。数据库将写入文件 `/var/lib/tripwire/host.twd`，其中 `host` 将被替换为你的计算机主机名。

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

要修改 Tripwire 的策略文件，你必须首先编辑文本配置文件 `/etc/tripwire/twpol.txt`。在编辑器中打开该文件，注释掉提及那些导致错误消息的缺失文件的行。例如，如果你想消除缺失文件 `/usr/bin/dos` 的错误消息，请在策略文本文件中查找以下行：

```
/usr/bin/dos      -> $(SEC_SUID)  ;
```

在行的开头放置 `#` 字符以注释掉该行。它现在应如下所示：

```
#  /usr/bin/dos      -> $(SEC_SUID)  ;
```

现在你必须处理策略文本文件并创建 Tripwire 在创建或检查校验和数据库时实际使用的加密和数字签名策略文件。输入 `tripwire` 命令，并将 `--update-policy` 参数和策略文本文件的名称传递给它：

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

我将我的 Tripwire 可执行文件和数据库存储在 CD-R 可写 CD-ROM 驱动器上。当然，在运行 `tripwire` 命令时，你需要指定不同的文件路径。可以使用 `-d` 参数来更改校验和数据库的位置。在我的 Linux 系统 `ratbert` 上，我通过加载我的 Tripwire CD 并输入以下内容来运行 `tripwire` 命令：

```
# /mnt/cdrom/tss/bin/tripwire --check -d /mnt/cdrom/tss/db/ratbert.db
```

如果我升级操作系统，我必须生成一个新数据库并将其烧录到一张新的 CD 上，但这是确保我的 Tripwire 数据库未被破坏所需支付的一点小小代价。

## 防御拒绝服务攻击

入侵并非你的系统可能面临的唯一安全风险。你的计算机可能遭受拒绝服务攻击。这是一种试图让你的计算机崩溃或至少将其性能降低到不可用水平的攻击。有各种各样的拒绝服务利用方法。大多数都集中在过载某些系统资源，例如可用的磁盘空间或互联网连接。最常见的攻击及其防御方法在以下章节中讨论。

## 邮件轰炸

`邮件轰炸` 是向特定用户或系统发送如此多的电子邮件以至于计算机硬盘被填满的做法。有几种方法可以保护你自己免受邮件轰炸。你可以安装电子邮件过滤工具（如 `Procmail`）或配置你的 `sendmail` 守护进程。

> **交叉引用：** 参见第 19 章，以获取有关 `sendmail` 的更完整描述。

### 使用 Procmail 阻止邮件

`Procmail` 电子邮件过滤工具默认随 Red Hat Linux 安装，并与 `sendmail` 电子邮件守护进程紧密集成，因此可用于选择性阻止或过滤特定类型的电子邮件。你可以在 Procmail 网站 `www.procmail.org` 上了解更多关于 Procmail 的信息。

要为你的用户帐户启用 Procmail，请在你的主目录中创建一个 `.procmailrc` 文件。该文件的模式应为 `0600`（你可读，但其他人不可读）。输入以下内容，将 `evilmailer` 替换为正在对你进行邮件轰炸的实际电子邮件地址。
