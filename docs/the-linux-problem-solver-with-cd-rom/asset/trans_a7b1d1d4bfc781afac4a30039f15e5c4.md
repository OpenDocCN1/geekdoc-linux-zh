

这里 n 是在单个备份客户端上同时运行的备份连接的限制。你可以通过让机器同时备份两块磁盘来使其过载（“ thrash”），尤其是在其中一块磁盘是系统磁盘或具有活动交换空间时（即使你不使机器过载，也会使其变慢）。为了更精细地控制哪些磁盘和机器可以并行备份，你也可以通过在 amanda.conf 文件中的 dumptype 声明中包含它来按备份设置 maxdumps（然后在 disklist 文件中选择适当的转储类型）。计算 maxdumps 没有精确的公式；实际上，它应该大致是你正在备份的每台机器的磁盘数量。

## netusage limit

以每秒网络使用量指定限制，如 1000 Kbps。请记住注意默认值，因为对于现代系统来说它可能太小了。

## Restoring Files with amrecover

使用 amrecover 从磁带获取丢失文件是首选方式，这是一个与 restore 类似工作的程序。要启动它，运行

```
# amrecover config -t $TAPE
```

其中 config 是你想要使用的配置名称（这也会测试你对 /etc/inetd.conf 的修改）。如果一切正常，你会得到类似这样的响应（这里，atlantic 是磁带服务器）：

```
AMRECOVER Version 2.4.1p1. Contacting server on atlantic ...
220 atlantic AMANDA index server (2.4.1p1) ready.
200 Access OK
Setting restore date to today (1999-11-29)
200 Working date set to 1999-11-29.
200 Config set to daily.
200 Dump host set to atlantic.
Can't determine disk and mount point from $CWD
amrecover>
```

首先确定转储主机（即丢失文件的机器）是否正确；如果不正确，在 amrecover> 提示符下输入

```
sethost host
```

让它查看 host 上的文件系统。接下来你将输入

```
setdisk disk
```

设置目录（在上述主机上）文件曾经所在的位置。你可能还想指定 `setdate yyyy-mm-dd` 来查看特定日期的文件索引（而不是最近的）。现在你可以使用 `cd` 和 `ls` 来浏览备份中目录的内容。当你找到想要从归档中提取的文件或目录时，使用 `add name` 将 name 添加到要提取的文件或目录列表中。继续浏览归档，直到你对想要恢复的所有内容都使用了 `add`，然后输入 `list` 来确认你的选择。当你准备好时，输入 `extract` 从归档中提取文件。你需要回答几个问题；这里有一个示例对话：

```
Extracting files using tape drive /dev/nst0 on host atlantic.
The following tapes are needed: dailytapes01

Restoring files into directory /tmp
Continue? [Y/n]: y

Load tape dailytapes01 now
Continue? [Y/n]: y
...
```

回答完问题后，Amanda 会为你从磁带上抓取数据（在这个例子中，它将文件恢复到 /tmp 下；如果你不喜欢这样，使用 `lcd` 更改本地工作目录）。请记住，恢复通常需要一段时间。

使用 `help` 命令访问 amrecover 的在线帮助；它相当简略，但在需要时可以给你一点提示。

相关手册页：amrecover (8), amrestore (8)

## Using Amanda Log Files for Recoveries if amrecover Is Unavailable

如果 Amanda 实用程序 amrecover 和 amrestore 不可用，你可以直接从磁带上提取归档。为此快速进行，你需要访问日志文件（当然，你应该已经熟悉它们的诊断信息）。

一旦你找到了一个（我们称之为 logfile）具有适当的文件日期，找到开头附近类似这样的行：

```
START taper datestamp 19991110 label Daily05 tape 0
```

该行告诉你使用哪盘磁带。现在你必须弄清楚磁带上的哪个文件号是你正在寻找的，因此找到 logfile 中与磁带相关的部分：

```
# grep 'SUCCESS taper' logfile > /tmp/stuff
```

现在你必须找到对应于你想要恢复的机器和目录的行。为此在 vi 中快速操作，使用 `view /tmp/stuff`（以只读方式调用 vi），使用 `/dir` 命令搜索目录，并在光标位于正确行时按下 CTRL-G。行号会出现在编辑器底部。

一旦你找到了它，你就找到了磁带上的文件号——由于 Amanda 使用第一个文件（即 0）对磁带进行索引，文件号应与行号相同。

## 8.5 Crash Recovery

这听起来可能有点陈词滥调，但如果你遇到系统上的严重问题，不要惊慌。除了有人用大锤对你的硬盘进行“精细调整”之外，让系统重新上线只是将文件放回原位的问题。

在着手修复系统问题之前，确保你对问题是什么以及如何修复有非常清晰的认识。例如，如果你删除了 init 程序，你应该计划启动机器以便访问文件系统（以及 init 的副本）并将 init 放回去。但不要过度计划：更常见的是，你认为会完美奏效的方法根本行不通。

### The Rescue CD-ROM

除了包含本书其他章节引用的工具外，随附的 CD-ROM 还可以启动你的系统并提供一堆崩溃恢复工具。

### Creating a Boot Floppy

