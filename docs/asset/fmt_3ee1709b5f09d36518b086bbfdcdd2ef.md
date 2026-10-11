
服务名 协议 端口 用户 启动程序 路径 参数

- 服务名：服务的名称。
- 协议：使用的协议类型（TCP 或 UDP）。
- 端口：端口号（可以是多个，例如 `53 tcp/udp`）。
- 用户：以哪个用户身份运行启动的程序。
- 启动程序：要执行的程序文件路径。
- 参数：传递给程序的命令行参数。

配置文件还包含全局选项，可以影响所有服务：

- `onlyfrom`：限制哪些 IP 地址可以连接到服务。
- `allow`：允许哪些 IP 地址连接到服务。
- `sockettype`：指定是否使用 UNIX 域 Socket。
- `tcp`：指定是否使用 TCP 协议。
- `udp`：指定是否使用 UDP 协议。

# 第一部分：用户命令

## access_times

确定服务激活的时间段。区间的格式为 `hour:in-hour:inmin`（连接将在区间的边界接受）。小时范围从 `0` 到 `23`，分钟范围从 `0` 到 `59`。

## log_type

确定服务日志输出的去向。有两种格式：

### log_type

- SYSLOG syslog：日志输出发送到指定设施（facility）的 syslog。如果指定了级别，则消息将按该级别记录，而不是默认的级别 `LOG_INFO`。
- FILE file：日志追加到文件中，如果文件不存在则创建它。可以可选指定两个日志文件大小限制。第一个限制是**软限制**：当超过此限制时，xinetd 会记录一次（如果 xinetd 将日志发送到 syslog，则消息将以 `LOG_ALERT` 优先级级别发送）。第二个是**硬限制**：xinetd 将停止停止该受影响服务的日志记录（如果日志文件是公共日志，则可能会影响多个服务），并记录相关使用情况（如果 xinetd 将日志发送到 syslog，则消息将以 `LOG_ALERT` 优先级级别发送）。如果没有指定硬限制，默认在软限制的基础上增加 1%，但额外大小必须在参数范围内（`LOG_EXTRA_MIN` 和 `LOG_EXTRA_MAX`（定义在 `config.cfg` 中））。

## log_on_success

确定服务器启动和退出时记录的内容（日志条目中始终包含服务 ID）。可以指定以下值的任何组合：

- PID：记录进程 ID（如果服务由 xinetd 实现且没有派生（forking）另一个进程，则进程 ID 将为 `&`）。
- HOBST：记录远程主机地址。
- TIME：记录服务器启动的时间。
- USERID：使用 RFC 931 识别协议记录远程用户的用户 ID。此选项仅适用于多线程流服务。
- EXIT：记录服务器以退出状态或终止信号退出的事实（如果该选项，也会记录进程 ID）。
- DURATION：记录服务的持续时间。

## log_on_failure

确定服务器无法启动时（由于缺少资源或访问控制）记录的内容。日志条目中始终包含服务 ID 以及失败原因。可以指定以下值的任何组合：

- HOBST：记录远程主机地址。

## xinetd

| TIME | 记录服务器启动的时间。 |
| USERID | 使用 RFC 931 识别协议记录远程用户的用户 ID。此选项仅适用于多线程流服务。 |
| ATTEMPT | 记录发生失败尝试的事实。 |
| RECORD | 在服务器无法启动时记录来自远程端的信息。这允许对使用服务的尝试进行监控。例如，登录服务会记录本地用户、远程用户和终端类型。目前支持此选项的服务有 `login`、`shell` 和 `syslog`。 |

## rpc_version

确定 RPC 服务的 RPC 版本。版本可以是数字，也可以是 `number-range` 格式的范围。

## env

该属性的值是 `name=value` 格式的字符串列表。这些字符串将在启动服务器之前添加到环境中（因此，服务器的环境将包含 xinetd 的环境加上指定的字符串）。

## passenv

该属性的值是来自 xinetd 环境的列表变量列表，这些变量将传递给服务器。

## port

确定服务端口。如果为 `/etc/services` 列出的服务指定了此属性，则它必须等于文件中列出的端口号。

你不需要为每个服务指定上述所有属性。服务的必要属性如下：

- socket type
- user（仅针对未列出的服务）
- server（仅针对非内部服务）
- wait
- protocol（仅针对 RPC 和未列出的服务）
- rpc_version（仅针对 RPC 服务）
- port（仅针对未列出的服务）

以下属性支持赋值运算符，另有另外：

- only_from
- no_access
- log_on_success
- log_on_failure
- passenv
- env（不支持 `:=` 运算符）

这些属性可以在服务条目中出现多次。其余属性仅支持 `=` 运算符，且在每个服务条目中最多出现一次。

配置文件还可能包含一个默认条目，其格式如下：

```
{
  <attribute> = <value><value> ...
}
```

此条目为未指定这些属性的服务条目提供默认属性值。可能的默认属性有：

```
log_type (累积效应)
log_on_success (累积效应)
log_on_failure (累积效应)
only_from (累积效应)
no_access (累积效应)
passenv
instances (累积效应)
disabled
```

具有累积效应的属性可以多次指定，每次指定的值都会累加（也就是说，`=` 的作用等同于 `+=`）。除 `disabled` 之外，它们的含义与在服务条目中直接指定时相同。`disabled` 决定即使有条目，服务也是禁用的。

## 内部服务 (INTERNAL SERVICES)

xinetd 提供某些服务。

## 控制 xinetd

xinetd 在接收到信号时会执行某些操作。

- SIGUSR1：导致软重配置。
- SIGUSR2：导致硬重配置。
- SIGQUIT：导致程序终止。
- SIGTERM：终止所有运行中的服务器。
- SIGHUP：导致内部状态更新。
- SIGIOT：导致一致性检查。

## xinetd

在重配置时，日志文件会被关闭并重新打开。这允许移除旧日志文件。此外，以下属性在重配置无法更改：`socket_type`、`wait`、`protocol`。

## 日志格式 (LOG FORMAT)

日志条目是以下格式的行：
`entry: service-id-data`

数据取决于 `entry`。可能的 entry 类型有：

- START：服务器启动时生成。
- EXIT：服务器退出时生成。
- FAIL：无法启动服务器时生成。
- DATA：启动服务器失败且服务器支持 `RECORD` 选项时生成。
- USERID：使用 `USERID` 选项时生成。

在以下格式中，如果使用了相应的选项，则括号内的信息有效。

START 条目的格式为：
`START: service-id [from=%d.%d.%d.%d] [time=%time]`

时间格式为 年/月/日/时:分:秒。

EXIT 条目的格式为：
`EXIT: service-id [type=%d] [pid=%d] [duration=%d(sec)]`

`type` 可以是状态或信号。该数字是退出状态或导致进程终止的信号值。

FAIL 条目的格式为：
`FAIL: service-id reason [from=%d.%d.%d.%d] [time=%time]`

可能的原因包括：

- fork：连续派生尝试失败（该次数是可配置参数）。
- time：时间检查失败。
- address：地址检查失败。
- service_limit：将超过该服务的允许实例数量。
- process_limit：指定了派生进程数量限制并将超过该限制。

DATA 条目的格式为：
`DATA: service-id-data`

记录的数据取决于服务。

- login：remote-user=%s local-user=%s tty=%s
- exec：remote-user=%s verify=status command=%s 可能的状态值为：
    - ok：密码正确。
    - failed：密码错误。
    - baduser：不存在该用户。
- shell：remote-user=%s local-user=%s command=%s
- finger：接收到的字符串或空行。

# 第一部分：用户命令

USERID 条目的格式如下：

USERID: text

text 是远程 RFC 931 守护进程的响应，排除端口号（端口号包含在响应中）。以下是一个示例：

```
# xinetd 示例配置文件
#
defaults {
  log_type = FILE /var/log/servicelog
  log_on_success = PID
  log_on_failure = HOST TIME RECORD
```
