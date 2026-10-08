

## syslogd 和 syslog.conf

**syslogd** 守护进程管理您系统上的所有日志，并协调网络中其他系统的所有日志记录操作。**syslogd** 的配置信息保存在 `/etc/syslog.conf` 文件中，该文件包含系统日志文件的名称和位置。在这里，您可以找到诸如 `/var/log/messages` 和 `/var/log/maillog` 等条目的其他信息。每当您对 `syslog.conf` 文件进行修改时，您需要使用以下命令重启 **syslogd** 守护进程（或使用 system-config-services，系统 \| 管理 \| 服务器设置 \| 服务）：

```bash
service syslog restart
```

### syslog.conf 中的条目

**syslog.conf** 中的一个条目由两个字段组成：*选择器* 和 *动作*。选择器是指要记录的服务类型，例如邮件或新闻，而动作是指消息放置的位置。动作通常是一个日志文件，但它也可以是一个远程主机或通向另一个程序的管道。服务类型被称为*设施*（facility）。**syslogd** 守护进程使用若干术语来指定某些类型的服务（见表 27-9）。设施可以进一步通过优先级进行限定。*优先级*（priority）指定了由该设施产生的消息类型；**syslogd** 使用若干指定术语来表示不同的优先级。*扇区*（sector）由设施（facility）和优先级（priority）组成，中间用点号分隔。例如，要保存邮件系统生成的错误消息，您使用由 **mail** 设施和 **err** 优先级组成的扇区，如下所示：

```text
mail.err
```

要将这些消息保存到 `/var/log/maillog` 文件，您指定该文件作为动作，从而得到以下条目：

```text
mail.err /var/log/maillog
```

**syslogd** 守护程序还支持使用 `*` 作为匹配字符，以匹配扇区中的所有设施或所有优先级：`cron.*` 将匹配所有 **cron** 消息，无论优先级如何；`*.err` 将匹配来自所有设施的错误消息；而 `*.*` 将匹配所有消息。以下示例将所有邮件消息保存到 `/var/log/maillog` 文件，并将所有严重消息保存到 `/var/log/mycritical` 文件：

```text
mail.* /var/log/maillog
*.crit /var/log/mycritical
```

### 优先级

当您为某个设施指定优先级时，所有具有更高优先级的消息也会被包含在内。因此，**err** 优先级还包含 **crit**、**alert** 和 **emerg** 优先级。如果您只想选择特定优先级的消息，请使用 `=` 运算符对优先级进行限定。例如，`mail.=err` 将仅选择错误消息，而不包括 **crit**、**alert** 或 **emerg** 消息。您还可以使用 `!` 运算符来限制优先级。这将排除具有指定优先级及更高优先级的消息。例如，`mail.!crit` 将排除 **crit** 消息，同时也排除更高优先级的 **alert** 和 **emerg** 消息。要专门排除某个整个设施的所有消息，请使用 **none** 优先级；例如，**mail.none** 会排除所有邮件消息。这通常用于在同一个条目中定义多个扇区时。

您可以通过用逗号分隔来在给定扇区中列出多个优先级或设施。您也可以使用分号在同一条目中放置多个扇区。

TABLE 27-9 Syslogd 设施、优先级和运算符

| 设施 | 描述 |
| --- | --- |
| **auth-priv** | 安全/授权消息（私有） |
| **cron** | 时钟守护进程（cron 和 at）消息 |
| **daemon** | 其他系统守护进程消息 |
| **kern** | 内核消息 |
| **lpr** | 行式打印机子系统消息 |
| **mail** | 邮件子系统消息 |
| **mark** | 仅内部使用 |
| **news** | Usenet 新闻子系统消息 |
| **syslog** | Syslog 内部消息 |
| **user** | 通用用户级消息 |
| **uucp** | UUCP 子系统消息 |
| **local0 到 local7** | 保留用于本地使用 |

| 优先级 | 描述 |
| --- | --- |
| **debug** | 7，调试消息，最低优先级 |
| **info** | 6，信息性消息 |
| **notice** | 5，通知，正常但重要的条件 |
| **warning** | 4，警告 |
| **err** | 3，错误消息 |
| **crit** | 2，严重状态 |
| **alert** | 1，警报，必须立即采取行动 |
| **emerg** | 0，紧急消息，系统不可用，最高优先级 |

| 运算符 | 描述 |
| --- | --- |
| \* | 匹配扇区中所有设施或优先级 |
| = | 限制为指定优先级 |
| ! | 排除指定优先级及更高优先级 |
| / | 保存消息的文件 |
| @ | 发送消息的主机 |
| \| | 发送消息的 FIFO 管道 |

第一个示例将保存所有具有 **info** 优先级的消息到 `/var/log/messages` 文件，排除所有邮件和认证消息（**authpriv**）。第二个示例将保存所有 **uucp** 和 **news** 设施中 **crit** 及更高优先级的消息到 `/var/log/spooler` 文件：

```text
*.info;mail.none;news.none;authpriv.none /var/log/messages
uucp,news.crit /var/log/spooler
```

### 动作和用户

在动作字段中，您可以指定文件、远程系统、用户或管道。文件的动作条目必须以 `/` 开头，并指定其完整路径名，例如 `/var/log/messages`。要将消息记录到远程主机，您只需指定带 `@` 符号的主机名。以下示例将所有内核消息保存到 **rabbit.trek.com** 上：

```text
kern.* @rabbit.trek.com
```

要将消息发送给用户，请列出他们的登录名。以下示例将向用户 **chris** 和 **aicina** 的控制台发送严重新闻消息：

```text
news.=crit chris,aicina
```

您还可以将消息输出到命名管道（FIFO）。动作字段的管道条目以 `|` 开头。以下示例将内核调试消息通过命名管道 `/usr/adm/debug` 传送：

```text
kern.=debug | /usr/adm/debug
```

### /etc/syslog.conf 的一个示例

Fedora 系统的默认 `/etc/syslog.conf` 文件显示如下。消息记录在 `/var/log` 目录中的各种文件里。

```text
/etc/syslog.conf
# 将所有内核消息记录到控制台。
#kern.*                     /dev/console
# 记录除邮件外级别为 info 或更高的所有内容。
# 不要记录私有认证消息！
*.info;mail.none;news.none;authpriv.none;cron.none          /var/log/messages
# authpriv 文件具有受限访问权限。
authpriv.*                                        /var/log/secure
# 将所有邮件消息记录在一个地方。
mail.*                                            /var/log/maillog
# 记录 cron 相关信息。
cron.*                                            /var/log/cron
# 每个人都会收到紧急消息
*.emerg                                             *
# 将 uucp 和 news 中级别为 err 或更高的错误消息保存到专门文件中。
uucp,news.crit                                      /var/log/spooler
# 也将启动消息保存到 boot.log
local7.*                                            /var/log/boot.log
# INN
news.=crit    /var/log/news/news.crit
news.=err     /var/log/news/news.err
news.notice   /var/log/news/news.notice
```

##  Linux 审计系统：auditd

Linux 审计系统提供系统调用审计。审计由一个名为 **auditd** 的服务器执行，日志保存在 `/var/log/audit` 目录中。它旨在补充 SELinux，后者将其消息保存到 `/var/log/audit/audit.log` 文件中的审计日志。审计日志记录服务为像 SELinux 这样的服务提供专门的日志记录。日志位于 `/var/log/audit`。为了细化审计，您可以创建审计规则以检查特定的系统调用，例如由特定用户或组生成的调用。

您可以使用 `/etc/init.d/auditd` 服务脚本来启动和关闭 **auditd** 服务器。使用 **system-config-services** 或 **service** 命令来启动和停止服务器。

```bash
service auditd start
```

**auditd** 的配置位于 `/etc/audit/auditd.conf` 和 `/etc/sysconfig/auditd` 文件中。主要配置由 `/etc/audit/auditd.conf` 处理，其中包含日志文件名称、日志格式、日志文件最大尺寸以及磁盘空间减少时应采取的操作等选项。有关所有选项的详细说明，请参阅 **auditd.conf** 手册页。`/etc/sysconfig/auditd` 文件设置服务器启动选项和本地位置（例如 **en_US**）。

audit 软件包包含 **auditd** 服务器和三个命令：**atrace**、**ausearch** 和 **auditctl**。您使用 **ausearch** 查询审计日志。您可以按各种 ID 进行搜索；按进程、用户、组或事件；以及按文件名甚至时间或日期。有关完整列表，请查阅 **ausearch** 手册页。**atrace** 是一个专门用于跟踪特定进程的工具。它的操作类似于 **strace**，记录特定进程的系统调用和操作。

您可以使用 **auditctl** 工具来控制 **auditd** 服务器的行为。使用 **auditctl**，您可以打开或关闭审计，检查状态，并为特定事件添加审计规则。有关详细说明，请查阅 **auditctl** 手册页。

审计规则组织在预定义列表中，针对系统调用具有特定的操作集合。目前有三个列表：**task**、**entry** 和 **exit**，以及三个操作：**never**、**always** 和 **possible**。在添加规则时，列表和操作配对，用逗号分隔，例如：

```text
exit,always
```

要添加规则，请使用 `-a` 选项。使用 `-S` 选项可以指定特定的系统调用，使用 `-F` 选项可以指定字段。有许多您可以使用的字段，例如 **loginuid**（用户登录 ID）、**pid**（进程 ID）和 **exit**（系统调用退出值）。对于字段，您指定一个值，例如对于登录 ID 为 510 的用户，使用 `loginuid=510`。根据文档描述，以下规则检查特定用户打开的所有文件：

```bash
auditctl -a exit,always -S open -F loginuid=510
```

