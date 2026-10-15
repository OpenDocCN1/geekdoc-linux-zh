

在工作负载定义窗口中，如图 7-4 所示，首先，你需要为工作负载指定一个名称，然后点击 Add 将一条 SQL 语句添加到工作负载中，并指定 SQL 语句名称和执行频率。此处也允许添加多条 SQL 语句，你只需再次选择 Add 即可添加额外的 SQL 语句。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_273_0.png)

### 图 7-4 为 Design Advisor 定义工作负载

你也可以选择 Import，该选项位于窗口右侧，用于从已解释的 SQL 语句导入工作负载，如图 7-5 所示。

- 1. 选择 SQL 语句的来源。
- 2. 点击要导入的语句旁边的复选框。
- 3. 点击 OK。

SQL 语句来源：已解释的 SQL 语句

导入 SQL 语句：全选、取消全选、确定、取消、应用、帮助

### 图 7-5 导入已解释的 SQL 语句以定义工作负载

下一步是指定需要收集统计信息的表。如前所述，咨询引擎结合工作负载信息和数据库信息（如统计信息）来推荐索引。因此，如果涉及表的最新统计信息不存在，你需要先收集它们，以使推荐的索引可用。图 7-6 显示了一些表被选中进行统计信息更新。

正在更新目录统计信息...

为了提供最佳建议，你数据库目录中的表统计信息必须是最新的。如果要更新表统计信息，请选择指定工作负载所需的表。更新表统计信息会增加计算时间。

可用表 已选表 DB2INST1 EMPLOYEE SALES 返回 下一步 完成 取消

### 图 7-6 为 Design Advisor 更新目录统计信息

然后你可以在磁盘使用窗口中指定推荐对象的默认表空间和组合最大磁盘空间。你可以在计算窗口中指定顾问引擎何时计算建议。如果想立即开始计算，请在窗口中选择 Now，然后建议将在建议窗口中给出，如图 7-7 所示。

在此，如果你想更改推荐索引的名称而不是使用 DB2 提供的名称，可以点击名称字段中显示的原始名称，然后输入你想要的名称。你可以点击 Show SQL 以获取创建索引的详细 SQL 语句，并且你也可以切换 Create 字段中的复选框来指出是否希望由 DB2 创建该索引。

![](img/d95c931f4f3da4a6bd0ee55148fefad7_275_0.png)

### 图 7-7 Design Advisor 推荐的索引

如果为所选表已存在某些索引，Design Advisor 可以告诉你这些索引在指定工作负载中是否未被使用。然后你可以指定是否要删除这些未使用的索引——在选择这样做之前，请确保删除“未使用”的索引不会影响其他工作负载。

剩余的步骤是安排推荐的 SQL 语句的运行，包括创建索引和删除索引，然后相关索引将被创建或删除。

如果你熟悉命令行，也可以从命令行运行 Design Advisor。示例 7-1 包含三个步骤。第一步是定义工作负载，第二步是为相关表运行统计信息，然后第三步是从命令行运行 db2advis 实用程序以获得建议。从输出中可以看到，有无推荐索引的工作负载运行的 timerons 显示出来，并且使用推荐索引带来的改进也得到了评估。此外，通过使用参数 -o，推荐的索引创建脚本可以放入一个文件中。

### 示例 7-1 使用 db2advis 为特定工作负载推荐索引创建

```
$ cat sample.sql
--#SETFREQUENCY 100
select count(*) from sales where region = ?;
--#SETFREQUENCY 3
select projno, sum(comm) tot_comm from employee, emp_act
where employee.empno = emp_act.empno and
employee.job='DESIGNER'
group by projno
order by tot_comm desc;
--#SETFREQUENCY 50
select * from sales where sales_date = ?;

$ db2 "runstats on table db2inst1.employee with distribution allow write access"
DB20000I The RUNSTATS command completed successfully.
$ db2 "runstats on table db2inst1.sales with distribution allow write access"
DB20000I The RUNSTATS command completed successfully.
$ db2 "runstats on table db2inst1.emp_act with distribution allow write access"
DB20000I The RUNSTATS command completed successfully.

$ db2advis -d sample -i sample.sql -t 0 -o ad1.sql
execution started at timestamp 2002-11-11-17.33.32.188732
  found [3] SQL statements from the input file
  recommending indexes...
Initial set of proposed indexes is ready.
Found maximum set of [4] recommended indexes
Cost of workload with all indexes included [1.258857] timerons
total disk space needed for initial set [ 0.035] MB
total disk space constrained to          [ -1.000] MB
  4 indexes in current solution
[101.4306] timerons (without indexes)
[ 1.2589] timerons (with current solution)
[%98.76] improvement
```

