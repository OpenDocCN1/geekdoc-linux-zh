
### 描述

`mailp` 命令是 Solaris 8 运行环境中新出的命令，是 `mp(1)` 程序的前端。`mailp` 命令具有与 `mp` 选项不同的名称，描述如下：

- `mailp` 打印邮件消息。
- `newsp` 打印 USET 文章。
- `digestp` 打印 USenet 摘要文件。
- `filep` 打印普通 ASCII 文件。
- `ofilaxp` 按 Filofax 个人组织工具格式打印。
- `franklin` 按 Franklin Planner 个人组织工具格式打印。
- `timeman` 按 Time Manager 个人组织工具格式打印。
- `timesysp` 按 Time/System International 个人组织工具格式打印。

`mailp` 相关程序按顺序读取每个文件名，并生成内容的美化版本。如果你没有提供文件名参数，`mailp` 以以下两种方式工作：

- 使用 `-D` 选项，它作为 X 打印服务器客户端，产生目标打印机的 PDL 并将其置入。
- 使用 `-d` 或 `-P` 选项，它生成并置置 PostScript 输出。

# `mailp`

## 763

### 选项

- `-d printer` 将输出发送到指定的打印机。否则，将输出发送到 `PR` 环境变量中 PDL 指定的打印机。
- `-D` 为目标打印机生成输出并将其置置到打印机。
- `-F` 不再打印邮件文章收件者的名称，顶部头部显示邮件文章发件者的名称。此选项对于有自己个人打印机的人很有用。
- `-h` 禁用横幅打印。通常出现在横幅页上的大部分信息都在 `mp` 横幅中输出。
- `-1` 以横向模式格式输出，并在纸上打印两页文本。
- `-P printer` 与 `-d` 选项相同。为了向后兼容，在 `mailp` 中使用的 `-P` 选项（在 `mp(1)` 中直接将 PDL 置置到目标打印机）会产生 PostScript。
- `-s subject` 使用作为打印输出的新主题。在打印命令行上指定的普通 ASCII 文件时，主题默认为每个文件名。

### 操作数

- `filename` 要读取的文件名。

## 环境变量

如果你没有指定 `-d`、`-D` 或 `-P` 选项，`mailp` 使用 `PRINTER` 变量来确定接收 `mp(1)` 程序输出的打印机。如果未找到 `PRINTER` 变量，默认目标是 PostScript。

## 退出状态

- `0` 成功完成。
- `1` 发生了错误。

### 属性

查看 `attributes(5)` 了解以下属性的描述。

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWmp |

### 相关

- `mp(1)`, `attributes(5)`

# `mailq` — 打印邮件队列

概要
`/usr/bin/mailq` `[-q subarg]` `[-v]`

描述
`mailq` 显示等待交付的邮件摘要。
每条邮件的第一行显示在该主机上使用的内部标识符、邮件大小（字节）、进入队列的时间以及邮件的信发件者。
邮件的第二行显示留在队列中的错误消息。如果是首次处理邮件，则不显示此行。
`mailq` 命令等同于 `sendmail -bp`。从 Solaris 9 版本开始，它检查授权属性 `solaris.mail.mailq`。如果调用用户检查通过，则执行带有剩余参数的 `sendmail -bp`。否则打印错误消息。此属性默认对所有用户启用。可以通过修改 `prof_attr(4)` 中的 Solaris 用户项来禁用它。

### 选项

- `-qp[time]` 与 `-qtime` 类似，不同之处在于不是定期派生子进程处理队列，而是为每个队列启动一个持久的子进程，在处理队列和睡眠之间交替。使用参数指定睡眠时间。如果上一次队列为空，进程至少睡眠 5 秒。Solaris 9 版本新增。
- `-qf` 处理一次队列中的保存邮件，且不派生 `( )` 而在前台运行。Solaris 9 版本新增。
- `-qG name` 仅处理名为 `name` 的队列中的任务。
- `-q[!]I` 限制处理任务为包含队列 ID 作为子字符串的任务。使用 `!` 反转字符串参数。Solaris 9 版本新增。
- `-q[!]R` 限制处理任务为包含收件者之一作为子字符串的任务。使用 `!` 反转字符串参数。Solaris 9 版本新增。
- `-q[!]S` 限制处理任务为包含发件者作为子字符串的任务。使用 `!` 反转字符串参数。Solaris 9 版本新增。

## `mailstats` 765

`-v`
打印详细信息。此选项会在消息的第一行添加消息优先级以及单个字符指示符（`+` 或空格），用于指示是否发送了警告消息。此外，收件人之间可以夹杂指示“控制用户”的额外行；此信息显示了代表此消息执行的任何程序的所有者，以及该命令从哪个别名扩展而来（如果有的话）。

## 退出状态

- `+0` 成功完成。
- `>0` 发生错误。

### 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| Availability | SUNWndmu |

## 参见

`sendmail(1M)`, `prof_attr(4)`, `attributes(5)`

![](img/185d23104c385dfb6a62d64cc96b8997_794_0.png)

## `mailstats` — 打印 sendmail 收集的统计信息

### 语法

```
/usr/bin/mailstats [-o] [-c configfile] [-C configfile] [-f statisticsfile] [-p] [-P]
```

### Description

`mailstats` 命令打印 `sendmail(1M)` 程序收集的关于邮件使用的统计数据。如果 `sendmail` 的 `StatusFile` 配置选项（定义在 `/etc/mail/sendmail.cf` 中）指定的文件存在，则会这些统计数据。`StatusFile` 配置选项是 Solaris 9 版本中新增的。从 Solaris 9 版本开始，默认的统计文件为 `/etc/mailstats`。

`mailstats` 命令首先打印统计文件的创建时间和最后修改时间。然后，它会打印一个表格，单行显示每个发送器（mailer）的统计数据，每行包含以下由空格分隔的字段：

- `M` 发送器编号。
- `msgsfr` 来自发送器的消息数。
- `bytes_from` 来自发送器的字节数（KB）。
- `msgto` 发往发送器的消息数。
- `bytes_to` 发往发送器的字节数（KB）。

![](img/185d23104c385dfb6a62d64cc96b8997_794_1.png)

![](img/185d23104c385dfb6a62d64cc96b8997_794_2.png)

![](img/185d23104c385dfb6a62d64cc96b8997_794_3.png)

## 766

## `mailstats`

- `msgsrej` 被发送器拒绝的消息数。
- `msgsdis` 被发送器丢弃的消息数。
- `Mailer` 发送器的名称。

![](img/185d23104c385dfb6a62d64cc96b8997_795_0.png)

在此显示之后，会显示一行包含所有发送器的数值总和，与之前的信息之间由一条仅包含等号 (`=`) 的行隔开。
要每天重新初始化统计文件，请在 `crontab(1)` 中添加以下条目。

![](img/185d23104c385dfb6a62d64cc96b8997_795_1.png)

```
mailstats -p > /dev/null
```

### Options

- `-c configfile`
- `-C configfile`

指定 `sendmail` 配置文件。`-C` 选项是 Solaris 9 版本新增的。

```
-f statisticsfile
```

指定 `sendmail` 统计文件。

![](img/185d23104c385dfb6a62d64cc96b8997_795_2.png)

- `-o` 不显示发送器名称。Solaris 9 版本新增。

![](img/185d23104c385dfb6a62d64cc96b8997_795_3.png)

- `-p` 以程序可读模式输出信息并清除统计数据。Solaris 9 版本新增。

![](img/185d23104c385dfb6a62d64cc96b8997_794_4.png)

- `-P` 以程序可读模式输出信息但不清除统计数据。Solaris 9 版本新增。

## Examples

以下示例显示了使用 ESMTP 和 Cyrus 发送器的系统输出。

```
$ mailstats

Statistics from Fri Jul 20 14:23:08 2001

M msgsfr bytes_from msgoito bytes_to msgsrej msgsdis Mailer

5 1501 33183K 302 10612K 57 0 esmtp

9 290 23568K 1523 44588K 1 0 cyrus

T 1791 56751K 55200K 58 0

C 1791 1825 58
```
