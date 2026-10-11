

在关闭服务器之前，你应该像处理其他分区一样，卸载 `/crypt` 文件系统，同时应该断开 `ppd0` 驱动的连接，方法如下：

```bash
[ramon]$ sudo umount /crypt
[ramon]$ sudo ppddsetup -d /dev/ppdd0
```

PPDD 使用由单个口令派生的密钥对整个文件系统加密，并允许用户通过标准的 Linux 权限模型访问文件系统内的文件。这使得 PPDD 成为保护服务器磁盘免受物理窃取系统的入侵者读取的良好选择，同时也适用于保护落入他人手中的备份介质。

## 小结

本章考察了系统级 Linux 安全涉及的问题，并提供了推荐的一组配置和实用工具，有助于保护你的服务器免受本地用户的未授权访问。虽然所有流行的 Linux 发行版都越来越注重安全性，但每天仍会有大量漏洞被报告。

理解所有内核参数的影响并认识到哪些参数会直接影响服务器的安全性至关重要。你应该构建自己的定制内核，既为了提高效率，也为了安全性和问责制。

你应该保护服务器免受 root 提权攻击。一种方法是通过持续监控系统文件的权限，并警惕 `setuid`/`setgid` 可执行文件的危险。为用户设置正确的默认 `umask` 可以确保他们以安全的权限创建文件。此外，使用 `ulimit` 命令限制核心文件大小可以防止一种常见的 root 越权攻击类型。

当所有其他方法都失效时，文件系统加密可以保护已泄露的数据。加密文件系统（CFS）为保护用户信息提供了良好的粒度，而实用隐私磁盘驱动程序（PPDD）是一种高效、透明的批量加密文件系统（和备份）的方法。

下一章，第 3 章，涵盖系统的监控和审计，并描述了你可以用来确保系统文件完整性的工具。这是系统安全的重要组成部分，应与本章的建议结合使用。

# 3

## 系统监控与审计

监控系统的异常行为是系统管理和信息安全中的一项基本任务。大多数攻击者都会在系统日志文件中留下“痕迹”，审查这些日志是网络取证过程中的一个基本步骤。更重要的是，定期审查日志文件，寻找异常或可疑的用户行为，可以防止攻击并增强服务器的整体安全性。

有些攻击者可能能够侵入你的系统，而不在日志文件中留下任何证据。然而，即使是最好的攻击者，如果没有被注意，也无法删除或修改历史文件。审查日志文件只是整体安全计划中的一个关键部分。

你应该在系统日志文件中查找以下内容：

- 反复的身份验证失败
- 异常关机
- 试图通过你的邮件服务器中继消息的尝试
- 任何看似异常的事件

单个用户的单次身份验证失败可以归因于密码输入错误。单个用户的多次身份验证失败可以归因于急性“手误”综合征。然而，多个用户的多次身份验证失败是正在进行的攻击的明确信号，或者表明你的某个内部用户可能正在尝试猜测 root 密码，以获取对服务器的更大访问权限。

通过集中式 syslog 设施的使用，Linux 提供了丰富的实时诊断功能，这些功能往往未被充分利用，并非因为它们没有提供正确的信息类型，而是因为大多数系统管理员不知道确切如何使用这些诊断功能。问题在于标准的 Linux syslog 文件过于冗长，毫无价值。典型的 Red Hat 或 Caldera 发行版上的 `/var/log/messages` 文件在平均负载服务器的一天中可能增长 500–600K 字节。

人工检查日志文件有两个主要缺点：

- 这项任务乏味且昂贵，因为它必须由受过培训、能识别故障迹象的（高薪的）系统管理员来执行。
- 人类容易出错，尤其是在扫描充满重复序列的大型文本文件时。

幸运的是，Linux 社区应对了这一挑战，并开发了许多有用的日志监控工具，可以以批处理方式运行，以识别已知会导致问题的特定关键字或模式。本章后面“系统日志监控”部分介绍了使用两个此类工具：swatch 和 logcheck 的日志监控概念。

## 使用 syslog 进行系统日志记录

syslog 实用工具允许系统管理员从中心位置配置和管理由异构系统实用工具和应用程序生成的日志文件。Linux 标准附带了已配置的 syslog 实用工具，并且在启动时 syslgd 守护进程处于活动状态。系统管理员在 `/etc/syslog.conf` 文件中指定他们希望看到哪些消息被记录，而应用程序将消息定向到适当的日志文件。大多数通用消息都定向到 `/var/log/messages` 文件，尽管系统管理员可以选择任意文件作为目标。一般来说，Linux 使用以下初始日志文件：

`/var/log/messages` 这是主要的 Linux 日志文件，用于记录大多数常见系统事件。

`/var/log/secure` 从 `/etc/inetd.conf` 启动的守护进程的身份验证失败会记录在这里。（第 4 章“网络服务配置”讨论了 inetd 实用工具。）

`/var/log/maillog` sendmail 守护进程以冗长（且通常非常繁忙）著称，因此专门使用这个单独的日志文件来跟踪邮件投递消息是有意义的。

`/var/log/spooler` 这是其他守护进程如 UUCP 和 News (NNTP) 记录其消息的日志文件。

`/var/log/boot.log` 系统启动时显示的启动消息通常记录在此文件中。

这些五个日志文件由系统通过 /etc/logrotate.d/syslog 脚本自动轮转。轮转基本上意味着将当前日志文件重命名为类似 logfile.1 的名称，同时创建一个名为 logfile 的新（空）文件，仅记录自上次轮转以来发生的事件。在下一次轮转时，logfile.1 文件被重命名为 logfile.2，而 logfile.11 文件（如果你只保留 10 个日志文件）将被删除。

### syslog.conf 文件

列表 3.1 展示了 Linux 系统上典型的 syslog.conf 文件。它包含了对本节前面描述的五个日志文件的引用。

**列表 3.1 典型的 Linux /etc/syslog.conf 文件**

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
kernel.*                              /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none        /var/log/messages

# The authpriv file has restricted access.
authpriv.*                            /var/log/secure

# Log all the mail messages in one place.
mail.*                                /var/log/maillog

# Everybody gets emergency messages, plus log them on another
# machine.
*.emerg                                 *
*.emerg                                 @loghost

# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit                        /var/log/spooler

# Save boot messages also to boot.log
local7.*                              /var/log/boot.log
```

syslog.conf 文件中条目的通用格式如下：

*facility.priority[*;**facility.priority[*] [TAB]*action*

每个字段的定义如下：

*facility*  *facility* 字段是你想要记录事件来源的子系统。当前支持的子系统有：

- auth: 安全和身份验证消息
- authpriv: 私有安全和身份验证消息
- cron: 时钟/调度守护进程
- daemon: 其他系统守护进程
- kern: Linux 内核消息
- lpr: 行打印机系统消息
- mail: 邮件系统
- news: 网络新闻子系统
- sysloger: 内部 syslog 消息
- uucp: Unix-to-Unix 复制子系统
- local0–local7: 保留供本地使用

特殊字符 * 可用于表示任何（及所有）设施。

*priority*  *priority* 字段指定给定子系统中消息的优先级水平。当前的优先级是（按严重程度升序排列）：

- debug: 用于故障排除的调试级别消息
- info: 信息消息
- notice: 具有特殊兴趣的正常消息
- warning: 预示即将发生故障的异常消息
- error: 故障条件消息
- crit: 关键错误条件消息
- alert: 需要立即采取行动的条件
- emerg: 导致系统故障的错误条件

