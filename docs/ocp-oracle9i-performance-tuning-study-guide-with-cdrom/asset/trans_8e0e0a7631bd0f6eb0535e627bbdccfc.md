

表 6.1 中显示的 `init.ora` 参数取代了已弃用的 Oracle8i 参数 MTS_DISPATCHERS、MTS_MAX_DISPATCHERS、MTS_SERVERS、MTS_MAX_SERVERS 和 MTS_CIRCUITS。

虽然 DISPATCHERS 和 SHARED_SERVERS 参数用于在实例启动时建立这些进程的最小生成数量，但两者都可以上调至 MAX_DISPATCHERS 和 MAX_SHARED_SERVERS 指定的上限值。然而，虽然 Dispatcher 进程必须由 DBA 使用 ALTER SYSTEM 命令显式启动，但共享服务器进程可以根据已连接应用程序用户对这些资源的需求，由 PMON 后台进程动态启动和停止。

确定在实例启动时应生成多少个 Dispatcher 和共享服务器，可以通过在初始配置完成后监控共享服务器环境的性能来决定。

数据库管理员不能使用共享服务器连接来执行 DBA 操作，如数据库启动、关闭等。

## 衡量共享服务器性能

一旦配置了共享服务器选项，就必须对其进行监控和调整以获得最佳性能。就像共享池和数据库缓冲区缓存一样，可以使用几个动态性能视图来监控共享服务器环境的性能。这些动态性能视图在表 6.2 中有描述。

### 表 6.2 共享服务器动态性能视图

| 视图名称 | 描述 |
| :--- | :--- |
| V$SHARED_SERVER | 包含关于共享服务器进程的详细统计信息，包括每个共享服务器进程的空闲和忙碌时间。 |
| V$QUEUE | 包含关于共享服务器请求和响应队列争用的信息。 |
| V$SHARED_SERVER_MONITOR | 包含关于共享服务器进程的统计信息，包括自实例启动以来由 PMON 动态启动和终止的共享服务器。 |
| V$DISPATCHER | 包含关于共享服务器 Dispatcher 进程的详细统计信息，包括每个 Dispatcher 进程的空闲和忙碌时间。 |
| V$DISPATCHER_RATE | 包含关于 Dispatcher 活动的历史和实时统计信息。 |
| V$CIRCUIT | 包含用户进程通过 Dispatcher、请求队列、共享服务器、响应队列并返回到用户进程所经过的路径（即电路）的统计信息。 |

上述每个视图都可以用于监控共享服务器架构的两个动态组件：共享服务器进程和 Dispatcher 进程。

Oracle 目标 诊断并解决 Oracle 共享服务器进程的性能问题

## 监控共享服务器进程性能

监控共享服务器进程性能的一种方法是监控可用服务器进程处理数据库请求的速率。这个忙碌比率可以使用 V$SHARED_SERVER 动态性能视图计算得出。该视图中用于监控共享服务器忙碌比率的有用列在表 6.3 中显示。

图 6.2 展示了如何通过查询这些列来计算共享服务器忙碌比率。

### 表 6.3 V$SHARED_SERVER 中的选定列

| 列名 | 描述 |
| :--- | :--- |
| NAME | 共享服务器进程名称 |
| REQUESTS | 共享服务器在运行期间处理的请求总数 |
| BUSY | 共享服务器在运行期间忙碌的总时间（以百分之一秒为单位） |
| IDLE | 共享服务器在运行期间空闲的总时间（以百分之一秒为单位） |

### 图 6.2 计算共享服务器忙碌比率

```sql
SQL> SELECT name, DECODE(busy+idle, 0, 0,
2    FROM v$shared_server
3         ROUND((busy/(busy+idle))*100,4)) "BUSY_RATE"
4  WHERE status != 'QUIT' ;
```

NAME   BUSY_RATE
-------- ----------
5000   12.34
5001   16.85
5002    9.73

上述查询的输出显示，最多情况下，共享服务器进程在处理数据库请求时，忙碌时间占比仅为 16.85%。

> 较高或上升的共享服务器忙碌比率表明可能需要在实例启动时生成额外的共享服务器进程。

当用户进程使用共享服务器发起数据库请求时，其请求最初由 *Dispatcher* 进程放入请求队列中。如果共享服务器进程太少，这些请求在等待服务时可能会经历延迟。可以使用 **V$QUEUE** 动态性能视图来监控对共享服务器进程的访问等待。该视图中用于监控共享服务器争用的有用列在表 6.4 中显示。

### 表 6.4 V$QUEUE 中的选定列

| 列名 | 描述 |
| :--- | :--- |
| TYPE | 统计信息对应的队列类型，可以是 DISPATCHER 或 COMMON（共享服务器） |
| TOTALQ | 放入队列中的项目总数 |
| WAIT | 队列中所有项目等待访问共享服务器进程的总时间，以百分之一秒为单位 |

通过查询这些列，可以计算访问共享服务器的平均等待时间。这种类型的查询在图 6.3 中显示。

### 图 6.3 计算共享服务器的平均等待时间

```sql
SQL>SELECT DECODE(totalq,0,'TOTALQ IS ZERO',
2
ROUND(SUM(wait)/SUM(totalq),4) "AVG DISPATCHER WAIT"
3
FROM v$queue
4
WHERE type = 'COMMON'
5
GROUP BY totalq;
```

AVG DISPATCHER WAIT
---------------
.0003

上述查询的输出显示，平均而言，用户进程等待共享服务器进程处理其数据库请求的时间为 0.0003 百分之一秒。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_340_0.png)

对共享服务器进程的较高或增加等待可能表明需要在实例启动时生成额外的共享服务器进程。

## 监控 Dispatcher 性能

与共享服务器类似，Dispatcher 进程的性能也可以通过“忙碌比率”来监控。该比率可以使用 V$DISPATCHER 动态性能视图计算得出。该视图中用于监控 Dispatcher 忙碌比率的有用列在表 6.5 中显示。通过查询这些列，可以使用图 6.4 中显示的 SQL 语句来计算 Dispatcher 忙碌比率。

### 表 6.5 V$DISPATCHER 中的选定列

| 列名 | 描述 |
| :--- | :--- |
| NETWORK | Dispatcher 使用的协议（网络地址） |
| STATUS | Dispatcher 的当前状态。可能的 Dispatcher 状态有：WAIT（空闲）、SEND（发送消息）、RECEIVE（接收消息）、CONNECT（建立连接）、DISCONNECT（断开会话）、BREAK（执行中断）、TERMINATE（终止连接）、ACCEPT（接受连接）、REFUSE（拒绝连接） |
| OWNED | 此 Dispatcher 拥有的虚电路数量 |
| BUSY | Dispatcher 忙碌的总时间（以百分之一秒为单位） |
| IDLE | Dispatcher 空闲的总时间（以百分之一秒为单位） |

### 图 6.4 确定 Dispatcher 忙碌比率的查询

```sql
SQL> SELECT name "DISPATCHER", network, (ROUND(SUM(busy)/(SUM(busy)+SUM(idle)),4))*100 "BUSY_RATE" FROM v$dispatcher GROUP BY name, network;
```

| DISPATCHER | NETWORK | BUSY_RATE |
| :--- | :--- | :--- |
| D000 | ADDRESS=<PROTOCOL=tcp)(HOST=moderne)(PORT=45280)) | 33.23 |
| D001 | ADDRESS=<PROTOCOL=tcp)(HOST=moderne)(PORT=45282)) | 27.12 |
| D003 | ADDRESS=<PROTOCOL=tcp)(HOST=moderne)(PORT=45283)) | 17.29 |

上述查询的输出显示，最多情况下，TCP/IP 网络协议的三个 Dispatcher 进程在处理数据库请求时，忙碌时间占比仅为 33.23%。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_341_0.png)

Oracle 建议在 Dispatcher 忙碌率持续超过 50% 时增加额外的 Dispatcher 进程。

