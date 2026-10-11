
## *EMPLOYEE_HISTORY* 表的内容

![](img/832fbc6aca8b6075843ca6f2356c0a8d_201_0.png)

图 3.19 展示了该表数据在 IOT 段和 IOT 溢出段之间的物理存储方式。

## *EMPLOYEE_HISTORY* 数据的物理存储

![](img/832fbc6aca8b6075843ca6f2356c0a8d_201_1.png)

请注意图 3.19 中，与员工 107（Gastel）相关的所有行数据都能容纳在分配给 *EMPLOYEE_HISTORY* IOT 的一个块中。然而，员工 112（Macomber）的职称过长，无法放入 PCTTHRESHOLD 预留的空间。因此，Macomber 的行在 INCLUDING 列（*FIRST_NAME*）处被截断，剩余的列数据则存储在属于另一个表空间中溢出段的块里。关于如何找到此溢出段，将在下一节中讨论。

位图索引（Bitmapmed indexes）可以建立在堆表和索引组织表上。当在堆表上建立位图索引时，该索引存储位图及物理行 ID 以定位堆表中的行。然而，在 IOT 上的位图索引必须利用映射表来定位被索引的 IOT 行。*映射表*将索引的物理行 ID 映射到索引组织表使用的相应逻辑行 ID。由于 IOT 在添加或删除数据时，其物理行 ID 可能会发生变化（因为 IOT 叶子块可能会像 B-树索引一样在满时发生分裂），所以 IOT 使用逻辑行 ID 来管理对其行的索引访问。因此，如果没有这个映射表，IOT 中的叶子块分裂会改变行的物理行 ID，并导致相关的位图索引项无法使用。

由于使用了这种中间映射表，随着时间的推移，位图映射索引（Bitmapmapped index）条目可能无法准确反映被索引 IOT 中逻辑行 ID 和物理行 ID 之间的真实映射关系。这降低了索引的有效性。你可以通过发出以下查询来查看映射表与位图索引不同步的程度：

```sql
SELECT index_name, pct_direct_access
FROM dba_indexes
WHERE pct_direct_access IS NOT NULL;
```

只有 IOT 表的 PCT_DIRECT_ACCESS 值才非空。任何 PCT_DIRECT_ACCESS 值超过 30% 的索引，都应重建其位图映射索引以保持其有效性。

> 每个 IOT 只需维护一个映射表，即使该 IOT 上有多个位图索引。
>
> Oracle9i 的文档存在一个错误，声称可以使用以下命令在 EMPLOYEE_HISTORY IOT 上重建映射表：
>
> `ALTER TABLE employee_history MAPPING TABLE UPDATE BLOCK REFERENCES;`
>
> 然而，截至本文写作时，此命令不可用。

## 索引数据字典视图

数据字典视图 DBA_INDEXES、DBA_SEGMENTS 和 DBA_TABLES 都包含有关你迄今已了解的一种或多种索引类型的信息。

### DBA_INDEXES

DBA_INDEXES 是包含 DBA 所需大多数索引信息的数据字典视图。表 3.23 描述了 DBA_INDEXES 视图中与前面章节讨论的索引相关的列。

#### 表 3.23 选定的 DBA_INDEXES 列描述

| 列名 | 描述 |
| :--- | :--- |
| INDEX_TYPE | 指定索引的类型：<br>NORMAL（标准 B-树）<br>NORMAL/REV（反向键）<br>FUNCTION-BASED NORMAL<br>BITMAP<br>IOT—TOP（索引组织表）<br>CLUSTER<br>LOB（大对象） |
| COMPRESSION | 指示索引是否压缩。使用两个值：<br>DISABLED<br>ENABLED |
| FUNCIDX_STATUS | 指示函数索引的状态：<br>NULL（不是函数索引）<br>ENABLED<br>DISABLED |

图 3.20 展示了一个针对 DBA_INDEXES 的示例查询，显示了我们讨论过的索引信息。

#### 图 3.20 显示索引类型的示例查询

```sql
SQL> SELECT index_name, index_type, table_name, compression, funcidx_status
FROM dba_indexes
WHERE table_name in ('EMPLOYEE_HISTORY','EMPLOYEE')
ORDER BY index_name;

INDEX_NAME            INDEX_TYPE        TABLE_NAME       COMPRESS FUNCIDX_STATUS
EMPLOYEE_EMP_ID_IDX   NORMAL/REV        EMPLOYEE         DISABLED
EMPLOYEE_FIRST_NAME_UPPER_IDX FUNCTION-BASED NORMAL EMPLOYEE DISABLED ENABLED
EMPLOYEE_GENDER_IDX   BITMAP            EMPLOYEE         DISABLED
EMPLOYEE_LAST_NAME_IDX NORMAL            EMPLOYEE         DISABLED
SYS_IOT_TOP_8372      IOT - TOP         EMPLOYEE_HISTORY   DISABLED
```

### DBA_SEGMENTS

图 3.19 中查询缺失的唯一信息是 IOT EMPLOYEE_HISTORY 的溢出段详情。该信息可从 DBA_SEGMENTS 获取，如下所示。

```sql
SQL> SELECT segment_name,
2  segment_type,
3  tablespace_name
4  FROM dba_segments
5  WHERE segment_name LIKE '%IOT%';

SEGMENT_NAME    SEGMENT_TYPE    TABLESPACE_NAME
SYB_IOT_OVER_16102 TABLE APPL_OF
SYB_IOT_TOP_16102 INDEX APPL_IDX
```

此查询显示了 IOT EMPLOYEE_HISTORY 的两个组成部分：索引本身 SYB_IOT_TOP_16102 和溢出段 SYB_IOT_OVER_16102。名称中的数字部分是在创建 IOT 时由系统生成的。

### DBA_TABLES

为了更清楚地看出 EMPLOYEE_HISTORY IOT 及其关联溢出段之间的关系，我们可以如下查询 DBA_TABLES。

```sql
SQL> SELECT table_name,
2  iot_name,
3  iot_type,
4  tablespace_name
5  FROM dba_tables
6  WHERE table_name = 'EMPLOYEE_HISTORY'
7  OR iot_name = 'EMPLOYEE_HISTORY';

TABLE_NAME          IOT_NAME          IOT_TYPE      TABLESPACE
EMPLOYEE_HISTORY    IOT              SYB_IOT_OVER_16102
EMPLOYEE_HISTORY    IOT_OVERFLOW      APPL_OF
```

请注意，表 SYB_IOT_OVER_16102 的关联表条目为 EMPLOYEE_HISTORY。此外，请注意 EMPLOYEE_HISTORY 表的 TABLESPACE_NAME 条目为 NULL，因为实际存储数据的段是索引，而不是表。

## 监控索引以确定使用情况

### 目标

### 识别未使用的索引

根据优化器选择的执行计划，某些应用程序索引可能在应用程序用户工作期间从未被使用。如果索引未被使用，删除该索引可能通过消除在对被索引表执行 DML 时的索引维护开销来提高性能。删除未使用的索引还将释放表空间供其他索引使用。Oracle9i 引入了一个新的数据字典视图 V$OBJECT_USAGE，可用于识别未使用的索引。监控索引使用技术在此简要说明：

你可以使用以下命令来激活名为 EMP_LAST_NAME_IDX 的索引监控：

```sql
ALTER INDEX hr.emp_last_name_idx MONITORING USAGE;
```

在正常的用户活动一段时间后，你可以使用以下命令禁用监控：

```sql
ALTER INDEX hr.emp_last_name_idx NOMONITORING USAGE;
```

然后，你可以查询 V$OBJECT_USAGE 动态性能视图中的 INDEX_NAME 和 USED 列，以确定该索引是否在监控期间被访问过。USED 列中的 YES 值表示该索引在监控期间至少被访问过一次。USED 列中的 NO 值表示该索引在监控期间未被访问，可能是删除的候选对象。

## 分区

减少查询执行期间 I/O 量的另一种技术是将表数据划分为更小的子集，称为*分区*。一旦正确分区、索引和分析，大表查询将从 CBO 使用分区消除（partition elimination）以跳过不包含相关数据的表分区的能力中受益。此外，许多表维护操作也可以在分区级别执行。Oracle9i 提供了四种表分区方法。

### 目标

描述分区方法

### Oracle 表分区方法

在对表进行分区之前，必须选择合适的分区方法。分区方法的选择通常由分区键中存储的数据驱动——即你希望作为细分表数据基础的列。例如，假设你是一所大型大学的 DBA。作为更大的数据仓库倡议的一部分，大学的数据架构师要求你构建一个大表（即 STUDENT_HISTORY），用于存储该机构学术项目毕业生在五年期间的信息。每年会为当年的毕业生添加一组新记录，而最旧的记录（来自五年前的毕业生）将从表中清除。为简单起见，假设该表由表 3.24 中显示的四列组成。

**表 3.24 STUDENT_HISTORY 表描述**

| 列名 | 描述 |
| :--- | :--- |
| STUDENT_ID | 学生标识号 |
| DEGREE | 学生获得学位的三个字符缩写：BS, BA, BBA, MFA, MA, MBA, MFA, MS, PHD |
| GRADUATION_DATE | 学生从大学毕业的日期 |
| FINAL_GPA | 学生毕业时的最终平均绩点 |

此示例表结构将用于演示四种类型的分区：

- 范围分区

