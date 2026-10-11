
Cohesive Systems, 1993年5月20日

# makeactive, makehistory, newsreque

用于恢复 Usenet 数据库的工具

## 概要

```
makeactive [-m list] [-0]
makehistory [-b] [-f filename] [-i] [-o] [-n] [-r s size]
tnmpir [-u -v]
newsreque -a active [-h history] [-d days] [-l] [-n newsfeeds] [-input]
```

## 描述

`makeactive` 调用 `find(1)` 获取新闻树 `/news/spool` 中所有目录的列表。它会丢弃名为 `last+found` 的目录，因为这些目录包含点。它扫描所有其他目录中的全数字文件名，并确定最大和最小数字。程序的输出是一组 `active(5)` 文件行。由于文件名中包含点，无法知道某组是否被修改或禁用。（例如，有一个 `comp.sources.unix` 组，但没有 `comp.sources`。）

如果使用 `-o` 标志，`makeactive` 会读取组名的 active 文件列表并重命名所有组。如果 active 文件有头部，则保留找到的头部。这类似于 `etlink(8)` 的重编号命令，区别是 `indent(8)` 应该被节流或不运行。不要将输出重定向到标准 active 文件使用此标志。

如果使用 `-m` 标志，`makeactive` 尝试尽可能增加最大和最小数字。如果在新闻组中发现了文章，则数字是有效的。如果在新闻组中未发现文章，则保留旧文件中的数字，并将数字设置为高值加一。此标志仅允许在使用 `-o` 标志时使用。

如果发生任何问题，`makeactive` 将以非零状态退出。该程序的典型用法是配合以下 `/bin/sh`：

```
echo "Rebuilding active file"
TEMP=$(tnnmpir /tmp)/act$
if [ f /var/lib/news/active ]; then
  if makeactive -0 $(TEMP); then
    mv $(TEMP) /var/lib/news/active
  fi
else
  if makeactive >$(TEMP); then
    # 编辑以恢复受审核
    # 和别名组。
    mv $(TEMP) /var/lib/news/active
  fi
fi
echo reload "New active file"
```

## makehistory

`makehistory` 重建 `history(5)` 文本文件和相关的 `dbz(3)` 数据库。文本文件的默认名为 `/news/lib/history`；若要指定不同名称，使用 `-f` 标志；`makehistory` 扫描 `active(5)` 文件以确定置存区 `/news/spool/` 内哪些新闻组目录应该被扫描。如果某个组被删除但置存区存在，`makehistory` 会忽略它。程序读取每个文件并为其写入一条历史记录。如果使用 `-b` 标志，`makehistory` 会移除其包含点的历史记录。在使用 `-i` 标志时，`makehistory` 会处理数据库中的任何文章。在输出重定向到数据库时，`makehistory` 会暂停。

# news.daily

# 1345

`nostat`

此关键字禁用由 `innstat` 生成的状态报告（参见 `newslog(8)`）。如果不使用此关键字，状态报告是在获取 `news.daily` 日志之前执行的首要函数。

`noexpire`

默认情况下，会调用 `expire` 来移除旧的新闻文章。使用此关键字将禁用此功能。

`noexplog`

`expire` 通常会将信息附加到 `/var/log/news/expire.log`（参见 `newslog(5)`）。此关键字导致 `expire` 的输出被作为 `news.daily` 输出的一部分进行处理。如果使用了 `expire` 关键字，则此关键字无效。

`flags='expire\args'`

默认情况下，调用 `expire` 时带有参数 `-vt`。使用此关键字会将参数更改为用户指定的参数。如果需要，请务必注意使用多个参数。如果使用了 `expire` 关键字，则此关键字无效。

`nlogs`

在过期处理后，会调用 `saturate(8)` 来处理日志文件。使用此关键字将禁用所有日志处理和日志文件清理操作。程序仅对日志文件进行信息扫描，不会更改其任何内容。如果使用了 `nlogs` 关键字，则此关键字无效。

`norotate`

默认情况下，日志处理负责日志处理中的轮转和清理部分。此关键字将禁用日志处理中的轮转和清理部分。程序仅对日志文件进行信息扫描，不会更改其任何内容。如果使用了 `norotate` 关键字，则此关键字无效。

`noremumber`

此关键字禁用 `retain(8)` 的返回操作。将设置所有新闻组（参见 `active(5)`）的低水位。

`norm`

默认情况下，任何两天未被修改的空 socket将被移除。使用此关键字将禁用此功能。

`nomail`

`news.daily` 会向管理员发送邮件消息。使用此关键字将导致此消息发送到 stdout 和 stderr。脚本使用的所有工具的 stdout 和 stderr 被重定向到文件中。如果文件为空，则不发送消息。

`expireover`

`expireoverflags='expireovern'`

在过期处理后调用 `expireover` 程序以清理数据库。如果使用了 `expireover`，则使用此关键字指定传递给 `expire` 的标志。如果使用了 `delete` 关键字，默认值是 `-z` 以及被删除的文件数；否则默认值为 `-`。

`/full`

在进行任何过期处理之前，会执行由 `gate` 文件指定的程序。典型的用法是使用备选的过期程序并使用 `expire` 关键字。可以指定多个程序；它们按顺序执行。

如果调用了 `sonat`，则会将 `rotate` 关键字传递给它。`expire` 是一个删除文件列表的脚本。文件列表被创建并放入文件管道中，以移除旧数据（通常是 `tastream(8)`）。如果出现问题，新闻消息将发送给管理员。如果没有问题，文件将被移动到 `/var/log/news/expire.log` 并保留在那里（出于安全起考虑），直到第二天。

`innwatch` 是一个在启动时运行的脚本。每五分钟会指定一次平均负载以及池中空闲块和节点数量。如果负载过高或磁盘已满，它将限制服务器性能。当满足条件时，它会解锁服务器。在每次循环中，它都会检查指定的日志文件查看其是否被修改，如果是，则将消息发送给新闻管理员。使用此 `signal(3)` 来接收关键新闻消息也是一个好主意。在接收到中断信号时，`innwatch` 会在文件 `~/innwatch.status` 中报告其状态。

`inncheck` 是一个 `perl(1)` 脚本，用于验证所有网络配置文件的语法和权限。如果没有指定文件，它将检查所有文件。文件名后可以跟一个等号和一个标志，用于指示文件的路径。例如，`news-/top` 在不需要安装的情况下检查新 `newsfeeds(5)` 的语法。`-v` 标志会在检查每个文件时打印信息。如果使用了 `-pedantic` 标志，它将检查文件中是否存在并非严格错误但指示潜在配置问题的遗漏。

如果指定了任何文件，则只检查这些文件的权限。`-noperms` 标志会抑制此行为。如果使用了 `-perms` 标志，脚本将验证所有文件的所有权权限。还可以使用 `-fix` 标志以便输出作为脚本执行。

## 第八部分：管理与特权命令

## 历史

`news.daily` 和本手册由 Landon Curt Null (`chongo@toad.com`) 和 Rich Salz (`rsalz@uunet.net`) 编写。

`inncheck` 由 Brendan Keefe (`brendan@uunet.net`) 编写。

## 作者

Landon Curt Null (`chongo@toad.com`) 和 Rich Salz (`rsalz@uunet.net`) 编写了 `news.daily` 和本手册。

Brendan Keefe (`brendan@uunet.net`) 编写了 `inncheck`。

## 另请

`active(5)`, `expire(8)`, `inncheck(1)`, `innwatch(8)`, `newsfeeds(5)`, `newslog(5)`, `saturate(8)`, `signal(3)`, `retain(8)`。

# 第八部分：管理与特权命令

## 概要

```
nnrpd [ -r reason ] [-s title padding] [-S host] [-t]
```

## 描述

`nnrpd` 是一个用于新闻阅读器的 NNTP 服务器。它在标准输入上接受命令，并在标准输出上进行响应。它由 `init(8)` 调用，并将这些描述符附加到远程客户端连接上。

如果使用 `-r` 标志，则 `nnrpd` 将接收到的连接原因作为文本。当 `init` 处于暂停或节流状态时，会使用此标志。

与 `init` 不同，`nnrpd` 接受所有用于用户读取和发布的 NNTP 命令。
