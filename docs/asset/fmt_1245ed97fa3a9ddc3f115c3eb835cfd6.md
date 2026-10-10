
此时 `postmaster` 将处于“静默模式”。注意最后一个示例结尾没有和符号（`&`），所以 `postmaster` 将在前台运行。

# 第9章 Linux 上的 PostgreSQL

## 使用 pg_options

可选文件 `data/pg_options` 包含了后端用于控制跟踪消息和其他后端可调参数的运行时选项。后端在收到 `SIGHUP` 信号时会重新读取该文件。

这使得能够在无需重启 `Postgres` 的情况下动态更改运行时选项。该文件中指定的选项可能是 `trace` 包（`backend/utils/misc/trace.c`）使用的调试标志，也可能是后端用于控制其行为的数值参数。这些选项在后端启动时初始化为零。所有新后端在启动时都会读取新的或修改后的选项。要使对正在运行的后端的更改生效，我们需要向主进程（`postmaster`）发送一个 `SIGHUP` 信号。该信号将自动发送到所有后端。我们也可以通过直接向特定后端发送 `SIGHUP` 来激活该后端的更改。

也可以通过 `Postgres` 的 `-T` 选项来指定 `pg_options`：
`postgres options -T "verbose=2,query,hostlookup-"`

用于打印错误和调试消息的函数现在可以利用 `syslog(2)` 功能。打印到 `stdout` 或 `stderr` 的消息将带有时间戳前缀，且包含后端的 `pid`：

```
#timestamp #pid #message

980127.17:52:14.173 [2971] StartTransactionCommand

980127.17:52:14.174 [2971] ProcessUtility: drop table t:

980127.17:52:14.186 [2971] SIInCNumEntries: table is 70% full

980127.17:52:14.186 [9286] Async_NotifyHandler

980127.17:52:14.186 [9286] Waking up sleeping backend process

980127.19:52:14.292 [9286] Async_NotifyFrontend

980127.19:52:14.413 [9286] Async_NotifyFrontend

980127.19:52:14.466 [9286] Async_NotifyHandler done
```

这种格式提高了日志的可读性，并让人们能够确切了解哪个后端在什么时间做了什么操作。它也便于编写简单的 `awk` 或 `perl` 脚本，通过监控日志来检测数据库错误或问题，或计算事务统计信息。

打印到 `syslog` 的消息使用日志设施 `LOG_LOCAL`。`syslog` 的使用可以通过 `syslog` `pg_option` 控制。遗憾的是，许多函数直接调用 `printf()` 将消息打印到 `stdout` 或 `stderr`，而这些输出无法重定向到 `syslog` 或在其中包含时间戳。建议将所有对 `printf` 的调用替换为 `PRINTF` 宏，以便我们统一控制所有输出。

`pg_options` 文件的格式如下：

```
# comment

option=integer_value # 为选项设置值

option # 设置选项 = 1
```
