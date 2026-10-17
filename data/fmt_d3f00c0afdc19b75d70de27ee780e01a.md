
Unix 系统和 Windows 2000 系统上的 `%ORACLE_BASE%\admin\SID\dump`，其中 `SID` 是生成文件的 Oracle 实例名称。后台进程跟踪文件在跟踪文件名包含了生成它的后台进程名称。Unix 和 Windows 2000 后台跟踪文件名示例见表 2.2。

### 表 2.2 示例后台进程跟踪文件名

| 进程名称 | Unix 系统 | Windows 2000 系统 |
| --- | --- | --- |
| 进程监控 (PMON) | Pmon_nnnn.trace | sidPMON.trace |
| 级监控 (SMON) | Smon_nnnn.trace | sidSMON.trace |
| 数据库写入进程 (DBW0) | dbw0_nnnn.trace | sidDBW0.trace |
| 日志写入进程 (LGWR) | Lwr_nnnn.trace | sidLGWR.trace |
| 检查点进程 (CKPT) | Cpkt_nnnn.trace | sidCKPT.trace |
| 归档进程 (ARCO) | Arc0_nnnn.trace | sidARCO.trace |

## 事件跟踪文件

Oracle9i 服务器具有你可以配置的特殊选项，以启用对特定数据库事件收集详细的跟踪信息。数据库事件是发生在数据库中的特定操作或活动。默认情况下，大多数数据库事件不会导致跟踪文件的创建。然而，通过向你想要跟踪的数据库初始化文件添加 `trace` 参数，可以强制某些数据库事件创建其活动的跟踪文件。跟踪文件将在初始化文件中 `BACKGROUND_DUMP_DEST` 参数指定的位置创建。

作为故障排除工作的一部分，你偶尔可能会被 Oracle Worldwide Support 要求激活数据库事件的跟踪，作为故障排除或调优工作的一部分。这些事件的跟踪通常在实例端通过向初始化文件添加新行来完成。如果多个跟踪事件被添加到

在 `init.ora` 中，应该将它们分组并进行适当的注释。

`init.ora` 中的条目如下所示：

```
EVENT="10046 trace name context forever, level 12*"
```

双引号是该参数实际语法的一部分。请注意，事件条目由两个部分组成：

- 要跟踪的事件，由数字指定（上述示例中为 10046）
- 执行跟踪的级别，由数字指定（上述示例中为 12）

事件及其关联层级的数值值并没有广泛且详尽的文档说明。在大多数情况下，当需要使用跟踪事件时，Oracle 全球支持人员将向您提供这些值。将它们设置为适当的值对于事件跟踪的正常工作至关重要。

## 用户跟踪文件

用户跟踪文件位于由 `init.ora` 参数 `USER_DUMP_DEST` 指定目录中。遵循 OFA 模型的系统，该目录在 Unix 系统上为 `$ORACLE_BASE/admin/SID/dump`，在 Windows 2000 系统上为 `%ORACLE_BASE%\admin\%SID%\dump`，其中 `SID` 是生成该文件的 Oracle 实例名称。用户进程跟踪在跟踪名称中包含了操作系统进程标识。在 Unix 系统上，它们还包含了用户生成时所连接的实例名称。此处显示 Unix 和 Windows 2000 背景跟踪文件的示例：

- Unix 系统：`ora_prod_4327.trc`
- Windows 2000 系统：`ora00117.trc`

可以对 `V$PROCESS` 和 `V$SESSION` 动态性能视图执行查询，以识别哪个用户了特定的跟踪文件。以下代码演示了如何将用户跟踪文件与生成它的用户会话匹配。

```sql
SQL> SELECT s.username, p.spid
  FROM v$session s, v$process p
  WHERE s.paddr = p.addr
  AND p.background is null;
```

| USERNAME | SPID |
|---|---|
| MATT | 4292 |
| DBSNMP | 4377 |
| SYSTEM | 4372 |
| JOE | 4437 |
| BRENDA | 4368 |
| EMILY | 4469 |

使用此 SQL 查询的输出可以看出，名为 `ora_prod_4292.trc` 或 `ora04292.trc` 的跟踪文件属于 Matt 的会话。请注意，通过共享服务器进程、使用 X/Open 接口的事务管理器或 Oracle 调用接口 (OCI) 连接的会话进行跟踪可能会为每个用户会话生成多个跟踪文件。

接下来的章节解释了如何为整个实例和单个用户激活跟踪。使用 `TKPROF` 工具对生成的跟踪文件进行格式化的技巧可以在第 3 章“SQL 应用调优与设计”中找到。

## 激活用户跟踪

当用户的服务器进程发生处理错误时，Oracle 有时创建一个用户跟踪文件。下面的代码列表显示了在 Windows 2000 Oracle9i 服务器上发生死锁错误时生成的用户跟踪文件的输出部分。死锁将在第 9 章“调优冲突”中进行更详细的讨论。

```
Dump file d:\oracle\admin\SEED\dump\ORA00476.TRC
Fri Jan 04 20:57:08 2002
ORACLE V9.0.1.1.1 - Production vsnsta=0
nsql=10 vsnxter=3
Windows 2000 Version 5.0 Service Pack 1, CPU type 586
Oracle9i Enterprise Release 9.0.1.1.1 - Production
With the Partitioning option
JServer Release 9.0.1.1.1 - Production
Windows 2000 Version 5.0 Service Pack 1, CPU type 586
Instance name: prod
Redo thread mounted by this instance: 1
Oracle process number: 9
Windows thread id: 476, image: ORACLE.EXE
```

*** 2002-01-04 20:57:08.000

*** SESSION ID:(8.5) 2002-01-04 20:57:08.000

DEADLOCK DETECTED

此会话当前的 SQL 语句:

update payroll.deductions set FICA = '120' where emp_id = '101'

```

以下死锁并非 ORACLE 错误。它是由于用户在应用程序设计中的错误或发布了错误的即时 SQL 导致的死锁。以下信息可能有助于确定死锁：
死锁图：

虽然死锁等事件会自动生成跟踪文件，但除非用户或 DBA 请求，否则不会对用户会话进行全范围跟踪。可以使用以下任一方法在实例级别或会话级别激活全用户跟踪。

### 实例级跟踪

通过通过设置 `init.ora` 参数 `SQL_TRACE=TRUE`，针对实例的所有进程都将创建它们自己的跟踪文件。使用这种特定的跟踪方法应要谨慎，因为它会对系统产生巨大的开销。该参数的默认值为 `FALSE`。

### 用户级跟踪

用户可以使用以下 SQL 命令开启或关闭跟踪：

```sql
ALTER SESSION SET SQL_TRACE=TRUE;
```

停止跟踪：

```sql
ALTER SESSION SET SQL_TRACE=FALSE;
```
