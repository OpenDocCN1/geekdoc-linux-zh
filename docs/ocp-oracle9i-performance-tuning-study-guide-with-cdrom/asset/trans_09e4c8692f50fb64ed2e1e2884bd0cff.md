

## 图 5.3 显示缓冲区高速缓存命中率统计包的 STATS PACK 输出

![](img/832fbc6aca8b6075843ca6f2356c0a8d_293_0.png)

## 使用 REPORT.TXT 输出

通过运行 `UTLBSTAT.SQL` 和 `UTLESTAT.SQL` 生成的 `REPORT.TXT` 文件还包含一个部分，该部分显示了计算数据库缓冲区高速缓存命中率所需的统计信息。这些统计信息包括与图 5.2 中从 `V$SYSSTAT` 查询的相同的“物理读”（Physical Reads）、“直接物理读”（Physical Reads Direct）、“直接物理读 (LOB)”（Physical Reads Direct (LOB)）和“会话逻辑读”（Session Logical Reads）统计信息。图 5.4 展示了 `REPORT.TXT` 样本的相关部分。

## 图 5.4 显示缓冲区高速缓存统计信息的 REPORT.TXT 输出

```sql
SQL> select ni.name "Statistic", 
2  ni.change "Total", 
3  round(ni.change/(trans.change/2),2) "Per Transaction", 
4  round(ni.change/((start_users + end_users) / 2),2) "Per Logon", 
5  round(ni.change/(to_number(to_char(end_time, 'J'))*60*60*24 -
6  to_number(to_char(start_time, 'J'))*60*60*24 + 
7  to_number(to_char(end_time, 'SSSSS'))) - 
8  to_number(to_char(start_time, 'SSSSS'))), 2) "Per Second"
9  from v$sysstat ni,
10 v$sysstat trans,
11 v$sysstat_dates 
12 where trans.name='user commits'
13 and ni.change != 0
14 order by ni.name;
```

| 统计项 | 总计 | 每事务 | 每次登录 | 每秒 |
|---|---|---|---|---|
| 物理读 | 4832 | 37.33 | 584.00 | 19.38 |
| 直接物理读 | 266 | 1.91 | 25.75 | .99 |
| 直接物理读 (lob) | 22 | .21 | 1.32 | .02 |
| 物理写 | 19950 | 184.72 | 2495.75 | 95.51 |
| 直接物理写 | 206 | 1.91 | 25.75 | .99 |
| 直接物理写 (lob) | 97 | .90 | 1.32 | .42 |
| 非检查点物理写 | 6508 | 60.26 | 813.50 | 31.29 |
| 预取块 | 3107 | 28.77 | 388.38 | 14.94 |
| 进程最后非空闲时间 | 5033083984 | 46602629.48 | 629135498.00 | 24197519.15 |
| 递归调用 | 170049 | 1574.53 | 21256.13 | 817.54 |
| 通过调用/回调获取的行数 | 18223 | 168.73 | 2277.88 | 87.61 |
| 会话连接时间 | 5033083984 | 46602629.48 | 629135498.00 | 24197519.15 |
| 会话逻辑读 | 704252 | 6520.85 | 88031.50 | 3393.83 |
| 会话工作单元内存 | 63572 | 605.30 | 8071.50 | 314.29 |

使用这些统计信息，数据库缓冲区高速缓存命中率的计算公式为：

$1 - \frac{(4832 - 266 - 22)}{704252} = 0.99349$

或者命中率为 99.35%。

### 非命中率性能度量指标

命中率是衡量缓冲区高速缓存性能的有效指标之一。然而，还有几种非命中率指标用于衡量数据库缓冲区高速缓存的性能。这些指标是动态性能视图中找到的与缓冲区高速缓存相关的系统统计信息，以及来自 `STATSPACK` 和 `REPORT.TXT` 的输出。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_294_0.png)

由于这些统计信息可以帮助您找到真正的调优问题点，因此将缓冲区高速缓存命中率作为起点往往比盲目增加缓冲区高速缓存的大小更有效。

以下系统统计信息涉及在数据库缓冲区高速缓存中寻找空闲缓冲区的过程。有三个统计信息用于衡量此活动：

- **空闲缓冲区检查次数 (Free Buffer Inspected)**：用户服务器进程在找到空闲缓冲区之前检查的缓冲区高速缓存中的缓冲区数量。一个密切相关的统计项是 `dirty_buffer_inspected`，它表示用户进程在尝试查找空闲缓冲区时发现的脏缓冲区总数。
- **空闲缓冲区等待 (Free Buffer Waits)**：用户服务器进程在空闲缓冲区检查活动期间经历的等待次数。每当服务器进程必须等待数据库写入器（Database Writer）将脏缓冲区写入磁盘时，就会发生这些等待。
- **缓冲区忙等待 (Buffer Busy Waits)**：用户服务器进程等待空闲缓冲区可用的次数。每当用户服务器进程请求的缓冲区已在内存中但被另一个进程使用时，就会发生这些等待。这些等待可能发生在回滚段缓冲区以及数据和索引缓冲区上。

这些统计信息中任何一个的高值或持续增加的值都表明，用户服务器进程正在花费太多时间在数据库缓冲区高速缓存中搜索和等待访问空闲缓冲区。

可以使用 `V$SYSSTAT` 和 `V$SYSTEM_EVENT` 动态性能视图来监控这些缓冲区高速缓存性能的次要指标。

`V$SYSSTAT` 视图包含有关“空闲缓冲区检查次数”的统计信息，而 `V$SYSTEM_EVENT` 视图包含有关“空闲缓冲区等待”和“缓冲区忙等待”的统计信息。可以使用以下 SQL 语句将这三个统计信息合并到一个查询中：

```sql
SQL> SELECT name, value
2    FROM v$sysstat
3    WHERE name IN ('free buffer inspected')
4    UNION
5    SELECT event, total_waits
6    FROM v$system_event
7    WHERE event in ('free buffer waits','buffer busy waits');
```

| 名称 | 值 |
|---|---|
| 缓冲区忙等待 | 170 |
| 空闲缓冲区检查次数 | 0 |

这些统计信息也包含在 `STATSPACK` 和 `REPORT.TXT` 的输出中。图 5.5 和 5.6 展示了显示这些统计信息的 `STATSPACK` 输出样本。

## 图 5.5 显示空闲缓冲区检查次数统计信息的 STATSPACK 输出

```text
Instance Activity Stats for DB: PROD Instance: prod Snaps: 1 - 2
Statistic                 Total per Second per Trans
---------------------------- ---------------- ------
<snip>
enqueue waits             0      0.0    0.0
execute count            142      0.2    47.3
free buffer inspected     41      0.1    13.7
free buffer requested    704      1.1   234.7
immediate (CR) block cleanout app  0      0.0    0.0
immediate (CURRNT) block cleanup 16      0.0    5.3
<snip>
```

## 图 5.6 显示缓冲区忙等待统计信息的 STATSPACK 输出

```text
Buffer Pool Statistics for DB: PROD Instance: prod Snaps: 1 - 2
-> Standard block size Pools D: default, K: keep, R: recycle
-> Default Pools for other block sizes: 2k, 4k, 8k, 16k, 32k
                                Free                Buffer
        Number of Cache  Buffer   Physical   Physical  Write           Busy
P  Buffers Hit %        Gets     Reads    Writes  Waits Complete Waits Waits
----------------------------------------------------------
D       6,010  100.0     3,165       0          236      2     0       12
```

图 5.7 和 5.8 展示了显示这些统计信息的 `REPORT.TXT` 输出样本。

## 图 5.7 显示空闲缓冲区检查次数统计信息的 REPORT.TXT 输出

```sql
SQL> select nl.name 'Statistic',
2         nl.change 'Total',
3         round(nl.change/(trans.change/2),2) "Per Transaction",    
4         round(nl.change/((start_users + end_users)/2),2) "Per Logon",
5         round(nl.change/to_number(to_char(end_time, 'J'))*60*60*24
6               - to_number(to_char(start_time, 'J'))*60*60*24 -
7               to_number(to_char(end_time, 'SSSSS'))
8               + to_number(to_char(start_time, 'SSSSS'))
9               , 2) "Per Second"
10        from
11           stats$stats nl,
12           stats$stats trans,
13           stats$dates
14        where
15           trans.name='user commits'
16           and nl.change != 0
17        order by nl.name;
```

| 统计项 | 总计 | 每事务 | 每次登录 | 每秒 |
|---|---|---|---|---|
| <snip> |  |  |  |  |
| 队列超时 | 5 | .05 | .63 | .02 |
| 队列等待 | 9 | .08 | 1.13 | .04 |
| 执行计数 | 80502 | 745.39 | 10062.75 | 387.05 |
| 空闲缓冲区检查次数 | 10 | .25 | 1.45 | .13 |
| 空闲缓冲区请求次数 | 17415 | 161.25 | 2176.88 | 83.73 |
| 即时 (CR) 块清除 | 427 | 3.95 | 52.38 | 2.05 |

## 图 5.8 显示缓冲区忙等待统计信息的 REPORT.TXT 输出

```sql
SQL> Rem System wide events for non-background processes (EMON,
SQL> Rem EMON, etc). Times are in hundredths of seconds. Each one of
SQL> Rem these is a context switch which costs CPU time. By looking at
SQL> Rem the Total Time you can often determine what is the bottleneck
SQL> Rem that processes are waiting for. This shows the total time spent
SQL> Rem waiting for a specific event and the average time per wait on
SQL> Rem that event.
SQL> select nl.event "Event Name",
2         nl.event_count "Count",
3         nl.time_waited "Total time",
4         round(nl.time_waited/nl.event_count, 2) "Avg Time"
5         from stats$event nl
6         where nl.event_count > 0
7         order by nl.time_waited desc;
```

| 事件名称 | 计数 | 总时间 | 平均时间 |
|---|---|---|---|
| SQL*Net 客户端消息 | 40057 | 35572 | .89 |
| 队列 | 21 | 4724 | 224.95 |
| 库缓存加载锁 | 18 | 3487 | 193.72 |
| 日志文件切换完成 | 39 | 2672 | 68.51 |
| 数据文件顺序读 | 290 | 2024 | 6.98 |
| 数据库名称 IPC 响应 | 29 | 1476 | 50.90 |
| 日志文件同步 | 98 | 1101 | 11.23 |
| 数据文件随机读 | 450 | 1059 | 2.35 |
| 日志缓冲区空间 | 162 | 1011 | 6.24 |
| 切换日志文件命令 | 5 | 651 | 130.20 |
| 缓冲区忙等待 | 170 | 246 | 1.45 |
| 控制文件顺序读 | 56 | 244 | 4.36 |
| 闩锁释放 | 119 | 195 | 1.64 |

