
b. 必须在 `N` 与单位之间没有空格。例如，`3m` 正确，但 `3 m` 不正确。

c. `h` = hours，`d` = days，`w` = weeks，`m` = months，`y` = years

例如，以下是之前示例中经过扩展以包含轮转选项的 `syslog.conf` 配置行：

```
### Rotate at 500MB, keep 4 files
mail.debug  /var/log/mail        rotate size 500m files 4

### Rotate after 1 week, keep 10 files, compress the file
user.debug  /var/log/user        rotate files 10 time 1w compress

### Rotate after 100KB or 2 months, whichever occurs first, keeping 4 files
kern.debug  /var/log/kern        rotate size 100k files 4 time 2m

### Keep 1 year of weekly logs, compress the file, move the file to /logs
syslog.debug /var/log/messages   rotate files 52 time 1w compress archive /logs
```

## 11.4 LOGROTATE：管理日志文件

Erik Troan 的出色 `logrotate` 实用程序实现了各种日志管理策略，并且是所有示例 Linux 发行版的标准。它也可以在 Solaris、HP-UX 和 AIX 上运行，但你需要自行安装。我们更喜欢 `logrotate` 而不是 Solaris 提供的较差的 `logadm` 包。

`logrotate` 配置文件由一系列用于要管理的日志文件组的规范组成。出现在日志文件规范上下文之外的选项（例如以下示例中的 `errors`、`rotate` 和 `weekly`）适用于所有后续规范。它们可以在特定文件的规范中被覆盖，并且也可以在文件后面的位置重新指定以修改默认值。

### 日志文件轮转定义和选项

```
/var/log/messages {

  postrotate

    /bin/kill -HUP `cat /var/run/syslogd.pid`

  endscript

}
```

```
/var/log/samba/*.log {

  notifempty

  copytruncate

  sharedscripts

  postrotate

    /bin/kill -HUP `cat /var/lock/samba/*.pid`

  endscript

}
```

此配置每周轮转一次 `/var/log/messages`。它保留文件的五个版本，并在每次重置文件时通知 `syslogd`。Samba 日志文件（可能有多个）也每周轮转，但不是移开后重新启动，而是复制后截断。只有在所有日志文件都已轮转后，才向 Samba 守护进程发送 `HUP` 信号。

### 表 11.7 logrotate 选项

| Option | Meaning |
|---|---|
| `compress` | Compresses all noncurrent versions of the log file |
| `daily`, `weekly`, `monthly` | Rotates log files on the specified schedule |
| `delaycompress` | Compresses all versions but current and next-most-recent |
| `endscript` | Marks the end of a prerotate or postrotate script |
| `errors emailaddr` | Emails error notifications to the specified emailaddr |
| `missingok` | Doesn't complain if the log file does not exist |
| `notifempty` | Doesn't rotate the log file if it is empty |
| `olddir dir` | Specifies that older versions of the log file be placed in dir |
| `postrotate` | Introduces a script to run after the log has been rotated |
| `prerotate` | Introduces a script to run before any changes are made |
| `rotate n` | Includes n versions of the log in the rotation scheme |
| `sharedscripts` | Runs scripts only once for the entire log group |
| `size logsize` | Rotates if log file size > logsize (e.g., 100K, 4M) |

`logrotate` 通常由 `cron` 每天运行一次。其标准配置文件是 `/etc/logrotate.conf`，但多个配置文件（或包含配置文件的目录）可以出现在 `logrotate` 的命令行上。Linux 发行版利用此功能，将 `/etc/logrotate.d` 目录定义为 `logrotate` 配置文件的标准位置。许多 `logrotate` 感知的软件包可以在其安装过程中添加日志管理指令，从而大大简化管理。

除了 `logrotate`，Ubuntu 还提供了一个更简单的程序 `savelog` 来管理单个文件的轮转。它比 `logrotate` 更直接，且不使用（或不需要）配置文件。一些软件包更喜欢使用自己的 `savelog` 配置而不是 `logrotate`。

## 11.5 将日志文件压缩为有用信息

`Syslog` 对于排序和路由日志消息非常有用，但归根结底，其最终产品仍然是一堆日志文件。虽然它们可能包含各种有用信息，但当出现问题时，这些文件不会主动来找你。还需要另一层软件来分析日志并确保重要消息不会淹没在杂音中。

有多种免费工具可填补这一空白，而且大多数工具都非常相似：它们扫描最近的日志条目，将其与正则表达式数据库进行匹配，并以引人注意的方式处理重要消息。这些工具主要的区别在于灵活程度以及其即用型模式数据库的大小。

两种更常用的日志后处理器是 Todd Atkins 的 `swatch` 和 Craig Rowland 的 `logcheck`。两者都可在 `sourceforge.net` 上获得（`logcheck` 随 `sentrytools` 包提供：`sourceforge.net/projects/sentrytools`）。

`swatch` 是一个 Perl 脚本，其指令来自配置文件。配置语法相当灵活，并提供了 Perl 完整的模式匹配功能。虽然 `swatch` 可以一次性处理整个文件，但它主要用于持续运行，以便像 `tail -f` 一样在消息到达时进行审查。`swatch` 的缺点是你必须基本上从头开始构建自己的配置；它不知道特定系统及其可能生成的实际日志消息。

`logcheck` 是一个用 `sh` 编写的更基础的脚本。发行版还包含一个 C 程序，`logcheck` 用它来帮助记录其在日志文件中的位置。`logcheck` 知道它在日志文件中读到哪里，因此在启动或关闭时消息溜走的可能性可能更小。此外，`logcheck` 可以通过 `cron` 按间隔运行，而不是持续运行。

`logcheck` 附带了多个不同版本 UNIX 和 Linux 的示例数据库。即使你不想使用实际脚本，也值得查看这些模式，看看是否有你想借鉴的模式。

这些工具的缺点是每次只能处理单个日志文件。如果你 `syslog` 配置将消息排序到多个不同文件中，你可能希望将一些消息复制到一个经常截断或轮转的中央文件中，然后使用该汇总文件来提供后处理脚本。这比设置复杂的脚本网络来处理多个文件更容易。

`Splunk` (`splunk.com`) 将来自许多不同来源的日志和状态消息整合到一个可搜索的消息数据库中。基本版本是免费的。

`SEC`（Simple Event Correlator，简单事件关联器）是一种不同类型的日志管理工具。它是一个 Perl 脚本，从文件、命名管道或标准输入读取行，并通过将行与正则表达式匹配，将它们转换为各种类别的“输入事件”。然后，配置规则指定输入事件应如何转换为输出事件，例如执行特定脚本或向指定管道或文件发送消息。

`SEC` 发行版可从 `kodu.neti.ee/~risto/sec` 获取，并包含带有示例的详尽手册页。网站上还提供了其他示例。`SEC` 不像上面列出的其他工具那样“开箱即用”，但它是构建自定义日志分析工具的良好基础。
