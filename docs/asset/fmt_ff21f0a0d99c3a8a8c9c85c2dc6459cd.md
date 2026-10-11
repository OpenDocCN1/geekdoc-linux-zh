
内核的持续日志由一个名为 `klogd` 的守护进程处理。`klogd` 的功能实际上是 `dmesg` 功能的超集；除了转储内核日志并退出外，它还可以在消息从内核缓冲区生成时从内核缓冲区中读取消息，并将其传递给文件或 syslog。在正常运行时，`klogd` 根据“内核”设施的指令处理消息（这些消息实际上被发送到 `/var/log/messages`）。

我们示例发行版的启动脚本在初始转储日志消息时，没有使用 `dmesg -c` 标志，这意味着内核消息缓冲区被读取但没有重置。当 `klogd` 启动时，它会在缓冲区中找到与 `dmesg` 看到的同一组消息，并将它们提交给 syslog。由于这个原因，某些条目会同时出现在 `dmesg` 或 `boot` 文件中，以及出现在另一个由 syslog 管理的文件（如 `/var/log/messages`）中。

内核日志的另一个问题是系统控制台的适当管理。在系统启动期间，让所有输出到控制台至关重要。一旦系统运行，控制台消息可能比帮助更多的是麻烦，特别是当控制台用于登录时。

`dmesg` 和 `klogd` 都允许你通过命令行标志设置内核的控制台日志级别。例如：

```
$ dmesg -n 2
```

级别 7 最详细，包含了调试信息。级别 1 仅包含 panic（崩溃）消息（数字越小的级别越严重）。无论消息是否被转发到控制台，所有消息都会继续发送中央缓冲区（并发送 syslog）。

内核在 `/proc/sys` 目录下提供了一些控制文件，允许从源头限制泛滥的日志消息。请参阅书中从第 874 页开始的“Linux 内核参数”章节，获取更多关于设置内核参数的通用机制的信息。特定的控制文件是 `/proc/sys/kernel/print_ratelimit`，它指定了激活限制后内核消息之间必须经过的秒数（默认值为 5），以及 `/proc/sys/kernel/print_ratelimit`（此处原文重复），它指定了在激活限制前允许多少组消息（默认值为 10）。这些参数是建议性的，它们不能绝对保证消息流将……

遗憾的是，系统启动脚本的日志记录并没有内核日志那样管理良好。红帽企业 Linux 使用 `itlog` 来捕捉启动命令的输出并提交给 syslog。遗憾的是，每当运行命令时都不会提到 `itlog`，因此这些信息是以一定的复杂性为代价的。消息最终进入 `/var/log/boot.log`。

我们的其他示例系统没有一致地尝试捕捉启动脚本输出的历史。某些信息由单个命令和守护进程记录，但很多内容未被记录。

![](img/cb325d29f74eb66e46eaf8d38883ecfe_245_0.png)

Fedora 过去使用与红帽相同的 `initlog` 系统，但用于提交日志条目的命令已在启动文件中被注释掉。幸运的是，有一个实用函数的中心库 `/etc/init.d/functions`，你可以在那里取消 `initlog` 行的注释以重新启用它们。

### 10.3 LOGROTATE：管理日志文件

Erik Troan 编写的 `logrotate` 工具实现了多种日志管理策略，它是我们所有示例发行版的标准配置。

`logrotate` 配置文件由一组针对待管理日志文件组规范组成。出现在日志规范上下文之外的选项（例如后续示例中的 `errors`、`rotate` 和 `weekly`）适用于所有后续的规范；它们可以在特定日志文件的规范内被覆盖，也可以在文件的后半部分指定以修改默认值。

这里是一个处理不同日志文件的略显刻意的示例：

```
# 全局选项
errors errors@book.admin.com
rotate 5
weekly
```

```
# 日志文件轮转定义和选项
/var/log/messages {
  postrotate
  /bin/kill -HUP `cat /var/run/syslogd.pid`
  endscript
}
/var/log/samba/*.log {
  notifempty
  copytruncate
  sharedscripts
  postrotate
  /bin/kill -HUP `cat /var/lock/samba/*.pid`
  endscript
}
```

该配置每周轮转一次 `/var/log/messages`。它保留该文件的五个版本，并在每次文件重置时通知 `syslogd`。Samba 日志文件（共有多个）也会进行轮转，但它们不是被移动，而是被复制然后截断。只有在日志文件轮转后，才会向 Samba 守护进程发送 HUP 信号。

`logrotate` 通常位于标准配置文件 `/etc/logrotate.conf`，但多个配置文件（或包含文件的目录）可以出现在 `logrotate` 的命令行中。我们的示例发行版使用了此特性，定义了 `/etc/logrotate.d` 目录，表 10.2 列出了最实用的 `logrotate` 选项。

**表 10.2 logrotate 选项**

| 选项 | 含义 |
| :--- | :--- |
| compress | 压缩日志文件的所有非当前版本 |
| daily, weekly, monthly | 按指定的调度轮转日志文件 |
| delaycompress | 压缩当前和最近一次之外的所有版本 |
| endscript | 标记 postrotate 脚本的结束 |
| errors | 向指定的邮件地址发送电子邮件通知 |
| missingok | 如果日志文件不存在则不报错 |
| notempty | 如果日志文件为空则不进行轮转 |
| olddir | 指定在轮转后将旧日志放在目录中 |
| postrotate | 在轮转后运行脚本 |
| prereate | 在轮转前运行脚本 |
| n | 保留 n 个日志版本 |
| sharedscripts | 仅在所有脚本执行后运行一次脚本 |
| size | 当大小大于 logsize 时轮转 |

### 10.4 Syslog：系统日志

由 Eric Altman 编写的 `syslog` 是一个全面的日志系统。它有两个重要的功能：让程序员从繁琐的日志文件写入中解放出来，并在消息生成时将其传递给文件或 syslog。在正常运行时，`klogd` 根据“内核”设施的指令处理消息（这些消息实际上被发送到 `/var/log/messages`）。

（注：此处原文似乎存在部分段落与 dmesg/klogd 混淆，翻译已根据上下文逻辑进行了处理）

#### Syslog 的替代方案

尽管 `syslog` 长期以来 Unix 和 Linux 的主流日志系统，但开发了一些替代方案以试图解决其缺点。其中之一 `syslog-ng`（下一代 syslog）现在默认用于 SUSE 系统。从配置角度来看，它与标准的 `syslog` 非常不同。

#### Syslog 架构

Syslog 由三部分组成：

- syslog，守护进程（以及其配置文件 `/etc/syslog.conf`）
- openlog，el. 将消息提交给 syslog 的库函数
- logger，从 shell 提交日志条目的用户级命令

在下面的讨论中，我们首先介绍 `syslog` 的配置，然后简要介绍如何在 Perl 脚本中使用 `syslog`。

syslog 在启动时启动并持续运行；它无法通过 inetd 管理。感知 syslog 的程序使用 syslog 库函数将日志条目写入特殊文件 `/dev/log`（一个 Unix 域接字）。syslog 从该文件读取消息，控制其配置，并将其分发到相应的目的地。如果你修改了 `/etc/syslog.conf`，必须向 syslog 发送信号以使更改生效。

挂断信号（HUP，信号 1）会导致 syslog 关闭其日志文件，重新读取配置文件并重新记录。TERM 信号让 syslog 退出。

syslog 将进程 ID (PID) 写入 `/var/run/syslog.pid` 文件。这种约定使得从脚本向 syslog 发送信号变得容易。例如，该命令发送挂断信号：

```
# kill -HUP /bin/cat /var/run/syslog.pid
```

尝试压缩或轮转 syslog 正在打开的文件是不健康的，并会产生不可预测的结果。正确的做法是移动旧日志，重建具有相同所有权权限的日志，然后向 syslog 发送 HUP 信号。这一过程可以通过 `logrotate` 轻松实现；参见第 208 页的示例。

#### 配置 syslog

配置文件 `/etc/syslog.conf` 控制 syslog 的行为。它是一个具有简单格式的文本文件。空行和在列中带有井号（#）的行会被忽略。基本格式为：

selector <Tab> action

## 10.4 Syslog：系统事件记录器

例如，该行

`mail.info /var/log/maillog`

将导致来自邮件系统的消息保存到 /var/log/maillog 文件中。

选择器（Selectors）通过以下语法识别发送日志消息的程序（“facility”，设施）以及消息的严重程度级别（level）：
