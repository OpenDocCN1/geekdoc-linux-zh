
| SCOTT | 7 TX | None Exclusive | 131087 | 2328 |

| AMY | 8 TX | None Exclusive | 131099 | 2332 |

| MANISH | 10 TX | None Exclusive | 131099 | 2332 |

| BOLDT | 12 TX | None Exclusive | 131099 | 2332 |

列表 25.6 是一个通用脚本，显示带有 SID 和用于杀死会话的序列号的锁；该脚本生成的报告提供了持有锁的会话的信息，并提供了使用 `ALTER SYSTEM KILL SESSION` 命令杀死会话所需的信息。

# 第 25 章 完整性管理

## 列表 25 显示持有锁的会话信息

`set linesize 132 pages 66`

```
break on Kill on username on terminal
column Kill heading 'Kill String' format a13
column res heading 'Resource Type' format 999
column id1 format 9999990
column id2 format 9999990
column mode heading 'Lock Held' format a20
column request heading 'Lock Requested' format a20
column serial# format 999999
column username format a10 heading "Username"
column terminal heading Term format a6
column tab a35 heading "Table Name"
column owner format a9
column Address format a18
select nvl(S.USERNAME, 'Internal') username,
nvl(S.TERMINAL, 'Node') terminal,
L.SID||'S.SERIAL#||substr(T1.NAME,1,20) tab,
decode(L.LMODE,
1,'No Lock',
2,'Row Share',
3,'Row Exclusive',
4,'Share',
5,'Row Exclusive',
6,'Exclusive',null) lmode,
decode(L.REQUEST,
1,'No Lock',
2,'Row Share',
3,'Row Exclusive',
4,'Share',
5,'Row Exclusive',
6,'Exclusive',null) request
```

```
from V$LOCK L
V$SESSION S,
SYS.OBJ$ U1,
SYS.OBJ$ T1
where L.SID = S.SID
```

and T1.OBJ# = decode(L.ID2,0,L.ID1,L.ID2)

and U1.USER = T1.OWNER

and S.TYPE = 'BACKGROUND'

order by 1,2,5

上述 SQL 语句的输出如下：

| 用户名 | 杀死字符串 | 表名 | 持有锁 | 请求锁 |
|---|---|---|---|---|
| SAMUEL | tty 7,5159 | SAMUEL.TABLE_CONFIG | Row Excl | |
| YA-MEI | tty 8,941 | SCOTT.SCHEDULE | Row Excl | |
| BARRETT | tty 6,885 | SYS.CLUSTERS | Exclusive | |
| | | SCOTT.ACCOUNT | Row Excl | |

执行以下命令演示杀死会话：

```
ALTER SYSTEM KILL SESSION '6,885'
```

这将杀死 Barrett 的会话。另一个有用的脚本可以在 `$ORACLE_HOME/rbms/admin` 目录下找到。该脚本名为 `utlock.sql`，它以树的形式打印锁信息。这更容易识别谁正在锁定资源。

## 避免锁的解决方案

本节提供了一些避免锁的通用做法。某些应用程序使用控制表来生成序列号。这种类型的典型示例是控制表中的下一个序列号。在多个会话尝试进入数据库的序列号的用户环境中，控制表可能会成为瓶颈。这种类型的序列号产生的另一个瓶颈是当一个会话更新控制表中的序列号，然后在提交之前进行某些处理。

对此有几种可能的解决方案：

- 减少更新控制表中的序列号的时间，一旦获取下一个数字，立即将其提交到数据库，从而允许其他用户对表的并发访问。
- 考虑使用序列 `sequences`。序列的使用大大简化了应用程序代码。在之前的逻辑中，需要执行 `select` 和 `update`。然而，从序列完成 `select` 后，序列号自动增加，因此瓶颈被完全消除。缺点是生成的最后一个数字在使用后无法回滚，导致空隙。

批量处理本质上是从要处理的表中选择记录，对它们进行处理，然后用新值更新。在程序处理之前锁定这些记录是非常重要的，因为批处理作业会在会话更新时从表中选择旧值。为了防止这种情况发生，伪 SQL 代码见列表 25.7。

### 列表 25.7 批量处理伪代码

```
Begin

Declare c_emp for

Select * from emp

<Where Clause >

For Update;

v_emp c_emp%RowType;

Begin

Open c_emp;

Loop

Begin

Fetch c_emp into v_emp;

  -- some processing --

  Update emp

  Set sal = X,

  incr = Y

  Where emp_id = v_emp.emp_id;

End;
```

在此代码中，注意要处理的整个记录集都被锁定了；它们在处理之前需要锁定，以便另一个会话在处理期间无法更新这些记录。此代码的缺点是，即使记录已被处理，在所有记录处理完成之前仍然被锁定。如果处理时间很长，这些记录的锁定将防止其他其他会话并发访问。根据给定时间对这些记录的需求，这种锁定策略可能会成为性能瓶颈。用于应对这种情况的替代代码见列表 25.8。

### 列表 25.8 最大并发的批量处理伪代码

```
Begin

Declare c_emp for

Select rowid from emp

<Where Clause >;

v_emp c_emp%RowType;

r_emp emp%RowType;

Begin

Open c_emp;

Loop

Begin

Fetch c_emp into v_emp;

Select *

Into r_emp

From emp

Where rowid = v_emp.rowid;

<Where Clause >

For Update;

-- Do some processing -

Update emp

Set sal = X,

ner = Y

Where rowid = v_emp.rowid

<Where clause >;

Commit;

End;

End Loop;

Close c_emp;

End;
```

注意列表 25.8，外部游标只是从表中选择所有行。外部游标为内部 `select` 提供值，而内部 `select` 每次通过 `update` 子句只锁定一个行。列表 25.8 中的 `commit` 现在移动到了循环内部；因此，在更新每行行后，都会执行 `commit`，从而最大化了其他用户对表的并发访问。你可能想尝试移动列表 25.7 脚本中的 `commit`，遗憾的是，如果在 Oracle 6.0 中这样做这样做，游标也会被关闭，导致 PL/SQL 循环终止。一旦通过 `open` 子句打开游标，表中的所有相关行都会被锁定。当执行 `commit` 时，游标会丢失其上下文并显示以下消息：

```
ORA-01002: fetch out of sequence
```

因此，有必要按照所示风格进行编码。

在使用带有行级触发器的表时要小心。例如，一个表可以有一个行级触发器，当表的记录被更新时，触发器可能会导致其他表被更新。这会导致单条 `update` 语句获取大量的锁。

## 锁与分布式数据库

当事务尝试同时更新两个分布式数据库时，分布式数据库必须处理固有的更新问题，这被称为两阶段提交 `2PC`。以下 SQL 语句了这一点：

```sql
APPLY UPDATE A (DB1)
APPLY UPDATE B (DB2)
IF A = OK AND B = OK
COMMIT A
-- 在此点发生致命的暴露
COMMIT B
ELSE
ROLLBACK A
ROLLBACK B
```
