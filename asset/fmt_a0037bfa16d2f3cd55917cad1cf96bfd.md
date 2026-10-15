
```
Memory for instance

monh    other    fcmbp
16.0K   6.9M     16.6M

Memory for database: SAMPLE

utilh   pckcacheh catcacheh bph     bph     bph     bph
16.0K   640.0K   160.0K   45.3M   656.0K  400.0K  272.0K

bph     lockh    dbh      other   appctlh appctlh appctlh
208.0K  448.0K   1.5M     54.7M   16.0K   16.0K   16.0K

appctlh
320.0K
```

在上面的示例中，`IBMDEFAULTBP` 缓冲池的大小通过动态方式从默认的 1000 个 4K 页更改为 10000 个 4K 页。通过 `db2mtrk` 可以非常清晰地监控 DB2 所做的更改。第一个 `db2mtrk -i -d` 命令可用于获取更改前 `IBMDEFAULTBP` 的缓冲池大小，在示例中以粗体显示；该“`bph`”的值为 4.1 MB。然后，可以使用 `ALTER BUFFERPOOL` 命令并指定“`immediate`”参数，动态更改 `IBMDEFAULTBP` 缓冲池的大小。执行该操作后，可以使用示例中所示的第二个 `db2mtrk -i -d` 命令获取 `IBMDEFAULTBP` 当前的缓冲池大小。可以看到，缓冲池大小现在已经改为 45.3M（以粗体突出显示）。

> 注：您可能已经注意到，示例中仅对于一个数据库显示了多个“`bph`”；这是因为，除了用户创建的缓冲池之外，DB2 还创建了四个隐藏缓冲池供内部使用。

有关 `db2mtrk` 命令参数的详细说明以及 `db2mtrk` 输出字段的说明，请参阅 Memory Tracker 工具的联机帮助信息。

## 应用程序开发

对于数据库而言，有效支持各种开放标准和用于应用程序开发的开源产品已变得越来越重要。DB2 UDB 为许多标准接口提供了访问能力，并附带一整套开发工具。

本章讨论以下主题：

- 应用程序配置

- DB2 应用程序对象

- 编程语言

- 应用程序开发工具

### 8.1 应用程序配置

DB2 支持本地和远程应用程序开发。在应用程序看来，数据库始终是本地数据库。图 8-1 说明了两种不同的开发配置。示意图左侧表示本地开发环境，其中数据库和应用程序位于同一台机器上。右侧表示客户端-服务器开发环境，其中数据库和应用程序位于不同的机器上。无论采用哪种配置，数据库在应用程序面前始终显示为本地数据库。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_285_0.png)

图 8-1 开发配置

DB2 UDB 的特殊功能之一是，多个 DB2 UDB 版本可以在同一系统中共存。例如，可以在同一台机器上运行 DB2 版本 7.2 实例和 DB2 版本 8.1 实例。此场景的示例请参见图 8-2。使用 DB2 版本 8，现在不仅可以在同一台机器上运行多个 DB2 版本，还可以在同一台机器上运行 DB2 的不同发行版。例如，可以在同一台机器的不同实例中运行 V8.1 FixPak 1 和 V8.1 FixPak 2。在版本 8 之前，在一个版本级别内只能运行一个发行版和 FixPak 级别，也就是说，DB2 版本 7.2 FixPak 4 和版本 7.2 FixPak 5 无法在同一台服务器上运行。

![Linux 服务器](img/d95c931f4f3da4a6bd0ee55148fefad7_286_0.png)

图 8-2 一个主机上的多个数据库管理器实例版本

### 8.2 DB2 应用程序对象

DB2 UDB 支持存储过程（SP）、用户自定义函数（UDF）和触发器，它们都用于开发应用程序。DB2 V8 还提供了一个名为“开发中心”的图形化工具，它是应用程序开发客户端的一个组件。该工具用于开发 SP 和 UDF。有关此工具的更多信息，请参见第 284 页的 8.4“应用程序工具”。

#### 8.2.1 触发器

触发器是一组定义好的 SQL 语句，作为 DB2 对象存储在 DB2 数据库中。当对某个 DB2 表发生特定事件时，将执行这组 SQL 语句。可能调用触发器的事件类型是对给定 DB2 表执行 Insert、Update 或 Delete 操作。触发器可以设置为在 insert、update 或 delete 事件之前、之后执行，或者代替这些事件执行。

- 无级联前触发（No cascade before）：定义的操作将在触发操作执行之前执行。

- 后触发（After）：所有被触发的操作将在触发操作完成后应用。

+   而不是：原始操作将被触发器中定义的操作所替换

触发器是通过使用 `create trigger` DDL 语句来定义的。

> 注意：`create trigger` 语句在“SQL 参考”中的第 5 章“语句”中有更详细的解释（在第 303 页的“其他出版物”中列出）。

以下场景在我们的示例数据库中给出。

当更新表 `EMPLOYEE` 中的 `salary` 列或 `bonus` 列时，触发器会将旧数据保存到历史表中以满足审计要求。

## 示例 8-1 存储历史数据的触发器示例

```
connect to sample;

create table employee_hist(
    empno        char(6),
    salary_old   decimal(9,2),
    salary_new   decimal(9,2),
    bonus_old    decimal(9,2),
    bonus_new    decimal(9,2),
    chg_date     timestamp);

create trigger employee_audit
 after update of salary, bonus on employee
 referencing OLD as old_row NEW as new_row
 for each row mode db2sql
 insert into employee_hist
   Values(old_row.empno,
          old_row.salary,
          new_row.salary,
          old_row.bonus,
          new_row.bonus,
          current timestamp);
```

现在我们修改 `employee` 表中的任何薪资金额以触发触发器并填充 `employee_hist` 表。通过从 `employee_hist` 中选择数据，您可以看到我们的触发器的工作方式。

## 示例 8-2 每次更新都会强制向 employee_hist 插入

```
db2 "update employee set salary = 55000 where empno = '00070'"
db2 "update employee set salary = 45000 where empno = '000110'"
```

```
no external action
deterministic
return
select (salary_new - salary_old) as salary_diff from employee_hist h , employee o
where h.empno = emp
and h.empno = o.empno
and h.chg_date = (select max(chg_date)
from employee_hist
where empno = h.empno)
```

```
db2inst1@db1nx02:~/tpc> db2 "select empno, firstnme, lastname, salary_diff(empno) as salary_diff from employee where empno in ('000110','000070')"
```

| EMPNO | FIRSTNME | LASTNAME | SALARY_DIFF |

| --- | --- | --- | --- |

| 000110 | VINCENZO | LUCCHESSI | -25000.00 |

| 000070 | EVA | PULASKI | 10000.00 |

2 record(s) selected.

> 注意：语句 `select max(chg_date)` 是必要的，因为对于每个 `empno`，`employee_hist` 表中可能存在多行，但 UDF 只能返回一行。

#### 8.2.3 存储过程

存储过程有助于减少客户端与服务器之间不必要的数据传输。SQL 语句和定义存储在数据库服务器上。客户端仅通过网络发送必要的数据来调用存储过程并获取结果返回。这有助于提高客户端服务器应用程序的整体性能。
