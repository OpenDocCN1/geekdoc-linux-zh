

一个 **cron** 配置文件被称为“crontab”，是“cron table”的缩写。单个用户的 crontabs 存储在 **/var/spool/cron/** 下。每个用户最多有一个 crontab 文件：一个用于 root，一个用于 jsmith，等等。Crontab 文件以它们所属用户的登录名命名，cron 使用这些文件名来确定在运行每个文件中的命令时使用哪个 UID。crontab 命令将 crontab 文件传输到该目录以及从该目录传输。

尽管具体实现各不相同，但所有版本的 **cron** 都力求最大限度地减少重新解析配置文件和进行时间计算所花费的时间。**crontab** 命令通过在 crontabs 更改时通知 cron 来帮助保持 cron 的效率。因此，你不应该直接编辑 crontab 文件，因为这可能导致 cron 无法注意到你的更改。如果你遇到 cron 似乎不承认已修改的 crontab 的情况，发送 HUP 信号将强制它在大多数系统上重新加载。

> 有关 syslog 的更多信息，请参阅第 11 章。

**cron** 通常静默地工作，但大多数版本可以保留一个日志文件（通常为 **/var/log/cron** 或 **/var/adm/cron/log**），其中列出了执行的命令以及它们运行的时间。有关日志记录默认值，请参阅第 287 页的表 9.2。

在某些系统上，创建日志文件即可启用日志记录，删除日志文件则关闭日志记录。在其他系统上，日志记录的开关在配置文件中设置。另一种变体是 **cron** 使用 syslog。日志文件增长很快且很少有用：除非你在调试特定问题或有特定的审计要求，否则请保持日志记录关闭。

## 9.2 CRONTAB 文件的格式

系统中所有 crontab 文件共享相似的格式。注释以行首的井号（#）引入。每行非注释行包含六个字段，表示一条命令：

```
minute hour dom month weekday command
```

前五个字段告诉 **cron** 何时运行命令。它们由空白字符分隔，但在 **command** 字段中，空白字符会传递给 shell。时间规范中的字段解释如表 9.1 所示。

**表 9.1 Crontab 时间规范**

| Field | Description | Range |
|---|---|---|
| *minute* | Minute of the hour | 0 to 59 |
| *hour* | Hour of the day | 0 to 23 |
| *dom* | Day of the month | 1 to 31 |
| *month* | Month of the year | 1 to 12 |
| *weekday* | Day of the week | 0 to 6 (0 = Sunday) |

每个与时间相关的字段可能包含

- 一个星号，匹配所有内容
- 一个整数，精确匹配
- 由连字符分隔的两个整数，匹配一个值范围
- 一个范围后跟斜杠和步长值，例如 1-10/2（仅 Linux）
- 逗号分隔的整数或范围列表，匹配任意值

例如，时间规范

```
45 10 * * 1-5
```

表示“周一至周五上午 10:45”。提示：除非你希望命令每分钟运行一次，否则不要在第一个字段中放置星号。

weekday 和 dom 字段存在潜在的歧义需要注意。每天既是星期几也是月份中的某一天。如果同时指定了 weekday 和 dom，则一天只需满足其中一个条件即可被选中。例如，

```
0,30 * 13 * 5
```

表示“每周五每半小时，以及每月 13 日每半小时”，而不是“每周五 13 日每半小时”。

命令是要执行的 sh 命令行。它可以是任何有效的 shell 命令，不应加引号。命令被视为一直延续到行尾，可能包含空格或制表符。

尽管 sh 参与执行命令，但 shell 不作为登录 shell 运行，也不读取 ~/.profile 或 ~/.bash_profile 的内容。因此，命令的环境变量可能与你预期的设置有所不同。如果一个命令在 shell 中执行时工作正常，但在 crontab 文件中引入时却失败，环境很可能是罪魁祸首。如有必要，你始终可以将命令包装到一个设置适当环境变量的脚本中。

百分号（%）在 command 字段中表示换行。只有第一个百分号之前的文本包含在实际命令中。剩余的行作为标准输入提供给命令。

以下是一些合法的 crontab 命令示例：

```
echo 'The time is now `date` > /dev/console
mail -s Reminder evi@anchor % Don't forget to write your chapters.
cd /etc; /bin/mail -s "Password file" evi < passwd
```

下面是一些完整的 crontab 条目的额外示例：

```
30 2 * * 1    (cd /home/joe/project; make)
```

