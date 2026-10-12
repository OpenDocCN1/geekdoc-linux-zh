
在对表进行分区之前，必须选择合适的分区方法。分区方法的选择通常由分区键中存储的数据驱动——即你希望作为细分表数据基础的列。例如，假设你是一所大型大学的 DBA。作为更大的数据仓库倡议的一部分，大学的数据架构师要求你构建一个大表（即 `STUDENT_HISTORY`），用于存储该机构学术项目毕业生在五年期间的信息。每年会为当年的毕业生添加一组新记录，而最旧的记录（来自五年前的毕业生）将从表中清除。为简单起见，假设该表由表 3.24 中显示的四列组成。

### 表 3.24 `STUDENT_HISTORY` 表描述

| 列名 | 描述 |
| :--- | :--- |
| `STUDENT_ID` | 学生标识号 |
| `DEGREE` | 学生获得学位的三个字符缩写：BS, BA, BBA, MFA, MA, MBA, MFA, MS, PHD |
| `GRADUATION_DATE` | 学生从大学毕业的日期 |
| `FINAL_GPA` | 学生毕业时的最终平均绩点 |

此示例表结构将用于演示四种类型的分区：

- 范围分区

## 范围分区

范围分区是对 `STUDENT_HISTORY` 表内容进行细分的一种选择。范围分区使用列值的范围来决定数据行将被插入到哪个分区。假设你决定使用范围分区对 `GRADUATION_DATE`（毕业日期）列来分区 `STUDENT_HISTORY` 表。这意味着 `GRADUATION_DATE` 是分区键：

```sql
SQL> CREATE TABLE student_history
2  (student_id      NUMBER(10),
3  degree          VARCHAR2(3),
4  graduation_date DATE,
5  final_gpa       NUMBER)
6  PARTITION BY RANGE (graduation_date)
7  (PARTITION p_1997 VALUES LESS THAN
8    (TO_DATE('01-JUN-1997','DD-MON-YYYY')) TABLESPACE hist_tab01,
9   PARTITION p_1998 VALUES LESS THAN
10   (TO_DATE('01-JUN-1998','DD-MON-YYYY')) TABLESPACE hist_tab02,
11   PARTITION p_1999 VALUES LESS THAN
12   (TO_DATE('01-JUN-1999','DD-MON-YYYY')) TABLESPACE hist_tab03,
13   PARTITION p_2000 VALUES LESS THAN
14   (TO_DATE('01-JUN-2000','DD-MON-YYYY')) TABLESPACE hist_tab04,
15   PARTITION p_2001 VALUES LESS THAN
16   (TO_DATE('01-JUN-2001','DD-MON-YYYY')) TABLESPACE hist_tab05,
17   PARTITION p_ERROR VALUES LESS THAN
18   (MAXVALUE) TABLESPACE hist_tab06);
```

上述语法将创建一个包含六个分区的表，名称从 `P_1997` 到 `P_2001`，以及 `P_ERROR`。出于性能考虑，这些分区中的每一个在物理上都存储在一个独立的表空间中（`HIST_TAB01` 到 `HIST_TAB06`）。插入到表中的每一行都将根据学生的毕业日期被放置到相应的分区中。图 3.21 展示了这一概念。

### 图 3.21 范围分区的 `STUDENT_HISTORY` 表

```sql
INSERT INTO
  student_history
  (student_id, degree,
   graduation_date, final_gpa)
VALUES
  (123456789,'BBA','12-MAY-99',3.75);
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_208_0.png)

在检查上述结构时，应考虑与范围分区相关的若干规则：

- 分区键可以由最多 16 列组成。
- 一个表最多可以有 65,636 个分区。
- 分区范围之间不能有空隙。例如，你不能拥有 1991–1993 年 和 1995–2001 年 的毕业日期分区（跳过了 1994 年）。
- 存储在分区中的所有行，其值必须小于且不等于该分区的上界。换句话说，如果插入一条毕业日期为 01-JUN-2000 的学生记录，该记录将存储在 `P_2001` 分区中，而不是 `P_2000` 分区。因此，插入毕业日期为 01-JUN-2001 或更晚的学生记录将导致该记录存储在 `P_ERROR` 分区中。
- `LESS THAN` 子句中指定的值必须是一个字面量、日期，或者是通过 `TO_DATE` 函数填充后的常量。日期值也必须使用 `TO_DATE` 函数来包含世纪。
- 范围分区表不能包含 `LONG` 或 `LONG RAW` 数据类型的列。
- 会导致记录跨越分区边界的更新操作不被允许，除非在创建表时指定了 `ENABLE ROW MOVEMENT` 子句。如果没有此子句，尝试将学生的毕业日期从 16-MAY-95 更新为 16-MAY-96 将需要将该记录从分区 `P_1995` 移动到 `P_1996`，这是不被允许的。
- 尝试插入不符合任何已定义分区范围值的记录将导致 `ORA-14400`：*插入分区键超出了最高合法分区键值错误*。如果未指定带有 `MAXVALUE` 子句的 `P_ERROR` 分区，则插入毕业日期为 01-JUN-2001 或更晚，或值为 `NULL` 的学生记录将不被允许。

如果每年毕业的学生人数差异较大，选择 `GRADUATION_DATE` 作为表的分区键可能效率较低。如果是这种情况，那么存储在每个分区内的行数将变得不均匀，有些分区的增长速度远快于其他分区。虽然这种不均匀并不总是对性能有害，但它可能导致并行操作（如并行查询和并行 DML）的性能低下。如果是这种情况，则可以考虑使用哈希分区代替范围分区。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_209_0.png)

> “并行操作的更多细节将在第 10 章“操作系统调优”中描述。”

### 列表分区

列表分区与范围分区类似，不同的是它们基于一组指定的值，而非值的范围。例如，假设你决定使用列表分区对 `DEGREE`（学位）列来分区 `STUDENT_HISTORY` 表。这意味着 `DEGREE` 是分区键：

```sql
SQL> CREATE TABLE student_history
2  (student_id        NUMBER(10),
3   degree            VARCHAR2(3),
4   graduation_date DATE,
5   final_gpa         NUMBER
6  PARTITION BY LIST (degree)
7  (PARTITION p_undergrad VALUES ('BS', 'BA', 'BBA', 'BFA')
8   TABLESPACE hist_tab01,
9   PARTITION p_graduate VALUES ('MA', 'MBA', 'MFA', 'MS')
10  TABLESPACE hist_tab02,
11  PARTITION p_doctorate VALUES ('PHD')
12  TABLESPACE hist_tab03);
```

上述语法将创建一个包含三个分区的表，名称分别为 `P_UNDERGRAD`、`P_GRADUATE` 和 `P_DOCTORATE`。出于性能考虑，这些分区中的每一个在物理上都存储在一个独立的表空间中（`HIST_TAB01` 到 `HIST_TAB03`）。插入到表中的每一行都将根据学生的学位代码被放置到相应的分区中。图 3.22 展示了这一概念。

### 图 3.22 列表分区的 `STUDENT_HISTORY` 表

![](img/832fbc6aca8b6075843ca6f2356c0a8d_210_0.png)

在检查上述结构时，应考虑与列表分区相关的一条规则：不符合分区键任何条件的值将引发 `ORA-14400` 错误。与范围分区不同，Oracle9i Release 1 目前不支持使用 `MAXVALUE` 选项来消除此问题。

> 特定的物理段属性，如 `STORAGE` 参数，可以在分区级别进行分配。这些属性将覆盖表的默认属性。

### 哈希分区

哈希分区使用哈希算法将插入的记录分配到各个分区中。这样做保持每个分区中的记录数量相对均匀，从而改善并行操作（如并行查询和并行 DML）的性能。假设你决定使用哈希分区对 `STUDENT_ID` 列，而不是使用范围分区来分区 `STUDENT_HISTORY` 表。这意味着 `STUDENT_ID` 是分区键：
