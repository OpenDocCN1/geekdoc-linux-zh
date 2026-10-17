
### 优先级

当您为某个设施指定优先级时，所有具有更高优先级的消息也会被包含在内。因此，`err`优先级还包含`crit`、`alert`和`emerg`优先级。如果您只想选择特定优先级的消息，请使用`=`运算符对优先级进行限定。例如，`mail.=err`将仅选择错误消息，而不包括`crit`、`alert`或`emerg`消息。您还可以使用`!`运算符来限制优先级。这将排除具有指定优先级及更高优先级的消息。例如，`mail.!crit`将排除`crit`消息，同时也排除更高优先级的`alert`和`emerg`消息。要专门排除某个整个设施的所有消息，请使用`none`优先级；例如，`mail.none`会排除所有邮件消息。这通常用于在同一个条目中定义多个扇区时。

您可以通过用逗号分隔来在给定扇区中列出多个优先级或设施。您也可以使用分号在同一条目中放置多个扇区。

TABLE 27-9 Syslogd 设施、优先级和运算符

| 设施 | 描述 |
| --- | --- |
| `auth-priv` | 安全/授权消息（私有） |
| `cron` | 时钟守护进程（cron 和 at）消息 |
| `daemon` | 其他系统守护进程消息 |
| `kern` | 内核消息 |
| `lpr` | 行式打印机子系统消息 |
| `mail` | 邮件子系统消息 |
| `mark` | 仅内部使用 |
| `news` | Usenet 新闻子系统消息 |
| `syslog` | Syslog 内部消息 |
| `user` | 通用用户级消息 |
| `uucp` | UUCP 子系统消息 |
| `local0 到 local7` | 保留用于本地使用 |

| 优先级 | 描述 |
| --- | --- |
| `debug` | 7，调试消息，最低优先级 |
| `info` | 6，信息性消息 |
| `notice` | 5，通知，正常但重要的条件 |
| `warning` | 4，警告 |
| `err` | 3，错误消息 |
| `crit` | 2，严重状态 |
| `alert` | 1，警报，必须立即采取行动 |
| `emerg` | 0，紧急消息，系统不可用，最高优先级 |

| 运算符 | 描述 |
| \* | 匹配扇区中所有设施或优先级 |
| = | 限制为指定优先级 |
| ! | 排除指定优先级及更高优先级 |
| / | 保存消息的文件 |
| @ | 发送消息的主机 |
| \| | 发送消息的 FIFO 管道 |

第一个示例将保存所有具有`info`优先级的消息到`/var/log/messages`文件，排除所有邮件和认证消息（`authpriv`）。第二个示例将保存所有`uucp`和`news`设施中`crit`及更高优先级的消息到`/var/log/spooler`文件：

```text
*.info;mail.none;news.none;authpriv.none /var/log/messages

uucp,news.crit /var/log/spooler
```

### 动作和用户

在动作字段中，您可以指定文件、远程系统、用户或管道。文件的动作条目必须以`/`开头，并指定其完整路径名，例如`/var/log/messages`。要将消息记录到远程主机，您只需指定带`@`符号的主机名。以下示例将所有内核消息保存到`rabbit.trek.com`上：

```text
kern.* @rabbit.trek.com
```

要将消息发送给用户，请列出他们的登录名。以下示例将向用户`chris`和`aicina`的控制台发送严重新闻消息：

```text
news.=crit chris,aicina
```

您还可以将消息输出到命名管道（FIFO）。动作字段的管道条目以`|`开头。以下示例将内核调试消息通过命名管道`/usr/adm/debug`传送：

```text
kern.=debug | /usr/adm/debug
```

### /etc/syslog.conf 的一个示例

Fedora 系统的默认`/etc/syslog.conf`文件显示如下。消息记录在`/var/log`目录中的各种文件里。

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

## Linux 审计系统：auditd

Linux 审计系统提供系统调用审计。审计由一个名为`auditd`的服务器执行，日志保存在`/var/log/audit`目录中。它旨在补充 SELinux，后者将其消息保存到`/var/log/audit/audit.log`文件中的审计日志。审计日志记录服务为像 SELinux 这样的服务提供专门的日志记录。日志位于`/var/log/audit`。为了细化审计，您可以创建审计规则以检查特定的系统调用，例如由特定用户或组生成的调用。

您可以使用`/etc/init.d/auditd`服务脚本来启动和关闭`auditd`服务器。使用`system-config-services`或`service`命令来启动和停止服务器。

```bash
service auditd start
```
