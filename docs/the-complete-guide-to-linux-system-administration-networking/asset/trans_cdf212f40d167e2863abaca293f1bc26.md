

# 表 13-3 syslog.conf 中用于指定设施的代码词

| 设施描述 | 设施名称 |
|---|---|
| 来自用户认证实用程序（如 login）的消息 | auth (formerly called security) |
| 特定用途（私有）用户认证消息 | auth-priv |
| 来自 cron 程序的消息（用于控制自动化、计划任务） | cron |
| 来自此处未另行列名的所有标准守护进程或服务器的消息 | daemon |
| 内核消息（通过 klogd） | kern |
| 打印机服务器消息 | lpr |
| 邮件服务器消息（来自邮件传输代理） | mail |
| 新闻服务器消息 | news |
| 关于系统日志进程本身的消息（如启动日志程序） | syslog |
| 来自终端用户启动的程序的消息 | user |
| 来自 uucp 程序的消息（很少使用） | uucp |
| Linux 发行版或程序员可为未被其他类别覆盖的特定需求定义的八个特定用途类别 | local0 through local7 |

![](img/43f64015de86d989e30eff5bb284fb96_626_0.png)

在许多情况下，多个程序使用相同的设施。特别是 daemon 设施，被许多程序使用。

## 优先级

所有 Linux 程序都会生成不同类型的消息。一些消息是信息性的；例如，它们可能会描述程序如何使用系统资源。其他消息表明存在潜在问题。还有其他消息表明存在严重或关键问题，这可能会损坏数据或关闭程序。每个程序都可以根据事件的严重程度生成具有不同优先级的消息。您可以配置系统，使不同优先级的消息以不同的方式记录。

表 13-4 显示了 syslog.conf 中可用的不同优先级，按从低到高的优先级列出。

# 表 13-4 syslog.conf 中使用的消息优先级

| 优先级描述 | 优先级名称 |
|---|---|
| 无优先级 | none |
| 程序员或测试程序工作方式的人员使用的调试消息 | debug |
| 关于程序正在做什么的信息性消息 | info |

# 表 13-4 syslog.conf 中使用的消息优先级（续）

| 优先级描述 | 优先级名称 |
|---|---|
| 关于程序执行时发生的值得注意事件的信息 | notice |
| 关于程序潜在问题的警告 | warning (formerly called warn) |
| 关于程序内部发生的错误通知 | err (formerly called error) |
| 描述可能导致程序关闭事件的严重错误消息 | crit |
| 会导致程序关闭并可能影响其他程序的错误消息 | alert |
| 关于可能导致系统崩溃事件的消息 | emerg (formerly called panic) |

当软件开发人员编写程序时，他或她会决定哪些事件与哪些优先级级别相关。例如，开发人员可能会设计一个程序，使某个事件生成优先级为 warning 的消息。另一位程序员可能会决定同一事件应生成优先级为 notice 的消息。因此，程序本身决定它们属于哪个设施，以及单个事件或消息应具有什么优先级。作为系统管理员，您只需根据其设施和优先级确定消息记录的位置。

## 操作

一旦设置了选择器（由设施和优先级组成），您可以为该选择器分配一个操作。操作决定 syslogd 和 klogd 对选择器定义的消息做什么。可能的操作如下列出：

- 使用给定的文件名将消息写入常规文件。（这是最常用的操作。）
- 将消息写入指定的终端。这可以是标准虚拟终端名称，从 /dev/tty1 到 /dev/tty6，或控制台设备 /dev/console。
- 将消息写入任何已登录用户的屏幕，该用户来自给定的用户列表。例如，如果操作是 root,lsnow，则选择器中的消息会写入用户 root 和 lsnow 的屏幕，前提是他们已登录。这可确保 root 以及可能的其他用户在发生可能导致程序关闭的严重错误时立即得到通知。
- 将消息写入远程系统上的日志文件。这是通过操作中的符号 @ 完成的。例如，您可以将操作指定为 @incline.xyz.com，以将给定选择器的日志消息发送到名为 incline.xyz.com 的系统上运行的 syslogd 守护进程。

将消息写入远程系统的选项在以下几种情况下很有用：

- 整合重要消息：组织中的许多系统可以将日志消息发送到单个系统，以便作为一个整体进行归档和研究。
- 保护故障系统上的信息：当系统因硬件故障而崩溃时，存储在硬盘上的任何系统日志文件都可能损坏，或至少在系统恢复之前无法访问。通过将日志文件存储在另一台系统上，您可以确保即使生成它们的系统发生故障，这些消息也可以被审查。
- 增强安全性：将日志文件远程存储使得入侵者更难删除可能存储在系统日志文件中的其活动记录。

## 配置文件语法

以下示例列表显示了 syslog.conf 文件中的行。注释行（以 # 字符开头）位于每个配置行之前并解释其目的。

```
# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
* info;mail.none;authpriv.none          /var/log/messages
# The authpriv log file has restricted access.
authpriv.*                             /var/log/secure
# Log all the mail messages in one place.
mail.*                                  /var/log/maillog
# Everybody gets emergency messages
* emerg                                 *
# Save boot messages also to boot.log
local7.*                                /var/log/boot.log
```

即使阅读了关于设施和操作的内容，配置文件语法的一些方面仍然不明显：

- 作为设施或优先级使用的星号（ * ）分别匹配所有设施或所有优先级。例如，选择器 * .emerg 选择来自任何设施的所有具有 emerg 优先级的消息。
- 作为操作使用的星号（ * ）意味着所有已登录的用户都可以在其屏幕上看到匹配的消息（如果他们有可接收消息的命令行）。上面的示例行中的 *.emerg 选择器将（ * ）用作操作。
- 设施和优先级由句点分隔。
- 多个选择器可以通过分号（ ; ）分隔包含在同一配置行中。
- 可以使用逗号分隔列表同时指定多个设施或优先级。例如，uucp,news.crit 匹配来自 uucp 或 news 设施的优先级为 crit 的消息。
- 关键字 none 作为优先级会排除来自指定设施的所有消息。例如，指定 * .info;mail.none 匹配来自任何设施的优先级为 info 或更高的消息，但排除来自 mail 设施的所有消息。
- 对于选择器中指定的任何优先级，所有该优先级以及所有更高优先级（更严重问题）的消息都包含在内。
- 同一消息可以通过在多行中包含相同的选择器并使用不同的操作，将其记录到多个位置。例如，关键的内核消息可能会显示在 /dev/console 设备上，并同时记录到远程机器以供以后分析，使用如下配置行：
  `*.crit    /dev/console,@logging_host`
- syslog.conf 中的配置行不会覆盖之前的配置行；syslog.conf 中一行配置的每个操作都会添加到已配置的所有内容中。

除了 syslog.conf 语法的这些基本规则外，偶尔还会使用几个特殊符号来更精确地指定设施或优先级。syslog.conf 的 man 手册对这些很少使用的功能有完整细节。

# 表 13-5 示例 syslog.conf 配置行

| 示例配置行 | 配置行的效果 |
|---|---|
| #kern.* /dev/console | 无；此行以注释字符开头 |
| kern.* /dev/console | 将所有内核消息（任何优先级）记录到控制台（计算机屏幕） |
| *.info,mail.none,authpriv.none /var/log/messages | 将来自任何设施、优先级为 info 或更高的所有消息记录到文件 /var/log/messages，但排除所有设施为 mail 或 authpriv 的消息，无论其优先级如何 |
| authpriv.* /var/log/secure | 将来自 authpriv 设施的所有消息记录到文件 /var/log/secure |
| uucp,news.crit /var/log/spooler | 将设施为 uucp 或 news 且优先级为 crit 或更高的任何消息写入文件 /var/log/spooler |
| *.emerg * | 在所有已登录用户的屏幕上显示优先级为 emerg 的任何消息 |
| mail.* /var/log/maillog | 将来自 mail 设施的所有消息记录到文件 /var/log/maillog |
| *.emerg @loghost | 将所有优先级为 emerg 的消息（来自所有设施）发送到名为 loghost 的计算机上运行的 syslogd 守护进程 |

更改 syslog.conf 配置文件后，您必须告诉 syslogd 和 klogd 重新读取配置文件，以便您的更改在系统上生效。您可以使用 service 命令执行此操作（syslog 服务会重启两个日志守护进程）：

```
# service syslog restart
```

