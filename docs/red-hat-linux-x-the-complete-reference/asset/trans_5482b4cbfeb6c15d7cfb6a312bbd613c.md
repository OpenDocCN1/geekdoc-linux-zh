

要将这些消息保存到 `/var/log/maillog` 文件，您将该文件指定为操作，这将生成以下条目：

```
mail.err /var/log/maillog
```

syslogd 还支持使用 `*` 作为匹配字符来匹配某个区段中的所有设施或优先级。`cron.*` 将匹配所有 cron 消息，无论其优先级如何；`*.err` 将匹配所有设施发出的错误消息；而 `*.*` 将匹配所有消息。以下示例将所有邮件消息保存到 `/var/log/maillog` 文件，并将所有严重（critical）消息保存到 `/var/log/mycritical` 文件：

```
mail.* /var/log/maillog
*.crit /var/log/mycritical
```

## 优先级

当为某个设施指定优先级时，所有具有更高优先级的消息也会被包含在内。因此，`err` 优先级也包含 `crit`、`alert` 和 `emerg` 优先级。如果您只想选择特定优先级，请使用 `=` 运算符来限定优先级。例如，`mail.=err` 将仅选择错误消息，而不包括 `crit`、`alert` 和 `emerg` 消息。您还可以使用 `!` 运算符来限制优先级。这将排除具有指定优先级及更高优先级的消息。例如，`mail.!crit` 将排除 `crit` 消息，以及更高优先级的 `alert` 和 `emerg` 消息。若要专门排除某个设施的所有消息，请使用 `none` 优先级。`mail.none` 会排除所有邮件消息。这通常用于在同一条目中定义多个区段时。

您可以通过用逗号分隔来在给定区段中列出多个优先级或设施。您可以通过用分号分隔，在同一条目中包含多个区段。第一个示例将排除所有邮件和认证消息（`authpriv`），并将所有具有 `info` 优先级的消息保存到 `/var/log/messages` 文件。第二个示例将 `uucp` 和 `news` 设施的所有 `crit` 消息及更高优先级的消息保存到 `/var/log/spooler` 文件：

```
*.info;mail.none;news.none;authpriv.none /var/log/messages
uucp,news.crit /var/log/spooler
```

## 操作用户

在操作字段中，您可以指定文件、远程系统、用户或管道。文件的操作条目必须以 `/` 开头，并指定其完整路径名，例如 `/var/log/messages`。要将消息记录到远程主机，只需指定带 `@` 符号的前缀的主机名即可。以下示例将所有内核消息保存在 `rabbit.trek.com` 上：

```
kern.* @rabbit.trek.com
```

要将消息发送给用户，请列出他们的登录名。以下示例将严重的新闻消息发送到用户 `chris` 和 `aleina` 的控制台：

```
news.=crit chris,aleina
```

您还可以将消息输出到命名管道（FIFO）。操作字段中的管道条目以 `|` 开头。以下示例将内核调试消息通过管道传送到命名管道 `|/usr/adm/debug`：

```
kern.*debug |/usr/adm/debug
```

### 表 27-9：Syslog 设施、优先级和运算符

| 设施 | 描述 |
|---|---|
| auth-priv | 安全/授权消息（私有） |
| cron | 时钟守护程序（cron 和 at）消息 |
| daemon | 其他系统守护程序消息 |
| kern | 内核消息 |
| lpr | 行式打印机子系统消息 |
| mail | 邮件子系统消息 |
| mark | 仅供内部使用 |
| news | Usenet 新闻子系统消息 |
| syslog | Syslog 内部消息 |
| user | 通用用户级消息 |
| uucp | UUCP 子系统消息 |
| local0 至 local7 | 保留供本地使用 |

| 优先级 | 描述 |
|---|---|
| debug | 7. 调试消息，最低优先级 |
| info | 6. 信息消息 |
| notice | 5. 通知，正常但重要的状况 |
| warning | 4. 警告 |
| err | 3. 错误消息 |
| crit | 2. 严重状况 |
| alert | 1. 警报，必须立即采取行动 |
| emerg | 0. 紧急消息，系统不可用，最高优先级 |

| 运算符 | 描述 |
|---|---|
| * | 匹配区段中的所有设施或优先级 |
| = | 限制为指定优先级 |
| ! | 排除指定优先级及更高优先级 |
| / | 保存消息的文件 |
| @ | 发送消息的主机 |
| \| | 发送消息的 FIFO 管道 |

## /etc/syslog.conf 示例

Red Hat 系统的默认 `/etc/syslog.conf` 文件如下所示。消息记录到 `/var/log` 目录中的各个文件。

```
# Log all kernel messages to the console.
#kern.*				/dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;news.none;authpriv.none;cron.none    /var/log/messages

# The authpriv file has restricted access.
authpriv.*                                            /var/log/secure
# Log all the mail messages in one place.
mail.*                                                /var/log/maillog
# Log cron stuff.
cron.*                                                /var/log/cron
# Everybody gets emergency messages
*.emerg                                               *
# Save mail and news errors of level err and higher in a special file.
uucp,news.crit                                        /var/log/spooler
# Save boot messages also to boot.log
local7.*                                              /var/log/boot.log
# INN
news.=crit                                            /var/log/news/news.crit
news.=err                                             /var/log/news/news.err
news.notice                                           /var/log/news/news.notice
```

## 性能分析工具和进程

Linux 将在系统上执行的每个任务视为一个进程，该进程被分配了一个编号和一个名称。您可以检查这些进程，甚至停止它们。Red Hat 提供了多种用于检查进程以及系统性能的工具。Red Hat 的 Procman 系统监视器等多个图形界面（GUI）工具提供了简单的监控功能。

## ps 命令

在命令行中，您可以使用 `ps` 命令列出进程。使用 `-aux` 选项，您可以列出所有进程。将输出管道传输到带有模式的 `grep` 命令，使您可以搜索特定进程。管道将前一个命令的输出作为下一个命令的输入传送。以下命令列出了所有 X Window System 进程：

```
ps -aux | grep 'X'
```

您系统上的许多实用程序提供了关于进程的详细信息，以及其他系统信息，如 CPU 和磁盘使用情况（参见表 27-10）。虽然这些工具最初是为在 shell 命令行中使用并显示文本行输出而设计的，但现在有几个版本提供了 KDE 和 GNOME 版本，它们提供图形界面用于显示结果和管理进程。

### 表 27-10：性能工具

| 性能工具 | 描述 |
|---|---|
| vmstat | 系统组件的性能 |
| top | 列出 CPU 密集型最高的进程 |
| free | 列出空闲 RAM 内存 |
| sar | 系统活动信息 |
| iostat | 磁盘使用情况 |
| Procman 系统监视器 | Red Hat 用于进程和使用率监视的系统监视器（在“系统工具”菜单中的“系统监视器”）。 |
| KDE 任务管理器和性能监视器 | KDE 用于进程和使用率监视的系统监视器 |

## vmstat, free, top, iostat, Xload, 和 sar

`vmstat` 命令输出详细列表，指示不同系统组件的性能，包括 CPU、内存、I/O 和交换操作。报告以带有不同组件字段的行发出。如果您提供时间段作为参数，它将在指定间隔（通常为几秒钟）重复。`top` 命令提供系统中 CPU 密集型最高的进程列表，显示哪些进程使用了最多的资源。列表是实时更新的，每几秒钟刷新一次。提供了用于更改进程状态（如优先级）的命令。

`free` 命令列出系统上空闲 RAM 内存的数量，显示使用了多少以及空闲多少，还显示用于缓冲区和服务换页内存的内容。`Xload` 是一个 X Window System 工具，显示负载、CPU 和内存。`iostat` 显示磁盘使用情况，而 `sar` 显示系统活动信息。

## Procman 系统管理器

Red Hat 的当前版本提供 Procman 系统管理器，用于显示系统信息和管理系统进程，可从“系统工具 | 系统监视器”访问。有两个面板，其中一个

