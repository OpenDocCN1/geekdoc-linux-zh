

# 第 10 章 测试 Sendmail

250-ENHANCEDSTATCODES
250-EXPN
250-VERB
250-8BITMIME
250-SIZE
250-DSN
250-ONEX
250-ETRN
250-AUTH DIGEST-MDS

>>> MAIL From:<root@ibis.foobirds.org...>
250 2.1.0 <root@ibis.foobirds.org...> Sender ok
>>> RCPT To:<craig@wren.foobirds.org...>
250 2.1.5 <craig@wren.foobirds.org...> Recipient ok
>>> DATA

354 输入邮件内容，以单独一行的 "." 结束
>>>
250 2.0.0 0eVKnjp00881 Message accepted for delivery
craig@wren.foobirds.org... Sent (0eVKnjp00881
Message accepted for delivery)
Closing connection to wren.foobirds.org.
>>> QUIT

221 2.0.0 wren.foobirds.org closing connection

与第 1 章不同，此 sendmail 命令没有使用 `-t` 选项运行。相反，远程接收者的地址是直接在命令行中输入的，并将一个文件的内容提供给 Sendmail 作为邮件内容。接收者是 `craig@wren.foobirds.org`，而文件是空设备 `/dev/null`。显然，空设备不会提供任何实际内容，因此我们正在发送一封空邮件。此测试的唯一目的是观察协议的交互。

> 提示：不要为了测试电子邮件而向其他用户发送空邮件。要测试你的系统，请专门为此目的获取一个免费的电子邮件账户，并将测试邮件发送到该账户的你自己。要测试远程系统，请在开始发送测试邮件之前先与该系统的管理员联系好。

列表 10.2 当然在提问：“你为什么要查看协议交互？”SMTP 已经存在很长时间了。它是一个非常简单的协议。每个人都运行得很好。你并不是在寻找 SMTP 协议的错误。在这样的测试中，你寻找的是意外的结果，可能是由于你自己的配置的更改，也可能是由于远程端的问题导致的。你想要确保：

- 远程端有响应。
- 远程服务器支持你的系统所需的扩展 SMTP 协议功能。
- 你的系统向远程服务器发送了一个有效地址，且远程服务器接受了它。
- 你的系统提供的交付地址对于远程系统是一个有效地址。

Sendmail 在详细模式（verbose mode）下运行主要是当你遇到问题并正尝试收集线索来帮助分析问题时。`-v` 选项用于以详细模式运行 Sendmail。它还用于在带有请求信息（而非邮件投递）的命令行选项运行 sendmail 命令时增加显示的详细程度。这些选项之一是 `-bh`，它也被称为 hoststat 命令。

# hoststat 命令

`-bh` 命令行选项请求 Sendmail 显示主机状态。在大多数系统中，主机状态请求不会产生响应，因为默认的 Sendmail 配置不维护持久的主机状态。通常，Sendmail 在内部会根据需要跟踪其出站网络连接的状态。在使用 `-bh` 选项产生任何效果之前，必须更改配置，以便 Sendmail 写入这些连接的持久日志，并可以用于创建主机状态报告。

在你的 m4 配置中定义 `confHOSTSTATUS_DIRECTORY`，以启用持久的主机状态日志，并标识存储状态的目录。提供的 `confHOSTSTATUS_DIRECTORY` 的参数是记录状态的目录路径。列表 10.3 显示了一个将主机状态记录在 `/var/state/sendmail` 中的配置。

![](img/b8082498451dba2bf0cf2907c85c4c83_293_0.png)

# 列表 10.3 使用主机状态目录

```
[root]# diff sendmail.mc host-status.mc
23a4
> define`confHOSTSTATUS_DIRECTORY`, `/var/state/sendmail')
[root]# m4 host-status.mc > host-status.cf
[root]# diff /etc/sendmail.cf host-status.cf
228c228
< # 0 HostDirectory=.hoststat
```

```
> 0 HostStatusDirectory=/var/state/sendmail
[root]# mkdir /var/state/sendmail
[root]# cp /etc/sendmail.cf /etc/sendmail.cf.bak
[root]# cp host-status.cf /etc/sendmail.cf
cp: overwrite? '/etc/sendmail.cf?' y
[root]# ../rc.d/init/sendmail restart
```

关闭 sendmail：
启动 sendmail：

列表 10.3 以一个 `diff` 命令开头，显示了用于构建 `sendmail.cf` 的 `sendmail.mc` 配置文件与新 `status.mc` 文件之间唯一的区别是一个 `define` 命令。该命令定义了 `CONFHOST_STATUS_DIRECTORY` 并将其赋值为 `/var/state/sendmail`。新配置文件通过 m4 处理以创建 `host-status.cf`。与当前 `sendmail.cf` 文件的 `diff` 显示，唯一的区别是一个选项命令 `(0)`。该选项命令将 `HostStatusDirectory` 设置为 `/var/state/sendmail`。设置此选项是 `CONFHOSTSTATUS_DIRECTORY` 对 Sendmail 配置产生的唯一影响。

注意，在原始的 `sendmail.cf` 文件中，`HostStatusDirectory` 被注释掉了；同时注意，它有一个默认值，如果删除行开头的 `#` 则将使用该值。默认路径是 `.hoststat`，这是一个相对路径。如果使用相对路径，主机状态目录将邮件队列目录下的子目录。邮件队列目录在 m4 配置中通过 `QUEUE_DIR` 定义，并在 `sendmail.cf` 文件中设为 `QueueDirectory` 选项。对于我们的 Linux 系统，它是 `/var/spool/mail`。在使用 `-bh` 选项产生任何效果之前，必须更改配置，以便 Sendmail 写入这些连接的持久日志，并可以用于创建主机状态报告。在主机状态日志之前，必须创建目录，我们通过 `mkdir` 命令在 `/var/state/sendmail` 中操作。在 `sendmail.cf` 之后，我们重启了 Sendmail。主机状态在 `/var/state/sendmail` 中。几分钟后，运行带有 `-bh` 和 `-v` 选项生成了 10.4 的输出。

# 列表 10.4 示例主机状态报告

```
[root]# sendmail -bh -v
-- Hostname --------- How ago ----------Results
ibis.foobirds.org    00:02:30     250 2.1.0 <root@ibis.foobirds.org...> Sender ok
go.mammals.org       00:01:50     Deferred: Network is unreachable
```

**注意** `-bh` 命令行选项可以通过 `hoststat` 命令调用。正如第 3 章（运行 Sendmail）中提到的 `-bd` 选项和第 6 章（使用 Sendmail 数据库）中提到的 `-bi` 选项一样，它可以通过 `newaliases` 命令调用。入站连接不被记录。每个日志目包含三个字段：

- **Hostname**：第一个字段提供远程主机的完整域名。
- **How ago**：第二个字段指示状态更新的时间。该字段的格式为 `dd:mm:ss`，其中 `dd` 是天，`hh` 是小时，`mm` 是分钟，`ss` 是秒。这两条记录都是在主机状态启用后几分钟内生成的。然而，这是一个持久的状态报告。随着时间的推移，除非远程主机的状态发生变化，否则这些条目会变旧。例如，到 goat 连接可能会恢复。
- **Results**：第三个字段显示了上次向由 hostname 字段标识的 goat 投邮件的结果。除非在使用 `-bh` 时使用了 `-v` 选项，否则结果可能会截断。列表 10.4 中的第一个条目显示两半分钟前成功向 birds.org 投递。每个条目的结果包含了远程系统的完整响应，包括 SMTP 响应代码、DSN 代码、消息 ID 和文本。

本地生成的结果显示 goat 所连接的网络不可用。此外，它显示邮件被延迟，这意味着消息已经在邮件队列中。

主机状态目录中的状态条目是持久的。它们会随着时间自动更新，但不会被删除。这意味着该目录会增长

