
```
$ ac
```

此命令根据 `/var/log/wtmp` 文件中的登录/注销情况打印连接时间。它可以打印单个用户或组的连接时间，以及总连接时间。`ac` 命令的用法是：`ac [options]`。常用的选项列在表 4.4 中。

## Sa

`sa` 命令汇总了所有命令的信息。它还将数据合并到 `savacct` 和 `usract` 中。切换开关用于显示输出。

```
语法：sa [options]
```

`sa` 的输出字段列在表 4.5 中。表4.5

| 字段标签 | 目的 |
|---|---|
| cp | 系统时间和用户时间的总和。 |
| re | 实际时间。 |
| k | 以 k 单位的平均 CPU 时间使用率。 |
| k* | CPU 时间（千秒）。 |
| avio | 平均 I/O 操作数。 |
| tio | I/O 操作总数。 |
| u | 用户时间。 |
| s | 系统时间。 |

```
$ sa
```

此命令按系统时间和用户时间的总和对输出进行排序。

```
$ sa -l -debug
```

此命令将用户时间和系统时间分开（默认情况下，它们相加并放在 `cp` 字段下）。它还显示用于调试的内部信息。

```
$ sa -f -v 5
```

此命令打印所有执行五次或少的命令。不再等待用户输入（`'y'` 将特定命令添加到“垃圾”组），所有回答均视为肯定。

表 4.6 `sa` 命令选项

| 选项 | 目的 |
| --- | --- |
| -b | 按用户时间和系统时间总和除调用次数对输出进行排序。 |
| -c, --percentages | 打印命令系统、用户和实际时间的百分比。 |
| -D | 按 l/O 对输出进行排序。 |
| -i | 不从 `savacct` 读取信息。 |
| -m | 按用户打印进程数、墙钟分钟和 CPU 分钟数。 |
| -n | 按调用次数对输出进行排序。 |
| -s | 将汇总的统计合并到 `savacct` 和 `usract`。 |
| -u | 打印统计文件中列出的每个命令的用户 ID 和命令名称。 |
| --other-savacct-file filename | 使用指定的文件名代替 `savacct`。 |
| --other-usracct-filename | 使用指定的文件名代替 `usacct`。 |
| --other-filename | 使用指定的文件代替 `acct/pact`。 |
| -h | 帮助。 |

## last

`last` 命令读取 `/var/log/wtmp` 并打印自 `wtmp` 文件创建以来所有登录和注销用户的连接时间。默认情况下，输出按最近到最远的条目进行排序。可以将用户名或 tty 名称作为参数，在这种情况下，将仅列出相应的条目。用户的重启、关机和登录情况记录在 `/var/log/wtmp` 中。`last reboot` 命令列出所有重启时间。`last` 命令的常见用法显示在表 4.7 中，并附有详细的选项列表。

语法：`last [options]`

### 示例

```
[sai@vis sai]$ last -n 6
assureddi pts/0 jar       Fri Feb 25 13:03 still logged in
wptate  pts/5 jar       Fri Feb 25 12:50 - 12:50 (00:00)
sai      pts/4 jar       Fri Feb 25 12:43 still logged in
subbaa pts/3 jar       Fri Feb 25 12:19 still logged in
wptate  pts/2 jar       Fri Feb 25 12:09 still logged in
ivd      pts/2 130.74.96.77 Fri Feb 25 12:00 - 12:01 (00:00)
wtmp begins Tue Feb 1 00:36:05 2000
[sai@vis sai]$ last -R -n ptm      pts/1
Thu Feb 24 10:09             still logged in
gun      ftp               Mon Feb 21 21:01 - 21:01 (00:00)
gun      pts/0               Mon Feb 21 20:58 - 12:56 (1+15:58)
gun      pts/0               Sun Feb 20 15:23 - 16:20 (00:56)
gun      pts/2               Fri Feb 18 16:21 - 16:24 (00:03)
gun      pts/0               Sun Feb 13 01:02 - 01:08 (00:05)
wtmp begins Tue Feb 1 00:36:05 2000
```

此命令指定主机名并将输出限制为用户图谱的行。

### 表 4.7 last 命令选项

| 选项 | 用途 |
|---|---|
| -n number | 限制显示的行数。 |
| -f filename | 读取文件名而非 `wtmp`。 |
| -R | 从输出列表中移除远程主机名。 |
| -X | 除了普通字段外，还打印运行级别变化、关机和时间变化。 |
| -h, -V | 帮助和版本号。 |

## lastcomm

`lastcomm` 是一个用于显示之前执行的命令信息的工具。这些信息存储在 `/var/log/pacct` 文件中。在不带任何参数执行时，`lastcomm` 将打印 `/var/log/pacct` 中找到的所有信息。它也接受参数来限制显示的信息。第一个参数用于搜索之前执行的命令名称，第二个参数用于搜索执行过命令的用户名称，第三个参数用于搜索执行命令的终端名称。

默认情况下，`lastcomm` 将显示匹配任何给定参数的所有记录。要强制 `lastcomm` 只显示匹配所有参数的记录，必须使用 `-strict-match` 选项。例如，命令 `lastcomm ls root tty0` 将显示任何命令、由 `root` 执行的命令以及在 `tty0` 上执行的任何命令的记录。`lastcomm --strict-match ls root tty0` 将匹配在 `tty0` 上执行的 `ls` 命令。

以下是 `lastcomm` 输出的示例：

```
root      0.00 secs Tue Mar 28 14:40 cat      X
root      2.52 secs Tue Mar 28 14:40 gunzip
epg       ??      0.01 secs Tue Mar 28 14:37 panel     F
epg       ??      0.00 secs Tue Mar 28 14:37 accton    S
root      0.00 secs Tue Mar 28 14:35
```

第一列显示命令名称，后面跟着任何标志 `S`、`F`、`C`、`D` 或 `X`。`S` 标志表示监控进程执行了该命令；`F` 表示它是通过 `fork` 调用创建而没有调用 `exit` 创建的；`D` 表示它被 `SIGTERM` 信号终止。下一列显示执行该命令的用户名称，后面跟跟描述符，`X` 表示命令执行所需的时间，最后是程序终止的时间。

### 选项

| | |
|---|---|
| -strict-match | 只显示匹配所有参数的记录 |
| -user NAME | 显示名为 `NAME` 的用户运行的命令记录 |
| -command NAME | 显示命令 `NAME` 的记录 |
| -tty NAME | 显示在 `tty NAME` 上运行的命令的记录 |
| -file FILENAME | 使用名为 `FILENAME` 的文件而非 `/var/log/pacct` |

## pac

`pac` 命令在 Linux 中提供打印机/绘图机核算。它根据纸张使用和成本打印用户的默认系统使用情况。`pac` 记录了用户在纸张使用和成本方面的默认系统使用情况……（此处原文存在大量重复，翻译时已去重并保留核心含义）。

### 表 4.9 /etc/printcap 条目

| 设置 | 目的 |
|---|---|
| sd=directory | 指定打印溢池目录。 |
| lf=file | 指定错误日志文件。 |
| lp=file | 指定设备文件。 |
| af=file | 指定计费文件。 |
| rw | 指定打印机可以读取和写入信息（可以向电脑发送状态信息）。 |
| ff=string | 指定导致打印机换页的字符串。 |
| fo | 在打开设备时输出换页。 |
| mc#number | 指定允许作业的最大副本数。 |
| mx#number | 指定允许的最大文件大小（块计数）。 |
| sc | 指定防止产生多个副本。 |
| sf | 指定防止换页。 |
| sh | 抑制表头的打印。 |
