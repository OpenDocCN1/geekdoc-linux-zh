
是否显示性能数据？默认是 `perfdat`。

## logfilocry

如果日志文件不存在，`check_logfile` 输出 `UNKNOWN`，遵循默认 `logfilocry`。参数 `nfilocry` 告诉插件在文件缺失时省略错误消息。

## case nocase

忽略大小写。默认的 `case` 与此相反。

## sticky=seconds

使用此选项，`check_logfiles` 在指定的时间内记录错误状态。通常，后续未发现匹配项的检查将返回 `OK`，导致管理员可能忽略重要的条目。

假设你只有在日志文件中两小时没有更多匹配项时才接受。带有 `sticky=7200` 的检查将宣布最多两小时的错误状态。如果期间没有新条目重启两小时的时间限制，`check_logfiles` 将返回 `OK`。

如果搜索模式包含 `okpattern`，`check_logfiles` 在匹配后将直接返回 `OK`，即使在指定时间过期之前也是如此。

## savethresholdcount

如果事件未达到阈值选项所需的匹配次数，则不会宣布错误。问题在于如何处理整体匹配。`savethresholdcount`（默认）会保存匹配次数到下次检查，并累加直到达到阈值并触发错误。参数 `nosavresholdcount` 防止事件计数器在检查之间始终重置为零。

## 7.6 监控登录用户数量

`check_users` 插件用于监控登录用户数：

```
user@linux:nagios/libexec$ ./check_users -w 5 -c 10
USERS CRITICAL - 20 users currently logged in |users=20;5;10;0
```

它只有两个选项：

- `-w number` / `--warning=number`

  这是登录用户数的阈值，超过该数量后插件将发出警告。

- `-c number` / `--critical=number`

  这是严重状态的阈值，通过登录用户数来衡量。

`|` 之后的性能数据像常一样只在命令行中可见；Nagios 不将其包含在 Web 界面中。

## 7.7 检查系统时间

### 7.7.1 通过 NTP 检查系统时间

`check_ntp` 和 `check_ntp_time` 插件将本地计算机的时钟与网络中可用的 NTP 服务器进行比较。如果 Nagios 服务器通过 NTP 准确同步时间，使其本身可以作为参考，那么它也可以作为网络插件使用，前提是网络中被检查的主机已安装 NTP 守护进程。

从 1.4.11 版本开始，`check_ntp_time` 和 `check_ntp_peer`（6.12 使用 `check_ntp_peer` 进行 NTP 服务器健康检查，第154页）替换了 `check_ntp`，后者包含了两个功能：本地系统时间与 NTP 服务器的比较，以及 NTP 服务器本身的健康检查。这里的选项同时适用于 `check_ntp` 和 `check_ntp_time`。

在最简单的情况下，调用 `check_ntp` 并指定要与本地计算机时间比较的计算机（此处：`ntpserver`）：

```
nagios@linux:nagios/libexec ~check_ntp -H ntpserver
NTP Offset -0.00950574924 secs (offset=-0.0095056s;60.000000;12.000000
```

这里的偏差表示最多 9.5 毫秒，这是一个很好的值。高偏差取决于具体的预期用途。如果你想比较几台计算机的日志文件条目，它们应当经过 NTP 同步。你完全可以使用 `-w 1 -c 2`，将两秒的偏差设为严重。在使用 Kerberos 进行身份验证的环境中，所有涉及主机的时间同步非常重要，但不如“严重”那么关键：Windows Server 2003 下的 Microsoft Active Directory 容忍五分钟的最大偏差，只有当出现更大的偏差时才会出现真实问题。

`check_ntp_time` 和 `check_ntp` 有以下选项：

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

```
-q / --quiet (仅限 check_ntp_time)
```

如果 NTP 服务器由于某种原因未提供偏移量，则返回 `UNKNOWN` 而不是 `CRITICAL`。

### 7.7.2 使用时间协议检查时间

除了网络 NTP，还有另一种更老、更简单的协议：RFC 868 中描述的时间协议，其通信通过 TCP 端口进行。在许多 Unix 系统中，服务器集成在守护进程中，因此不需要启动单独的守护进程。通过 `check_time`，Nagios 提供了一个相应的插件。

`check_time` 也可以作为网络插件使用，方式与 `check_ntp` 类似，但它假设时间服务对每个客户端都是可用的。在大多数情况下，它被用作本地插件，将其自己的时间与中心时间服务器进行比较（此处：`timesrv`）：

```
nagios@linux:nagios/libexec/~check_time -H timesrv -w 10 -e 60
TIME CRITICAL --1160 second time difference|time=0;offset=1160;0
```

`|` 之后的性能数据不在 Web 界面中显示，包含响应数（此处：零）；`offset` 描述了与时间服务器的差异（此处：1160 秒）。由于我们没有用 `-w` 或 `-c` 设置任何阈值，`check_time` 有以下选项：

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

```
-q / --quiet (仅限 check_ntp_time)
```

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

```
-q / --quiet (仅限 check_ntp_time)
```

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
