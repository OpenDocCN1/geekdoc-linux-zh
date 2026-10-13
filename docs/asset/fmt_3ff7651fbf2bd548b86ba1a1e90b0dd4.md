
### TMPDIR
设置 `LogSentry` 在处理期间写入临时文件的位置。该目录在 `LogSentry` 启动时创建，并在 `Logcheck` 完成前删除。您可以通过修改以下条目来更改位置：

```
TMPDIR=/tmp/logcheck$$-$RANDOM
```

### GREP
`logcheck.sh` 脚本依赖于支持 `-i`、`-v` 和 `-f` 选项的 `grep` 命令来搜索日志文件。默认情况下，使用 `egrep` 命令用于此目的。您可以通过修改以下变量将值更改为 `grep` 或其他命令：

```
GREP=egrep
```

### MAIL
`LogSentry` 使用 `mail` 命令发送电子邮件。要让 `LogSentry` 使用除 `mail` 命令之外的命令向管理员发送电子邮件，请更改以下 `mail` 变量：

```
MAIL=mail
```

### Filter files
`LogSentry` 定义了四个过滤文件。每个文件都包含用于查找消息或排除包含这些关键字的消息的关键字。以下变量设置为指示四个 `LogSentry` 过滤文件的位置：

```
HACKING_FILE=/etc/logsentry/logcheck.hacking

VIOLATIONS_FILE=/etc/logsentry/logcheck.violations

VIOLATIONS_IGNORE_FILE=/etc/logsentry/logcheck.violations.ignore

IGNORE_FILE=/etc/logsentry/logcheck.ignore
```

有关过滤文件的更多信息，请参阅本章后面的“更改 LogSentry 过滤文件”部分。

### Log files
您可能想要更改的 `/usr/sbin/logcheck.sh` 脚本中的最后条目指定了 `logcheck.sh` 脚本监控哪些日志文件。默认情况下，脚本运行 `logtail` 命令检查 `messages`、`secure` 和 `maillog` 文件（位于 `/var/log`）。以下行定义了要检查哪些日志文件，并确定 `logtail` 的输出临时写入的位置。

```
$LOGTAIL /var/log/messages > $TMPDIR/check.$$
```

```
$LOGTail /var/log/secure >> $TMPDIR/check.$$
$LOGTail /var/log/maillog >> $TMPDIR/check.$$
```

> **提示**：如果您愿意，可以通过添加与前面类似的更多行来检查更多日志文件。只需确保第一行包含单个箭头（以覆盖之前的检查文件），并且所有后续行都包含双箭头（以追加到当前检查文件）。

## 修改 LogSentry 过滤器文件

`/etc/logSentry` 目录包含四个过滤器文件，用于定义哪些消息会被匹配并通过电子邮件发送给管理员。这些文件的内容只是关键词。日志文件会被搜索（或 `grep`）这些关键词，并根据搜索结果进行排序或丢弃。

一些关键词过滤文件旨在发现系统被入侵或误用时会在日志消息中出现的词语或短语。其他关键词文件旨在查找不构成安全威胁的消息（以便这些消息可以从通过电子邮件发送的日志消息中排除）。既不匹配包含也不匹配排除的关键词的消息会被附加到电子邮件摘要输出的“异常系统事件”标题下。

您可以直接使用过滤器文件。然而，随着时间的推移，您可能出于多种原因想要修改这些文件。如果您在 `LogSentry` 电子邮件中收到重复的、无害的消息，您可以添加关键词来过滤掉这些消息。此外，随着您了解可能想要查找的新类型的安全漏洞，您也可以稍后添加关键词。

除了包含字母数字字符外，关键词还可以包含通配符。例如，您可以使用星号 (`*`) 匹配任意字符字符串，使用问号 (`?`) 匹配任意单个字符，或使用美元符号 (`$`) 匹配出现在行尾的关键词。

> **注意**：请谨慎使用通配符。错误的通配符可能导致包含或排除的消息过多或过少。

`/etc/logSentry` 目录中的四个 `LogSentry` 过滤器文件是：

- **logcheck.hacking**：包含出现在代表已知黑客攻击的日志消息中的关键词。
- **logcheck.ignore**：包含代表应始终忽略的消息的关键词。
- **logcheck.violations**：包含代表可能并不代表您系统真实入侵的负面活动的关键词。
- **logcheck.violations.ignore**：包含代表应从违规检查中找到的消息中忽略的关键词。

每个文件在以下各节中都有描述。

> 注意：需要指出的是，既未明确匹配（来自 `logcheck.hacking` 和 `logcheck.violations`）也未明确排除（来自 `logcheck.ignore` 和 `logcheck.violations.ignore`）的消息会被包含在 `Logcheck` 发送给管理员的电子邮件中。这些消息显示在总括标题“异常系统事件”下。

### logcheck.hacking

`/etc/logSentry/logcheck.hacking` 文件中的关键词旨在发现代表对您系统攻击的日志消息。此文件中关键词匹配的日志消息会以 `logcheck.hacking` 标题输出到发送给系统管理员的电子邮件中。

此标题下的消息是电子邮件中首先出现的内容。随着您了解代表不同类型系统攻击的消息，您可以向此文件添加其他关键词。

以下是出现在 `logcheck.hacking` 文件中的一些关键词示例：

```
"wiz"
"WIZ"
"debug"
"DEBUG"
ATTACK
nested
VRFY bbs
VRFY decode
VRFY udecode
rlogind.*: Connection from .*,* on illegal port
rshd.*: Connection from .*,* on illegal port
sendmail.*, user .*,* attempted to run daemon
wu-ftpd.*,*: refused connect from .*
tftp.*,*: refused connect from .*
login.*,*LOGIN FAILURE.*,* FROM .*,*root
login.*,*LOGIN FAILURE.*,* FROM .*,*guest
```

此文件中的大部分消息用于匹配有人使用 Internet Security Scanner（ISS）探测您的系统而产生的日志消息。ISS 是一种可以扫描一组 IP 地址以查找潜在安全弱点的工具。尽管 ISS 检查的大多数安全漏洞已随时间被修补，但这些日志消息会提醒您有人正在检查您系统的安全性。

上述文件中显示的 `debug` 和 `wiz` 关键词将捕获 ISS 尝试从 `sendmail` 服务访问 `wiz` 和 `debug` 服务的尝试。同样，`VRFY` 是 ISS 发送给 `sendmail` 服务请求的命令，用于询问不同的用户名。前面示例中显示的其他关键词短语匹配使用不同的 Linux 网络服务（例如 `rlogin`、`rshd`、`sendmail`、`uucico` 等）连接失败的尝试。

### logcheck.ignore

`/etc/logSentry/logcheck.ignore` 文件中的关键词用于查找应由 `LogSentry` 排除（即忽略）的日志消息，因此不会出现在电子邮件摘要中。此文件中的关键词减少了发送给管理员的日志消息数量，使查找真正问题变得更容易。以下是来自 `logcheck.ignore` 文件的一些关键词示例。

```
cron.*CMD
cron.*RELOAD
cron.*STARTUP
ftp-gw.*: exit host
ftp-gw.*: permit host
ftpd.*ANONYMOUS FTP LOGIN
http-gw.*: exit host
http-gw.*: permit host
identd.*Successful lookup
identd.*from:
named.*Response from
```

此文件中的大部分条目用于匹配代表各种系统服务正常运行的消息。前面示例中显示的关键词代表 `cron`、`ftp`、`http`、`identd` 和 `named` 功能的正常处理。

请注意，前一个示例中显示的所有关键词短语都包含星号 (`*`) 通配符。如果您向此文件添加自己的关键词，使用星号和其他通配符可以帮助您具体说明要排除的日志消息。

### logcheck.violations

有些词语暗示着计算机上存在负面行为。尽管这些词语可能与任何特定攻击无关，`LogSentry` 会记录包含这些词语的消息，并在以下标题下显示并通过电子邮件发送给系统管理员：

```
Security Violations
==================
```

以下是出现在 `logcheck.violations` 文件中的一些关键词示例：

```
ATTACK
BAD
DEBUG
FAILURE
ILLEGAL
```
