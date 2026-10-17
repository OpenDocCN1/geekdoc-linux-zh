
LGWR 写入所有在线重做日志后，LGWR 将重新开始写入第一个重做日志组。如果重做日志中的数据没有保存，日志中包含的重做信息将会丢失——限制你执行完整数据库恢复的能力。然而，在归档模式（Archive Mode）下运行的数据库在归档进程（`ARC0`）后台进程将日志内容复制到归档目标之前，不会重用在线重做日志。

7.1 展示了 Redo Buffer 机制的概念。

| Oracle 目标 | 描述性能与安全的权衡 |
| :--- | :--- |
| Oracle 的某些可选重做机制（如重做归档和备用数据库）可能会因为引起额外的 I/O 活动而阻碍性能。然而，使用这些功能导致的任何潜在性能下降，必须与这些功能提供的极大改进的恢复能力进行仔细权衡。不建议在非归档日志模式下运行生产数据库以避免额外的 I/O。 | 日志写进程在管理 Redo Log Buffer 内容方面通常做得很好。然而，接下来的章节将讨论在出现瓶颈时监控和调优这些重做组件的技术。 |

# 图 7.1 概念性重做日志缓冲区机制

![](img/c36db8fbb4893c630ad429a99bfd63e3_365_0.png)

## 调整重做日志缓冲区（Redo Log Buffer）

与共享池（Shared Pool）和数据库缓冲缓存（Database Buffer Cache）不同，重做缓冲区并不由 LRU 机制管理。LRU 列表的传送带概念在这里，重做日志缓冲区的管理机制可以被视为漏斗：事务重做信息从漏斗顶部进入，然后由 `LGWR` 后台进程定期清空漏斗底部。为了跟上进入重做日志缓冲区条目的量，每当发生以下事件时，`LGWR` 都会被将重做日志缓冲区的内容写入磁盘：

- 每当应用程序用户发出 `COMMIT` 命令时
- 每三秒
- 每当重做日志缓冲区填充三分之一时
- 每当重做日志缓冲区中的重做条目信息量达到 1MB 时
- 每当数据库检查点（`checkpoint`）发生时

重做日志缓冲区的大小由 `init.ora` 参数 `LOG_BUFFER` 决定。

![](img/c36db8fbb4893c630ad429a99bfd63e3_366_0.png)

每次执行 I/O 时，`LGWR` 都会写入自上次 `LGWR` 写操作以来添加到重做日志缓冲区的所有重做信息。

## 衡量重做日志缓冲区性能

衡量重做日志缓冲区性能的一种方法是用户服务器进程（Server Processes）在尝试向重做日志缓冲区放置条目时经历的等待次数和长度。这些等待可以在 `V$SYSSTAT` 和 `V$SESSION_WAIT` 动态视图中查看。这些统计信息也可以 `STATPACK` 输出以及由 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 生成的 `REPORT.TXT` 文件找到。

| Oracle Objective | 监控并调整重做日志缓冲区 |

## 使用 V$SYSSTAT 衡量重做日志缓冲区性能

`V$SYSSTAT` 中与调整重做日志缓冲区相关的数据库统计信息包括重做缓冲区分配重试（`redo buffer allocation retries`）、重做条目（`redo entries`）和重做日志空间请求（`redo log space requests`）。

统计信息 `redo entries` 报告了自启动以来用户服务器进程放入重做日志缓冲区中的条目数。统计信息 `redo buffer allocation retries` 指用户服务器进程由于 `LGWR` 尚未将当前条目写入在线重做日志（Online Redo Log），而必须等待并重试放入重做日志区的次数。使用这两个统计信息，可以通过对 `V$SYSSTAT` 执行以下查询来计算重做日志缓冲区重试率（Redo Log Buffer Retry Ratio）：

```SQL
SQL> SELECT retries.value/entries.value "Redo Log Buffer Retry Ratio"
  FROM v$sysstat retries,v$sysstat entries
  WHERE retries.name = 'redo buffer allocation retries'
  AND   entries.name = 'redo entries';
```

重做日志缓冲区重试率

```
.000345
```

理想情况下，你希望服务器进程永远不需要等待访问重做日志缓冲区。该比例值较高或不断增加表明重做日志缓冲区可能需要调整。

Oracle 建议此重做日志缓冲区重试率应小于 1%。

`V$SYSSTAT` 中的统计信息 `redo log space requests` 衡量了 `LGWR` 在从当前在线重做日志切换到下一个时，等待重做日志切换发生的频率：

```SQL
SQL> SELECT name, value
  FROM v$sysstat
  WHERE name = 'redo log space requests'
```

```
name               value
--------------------
redo log space requests  34
```

在重做日志切换期间，`LGWR` 无法清空重做日志缓冲区的内容。这可能导致用户进程在尝试访问重做日志缓冲区时经历等待。如上一节所述，这会产生重试请求。因此，`redo log space requests` 的值较高或不断增加表明你的重做日志可能太小，从而导致重做日志缓冲区重试率上升。这可能指示 I/O 冲突。下一章将讨论 I/O。

Copyright ©2002 SYBEX, Inc., Alameda CA www.syex.com

## 调整重做缓冲区

参考 Oracle9 Database Reference, Release 1 目录 C，“Statistic Descriptions”，获取 `V$SYSSTAT` 中所有统计信息的定义。

![](img/c36db8fbb4893c630ad429a99bfd63e3_368_0.png)

## 确定重做缓冲区的大小

假设你继承了一个用于公司的现有 Oracle 数据库。在检查了共享池和数据库缓存的命中率后，你意识到通过增大这些结构可以提高性能，但服务器没有足够的内存。重做日志缓冲区重试率很低——0.0012。在你放弃向老板要更多内存之前，检查重做日志缓冲区的大小。可能由于重试率低，重做日志缓冲区过大并浪费了内存。

假设你检查了重做日志缓冲区的大小，发现是 10MB。由于重做日志缓冲区填充三分之一就会信号 `LGWR` 写入，任何超过 1MB 的值大部分处于闲置。通过减少重做日志缓冲区的大小，可以将剩余的 9MB 分配给共享池或数据库缓存。这不会消耗额外的内存。

## 使用 V$SESSION_WAIT 衡量重做日志缓冲区性能

与显示整个实例统计信息的 `V$SYSSTAT` 不同，`V$SESSION_WAIT` 显示了用户会话等待的时间和事件。`log buffer space` 指由于 `LGWR` 尚未将重做缓冲区的内容写入在线重做日志，用户会话等待多久才能在重做日志缓冲区放置条目。你可以对 `V$SESSION_WAIT` 和 `V$SESSION` 执行以下查询来按用户监控此活动：

```SQL
SQL SELECT username, wait_time, seconds_in_wait
  FROM v$session_wait,v$session
  WHERE v$session_wait.sid = v$session.sid
  AND EVENT LIKE '%log buffer space%';
```

```
USERNAME SECONDS_IN_WAIT               STATE
USER                 20                WAITING
MATT               213               WAITED SHORT TIME
```

表 7.1 显示了 `V$SESSION_WAIT` 中 `STATE` 的可能值以及这些状态的描述。

## 表 7.1 V$SESSION_WAIT 中列的值和描述

| Value | Description |
| --- | --- |
| WAITING | 会话正在等待。 |
| WAITED UNKNOWN TIME | 上次等待时长未知。 |
| WAITED SHORT TIME | 上次等待小于 1/100 秒。 |
| WAITED KNOWN TIME | WAIT_TIME 列的值为实际等待时间。 |

*在不支持快速计时的操作系统上，除非 `init.ora` 参数 `TIMED_STATISTICS` 设置为 TRUE，否则可能始终不会显示。

与 `log buffer space` 的等待值较高或不断增加可能表明重做日志缓冲区需要调整。

![](img/c36db8fbb4893c630ad429a99bfd63e3_369_0.png)

参考 Oracle9 Database Reference, Release 1 目录 A，“Oracle Wait Events”，获取 `V$SESSION_WAIT` 和 `V$SYSSTAT` 中所有统计信息的定义。
