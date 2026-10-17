
```sql
SQL> SELECT DECODE(totalq_0, 'TOTALq IS ZERO',
2  FROM v$queue q, v$dispatcher d
3  ROUND(SUM(wait)/SUM(totalq),4) 'AVG DISPATCHER WAIT'
4  WHERE q.paddr = d.paddr
5  AND q.type = 'DISPATCHER'
6  GROUP BY totalq;

AVG DISPATCHER WAIT
-------------------
             .0093
```

此输出显示，平均而言，用户进程等待分发程序进程处理其数据库请求的时间为 .0093 百分之一秒。

> 对分发程序进程的等待时间高或呈增加趋势，可能表明需要在实例启动时生成更多的共享服务器进程。

上述针对 `V$QUEUE` 和 `V$DISPATCHER` 查询所指示的等待时间是分发程序争用的迹象。要确定共享服务器环境中是否正在发生分发程序争用，可以通过查询 `V$DISPATCHER_RATE` 动态性能视图来获得额外证据。下表 6.6 展示了该视图中对监控分发程序争用有用的选定列。

### 表 6.6 `V$DISPATCHER_RATE` 的选定列

| 列名 | 描述 |

|---|---|

| NAME | 分发程序名称 |

| CUR_IN_CONNECT_RATE | 分发程序当前处理来自应用程序用户请求的速率 |

| MAX_IN_CONNECT_RATE | 分发程序处理来自应用程序用户请求的最大速率 |

图 6.6 展示了一个针对 `V$DISPATCHER_RATE` 的查询，该查询比较了处理客户端请求的当前速率与处理客户端请求的最大速率。

## 图 6.6 当前与最大分发程序服务速率

```sql
SQL> SELECT name, cur_in_connect_rate, max_in_connect_rate,
           cur_in_connect_rate - max_in_connect_rate "VARIANCE"
    2  FROM v$dispatcher_rate;

NAME  CUR_IN_CONNECT_RATE MAX_IN_CONNECT_RATE VARIANCE
D000          12      22      10
D001           8      19      11
D002          11      28      17
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_343_0.png)

当前与最大分发程序服务速率之间的较大差异表明，可能需要额外的分发程序进程来改进共享服务器性能。

`V$SHARED_SERVER_MONITOR` 动态性能视图提供了共享服务器环境累积活动的概览。该视图包含五个列，如表 6.7 所示。

### 表 6.7 `V$SHARED_SERVER_MONITOR` 的列

| 列名 | 描述 |

| :--- | :--- |

| MAXIMUM_CONNECTIONS | 自实例启动以来，共享服务器选项使用的最大虚拟电路数 |

| MAXIMUM_SESSIONS | 自实例启动以来，已使用的最大共享服务器会话数 |

| SERVERS_STARTED | 自实例启动以来，由共享服务器选项自动启动的额外共享服务器总数——超出了由 `SHARED_SERVERS` init.ora 参数指定的共享服务器数量 |

| SERVERS_TERMINATED | 自实例启动以来，由共享服务器选项自动关闭的共享服务器总数 |

| SERVERS_HIGHWATER | 自实例启动以来运行的最大共享服务器数量——既包括在 init.ora 中显式启动的，也包括由 `PMON` 隐式启动的 |

图 6.7 展示了对 `V$SHARED_SERVER_MONITOR` 视图的示例查询。

## 图 6.7 显示共享服务器使用情况的 `V$SHARED_SERVER_MONITOR` 查询

```sql
SQL> SELECT *
2  FROM v$shared_server_monitor;

MAXIM_CONNECT MAXIM_SESSIONS SERVERS_STARTED SERVERS_TERMINATED SERVERS_HIGHWATER
             22             20               2                  1                  5
```

图 6.7 中查询的输出表明，当对由 `SHARED_SERVERS` init.ora 参数指定的三个共享服务器的需求无法满足应用程序用户的需求时，实例启动了两个额外的共享服务器进程。这两个动态启动的共享服务器中有一个在系统需求下降后自动关闭。

> **提示** `SERVERS_HIGHWATER` 的值与 init.ora 中 `SHARED_SERVERS` 的值之间的较大差异表明，应增加 init.ora 中 `SHARED_SERVERS` 的值。

偶尔，您可能需要跟踪用户进程从用户进程到分发程序，再到分配的共享服务器，再回到用户进程的路径。图 6.8 展示了如何使用 `V$CIRCUIT`、`V$SESSION`、`V$DISPATCHER` 和 `V$SHARED_SERVER` 之间的公共列连接这些视图，并构建这样的查询。

## 图 6.8 显示用户进程电路的查询

```sql
SQL>  SELECT s.username, d.name "DISPATCHER", ss.name "SHARED_SERVER"
     2  FROM v$session s, v$circuit c, v$dispatcher d, v$shared_server ss
     3  WHERE s.saddr = c.saddr
     4  AND    c.dispatcher = d.paddr
     5  AND    c.server = ss.paddr;

USERNAME    DISP  SHAR
---------   ----- ----
SYSTEM      D003  S000
JOE         D003  S001
BRENDA      D001  S002
EMILY       D000  S000
MATT        D002  S001
```

使用此查询的输出，您可以看到 Emily 的会话正在利用分发程序 D000 和共享服务器 S000 来处理她的数据库请求。此信息对于故障排除 Emily 会话潜在的性能问题可能有用。

一旦使用上述指标确定了当前的分发程序和共享服务器性能，就可以考虑下一节中讨论的调整措施，以改进共享服务器功能的性能。

## 改进共享服务器性能

共享服务器架构的性能问题通常与以下领域之一有关：

- SGA 组件未按共享服务器环境的需求进行适当调整

- 运行的共享服务器数量太少，无法充分处理用户请求

- 运行的分发程序数量太少，无法充分处理用户请求

在所有这些情况下，调整方案都属于“扩大规模”类别。以下章节将讨论每种情况。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_345_0.png)

Oracle 的共享服务器选项应被视为一种*垂直扩展*（scale up）特性，而非*提速*（speed up）特性。换句话说，虽然共享服务器特性允许您更好地利用可用的服务器资源，从而允许您使用相同的资源支持更多的应用程序用户，但它并不一定会同时提高系统的整体吞吐量或响应时间。

## 增加相关 SGA 组件的大小

由于共享服务器基于语句而非事务进行操作，通常在专用服务器配置下位于用户进程全局区域（PGA）内的用户全局区域（UGA）中的用户会话和游标状态信息（例如绑定变量值和会话设置），在共享服务器配置下会移动到 SGA 中的共享池。如您在第 4 章中学到的，共享池的主要功能是缓存 SQL 语句和数据字典信息。当共享服务器 UGA 信息的缓存被添加到共享池时，共享池的命中率可能会下降。因此，至少，当实施共享服务器选项时，共享池的大小必须增加。

- Oracle

- 目标

- *描述 UGA 和会话内存的考虑因素*

共享池应增加的数量可以通过查询 `V$SESSTAT` 和 `V$STATNAME` 动态性能视图来确定。以下查询可用于确定自实例启动以来用于存储用户会话和游标状态信息的最大内存量：

```sql
SQL> SELECT SUM(value) "Total UGA Bytes"
 2  FROM v$sesstat s, v$statname n
 3  WHERE n.name = 'session uga memory max'
 4  AND s.statistic# = n.statistic#;

Total UGA Bytes
365852
```
