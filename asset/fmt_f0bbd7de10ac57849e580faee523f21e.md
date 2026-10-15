
少数几家 Web 公司，如 `Linux Corporate Consulting` (`http://www.corplinux.com`) 和 `Linux Consulting` (`http://www.linux-consulting.com/`)，提供基于付费的支持服务，形式包括定制化的 `Linux` 服务器和客户端机器、`Linux` 系统管理工具和脚本、专用 `Linux` 软件以及 `Linux` 维护。顾问公司的数量正在快速增长。只需简单的网上搜索，就能找到开发您所需的任何 `Linux` 相关软件的顾问。

## 通用 Web 支持

几乎每个发行版都为该发行版的用户或其他有特定发行版问题的人提供至少一个邮件列表。消息发送到相应的列表，列表处理器根据需要将它们发送给该列表的其他成员。这是获取支持信息的一种非常有效的方法。您只需将问题通过电子邮件发送列表；其他人阅读您的帖子并将回复通过电子邮件发送回列表。有时列表处理器会创建列表的摘要版本（digest version），这意味着您不是单独接收每封邮件，而是在等待队列达到容量时收到一封组合帖子。

`Red Hat` 使用名为 `redhat-announce-list`、`redhat-watch-list` 和 `redhat-list` 的列表。该名称意味着发布影响 `Red Hat` 社区的事件。观察列表（watch list）向成员提醒安全问题，而红帽 列表用于通用问题。`redhat-list` 提供摘要格式。有关加入这些列表的信息可以在 `http://www.redhat.com/mailing-lists` 处获得。

`Debian` 发行版的列表多到无法一一列名，但您可以在 `http://www.debian.org/MailingLists/subscribe` 找到关于它们的信息以及如何订阅。

`Core Linux` 有若干个新闻组：通用（General）、硬件兼容性（Hardware Compatibility）、安装（Installation）、网络（Networking）、打印（Printing）、设置/配置（Setup/Config）、德语（German）和其他语言（Other Languages）。要了解这些新闻组的情况，请查看 `http://linux.corel.com/support/online.htm` 上的信息。

`Slackware` 有两个基本列表：`slackware-announce` 和 `slackware-security`。也都提供摘要格式。更多信息可以在 `http://www.slackware.com/lists` 找到。

`SuSE Linux` 也有几个邮件列表，包括用于发布的 `suse-announce`、用于通用讨论的 `suse-linux-e`、`suse-security` 以及 `suse-security-announce`。有关这些列表的信息可以在 `http://suse.com/` 处获得。

## 命令行工具

`Linux` 许多命令行工具来帮助您完成管理工作。本节介绍了帮助您更有效地使用命令的命令行技术，如管道（pipes）、重定向、通配符和波浪号。正如您所看到的，所有这些功能都由 shell 提供，对于 `Linux` 来说，就是 `Bash` shell。

### Bash 命令行功能

分配给用户的 shell 是该用户会话的命令解释器。命令从标准输入读取并由 shell 以特定方式进行解释；相同的命令在不同的 shell 中可能会有不同的解释。`Linux` 中的默认 shell 是 `Bourne Again Shell`，即 `Bash`。`Bash` shell 包含了 `Bourne` shell、`Korn` shell 和 `C` shell 的功能。`Bash` 从 `.bash_profile` 和 `.bashrc` 文件中读取配置，这些文件将在第 5 章结合用户特定启动脚本的背景进行进一步讨论。

`Bash` 像其他 shell 一样，具有某些特性，我们在此进行讨论。这些包括它对环境变量（environment variables）、管道和重定向、通配符（wildcards）、波浪号（tilde）以及历史列表（history list）的使用。

### 环境变量

环境变量是字符串，由 `Bash` 或其他程序设置，使其他程序可以使用这些数据。这些字符串被称为“环境”变量，是因为它们是全局可访问的，因此是环境的一部分。在 `Red Hat Linux` 的 `/etc/profile` 文件中设置了以下变量：

```
PATH
PS1
USER
LOGNAME
MAIL
HOSTNAME
HISTSIZE
HISTFILESIZE
INPUTRC
CALENDAR_DIR
```

`PATH` 变量在多个级别上被重新定义，因为不同的用户需要访问不同的文件和目录。在 `Bash` shell 中设置环境变量有两个步骤：设置值然后将其导出（export）。有时您会看到这是两个独立的命令：

```
HISTSIZE=1000
export HISTSIZE
```

执行以下单个步骤可能会更高效：

```
export HISTSIZE=1000
```

要显示环境变量的当前值，请使用 `echo` 命令：

```
echo HISTSIZE
```

你可以在 `C` 程序中通过 `getenv` 函数来访问这些变量。

## 管道与重定向

管道和重定向是如此强大的工具，以至于发现自己处于一个既不处理管道又处理得糟糕的系统时，会感到非常沮丧。大多数 `Unix` 类操作系统处理管道和重定向的方式都相似。

### 管道

当你在 `Linux` 中执行命令时，该命令会打开三个流。第一个流用于输入，称为标准输入 (stdin)。下一个流用于输出，称为标准输出 (stdout)。最后一个流是错误流，称为标准错误 (stderr)。管道是指将第一个程序的 `stdout` 传递给另一个程序的 `stdin` 的做法。你通过列出第一个命令，后跟一个管道符 ( | )，然后是接收第一个命令输出的命令来实现操作。例如，如果你的任务是备份系统上的某些文件，你可以将 `find` 命令输出的文件列表引导到 `cpio` 命令的 `stdin` 中，提示 `cpio` 只在磁带上存储列出的文件：

```
# find /home/user | cpio -ocvB /dev/st0
```

`find` 命令的输出看起来如下：

- `/home/user`
- `/home/user/.Xdefaults`
- `/home/user/.bash_logout`
- `/home/user/.bash_profile`
- `/home/user/.bashrc`
- `/home/user/calendar`

当此输出被管道到 `cpio` 命令时，这些文件中的每一个都会添加到归档并写入指定为 `/dev/st0` 的磁带驱动器（第一个 `SCSI` 磁带驱动器）。

如果你想排除所有扩展名为 `.au` 的音频文件，可以将 `find` 命令通过 `grep` 命令管道，然后传递给 `cpio` 命令。命令看起来会像这样：

```
# find /home/user | grep -v *.au | cpio -ocvB /dev/st0
```

在这种情况下，`find` 命令输出的文件列表将经过过滤，排除所有以 `.au` 扩展结尾的文件，只将剩余文件添加到归档中。

重定向是指改变流的来源或指向位置的做法。一种常见的用途是将系统日志重定向到控制台并在添加消息时更新它。如果你想让命令的输出指向 `/dev/tty9` 指定控制台设备而不是 `stdout`，你需要输入：

```
# tail -f /var/log/messages > /dev/tty9
```

当你执行此命令时，`tail` 命令的输出将重定向到 9 号控制台，导致系统日志 (`/var/log/messages`) 显示在那里。由于存在 `-f` 参数，当新输出写入系统日志时，它会随之追加。

有时你希望通过重定向从其他地方获取输入，可以使用上述说明的相同原理。假设一个文件包含一个按特定顺序排序的名称列表。通过更改 `sort` 命令的 `stdin`，我们可以让它从文件中读取名称、重新排序，并将它们写入 `stdout`。命令看起来如下：

```
# sort < namelist
```

`sort` 命令必须排在前面，否则 shell 将查找名为 `namelist` 的程序并向你报错。

当你需要从一个地方获取 `stdin` 并将 `stdout` 发送到另一个地方时，可以在同一个命令序列中使用两个重定向操作符。结果与你使用 `cp` 命令相同。使用重定向，它看起来如下：

```
# cat < namelist >newlist
```

重定向最常用的用途之一是将 `stdout` 和 `stderr` 都发送到文件中，以保存数据进行检查。这是一个追踪问题非常有用的工具。这可以针对任何 I/O 流完成，而不仅仅是 `stdout`。使用 `stdout` 和 `stderr` 的命令看起来如下：

```
# backup > backup.log 2>&1
```

上述重定向会导致 `backup.log` 覆盖任何现有文件。如果你想将命令的输出追加到 `backup.log` 而不是覆盖它，你应该使用 `>>` 符号。这种情况下命令看起来如下：
