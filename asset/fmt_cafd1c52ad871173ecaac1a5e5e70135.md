
以跟踪文件和执行计划的形式收集和分析应用程序信息是理解应用程序性能的第一步。了解应用程序如何受到 Oracle 优化器行为的影响也很重要。基于这些信息，接下来的部分将检查可用于提高应用程序性能的选项。这些技术分为两大类：通过存储最优计划和使用物化视图来提高执行路径，以及通过使用索引和集群来最小化 I/O。

# 改进执行路径

根据查询的复杂性、表的大小以及 Oracle 优化器考虑的替代方案数量，CBO 可能会选择不佳的执行计划，从而导致查询性能下降。Oracle 9i 使用两个功能——计划稳定性和物化视图——通过直接影响 CBO 对执行计划的选择来帮助提高性能。

### Oracle 目标

解释计划稳定性的概念

## 计划稳定性

您对数据库所做的更改可能会无意中影响执行计划。例如，为了提高数据库调优的某个方面而对 `init.ora` 参数所做的更改可能会导致 Oracle 优化器的行为与之前不同——这可能会损害之前经过良好调优的 SQL 语句。Oracle9i 允许您通过为指定的执行计划提供“稳定性”来解决此问题。计划稳定性是通过在数据字典中存储给定 SQL 语句的首选执行计划来实现的，然后在发出该 SQL 语句时始终使用该执行计划。

### Oracle 目标

使用存储的大纲

## 存储的大纲

Oracle9i 以*存储的大纲*形式在数据字典中维护这些预定义的执行计划。这些存储的大纲代表优化器在关联 SQL 语句执行时将使用的执行计划。即使收集了新的统计信息或对 `init.ora` 进行了与优化器相关的更改，该存储的执行计划也保持恒定。存储的大纲本质上是一组提示，用于复现优化器最初执行语句时使用的执行计划。

> 通过称为*计划等价性*的过程，SQL 语句必须与用于生成大纲的原始语句**完全**匹配，存储的大纲才能被使用。即使是添加提示或注释的相同语句也不会被视为存储大纲使用的等价语句。

## 创建存储的大纲

在使用共享大纲功能之前，必须执行几个配置步骤。这些步骤按执行顺序列出如下：

1. 确定您想要为哪些语句存储执行计划。很可能这些语句涉及数据相对静态的表和索引。利用高度易变数据的表和索引的查询可能受益于 CBO 的常规动态特性。如果您希望为每个语句生成存储的大纲，只需将 `init.ora` 参数设置为 `CREATE_STORED_OUTLINES=TRUE`。由于存储的大纲不太可能适用于每个 `SQL` 语句，因此应谨慎使用此选项。如果使用此选项，步骤 2–4 不适用。

2. 确定您识别出的语句是否可以归入两个或两个更广泛的语句类别。这样做将有助于确定语句是否有资格进行存储大纲执行。类别示例可能包括“访问 `EMPLOYEE` 表的查询”或“对 `DISTRIBUTOR` 表的 `ADDRESS` 列进行查找的查询”。在创建大纲时，如果不指定存储的大纲应属于哪个类别，它将存储在一个名为 `DEFAULT` 的类别中。存储的大纲类别可以按如下方式指定：
   - 在实例级别使用 `init.ora` 中的 `USE_STORED_OUTLINES` 参数。设置 `USE_STORED_OUTLINES=TRUE` 会自动使 Oracle9i 将大纲存储在 `DEFAULT` 类别中。
   - 在会话级别使用 `ALTER SESSION SET USE_STORED_OUTLINE` 命令。

3. 修改 `OUTLN` 模式。此模式存储数据库的所有存储的大纲。
   - 出于安全目的，更改 `OUTLN` 模式的密码。默认密码（`OUTLN`）已有详细文档记录。Oracle9i 在首次登录后自动提示您更改 `OUTLN` 用户的密码。
   - 将 `OUTLN` 模式的默认和临时表空间更改为除了 `SYSTEM` 表空间之外的其他空间。
   - 将 `OUTLN` 模式用于存储大纲的两个表（`OL$` 和 `OL$HINTS`）移出 `SYSTEM` 表空间，并移至 `OUTLN` 的新默认表空间。可以使用 Export 和 Import 实用程序或 `ALTER TABLE ... MOVE...` 命令来执行此操作。

4. 要为您识别出的语句创建存储的大纲，请使用以下命令：

```sql
SQL> CREATE OR REPLACE OUTLINE employee_mgr_last_name
   2  FOR CATEGORY employee_queries ON
   3  SELECT lastname
   4  FROM employee
   5  WHERE job_title = 'MGR';
```

其中 `EMPLOYEE_MGR_LAST_NAME` 是新存储概要的名称，`EMPLOYEE_QUERIES` 是将其分配到的类别名称。或者，你可以在当前会话中激活特定类别的概要，然后发出你希望为其创建概要的命令：

```
SQL> ALTER SESSION SET CREATE_STORED_OUTLINES = employee_queries;
SQL> SELECT lastname
    2  FROM employee
    3  WHERE job_title = 'MGR';
SQL> ALTER SESSION SET CREATE_STORED_OUTLINES = false;
```

其中 `EMPLOYEE_QUERIES` 是该存储概要将被分配的类别名称。存储概要的名称将由系统生成。

你还可以使用 Enterprise Manager 调优包中的 Outline Manager 图形用户界面工具来创建你的存储概要。图 3.11 显示了使用 Outline Manager 屏幕创建名为 `EMPLOYEE_STATE` 的概要。

### 图 3.11 Enterprise Manager 的 Outline Manager

![](img/832fbc6aca8b6075843ca6f2356c0a8d_174_0.png)

5. 接下来，使用以下三种方法之一激活存储概要功能：
   - 设置 `init.ora` 参数 `USE_STORED_OUTLINES=TRUE` 并重新启动实例。
   - 使用以下命令动态将实例置于存储概要模式：

```
SQL> ALTER SYSTEM SET USE_STORED_OUTLINES = true;
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_175_0.png)

上述命令将激活所有类别中的存储概要。若要选择性地激活特定类别，请使用：`ALTER SYSTEM SET USE_STORED_OUTLINES = employee_queries;`
   - 使用以下命令在会话级别开启存储概要功能：

```
SQL> ALTER SESSION SET USE_STORED_OUTLINES = true;
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_175_1.png)

上述命令将激活所有类别中的存储概要。若要选择性地激活特定类别，请使用：`ALTER SESSION SET USE_STORED_OUTLINE = employee_queries;`

## 存储概要的使用方式

当执行 SQL 语句时，Oracle 首先将该语句以及会话级或实例级概要类别与共享池中已缓存的语句和类别进行比较。如果在共享池中找到匹配项，则使用缓存的信息执行该语句。如果在共享池中找不到匹配项，Oracle 接下来会检查数据字典，以查看是否存在针对此语句和此类别的存储概要。如果数据字典中存在存储概要，优化器将使用存储的执行计划来执行查询。如果数据字典中不存在存储概要，CBO（基于成本的优化器）将按常规动态生成执行计划。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_175_2.png)

如果某个 SQL 语句在 `DEFAULT` 类别中存在存储概要，但在活动类别中不存在对应的概要，仍会使用 `DEFAULT` 存储概要。

## 管理存储概要

存储概要的需求会随时间变化。可能需要修改、删除、重命名概要，或将其从一个类别移动到另一个类别。这些维护操作使用 Outline Manager 图形用户界面工具、Oracle 提供的包 `OUTLN_PKG` 以及 `ALTER OUTLINE` 和 `DROP OUTLINE` 命令来执行。

### 使用 OUTLINE MANAGER

除了创建存储概要外，Outline Manager 图形用户界面工具还可用于修改现有的存储概要。图 3.12 显示了使用 Outline 编辑器更改名为 `EMPLOYEE_STATE` 的存储概要的访问方法（通过 `FULL` 提示）。

Outline 编辑器也可用于修改存储概要背后 SQL 语句的连接顺序、更改存储概要所属的类别，或删除存储概要。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_176_0.png)

### 使用 OUTLN_PKG

`OUTLN_PKG` 包包含三个可用于管理存储概要的过程。这些过程的名称和描述如表 3.15 所示。

#### 表 3.15 *OUTLN_PKG* 中的过程
