
```
*** 2002.02.13.10.07.14.777
*** SESSION ID:(16,43) 2002.02.13.10.07.14.750
ksged1: deadlock detected via did
DEADLOCK DETECTED
Current SQL statement for this session:
UPDATE emp
SET last_name = 'Smith'
WHERE id = 25

The following deadlock is not an ORACLE error. It is a
deadlock due to user error in the design of an application
or from issuing incorrect ad-hoc SQL. The following
information may aid in determining the deadlock:
Deadlock graph:... .
```

资深员工向新受训者提供的建议是合理的，因为通常再次尝试输入相同数据时，导致死锁所需的锁事件组合不太可能连续发生，因此不会导致另一个死锁错误。从 DBA 的角度来看，您应该监控 `USER_DUMP_DEST` 目录中包含死锁错误的跟踪文件。如果它们频繁发生，您应考虑修改应用程序代码或调整业务流程以减少死锁的发生。

### 衡量锁争用

如果让 Oracle 保持其默认机制，它通常能非常有效地管理锁。当锁争用发生时，可以使用 `V$LOCK` 和 `V$LOCKED_OBJECT` 动态性能视图、`DBA_WAITERS` 和 `DBA_BLOCKS` 数据字典视图，以及 `OEM` 性能管理器图形界面来识别锁争用。下面将讨论每种监控锁活动的方法。

> `DBA_BLOCKERS` 和 `DBA_WAITERS` 数据字典视图是通过在 Unix 系统上执行位于 `$ORACLE_HOME/rdbms/admin` 的 `CATBLOCK.SQL` 脚本，以及在 Windows 2000 系统上执行位于 `%ORACLE_HOME%\rdbms\admin` 的 `CATBLOCK.SQL` 脚本来创建的。

#### 使用 V$LOCK 监控锁争用

`V$LOCK` 动态性能视图包含有关在查询该视图时数据库当前持有的锁的数据。如下所示，该视图可以连接到 `DBA_OBJECTS` 和 `V$SESSION`，以便查看是谁在持有锁以及锁定的对象是什么：

```sql
SQL> SELECT s.username,
              DECODE(l.type,'TM','TABLE LOCK',
                    'TX','ROW LOCK',
                     NULL) 'LOCK LEVEL',
           o.owner, o.object_name, o.object_type
   FROM v$session s, v$lock l, dba_objects o
   WHERE s.sid = l.sid
     AND o.object_id = l.id1
     AND s.username IS NOT NULL;
```

| 用户名 | 锁级别 | 拥有者 | 对象名称 | 对象类型 |

|--------|--------|--------|----------|----------|

| JOE    | TABLE_LOCK | JOE | EMP | TABLE |

| SCOTT  | TABLE_LOCK | JOE | EMP | TABLE |

此示例显示用户 Scott 和 Joe 都锁定了由 Joe 拥有的 EMP 表。如果 Joe 打电话抱怨他的应用程序会话似乎无响应，此查询可能有助于判断 Joe 的事务是否卡在等待 Scott 提交或回滚其事务。然而，此查询并未明确指示哪个用户正在阻塞另一个用户。

#### 使用 V$LOCKED_OBJECT 监控锁争用

`V$LOCKED_OBJECT` 视图还列出了系统中每个用户当前持有的所有锁。然而，它还包含阻塞信息，显示哪个用户正在执行导致其他应用程序用户体验等待的锁定事务。可以使用以下查询来确定谁锁定了哪些对象，以及持有阻塞锁的用户是谁：

```sql
SQL> SELECT LPAD(' ',DECODE(l.indsn,0,3,0)) || l.oracle_username "User Name",
             o.owner, o.object_name, o.object_type
  FROM v$locked_object l, dba_objects o
 WHERE l.object_id = o.object_id
 ORDER by o.object_id, 1 desc;
```

| 用户名 | 拥有者 | 对象名称 | 对象类型 |

|--------|--------|----------|----------|

| SCOTT  | JOE | EMP | TABLE |

| BRENDA | JOE | EMP | TABLE |

| JOE    | JOE | EMP | TABLE |

| ROBIN  | APPS | PAYROLL | TABLE |

| REGI   | APPS | PAYROLL | TABLE |

查询输出显示，Scott、Joe 和 Brenda 都在锁定 Joe 的 EMP 表中的行，而 Robin 和 Regi 则锁定应用程序 PAYROLL 表中的行。此外，最左侧的用户名表示持有阻止其他用户继续工作的锁的用户。在第一个示例中，这意味着 Scott 在 Joe 的 EMP 表上的事务正在阻塞 Brenda 和 Joe 的事务。同样，Robin 在 PAYROLL 表上的事务正在阻塞 Regi 在该表上的事务。解决此类阻塞事务的技术将在下一节中介绍。

#### 使用 DBA_WAITERS 监控锁争用

`DBA_WAITERS` 数据字典视图包含关于等待其他用户会话释放锁的用户会话的信息。表 9.5 描述了该视图的内容。

**表 9.5** `DBA_WAITERS` 的内容

| 列名 | 描述 |

| :--- | :--- |

| WAITING_SESSION | 当前等待获取锁的用户会话的 SID |

| HOLDING_SESSION | 当前持有 WAITING_SESSION 中所示用户希望获取的锁的用户会话的 SID |

| LOCK_TYPE | 与 HOLDING_SESSION 关联的用户持有的锁类型 |

| MODE_HELD | 与 HOLDING_SESSION 关联的用户持有的锁模式 |

| MODE_REQUESTED | 与 WAITING_SESSION 关联的用户请求的锁模式 |

| LOCK_ID1 | 与 HOLDING_SESSION 关联的用户持有的第一个（通常为共享）锁的内部锁标识符 |

| LOCK_ID2 | 与 HOLDING_SESSION 关联的用户持有的第二个（通常为行排他）锁的内部锁标识符 |

图 9.7 展示了如何将 `DBA_WAITERS` 数据字典视图与 `V$SESSION` 动态性能视图连接，以便显示与等待会话和持有会话关联的用户名。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_529_0.png)

```sql
SQL> SELECT sw.username "WAITING_USER", bu.username "LOCKING_USER",
             dw.lock_type, dw.mode_held, dw.mode_requested
  FROM dba_waiters dw, V$session s, V$session bu
 WHERE dw.waiting_session = s.sid
   AND dw.holding_session = bu.sid;
```

| 等待用户 | 锁定用户 | 锁类型 | 持有模式 | 请求模式 |

|:---------|:---------|:-------|:---------|:---------|

| MATT     | JOE      | Transaction | Exclusive | Exclusive |

图 9.7 中的输出显示，用户 Matt 正在等待获取与用户 Joe 当前持有排他事务锁相同的表上的排他锁。

#### 使用 DBA_BLOCKERS 监控锁争用

通常，DBA 并不关心其他用户试图获取哪种类型的锁；他们只关心确定哪个用户引起了锁争用，以便使用下一节描述的技术之一来纠正锁争用。`DBA_BLOCKERS` 数据字典视图是这种简明锁定信息的最佳来源，因为 `DBA_BLOCKERS` 视图只包含一列 `HOLDING_SESSION`，显示正在阻塞其他应用程序用户锁请求的用户会话的 SID。以下示例展示了如何通过连接 `DBA_BLOCKERS` 和 `V$SESSION` 来识别阻塞其他用户的应用程序用户：
