

# UNIX 系统管理入门进阶版

# 让第三方知道你正在对其进行监控

如果你决定在监控过程中使用第三方数据（如本节中的 Yahoo! DNS 示例），请让第三方知道你正在使用他们的数据。他们可能提前向你通报变化。对于你与他们已经建立关系的组织（例如你的互联网服务提供商 ISP 或母公司），这种方法最为有效。

当像上一个示例那样间接监控第三方服务时，你还面临由于服务不可用而导致假警报的风险。这是一个可以接受的风险，如果发生次数较，可以让你的监控程序查询不同的地址，或者在循环中给它一系列地址以避免单点故障。你可以在第 8 章中阅读更多关于这些第三方中断的知识。

# 超时与重试

到本章目前为止，你学到的监控过程是通过测试服务并根据它们对测试的响应来判断服务的通过或失败。如果服务需要 2 小时才有响应，或者如果它们没有响应呢？你的监控工具应该具备在指定间隔后超时的能力，此时测试将认为服务已宕机。

超时值没有既定的规则；超时间隔的长度高度取决于每个服务的性质。DNS 驱动着让互联网更易用的名称到地址转换，需要极高的响应，因此 15 秒的超时是合理的。另一方面，SMTP 没有 DNS 那样对时间敏感，而且更容易由于服务器负载而变得缓慢。在发送邮件的通常时间基础上增加 20 秒并不重要，因此可能对于 SMTP 服务检查，30 秒的超时可能更合适。

偶尔，超时是一个偶然事件；几乎每个互联网用户都曾在浏览器中点击过链接，等待两分钟让 DNS 查询完成。这些超时可能是由网络拥塞或服务器活动的快速激增引起的——确定原因可能很困难。无论如何，大多数服务不应该因为单次超时就被标记为宕机；第一次测试后不久进行的的服务测试可能会得到成功的结果。如果服务在第二次测试中失败，则应该将其标记为宕机。并不是所有的监控系统都提供重复测试，但如果你的系统提供，你应该充分利用它。

# 日志记录

系统日志是系统管理员的好朋友。它们讲述了你基础设施中每个系统、服务和网络的故事。日志有很多类型，每个操作系统和应用程序记录信息的方式都不同。日志在 Unix 中最常见的表现是日志文件。这是一个简单的文本文件，应用程序或系统日志消息会被附加到其中。结构良好的日志包含了每条消息产生的日期和时间。

设施（Facilities）被进一步分为不同的级别。日志消息的级别由其紧急程度决定，因此你可以使用级别来将紧急消息与信息性消息区分开。例如，报告 Telnet 连接的消息可能被认为是信息性的，但报告磁盘故障的消息将是关键的。表 6.3 列出了预定义的 syslog 级别。

# 表 6.3 按严重程度递减排列的 syslog 级别及其描述

| 级别 | 描述 |
| --- | --- |
| emerg | 紧急情况 |
| alert | 需要立即采取的操作 |
| crit | 关键状态 |
| err | 任何其他错误 |
| warning | 警告消息 |
| notice | 非错误状况 |
| info | 信息性消息 |
| debug | 调试消息 |
| none | 不记录此设施 |

为了接收日志，机器必须运行 syslog 服务器，通常称为 syslogd。在标准实现中，通过编辑 `/etc/syslog.conf` 文件来配置 syslogd，该文件由选择器（selectors）和动作（actions）对组成。选择器仅仅是 syslog.conf 中优先级的文本表示；它通过在级别和设施前加上点连接形成。一个设施为 `auth` 级别为 `info` 的日志选择器为 `auth.info`。选择器用于“选择”对任何特定消息采取何种动作。

![](img/894492738e879267320b8d6f9a044180_173_0.png)

Unix 内内核大多数通过 syslog 记录日志的应用程序使用特殊的日志设备（例如 `/dev/log`）或 C 函数 `syslog()`。脚本 无法轻松利用这些日志机制，因此你应该使用 `-p` 标志配合 syslog 优先级；它接受来自命令行或标准输入的消息，并通过 syslog 路由到适当的目标地。`logger` 命令的基本用法如下：

```
logger [-p priority] [-t file] tag message ...
```

你可以使用 `-f` 标志从文件记录日志，还可以使用 `-t` 标志指定一个标签来识别发送日志的程序。以下示例显示从机器 `server1` 以 `daemon.info` 优先级记录消息“Shutting down web server”：

```bash
bash$ logger -p daemon.info "Shutting down web server"
```

此命令产生以下日志消息：

May 5 15:57:14 server1 Jeff: Shutting down web server

# 第 6 章 • 监控服务

服务器接收到日志时可以根据 syslog.conf 中指定的选择器执行几项操作。syslog 动作列表 6.4 中。

# 表 6.4 syslog 动作及其配置格式

| 动作 | 格式 |
| --- | --- |
| 追加到日志文件 | filename |
| 广播给用户 | username |
| 广播给所有用户 | * |
| 发送到远程服务器 | @server |

单行内可以指定多个选择器，通过将它们分开（例如用分号或逗号）来实现。以下 syslog 配置所示：

```
# 选择器
auth.info /var/log/auth.log
auth.err /var/log/auth.log
auth.crit /var/log/auth.log
auth.alert /var/log/auth.log
auth.emerg /var/log/auth.log
auth.notice /var/log/auth.log
auth.debug /var/log/auth.log
daemon.info /var/log/daemon.log
daemon.err /var/log/daemon.log
daemon.crit /var/log/daemon.log
daemon.alert /var/log/daemon.log
daemon.emerg /var/log/daemon.log
daemon.notice /var/log/daemon.log
daemon.debug /var/log/daemon.log
mail.info /var/log/mail.log
mail.err /var/log/mail.log
mail.crit /var/log/mail.log
mail.alert /var/log/mail.log
mail.emerg /var/log/mail.log
mail.notice /var/log/mail.log
mail.debug /var/log/mail.log
info.info /var/log/info.log
info.err /var/log/info.log
info.crit /var/log/info.log
info.alert /var/log/info.log
info.emerg /var/log/info.log
info.notice /var/log/info.log
info.debug /var/log/info.log
kern.info /var/log/kern.log
kern.err /var/log/kern.log
kern.crit /var/log/kern.log
kern.alert /var/log/kern.log
kern.emerg /var/log/kern.log
kern.notice /var/log/kern.log
kern.debug /var/log/kern.log
messages.info /var/log/messages.log
messages.err /var/log/messages.log
messages.crit /var/log/messages.log
messages.alert /var/log/messages.log
messages.emerg /var/log/messages.log
local.info /var/log/local.log
local.err /var/log/local.log
local.crit /var/log/local.log
local.alert /var/log/local.log
local.emerg /var/log/local.log
local.notice /var/log/local.log
local.debug /var/log/local.log
cron.info /var/log/cron.log
cron.err /var/log/cron.log
cron.crit /var/log/cron.log
cron.alert /var/log/cron.log
cron.emerg /var/log/cron.log
cron.notice /var/log/cron.log
cron.debug /var/log/cron.log
user.info /var/log/user.log
user.err /var/log/user.log
user.crit /var/log/user.log
user.alert /var/log/user.log
user.emerg /var/log/user.log
user.notice /var/log/user.log
user.debug /var/log/user.log
```

# syslog-ng

syslog 在早期是 Unix 的一个极好的补充，但它也有其局限性。最显著的局限性是区分 syslog 与其他系统的唯一区别就是优先级。如果两条日志具有相同的优先级，则没有办法对每条日志执行不同的动作，syslog 从配置角度来看认为它们是相同的。

