
以秒为单位的严重阈值，以标准阈值格式指定（24.1.5 指定阈值，第557页）。如果本地时间系统与 NTP 服务器的偏差超过给定秒数（默认 120 秒），状态变为 `CRITICAL`。

`-q` / `--quiet` （仅限 `check_ntp_time`）

如果 NTP 服务器由于某种原因未提供偏移量，则返回 `UNKNOWN` 而不是 `CRITICAL`。

```
-H address / --host=address
```
这是插件应与之比较本地系统时间的 NTP 服务器。

```
-p port / --port=port
```
NTP 服务器运行的 UDP 端口。默认是 123。

```
-w threshold / --warning=threshold
```
这是警告限值，以标准阈值格式指定（24.1.5 指定阈值，第557页）。如果本地时间系统的波动大于指定的阈值，则给出警告。默认为 60 秒。

```
-c threshold / --critical=threshold
```
以秒为单位的严重阈值，以标准阈值格式指定（24.1.5 指定阈值，第557页）。如果本地时间系统与 NTP 服务器的偏差超过给定秒数（默认 120 秒），状态变为 `CRITICAL`。

## 7.8 定期检查邮件队列

`check_mailq` 插件用于监控邮件队列的状态。它可以检查队列中的消息数量、队列的大小以及最旧消息的年龄。

可用选项：

- `-w threshold` / `--warning=threshold`

  这是警告限值，以标准阈值格式指定（24.1.5 指定阈值，第557页）。如果队列中的消息数大于指定的阈值，则给出警告。默认为 50。

- `-c threshold` / `--critical=threshold`

  以消息数为单位的严重阈值，以标准阈值格式指定（24.1.5 指定阈值，第557页）。如果队列中的消息数超过给定值（默认 100），状态变为 `CRITICAL`。

- `-q` / `--quiet` （仅限 `check_mailq`）

  如果邮件队列由于某种原因未提供状态，则返回 `UNKNOWN` 而不是 `CRITICAL`。

`|` 之后的性能数据像常一样只在命令行中可见；Nagios 不将其包含在 Web 界面中。

```
user@linux:nagios/libexec$ ./check_mailq -w 50 -c 100
QUEUE CRITICAL - 120 messages in queue |messages=120;50;100;0
```

## 7.9 关注文件的修改日期

通过 `check_fileage` 插件，你不仅可以监控文件的修改日期，还可以监控大小。在最简单的情况下，只需运行文件名和路径。

```
user@linux:nagios/libexec$ ./check_fileage /var/log/messages -w 240 -c 600
WARNING /var/log/messages is 376 seconds old and 7186250 bytes
```

在这里插件给出警告，因为设置的警告限制为 240 秒，严重限制为 600 秒。文件的最后修改是在 376 秒前——即在警告范围内。

只有在显式指定文件大小警告限制（选项 `-W`）时，`check_fileage` 才会考虑文件大小。如果文件小于给定的限制（字节），则插件可能会给出警告。警告和严重限制的默认都是零。

`check_fileage` 有以下选项：

- `-w integer` / `--warning-age=integer`

  如果文件旧于 `integer`¹（默认为 240 秒），插件发出警告。

- `-c integer` / `--critical-age=integer`
