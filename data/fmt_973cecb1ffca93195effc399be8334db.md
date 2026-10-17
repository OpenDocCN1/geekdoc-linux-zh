
# 调整共享服务器（Shared Server）选项

你可以通过查询 `V$SESSTAT` 视图来衡量共享服务器连接占用的内存量。该视图包含每个用户内存的信息。下面的查询显示了如何衡量自实例启动以来所有共享服务器会话占用的最大内存。你可以将其作为指南，以确定应该为大池（Large Pool）分配多少内存。此示例显示，所有共享服务器会话使用的最大内存约为 240KB。

```sql
select sum(value) 'Max MTS Memory Allocated' from v$sesstat, v$statname st = 'session uga memory max' and ss.statistic#;
```

`Max MTS Memory Allocated`

244416

# 确定是否有足够的分发器（Dispatchers）

可以通过查询 `V$DISPATCHER` 视图来监控分发进程。该视图包含有关分发进程繁忙程度的信息。查询此视图以确定启动更多分发器是否有利。下面的示例查询针对 `V$DISPATCHER` 视图运行，显示分发器的繁忙百分比：

```sql
Select name, (busy / (busy + idle))*100
"Dispatcher % busy Rate"
From V$DISPATCHER
```

| Protocol | Dispatcher % Busy Rate |
|---|---|
| D000 | .00070079 |
| D001 | .0059 |

这些分发器的繁忙时间非常短。如果分发器的繁忙时间超过 50%，你应该考虑考虑启动更多分发器。这可以通过 `ALTER SYSTEM` 命令动态完成。可以全部或增加一个或两个分发器，并监控分发器的繁忙率，查看它们是否降至 50% 以下。

# 确定用户等待分发器多久

要衡量用户等待分发器执行其请求的时间，请查看组合的 `V$QUEUE` 和 `V$DISPATCHER` 视图。见下列表示例：

```sql
SELECT decode(sum(totalQ),0,'No Responses',
  Sum(wait)/sum(totalQ)) "Average Wait time"
FROM V$QUEUE q, V$DISPATCHER d
WHERE q.type = 'DISPATCHER'
AND q.paddr = d.paddr;
```

```
Average Wait Time
-----------------
.0413
```

分发器的平均等待时间略多于百分之一秒。随时间监控此指标。如果该数字持续增加，你应该考虑添加更多分发器。

# 确定是否有足够的共享服务器（Shared Servers）

你可以使用 `V$SHARED_SERVER` 和 `V$QUEUE` 字典视图监控共享服务器。共享服务器负责执行客户端请求并将请求放在适当的分发器响应队列中。你最感兴趣的衡量是客户端请求在请求队列中等待的时间。请求在队列中停留越久，客户端等待响应的时间越久。以下语句将告诉你请求在队列中等待多久：

```sql
Select decode(totalQ,0,'No Requests') 'Wait Time',
Wait/totalQ || 'hundredths of seconds'
"Average Wait time per request"
from V$QUEUE
where type = 'COMMON'
```

# 总结 145

| Wait Time | Average Wait time per request |
|---|---|
| .023132 | hundredths of a second |

请求队列中的平均等待时间略多于百分之一秒。随时间监控此指标。如果该数字持续增加，你应该考虑添加更多共享服务器。

## 总结

共享服务器是 Oracle 服务器的一种配置，允许你在不需要额外资源的情况下支持更多的连接。理解共享服务器选项非常重要，因为当你面临服务器能够管理的进程数量问题时，它可以防止潜在且不必要的硬件升级。

在此配置下，用户连接共享称为“分发器”（`dispatchers`）的进程。分发器取代了专用服务器进程。

4. 在哪个文件中可以找到共享服务器配置参数？

+   A. `listener.ora`
+   B. `mts.ora`
+   C. `init.ora`
+   D. `tnsnames.ora`
+   E. `sqlnet.ora`

5. 下列哪项是共享服务器（Shared Server）的组件之一？

+   A. 共享用户进程 (Shared user processes)
+   B. 检查进程 (Checkpoint processes)
+   C. 调度器进程 (Dispatcher processes)
+   D. 专用服务器进程 (Dedicated server processes)

6. DBA 想要将数据库设置为共享服务器模式。在哪个文件中进行修改？

+   A. `tnsnames.ora`
+   B. `cman.ora`
+   C. `names.ora`
+   D. `init.ora`

7. 在 Oracle Net Manager 中选择哪项可以配置共享服务器？

+   A. 本地 (Local)
+   B. 服务命名 (Service Naming)
+   C. 监听器 (Listeners)
+   D. 配置文件 (Profile)
+   E. 以上均不是

8. DBA 想要在实例启动时启动两个 TCP/IP 调度器和一个 IPC 调度器。哪行代码可以实现这一目标？

+   A. `dispatchers=(protocol=tcp)(dispatchers=2) (protocol=IPC)(dispatchers=1)dispatchers=(protocol=tcp)(dispatchers=2) (protocol=IPC)(dispatchers=1)`
+   B. `dispatchers="protocol=tcp)(dispatchers=2) (protocol=IPC)(dispatchers=1)`
+   C. `dispatchers_start=(protocol=tcp)(dispatchers=2) (protocol=IPC)(dispatchers=1)`
+   D. `dispatchers_start=(pro=tcp)(dis=2) (pro=IPC)(dis=1)`

9. 在通过共享服务器进行通信期间，客户端连接绑定的共享内存称为什么？

+   A. 程序全局作用区 (Program Global Area)
+   B. 系统全局作用区 (System Global Area)
+   C. 虚拟电路 (Virtual Circuit)
+   D. 数据库缓冲缓存 (Database Buffer Cache)
+   E. 以上均不是
