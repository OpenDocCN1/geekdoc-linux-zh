
## 日志文件管理

虽然日志文件可能包含重要的系统信息，但随着时间的推移，它们可能会占用文件系统上不必要的空间。因此，定期清理日志文件的内容是非常重要的。

不要删除日志文件，因为权限和所有权也会被移除。

在清理日志文件之前，先将其打印并存储在安全的地方以备将来参考是一个良好的习惯。要清理日志文件，记住你可以使用 `>` 重定向符号。以下命令显示了在打印和清理 `/var/log/messages` 日志文件之前的大小：

```
[root@server1 #] ls -l /var/log/messages
-rw------- 1 root root 21705 Jul 14 10:52 /var/log/messages
```

```
[root@server1 root]# # lp -d printer1 /var/log/messages
[root@server1 root]# >/var/log/messages
[root@server1 root]# # ls -l /var/log/messages
-rw-r--r-- 1 root root 0 Jul 14 10:52 /var/log/messages
[root@server1 root]# # _
```

你还可以使用 `cron` 守护进程定期调度执行打印和清理日志文件的命令。

或者，你可以调度 `/etc/logrotate.conf` 文件以及存储在 `/etc/logrotate.d` 目录中的日志文件条目。`logrotate` 命令通常以循环的方式重命名日志文件；日志文件在第一个周期中被重命名为 `test.log.1`，并创建一个新的 `test.log` 来接收系统信息。在第二个周期中，`test.log.1` 被重命名为 `test.log.2`，`test.log` 被重命名为 `test.log.1`，并创建一个新的 `test.log` 文件来接收系统信息。

你可以指定 `logrotate` 保留的日志文件数量。如果 `logrotate` 配置为只保留两份日志文件（例如 `test.log.1` 和 `test.log.2`），则 `test.log.2` 将下一个周期中被删除。

`/etc/logrotate.conf` 文件的示例显示在输出输出：

```
[root@server1 root]# cat /etc/logrotate.conf
# 详情请查看 "man logrotate"
# 每周滚动日志文件
weekly
# 保留 4 周的备份
rotate 4
# 在滚动旧文件后创建新的（空）日志文件
create
# 如果你想压缩日志文件，请取消此行的注释
#compress
# RPM 包将日志滚动信息存入此目录
include /etc/logrotate.d
# 没有包处理 wtmp -- 我们将在这里对其进行滚动
/var/log/wtmp {
    monthly
create 0666 root utmp
rotate 1
}
# 也可以在此处配置系统特定的日志
[root@server1 root]# _
```

### 日志文件管理说明

在前面的输出中，任何 `#` 字符均表示命令并被忽略。其他行表示除非另有说明，此文件中包含的日志以及 `/etc/logrotate.d` 目录中的所有其他文件（`include /etc/logrotate.d`）均为每周滚动一次。此外，会保留四份旧文件。对于 `/var/log/wtmp`，每月滚动一次，保留一个旧文件，并创建一个所有者 `root` 和 `utmp` 且权限为 `0666` 的新文件。

`/etc/logrotate.conf` 文件指定了 `logrotate` 的参数。例如：

```
[root@server1 root]# cat /etc/logrotate.conf
# 详情请查看 "man logrotate"
# 每周滚动日志文件
weekly
# 保留 4 周的备份
rotate 4
# 在滚动旧文件后创建新的（空）日志文件
create
# 如果你想压缩日志文件，请取消此行的注释
#compress
# RPM 包将日志滚动信息存入此目录
include /etc/logrotate.d
# 没有包处理 wtmp -- 我们将在这里对其进行滚动
/var/log/wtmp {
    monthly
create 0666 root utmp
rotate 1
}
# 也可以在此处配置系统特定的日志
[root@server1 root]# _
```

## 表 11-4 系统日志守护进程使用的设施（续）

| 设施 (Facility) | 描述 |
|---|---|
| local07 | 指定本地消息；默认不使用，但可以为自定义用途进行定义 |

表 11-5 显示了按升顺序列出的可用优先级。

## 表 11-5 系统日志守护进程使用的优先级

| 优先级 (Priority) | 描述 |
|---|---|
| debug | 表示来自某个设施的所有信息 |
| info | 表示系统操作产生的普通信息消息 |
| notice | 表示应该注意并以备将来参考的信息，但并未指示存在问题 |
| warning or warn | 表示可能由错误引起的消息，但对系统操作至关重要 |
| error or err | 表示其他未由其他优先级描述的错误消息 |
| crit alert | 表示系统严重错误，如硬件故障；表示应立即纠正的错误，例如损坏的系统数据库 |
| emerg or panic | 表示非常严重的系统状况，通常会向所有用户进行广播 |
