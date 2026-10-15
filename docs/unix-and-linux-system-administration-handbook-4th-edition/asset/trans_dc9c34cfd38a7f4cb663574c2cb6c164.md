
most versions) 并且成为非常难以追踪的隐形错误。使用鼠标复制粘贴就是引入此类错误的一种方式。

选择器使用以下语法标识发送日志消息的程序（“facility”）以及消息的严重级别

```
facility.level
```

设施名称和严重级别都必须从一组定义的短列表中选择；程序不能自行创造。设施为内核、通用工具组以及本地编写的程序定义。其他所有内容都归类在通用设施 "user" 下。

选择器可以包含特殊关键字 * 和 none，分别表示全部或无。一个选择器可以包含用逗号分隔的多个设施。多个选择器可以用分号组合。

通常，选择器是 OR 关系：只要消息匹配任意一个选择器，就会受该行的操作影响。然而，级别为 none 的选择器会排除所列设施，而不论同一行上的其他选择器如何。

以下是格式化和组合选择器的一些示例：

```
facility.level          action
facility1,facility2.level   action
facility1.level1,facility2.level2   action
*.level                action
*.level,badfacility.none   action
```

表 11.2 列出了有效的设施名称。目前共有 21 个设施。

### 表 11.2 Syslog 设施名称

| Facility | Programs that use it |
|---|---|
| * | All facilities except "mark" |
| auth | Security and authorization-related commands |
| authpriv | Sensitive/private authorization messages |
| cron | The cron daemon |
| daemon | System daemons |
| ftp | The FTP daemon, ftpd |
| kern | The kernel |
| local0-7 | Eight flavors of local message |
| lpr | The line printer spooling system |
| mail | sendmail and other mail-related software |
| mark | Time stamps generated at regular intervals |
| news | The Usenet news system (obsolete) |
| syslog | syslogd internal messages |
| user | User processes (the default if not specified) |
| uucp | Obsolete, ignore |

不要太在意 syslog 对 auth 和 authpriv 的区分。所有与授权相关的消息都是敏感的，且都不应被全世界可读。

syslogd 本身会产生时间戳消息，如果 "mark" 设施出现在 syslog.conf 中以指定其目标位置，则会记录这些时间戳。时间戳可以帮助你判断机器是在凌晨 3:00 到 3:20 之间崩溃的，而不仅仅是“昨晚某个时间”。当你调试似乎定期出现的问题时，这些信息会非常有帮助。

表 11.3 按重要性降序列出了 syslog 的严重级别。

### 表 11.3 Syslog 严重级别（按严重程度降序）

| Level | Approximate meaning |
| --- | --- |
| emerg | Panic situations |
| alert | Urgent situations |
| crit | Critical conditions |
| err | Other error conditions |
| warning | Warning messages |
| notice | Things that might merit investigation |
| info | Informational messages |
| debug | For debugging only |

消息的严重级别指定了其重要性。各个级别之间的区别有时是模糊的。notice 和 warning 之间以及 warning 和 err 之间有明显区别，但 alert 与 crit 之间确切含义的差别则见仁见智。

在 syslog.conf 文件中，级别表示消息必须达到的最低重要性才能被记录。例如，来自邮件系统的级别为 warning 的消息会匹配选择器 mail.warning 以及选择器 mail.info、mail.notice、mail.debug、*.warning、*.notice、*.info 和 *.debug。如果 syslog.conf 指定将 mail.info 消息记录到文件中，mail.warning 消息也会被记录到那里。

作为基本语法的改进，Linux 版的 syslog 还允许在优先级级别前加上字符 = 和 !，分别表示“仅此优先级”和“除此优先级及更高优先级之外”。表 11.4 显示了示例。

![](img/14d78e3cecac4581d37024baf1e94cca_395_0.png)

### 表 11.4 syslog.conf 中 Linux 优先级级别限定符示例

| Selector | Meaning |
| --- | --- |
| mail.info | Mail-related messages of info priority and higher |
| mail.=info | Only messages at info priority |
| mail.info;mail.!err | Only priorities info, notice, and warning |
| mail.debug;mail.!warning | All priorities except warning |

