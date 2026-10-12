
## 图 3.21 范围分区的 STUDENT_HISTORY 表

```sql
STUDENT_HISTORY TABLE
Using GRADUATION_DATE
Range Partition Key

INSERT INTO
student_history
(student_id, degree,
graduation_date, final_jpa)
VALUES
(123456789, 'BBA', '12-MAY-99', 3.75);
```

在检查上述结构时，应考虑几条与范围分区相关的规则：
- 分区键可以最多由 16 个列组成。
- 一个表最多可以有 65,636 个分区。
- 分区范围之间不能有任何间隙。例如，你不能同时拥有 1991–1993 年和 1995–2001 年毕业日期的分区（跳过了 1994 年）。
- 存储在分区中的所有行值都小于且等于该分区的上限。换句话说，为在 2000年6月1日毕业的学生插入的记录将存储在 `P_2001` 分区中，而不是 `P_2000` 分区。因此，插入一个一个毕业日期为 2001年6月1日或更晚的学生记录将导致该记录存储在 `P_ERROR` 分区中。
- 指定的值必须是字面量、日期或常量。
- 除非指定了 `ENABLE MOVEMENT` 子句，否则不允许会导致记录跨越边界的更新。
- 尝试插入不符合任何定义分区的值将引发 `ORA-1400` 错误。

## 列表分区 (LIST PARTITIONING)

列表分区与范围分区类似，但它们是基于一组值而不是值的范围。例如，假设你决定在 `DEGREE` 列上使用列表分区来划分 `STUDENT_HISTORY` 表。这意味着 `DEGREE` 是分区键：

```sql
SQL CREATE TABLE student_history
2 (student_id NUMBER(10),
3 degree VARCHAR(32),
4 graduation_date DATE,
5 final_gpa NUMBER)
6 PARTITION BY LIST (degree)
7 (PARTITION p_undergrad VALUES ('BS','BA','BBA','BFA'))
8 TABLESPACE hist_tab01,
9 (PARTITION p_graduate VALUES ('MA','MBA','MFA','MS'))
10 TABLESPACE hist_tab02,
11 (PARTITION p_doctor VALUES ('PHD'))
12 TABLESPACE hist_tab03);
```

上述语法将创建一个包含三个分区的表，命名为 `P_UNDERGRAD`、`P_GRADUATE` 和 `P_DOCTOR`。插入到表的每行都将根据学位代码放在适当的分区中。图3.22 说明了这一概念。

## 图 3.22 列表分区的 STUDENT_HISTORY 表

与范围分区不同，列表分区不支持 `P_ERROR` 分区。Oracle9i Release 1 不支持使用 `MAXVALUE` 选项。

## 哈希分区 (HASH PARTITIONING)

哈希分区使用哈希算法将插入的记录分配到分区。其效果是保持每个分区中的记录数相对均匀，从而提高了并行查询和并行 DML 等并行操作的性能。假设你决定在 `STUDENT_ID` 列上使用哈希分区而不是范围分区来划分 `STUDENT_HISTORY` 表。这意味着 `STUDENT_ID` 是分区键：

```sql
SQL> CREATE TABLE student_history
2 (student_id NUMBER(10),
3 degree VARCHAR(32),
4 graduation_date DATE,
5 final_gpa NUMBER)
6 PARTITION BY HASH (student_id)
7 PARTITIONS 6
8 STORE IN (hist_tab01, hist_tab02, hist_tab03, hist_tab04, hist_tab05, hist_tab06);
```

上述语法将创建一个包含六个分区的表，由系统生成。每向 `STUDENT_HISTORY` 表插入新记录时，Oracle 将将 `STUDENT_ID` 中的值通过哈希算法，然后使用生成的哈希值来确定该行应该插入到哪个分区。图3.23 说明了这一概念。

### 172 第 3 章 • SQL 应用调优与设计

## 图 3.23 哈希分区的 STUDENT_HISTORY 表

STUDENT_HISTORY 表

使用 STUDENT_ID

哈希分区键

```sql
INSERT INTO
student_history
(student_id, degree,
graduation_date, final_gba)
VALUES
(123456789,'BBA','12-MAY-99',3.75);
```

![](img/c36db8fbb4893c630ad429a99bfd63e3_211_0.png)

在检查上述结构时，应考虑以下几个与哈希分区相关的规则：
- 分区键应具有高基数——该列应包含唯一值或极少数重复值。
- 当应用程序通过唯一键从分区表检索数据时，哈希分区的效果最好。在哈希分区表上进行范围查找无法从分区中获益。
- 当哈希分区表创建了适当的索引时，它们可以提高两个或多个分区表之间连接的性能。
- 不允许会导致记录跨越分区边界的更新。
- 可以在每个分区上建立本地哈希索引。

Copyright©2002 SYBEX, Inc., Alameda, CA

www.sysex.com

## 提高应用性能 173

> 注意：分区表的索引策略将在本节的稍后部分讨论。
> 提示：Oracle 建议分区总数应该是 2 的幂，以最大化提高哈希分区算法的有效性。

## 复合分区

顾如其名，复合分区代表范围分区和哈希分区的结合。当需要范围分区，但每个范围内的数值数量分布不均时，这种分区类型非常有用。复合分区创建的分区在随后又被进一步划分为子分区：

```sql
CREATE TABLE student_history (
student_id NUMBER(10),
degree VARCHAR2(3),
graduation_date DATE,
final_gpa NUMBER
)PARTITION BY RANGE (graduation_date)
SUBPART BY HASH(student_id) SUBPARTITIONS 4
STORE IN (hist_tab01, hist_tab02, hist_tab03, hist_tab04)
(PARTITION p_1997 VALUES LESS THAN
(DATE('01-JUN-1997','DD-MON-YYYY'))),
PARTITION p_1998 VALUES LESS THAN
(DATE('01-JUN-1998','DD-MON-YYYY'))),
PARTITION p_1999 VALUES LESS THAN
(DATE('01-JUN-1999','DD-MON-YYYY'))),
PARTITION p_2000 VALUES LESS THAN
(DATE('01-JUN-2000','DD-MON-YYYY'))),
PARTITION p_2001 VALUES LESS THAN
(DATE('01-JUN-2001','DD-MON-YYYY'))),
PARTITION p_ERROR VALUES LESS THAN (MAXVALUE));
```

上述语法将创建一个具有六个范围分区的表，命名为 P_1997 到 P_2001 以及 P_ERROR。每个范围分区都会被分为四个哈希子分区，每个子分区都有一个系统生成的分区名称。图 3.24 展示了这一概念。

### 174 第 3 章 · SQL 应用调优与设计

## 图 3.24 复合分区的 STUDENT_HISTORY 表

STUDENT_HISTORY 表

使用 GRADUATION_DATE 和 STUDENT_ID

复合分区键

```sql
INSERT INTO
student_history
(student_id, degree,
graduation_date, final_gpa)
VALUES
(12345678, 'BBA', '12-MAY-99', 3.75);
```

![](img/c36db8fbb4893c630ad429a99bfd63e3_213_0.png)

在检查上述结构时，应考虑以下几个与复合分区相关的指南：
- 分区仅是逻辑结构；表数据物理上存储在子分区级别。
- 复合分区对于分区级别的历史与日期相关的查询非常有用。
- 复合分区对于子分区级别的并行操作（包括查询和 DML）也有用。
- 通过使用复合本地索引也支持分区内连接。不支持全局本地索引。

本地索引和全局分区索引之间的区别将在下一节讨论。

## 为分区表建立索引
