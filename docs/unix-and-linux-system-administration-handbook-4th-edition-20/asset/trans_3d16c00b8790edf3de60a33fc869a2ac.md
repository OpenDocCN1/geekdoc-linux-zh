

## 第20 章

 电子邮箱

### amavisid 与 Exim 的连接

要配置 exim 将所有发往你域的邮件发送到 amavisid 进行病毒或垃圾邮件扫描，请将配置文件中的第一个路由器设置如下所示：

```
amavis:
no_verify_recipient
driver = mailroute
condition = ${if or eq [$interface_port] {10025} \
${eq[$received_protocol]} [scanned-ok] }} [0] {1}}
domain = local_domains
transport = amavis
route_list = * localhost byname
self = send
```

`condition` 行用于防止将源自端口 10025 的消息转发到 amavisid。该端口是 amavisid 在扫描后返回消息的端口，因此此类消息无法返回 amavisid，否则会产生循环。amavis transport 的配置如下：

```
amavis:
driver = smtp
port = 10024
allow_localhost
```

你必须在设置全局选项的配置文件开头添加此行：

```
local_interfaces = 0.0.0.0:25 127.0.0.1:10025
```

以告诉 exim 接受来自端口 25 的任何地址以及来自本地端口 10025（amavisid 返回端口）的消息。

这种配置允许所有扫描离线进行，因此响应病毒和垃圾邮件检测而生成的退信邮件本身会变成回声垃圾邮件（backscatter spam）。将 amavis 放在路由器列表的后面，并让 Exim 丰富的 ACL 处理最简单、最轻量的消息检查可能是一个更好的解决方案。更好的方法是使用 exim 的 `$(run...)` 检查进行联处理。Exim 内置的扫描功能使得 amavis 的吸引力略有下降。

### 日志

Exim 写入三种不同的日志文件：主日志（main log）、拒绝日志（reject log）和恐慌日志（panic log）。每条日志记录都包含写入消息的时间。你可以在 EDITIME 文件（在构建 exim 之前）或运行时配置文件的 `log_file_path` 选项中指定日志文件的位置。默认情况下，日志保留在 `/var/spool/exim/log` 目录下。

`log_file_path` 选项接受两个用逗号分隔的值。每个值必须是关键字 `syslog` 或嵌入了 `%s` 的绝对路径，其中 `%s` 可以替换为 `main`、`reject` 和 `panic`。例如，

```
log_file_path = syslog : /var/log/exim_%s
```

这将记录到 syslog（设施为 "mail"）以及 /var/log 目录下的 `exim_main`、`exim_reject` 和 `exim_panic` 文件。Exim 以 `info` 优先级将主日志提交到 syslog，以 `notice` 优先级提交拒绝日志，以 `alert` 优先级提交恐慌日志。

主日志包含每条消息到达和投递的一行。它可以使用 Exim 分发包中的 Perl 脚本 `eximstats` 进行汇总。

拒绝日志记录了因策略原因被拒绝的消息信息：恶意软件、垃圾邮件等。它包含了主日志中消息的摘要行，还包含了被拒绝消息的原始标头。如果你更改了策略，请检查拒绝日志以确保一切依然正常。

恐慌日志用于记录软件中的严重错误，exim 在放弃运行前会写入此处。如果没有出现问题，恐慌日志不应该存在。让 cron 为你检查，如果它存在，则找出导致恐慌的问题并删除该文件。Exim 在下次发生足以恐慌的情况时会创建它。

在调试时，你可以通过 `log_selector` 选项增加记录的数据量和类型。例如：

```
log_selector = +smtp_connection +snmp_incomplete_transaction + ...
```

`log_selector` 机制可以包含或排除的类别列在 Exim 规范靠近末尾的“Log files”章节中。大约有 35 种可能，包括 `+all`，这会填满你的磁盘！

exim 还会为它处理的每条消息保留一个临时日志。它以消息 ID 命名，位于 `/var/spool/exim/mslog`。如果你在某个特定目标上遇到问题，应该检查那里。

### 调试

Exim 拥有强大的调试辅助工具。你可以针对每个潜在的调试主题配置想要看到的信息量。`exim -d` 告诉 exim 进入调试模式，该模式将保持在前台运行且不记录自身的日志。你可以在 `-d` 后添加特定的调试类别，使用 `a` 或 `-d` 来请求调试输出关于字符串扩展的额外细节，使用 `acl` 请求关于 ACL 解释的额外细节（这两个类别是常见问题）。你可以调整超过 30 类的调试信息；请参阅列表页面。

调试邮件系统的一种常用技术是在非标准端口上启动 MTA，然后通过 `telnet` 与其通信。例如，要以守护模式启动 exim，监听端口 26 并开启调试信息，请使用：

```
$ exim -d -OX 26 -bd
```

![](img/579efec8c67772f31ecf34844bbb71a2_875_0.png)

然后你可以 `telnet` 连接到端口 26 并输入 SMTP 命令，尝试重现你正在调试的问题。

或者，你可以让 `swaks` 替你进行 SMTP 通信。运行 `swaks help` 可以获取一些文档说明。

