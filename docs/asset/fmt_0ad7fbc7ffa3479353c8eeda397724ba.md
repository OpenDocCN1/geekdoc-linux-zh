
`auth`        `user`

`auth-priv`   `uucp`

`cron`        `local0`

`daemon`      `local1`

`kern`        `local2`

`lpr`         `local3`

`mail`        `local4`

`mark`        `local5`

`news`        `local6`

`security`    `local7`

`syslog`

其中某些设施具有特殊含义。`security` 设施是 `auth` 的过时别名，`mark` 是一个内部设施，每 20 分钟向 `syslog` 发送一次消息。`local0` 留给任何本地定义的功能使用。

用于选择消息的第二个参数是优先级（`priority`）。它是对消息严重程度的指示。按增加顺序，优先级为：

```
debug      error
info       crit
notice     alert
warning    emerg
warn       panic
err
```

`error`、`warn` 和 `panic` 分别是 `err`、`warning` 和 `emerg` 的过时别名，不应使用。

选择器的格式为 `facility.priority`。这种形式匹配所有所选优先级以及所有更高优先级的消息；例如，`mail.info` 匹配所有 `mail`

![](img/f36419c0b225d12fa66de83fa271829b_458_0.png)

除 `debug` 以外的所有 `mail` 消息。如果你只想匹配特定的优先级，可以使用等号（`=`）。因此，`mail.=info` 将仅匹配 `info` 优先级的消息。

还有其他特殊字符。星号（`*`）意味着“所有”，因此 `mail.*` 匹配所有 `mail` 消息（等同于 `mail.debug`），而 `*.crit` 匹配所有优先级为 `crit` 及其以上的消息。

感叹号（`!`）否定一个条件，因此 `mail.!info` 等同于 `mail.=debug`，而 `mail.info` 等同于 `mail`。

你可以用逗号在单个选择器中组合多个设施，例如，`mail,news.crit` 匹配 `mail` 和 `news` 服务所有 `crit` 或更高优先级的消息。你也可以用分号组合多个选择器。在这种情况下，可以使用特殊优先级 `none` 来指定不来自给定服务的消息。例如，`*.crit;none` 匹配除 `mail` 设施之外的所有 `crit` 级或以上的消息。

# 动作

动作字段指定了对特定选择器匹配的消息做什么。动作的第一个字符指定了动作类型。

以斜杠（`/`）开头的动作指定了将追加消息的文件（例如 `/var/log/messages`）。如果该文件是 `tty`，则使用特殊的 `tty` 处理。如果你想将消息发送到控制台，使用 `/dev/console`。

连字符后跟斜杠（`-`）也指定了文件名，但指定在每次写入后不将文件刷新到磁盘。这使得 `syslog` 更高效，但带有系统崩溃时丢失消息的风险。它不应用于任何关键日志——例如，`/var/log/ppp`。

命名管道 `/dev/console` 用于 `xconsole` 工具。要使用它，必须通过 `-file` 选项调用 `xconsole`：

```
$ xconsole -file /dev/console
```

# 系统日志与计数

第 13 章

在挂载后，`klog` 使用系统调用读取消息。有关 `/proc` 文件系统的更多信息，请参阅第 15 章“高级系统管理”。

`klog` 使用 `kernel` 设施记录消息。其优先级由内核本身给出，并由相应的 `syslog` 优先级还原。内核优先级列在 `/usr/include/linux/kernel.h` 文件中。以下是该文件的相关部分，包括每个层级的含义：

```
#define KERN_EMERG "<0> /* 系统无法使用
#define KERN_ALERT "<1> /* 必须立即采取行动
#define KERN_CRIT "<2> /* 关键条件
#define KERN_ERR "<3> /* 错误条件
#define KERN_WARNING "<4> /* 警告条件
#define KERN_NOTICE "<5> /* 正常但重要的状态
#define KERN_INFO "<6> /* 提示信息
#define KERN_DEBUG "<7> /* 调试级别消息
```

通常，你可能希望记录所有可能影响系统运行状况的消息，即优先级为 `notice` 或更高的消息，甚至包括 `info`。在你的站点上开启几天并将所有日志记录到不同的文件中，可以让你了解哪些消息是有用的（当然，你不应该收到任何高于 `notice` 优先级的消息！）。要做到这一点，可以在 `/etc/syslog.conf` 中添加以下行：

```
kern.debug /var/log/kernel.debug
kern.info /var/log/kernel.info
kern.notice /var/log/kernel.notice
kern.warning /var/log/kernel.warning
kern.err /var/log/kernel.err
kern.crit /var/log/kernel.crit
kern.emerg /var/log/kernel.emerg
```
