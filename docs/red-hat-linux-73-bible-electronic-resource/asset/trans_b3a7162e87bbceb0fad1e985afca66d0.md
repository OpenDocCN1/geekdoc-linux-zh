

## 使用 syslogd 将日志重定向到日志主机

要将计算机的日志文件重定向到另一台计算机的 syslogd，您必须对本地 syslogd 的配置文件进行一些更改。您需要处理的文件是 /etc/syslog.conf。使用 su 命令获取 root 权限，然后使用文本编辑器（例如 vi）加载 /etc/syslog.conf 文件。您应该看到类似以下内容：

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*                                  /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none    /var/log/messages

# The authpriv file has restricted access.
authpriv.*                              /var/log/secure

# Log all the mail messages in one place.
mail.*                                  /var/log/maillog

# Log cron stuff
cron.*                                  /var/log/cron

# Everybody gets emergency messages, plus log them on another
# machine.
*.emerg                                 *

# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit                          /var/log/spooler

# Save boot messages also to boot.log
local7.*                                /var/log/boot.log

#
# INN
#
news.=crit                              /var/log/news/news.crit
news.=err                               /var/log/news/news.err
news.notice                             /var/log/news/news.notice
```

以 # 字符开头的行是注释。其他行包含两列信息，用冒号分隔（空格无效）。左字段是由分号分隔的消息类型和消息优先级列表。右字段是应写入这些消息的日志文件。要将消息发送到另一台计算机（日志主机）而不是文件，只需将日志文件名替换为 @ 字符，后跟日志主机的名称。例如，要重定向通常发送到 messages、secure 和 maillog 日志文件的输出，请对上面的文件进行以下更改：

```
# Log anything (except mail) of level info or higher.
# Don’t log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none @loghost

# The authpriv file has restricted access.
authpriv.* @loghost

# Log all the mail messages in one place.
mail.* @loghost
```

现在，消息将发送到名为 loghost 的计算机上运行的 syslogd。loghost 这个名称并非随意选择的。惯例是创建这样的主机名，并使其成为实际充当日志主机的系统的别名。这样，如果需要将日志主机的职责切换到另一台机器，您只需要更改 loghost 别名；您不需要在每台计算机上重新编辑 syslog.conf 文件。

## 理解 messages 日志文件

由于许多程序和服务会将信息记录到 messages 日志文件中，理解该文件的格式非常重要。检查此文件通常会为您提供系统出现问题的早期预警。文件中的每一行都是某个程序或服务记录的一条消息。以下是实际 messages 日志文件的一个片段：

```
May 20 18:26 ratbert PAM_pwdb[3043]: (su) session opened for root by (uid=0)
May 20 18:27 ratbert PAM_pwdb[3049]: (login)session opened for mary by (uid=0)
May 20 18:27 ratbert login[3049]: LOGIN ON tty1 BY mary FROM dexter
May 20 18:27 ratbert PAM_pwdb[3049]: (login) session closed for user mary
May 20 23:27 ratbert ftpd[3060]: ANONYMOUS FTP LOGIN FROM dexter.glaci.com [199.170.177.25], thad@glaci.com
May 20 23:28 ratbert ftpd[3060]: FTP session closed
```

当您知道要看什么时，这其实非常简单。每条消息分为五个主要部分。从左到右依次为：

- 消息记录时的日期和时间
- 消息来源计算机的名称
- 消息所属的程序或服务名称
- 发送消息的程序的进程号（用方括号括起来）
- 实际的文本消息本身

让我们查看上述文件片段中的最后一行。首先，我们看到它是在 5 月 20 日 23:28:01 记录的（以非军事时间表示为 11:28 p.m.）。此外，它来自名为 ratbert 的系统，并由该系统上的 FTP 守护进程（ftpd）发送。该 ftpd 的进程号为 3060。它发送的消息是“FTP session closed”。如果您查看上一行，会发现另一条消息，同样来自 ratbert 上进程号为 3060 的 ftpd。这条消息显示了相关 FTP 会话的开启。文件中的其他消息记录了密码验证、登录尝试和 su 会话。如您所见，messages 文件为您提供了系统上正在发生的活动的一个相当不错的快照。您应该检查的另一个文件是 secure 日志文件。它的格式与 messages 文件相同，但仅包含各种服务的登录尝试和失败信息。

通过偶尔审查 messages 文件和 secure 文件，可以在破解尝试成功之前发现它们。如果您看到针对特定服务的过多连接尝试，特别是当它们来自 Internet 上的系统时，您可能正在遭受攻击。

## 使用 Tripwire 检测被篡改的文件

如果尽管尽了最大努力，攻击者实际上还是进入了您的系统，您可以做什么来最大限度地减少损失？熟练的攻击者会删除或修改您的系统日志，使人几乎不可能确切知道他们做了什么。重要的系统程序可能已被特洛伊木马替换。后门可能隐藏在你的安全机制中。手动检查和修复损坏可能是一个痛苦的过程。

仅仅从备份恢复是不够的，因为你不能确定攻击者最初是什么时候闯入的。后门和特洛伊木马可能已经在你的系统上存在了一段时间，因此也已经存在于你的备份中。这会让人们很想从头开始重新安装整个操作系统。

不要绝望。安全工具 Tripwire 可以拯救你免于这种最坏情况的噩梦。Tripwire 是一个文件完整性检查系统，最初由普渡大学的 Eugene Spafford 博士和 Gene Kim 开发。现在由商业组织 Tripwire Security Systems, Inc. 维护和支持。就像物理绊线一样，Tripware 软件包可以在您的安全受到入侵时警告您。

具体而言，当重要的系统程序或配置文件被修改时，Tripwire 可以警告您，从而允许您仅修复或替换被修改的文件，而无需重新安装整个系统。它是通过为系统中每个重要文件保留一个加密校验和数据库来实现的。加密校验和是通过将文件的每个字节通过特殊的数学算法生成的唯一数字。即使更改文件中的单个字节，您也会更改文件生成的校验和数字。因此，通过将文件的当前校验和与存储在数据库中的旧校验和进行比较，可以判断文件是否已被更改。

## 配置 Tripwire

Tripwire 首次被添加到 Red Hat Linux 发行版中是在 7.1 版本。安装后，您需要配置它。您可以通过 root 用户运行 `twninstall.sh` 脚本开始，输入以下内容：

```
# /etc/tripwire/twninstall.sh
Creating key files...

(When selecting a passphrase, keep in mind good passphrases typically have upper and lower case letters, digits, punctuation marks, and are at least 8 characters in length.)

Enter the site keyfile passphrase: ******
Verify the site keyfile passphrase: ******
Enter the local keyfile passphrase: ******
Verify the local keyfile passphrase: ******
```

根据提示，您需要选择本地和站点口令。*口令*是用于对 Tripwire 创建和使用的各种文件进行数字签名的特殊密码。数字签名用于验证文件的来源和完整性。它是防止攻击者篡改 Tripwire 软件包的一种保护机制。安装脚本首先会提示您输入站点口令。当您输入口令时，它不会显示，因此会被要求再次输入以验证第一次是否输入正确。您在选择此口令时应像在选取登录密码一样小心。基本上，避免使用字典单词、专有名词以及其他容易猜到的密码。（脚本建议使用至少 8 个字符，并包含大小写字母、数字和标点符号的组合。）

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

Tripwire 软件现在已安装在您的系统上并准备就绪。Tripwire 策略文件的文本版本被复制到 /etc/tripwire/tw.pol 文件。主 tripwire 命令有四种运行模式。

