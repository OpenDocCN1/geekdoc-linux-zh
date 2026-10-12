
回滚段优化可能是数据库管理中最难以捉摸的方面之一。即使回滚活动达到了稳定状态且没有明显问题，一个大事务也会导致回滚段错误的发生。这会导致难以消除的回滚段问题。回滚段优化的目标通常涉及：
- 让数据库用户始终找到回滚段来存储其之前的映像而无需等待
- 让数据库用户始终获得完成事务所需的读一致性视图
- 确保数据库回滚段不会产生不 I/O
每个数据库至少包含一个回滚段，即系统回滚段。一旦创建了其他回滚段，该段仅用于数据一致性和事务控制。

## 衡量回滚段 I/O
通常，在尝试优化回滚段性能时，你应该监控以下四个领域：
- 回滚段头的竞争
- 回滚段区段的竞争
- 事务在回滚段内的环绕
- 动态区段分配
上述每个指标都可以使用 `V$` 视图、`STATPACK` 和 `REPORT` 的输出以及 `OEM Performance` 工具进行监控。

## 430 第 8 章 • 优化磁盘 I/O
由于回滚段可用于“撤销”用户的 `DML` 并使用之前的映像恢复原始数据，这些视图中的许多统计信息使用 `undo` 而不是 `rollback segment`。

| Oracle 目标 | 使用动态视图检查回滚段性能 |

## 衡量回滚段头竞争
`Oracle Server` 使用存储在每个回滚段头部事务表来跟踪使用该段存储之前的映像的事务。此头部通常缓存在数据库缓冲区缓存中，用户在尝试存储事务之前的映像时可以访问它。在繁忙的 `OLTP` 系统上，用户可能会等待访问回滚段头，导致事务性能下降。
你可以使用 `V$SYSTEM_EVENT`、`V$WAITSTAT` 和 `V$ROLLSTAT` 动态性能视图以及 `STATPACK` 和 `REPORT` 的输出来衡量这些等待发生的频率。

### 使用 V$SYSTEM_EVENT 视图衡量 Undo 头竞争
`V$SYSTEM_EVENT` 视图通过 `undo segment tx slot` 统计跟踪跟踪回滚段。以下查询显示了如何显示这些信息：
```
SELECT event, total_waits,
  time_waited, average_waited
  FROM v$system_event
  WHERE event like '%undo%';
```

| EVENT TOTAL_WAITS TIME_WAITED AVERAGE_WAIT |
| undo segment tx slot 28070 18 .000641254 |

# 调优回滚段 I/O
该查询表明，访问回滚段头块的平均等待时间为 `.0006` 100分之一秒，基本上为零。
理想情况下，`AVERAGE_WAIT` 统计数据的值应该始终保持在零或接近零。

## 使用 V$WAITSTAT 测量 Undo 头竞争
`V$WAITSTAT` 视图包含块争用的统计信息。这些统计数据中包含了应用程序用户访问回滚段头块时经历等待的计数。以下查询显示了这些信息在 `V$WAITSTAT` 视图中的呈现形式：
```sql
SQL> SELECT class, count
FROM v$waitstat
WHERE class IN ('undo header',
'system undo header')
```

| CLASS | COUNT |
| --- | --- |
| system undo header | 0 |
| undo header | 12 |

`system undo header` 统计数据涉及系统回滚段。`undo header` 统计数据针对非系统回滚段。该查询表明，系统回滚段头没有发生争用，但在 12 次情况下访问非系统回滚段头时发生了等待。
理想情况下，这些等待计数应该始终保持在零或接近零。

## 使用 V$ROLLSTAT 测量 Undo 头竞争
`V$ROLLSTAT` 视图包含有关数据库回滚段行为的详细信息。特别是 `USN`、`GETS` 和 `WAITS` 列，对于测量回滚段头的竞争特别有用。表 8.8 显示了这些列的描述。

#### 432 第 8 章 · 调优磁盘 I/O
表 8.8 显示了这些列的描述。

**用于测量头竞争的 V$ROLLSTAT 列**

| Column | Description |
| --- | --- |
| USN | Undo 段段号，分配给回滚段的内部系统生成的编号 |
| GETS | 用户服务器进程需要访问回滚段头并执行成功的次数 |
| WAITS | 用户服务器进程需要访问回滚段头并经历等待的次数 |

使用这些列，并通过公共列 `USN` 将 `V$ROLLSTAT` 与 `V$ROLLNAME` 视图连接，可以获取每个回滚段的名称，从而构建一个查询来返回数据库中每个回滚段头的获取比例（get ratio）：
```sql
SQL> SELECT n.name, s.usn,
  DECODE (s.waits,0,1
  1-(s.waits/s.gets))
  "RBS Header Ratio"
FROM v$rollstat s, v$rollname n
WHERE s.usn = n.usn
ORDER BY usn;
```

| NAME | USN | RBS Header Get Ratio |
| --- | --- | --- |
| SYSTEM | 0 | 1 |
| RBS01 | 1 | .97 |
| RBS02 | 2 | 1 |
| RBS03 | 3 | 1 |
| RBS04 | 4 | .8425 |
| RBS05 | 5 | 1 |
| RBSBIG | 6 | 1 |

该查询的输出显示，大多数回滚段没有发生访问头部的任何等待。只有 `RBS01` 和 `RBS04` 发生过等待。
`Oracle` 建议调优良好的 `OLTP` 系统，所有回滚段的回滚段头比例应达到 95% 或更高。

## 使用 STATSPACK 测量 Undo 头竞争
`STATSPACK` 工具的输出也为测量回滚段头竞争提供了有用信息。图 8.26 显示了包含回滚段性能统计的 `STATSPACK` 报告示例输出。

### 图 8.26 显示统计信息的 STATSPACK 输出
Rollback Segment Stats for DB: PROD Instance: prnd Snaps: 1 ~2
> "row waits" 的高值表明可能需要回滚段
> 使用 Undo 管理时，在开始和结束快照之间可能不会创建 RBS 等待，因为 RBS 可能根据需要动态创建和删除

| RBS NO | Table Gets | Pct waits | Undo Bytes written | wraps | Shrinks | Extends |
|---|---|---|---|---|---|--|
| 0 | 3.0 | 0.00 | 0 | 0 | 0 | 0 |
| 1 | 10.0 | 0.00 | 132 | 0 | 0 | 0 |
| 2 | 13.0 | 0.00 | 0 | 0 | 0 | 0 |
| 3 | 9.0 | 0.00 | 122 | 0 | 0 | 0 |
| 4 | 9.0 | 0.00 | 118 | 0 | 0 | 10 |
| 5 | 46.0 | 0.00 | 106,992 | 21 | 0 | 0 |
| 18 | 4.0 | 0.00 | 1,620 | 4 | 0 | 2 |
| 19 | 15.0 | 0.00 | 138 | 0 | 0 | 0 |

图 8.26 输出中的 `Pct Waits` 列显示，在尝试访问回滚头时，没有任何操作经历等待。

## 使用 REPORT.TXT 测量 Undo 头竞争
回滚段头统计信息也会写入 `REPORT.TXT`。图 8.27 和 2.8 显示了 `REPORT.TXT` 中包含回滚段争用的部分。

### 图 8.27 显示 undo 等待的 REPORT.TXT
```sql
SQL> buffer wait; 如果等待统计中的 'buffer busy wait' 值较高，则此表将识别哪个 undo_header 发生争用。如果 'undo header' 等待较高，则需要更多回滚段。检查 v$session 以获取发生争用的实际块。
select * from stats$wait
where count != 0;
```

| CLASS | COUNT |
| --- | --- |
| data block | 164 |
| segment header | 3 |
| undo header | 2 |
| undo block | 1 |

### 图 8.28 显示 undo 统计的 REPORT.TXT
```sql
SQL> set lines 189;
set numwidth 19;
Waits_for_trans_tbl 表示你应该添加回滚段。
select * from fromstat;
```

| UNDO_SEGMENT | TRANS_TBL_GETS | TRANS_TBL_WAITS | UNDO_SEGMENT_WRITTEN | SEGMENT_SIZE_BYTES | XACTS | SHRIN | WRAPS |
