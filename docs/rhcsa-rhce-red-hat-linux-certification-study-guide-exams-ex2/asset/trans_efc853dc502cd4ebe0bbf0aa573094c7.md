
## 练习 9-1
### 创建一个 cron 作业

在本练习中，你将修改基本的 Red Hat cron 作业设置，以便在每年的 1 月份的每个星期一的下午 1:05 读取一个文本文件。为此，你需要为年度 cron 作业创建一个目录。为此，请使用以下步骤：

- 1. 以普通用户身份登录。
- 2. 创建一个 /etc/cron.yearly 目录。添加一个名为 taxrem 的文件，该文件读取你主目录中的文本文件。taxrem 文件中如下所示的命令就足够了：
- 3. 使用 crontab -e 命令打开你账户的 crontab。
- 4. 向 crontab 添加适当的命令。根据所述条件，它应如下所示：
- 5. 不要忘记在脚本开头添加诸如 SHELL=/bin/bash 之类的指令。
- 6. 保存并退出。确认 /var/spool/cron 目录中存在用户 cron 文件。该文件应与用户名相同。

```
cat ~/reminder
```

确保在你主目录中的 reminder 文件中添加适当的行，例如 "Don’t forget to do your taxes!" 确保 taxrem 文件可执行，使用 chmod +x /etc/cron.yearly/taxrem 命令。

```
5 13 * 1 1 root run-parts /etc/cron.yearly
```

## 使用 at 系统运行作业

与 cron 类似，at 守护进程支持作业处理。然而，你可以设置 at 作业仅运行一次。cron 系统中的作业必须设置为定期运行。at 守护进程的工作方式类似于打印进程；作业被 spool 到 /var/spool/at 目录，并在指定时间运行。

你可以使用 at 守护进程运行你选择的命令或脚本。为本节目的假设，用户 michael 在其主目录中创建了一个名为 797 的脚本，用于将一些飞机销售数据库处理到同一目录中名为 sales 的另一个文件。

从命令行，你可以运行 at time 命令来启动在指定时间运行的作业。该时间可以是现在；在指定的分钟数、小时数或天数后；或在你选择的任何时间。表 9-4 中举例说明了几种示例。

你可以使用表 9-4 中显示的示例命令之一来打开一个 at 作业。它会打开一个不同的命令行界面，在其中你可以指定你选择的命令。对于本示例，假设你即将下班并希望在一小时后启动作业。根据指定的条件，运行以下命令：

```
$ at now + 1 hour
at> /home/michael/797 > /home/michael/sales
at> Ctrl-D
```

CTRL-D 命令退出 at shell 并返回到原始命令行界面。如图所示，atq 命令检查当前 at 作业的状态。所有待处理的作业都会列在 atq 命令的输出中：

```
$ atq
1 2012-12-21 03:00 am michael
```

如果作业有问题，你可以使用 atrm 命令将其删除。例如，你可以使用以下命令删除标记为作业 1 的作业：

```
$ atrm 1
```

## 安全的 cron 和 at

你可能不希望每个人都能在半夜运行作业。如果系统存在安全漏洞，有人可能会下载重要数据甚至更糟，而安全漏洞可能需要数天才能被发现。

表 9-4
at 命令示例

| 时间段 | 示例 | 作业开始时间 |
|---|---|---|
| 分钟 | at now + 10 minutes | 10 分钟后 |
| 小时 | at now + 2 hours | 2 小时后 |
| 天 | at now + 1 day | 24 小时后 |
| 周 | at now + 1 week | 7 天后 |
| n/a | at teatime | 下午 4:00 |
| n/a | at 3:00 12/21/12 | 2012 年 12 月 21 日凌晨 3:00 |

用户可以在 /etc/cron.allow 和 /etc/cron.deny 文件中进行配置。如果这两个文件都不存在，cron 使用仅限于 root 管理用户。如果 /etc/cron.allow 文件存在，只有在该文件中命名的用户才允许使用 cron。如果没有 /etc/cron.allow 文件，则只有 /etc/cron.deny 中命名的用户不能使用 cron。

这些文件格式为每用户一行；如果你在 /etc/cron.deny 中包含以下条目，并且 /etc/cron.allow 文件不存在，则用户 elizabeth 和 nancy 不允许设置自己的 cron 脚本：

```
elizabeth
nancy
```

然而，如果 /etc/cron.allow 文件确实存在，并且包含相同的用户列表，则它具有优先权。在这种情况下，用户 elizabeth 和 nancy 都允许设置自己的 cron 脚本。可能性范围总结在表 9-5 中。

表 9-5
cron.allow 和 cron.deny 的安全影响

|  | /etc/cron.deny 存在 | /etc/cron.deny 不存在 |
|---|---|---|
| /etc/cron.allow 存在 | 只有 /etc/cron.allow 中列出的用户可以运行 crontab -e；/etc/cron.deny 的内容将被忽略。 | 只有 /etc/cron.allow 中列出的用户可以运行 crontab -e。 |
| /etc/cron.allow 不存在 | /etc/cron.deny 中列出的所有用户都不能使用 crontab -e。 | 只有 root 用户可以运行 crontab -e。 |

at 系统的用户安全几乎相同。相应的安全配置文件是 /etc/at.allow 和 /etc/at.deny。可能性范围总结在表 9-6 中。

如果你对安全极度谨慎，可能适合仅在 /etc/cron.allow 和 /etc/at.allow 文件中包含所需用户。否则，服务账户中的安全漏洞可能会允许黑客从相关账户运行 cron 或 at 脚本。

表 9-6
at.allow 和 at.deny 的安全影响

|  | /etc/at.deny 存在 | /etc/at.deny 不存在 |
|---|---|---|
| /etc/at.allow 存在 | 只有 /etc/at.allow 中列出的用户可以运行 at 命令；/etc/at.deny 的内容将被忽略。 | 只有 /etc/at.allow 中列出的用户可以运行 at 命令。 |
| /etc/at.allow 不存在 | /etc/at.deny 中列出的所有用户都不能运行 at 命令。 | 只有 root 用户可以运行 at 命令。 |

## 认证目标 9.04
### 本地日志文件分析

维护安全系统的重要部分是监控系统上发生的活动。如果你知道通常会发生什么，例如了解用户何时登录系统，你可以使用日志文件来发现异常活动。Red Hat Enterprise Linux 附带了新的系统监控实用程序，可以在出现问题时帮助识别罪魁祸首。

RHEL 6 附带了一个增强的日志守护进程，称为 rsyslog。它包括 RHEL 5 中使用的内核和系统日志服务的功 能。rsyslog 服务记录所有进程活动。你可以使用由此生成的日志文件来跟踪系统上的活动。将 rsyslog 配置为多个系统的日志服务器是 RHCE 技能，在第 17 章中介绍。

rsyslog 守护进程默认处于活动状态，可以通过 /etc/init.d/rsyslog 脚本激活。它记录文件的方式基于 /etc/rsyslog.conf 文件中定义的配置。如果你熟悉 RHEL 5 的 syslogd 和 klogd 守护进程，rsyslog.conf 文件中的概念应该很熟悉。

在许多情况下，SELinux、Apache 和 Samba 等服务有自己的日志文件，在其各自的配置文件中定义。详细信息在与这些服务相关的章节中介绍。

### 系统日志配置文件

你可以通过 /etc/rsyslog.conf 配置文件配置要记录的内容。如图 9-12 所示，它包含针对不同设施（如果已安装相应软件包）的规则集：authpriv、cron、kern、mail、news、user 和 uucp。

每个设施都关联有几个不同的日志级别，称为优先级。按升序排列，日志优先级为 debug、info、notice、warn、err、crit、alert、emerg。还有一个通用的 none 优先级，不记录特定设施的任何消息；例如，authpriv.none 指令将省略所有身份验证消息。

对于每个设施和优先级，日志信息会被发送到特定的日志文件。例如，考虑 /etc/rsyslog.conf 中的以下行：

```
*.info;mail.none;news.none;authpriv.none;cron.none /var/log/messages
```

### 图 9-12
rsyslog.conf 日志配置文件

```
#### RULES ####
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
kern.*                                            /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none;cron.none          /var/log/messages

# The authpriv file has restricted access.
authpriv.*                                        /var/log/secure

# Log all the mail messages in one place.
mail.*                                            -/var/log/maillog

# Log cron stuff
cron.*                                            /var/log/cron

# Everybody gets emergency messages
*.emerg                                           *

# Save news errors of level crit and higher in a special file.
uucp,news.crit                                    /var/log/spooler

# Save boot messages also to boot.log
local7.*                                          /var/log/boot.log
```

该行将来自所有给定设施的日志信息发送到 /var/log/messages 文件。这包括

- 所有设施的 info 级别及以上消息
- 除 mail、news、authpriv（身份验证）和 cron 服务相关的日志消息外

你可以在 /etc/syslog.conf 中使用星号作为通配符。例如，以 *.* 开头的行告诉 rsyslog 守护进程记录所有内容。以 auth.* 开头的行表示你想要记录来自 authpriv 服务的所有消息。

默认情况下，rsyslog 记录给定优先级或更高优先级的所有消息。换句话说，cron.err 行将包括 cron 守护进程在 err、crit、alert 和 emerg 级别的所有日志消息。

rsyslogd 守护进程的大多数消息都写入 /var/log 目录中的文件。你应该定期扫描这些日志并查找可能指示安全漏洞的模式。也可以设置 cron 作业来查找此类模式。
