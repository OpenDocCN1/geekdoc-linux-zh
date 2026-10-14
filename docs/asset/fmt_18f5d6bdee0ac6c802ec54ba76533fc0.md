
# 分区示例

为了理解这些索引类型，首先请学习一些背景信息。回想一下，分区或非分区表都可以拥有分区或非分区索引；索引分区的唯一限制是聚集索引可能无法被分区。如果一个索引的最左侧列与分区键的顺序和数量完全相同，则该索引被视为`prefixed index`。此外，索引列可以是分区键的超集，但不能是其子集。

`global index`只能是前缀的，但其分区分布通常与其关联的表不同。如果需要全局非前缀索引，请改用普通索引。Oracle 选择不实现此功能，因为其使用开销的性能比普通索引更差。全局索引**不会**由 Oracle 维护。也就是说，一旦设置，索引分区与表分区之间的特定关系（值对应关系）**不会**由 Oracle 维护。全局索引的主要缺点是 Oracle 优化器无法利用其进行分区剪裁（partition elimination）。另一方面，全局索引提供了按关联表以外的值范围对索引进行区的选项。这在许多情况下非常有用，例如数据仓库以及与在线分析处理应用相关的多维数据库。此外，在存储空间紧张的情况下，全局索引是极具吸引力的选择，它们的分区数量可能比关联表少。列表 10.7 给出了一个分区表及其关联全局前缀索引的示例。

## 列表 10.7 分区表的全局前缀索引

```sql
SQL create table EMPS
(EMPID number(5), SSN number(9), EMPNAME varchar(30), EMPADDR varchar(25))
partition by range (EMPID)
(partition P1 values less than (33334),
partition P2 values less than (66668),
partition P3 values less than (100000));
```

```sql
SQL create index EMPS_IDX
on EMPS (EMPID, SSN)
global
partition by range (EMPID)
partition P2 values less than (50001),
partition P3 values less than (100000));
```

本地索引可以是前缀的，也可以不是。然而，索引分区与其关联的表分区之间存在一一对应的关系。这种关系在设置时是`equi-partitioned`的，并在之后由 Oracle 维护。Oracle 优化器可以利用分区剪裁，因此如前所述，它可能会提供与 RAID 相当的大幅性能提升。因此，本地索引的优势是自动的等分区维护，而其相关的缺点是具有限制性的，即必须与其关联表具有相同的分区方案（无论是否为前缀）。对于多个索引需求，这可能导致管理过于复杂。此外，关联的交错存储需求可能变成一个棘手的问题。

列表 10.8 给出了分区表及其关联本地前缀索引的示例。列表 10.9 给出了分区表及其关联本地非前缀索引的示例。请注意，在这两种情况下都没有使用 `PARTITION BY RANGE OR VALUES LESS THAN` 子句，因为 Oracle 知道这是一个本地索引，并将根据完全相同的表规范进行等分区。`LOCAL` 关键字会告知 Oracle。通过对比列表 10.8、10.9 与列表 10.7，可以查看本地索引与全局索引、本地前缀索引与本地非前缀索引之间的区别。

虽然本地索引分区的区别仅在于索引列的选择（这在实际上决定了它们是否为前缀），但全局索引分区的区别在于值范围的选择。

## 列表 10.8 分区表及其关联的本地前缀索引

```sql
SQL> create table EMPS
(EMPID number(5), SSN number(9),
EMPNAME varchar(30), EMPADDR varchar(75))
partition by range (EMPID)
(partition P1 values less than (33334),
partition P2 values less than (66668),
partition P3 values less than (1000000));
```

```sql
SQL> create index EMPS_IDX
on EMPS (EMPID, SSN)
local
(partition IP1,
partition IP2,
partition IP3);
```

## 列表 10.9 分区表及其关联的本地非前缀索引

```sql
SQL> create table EMPS
(EMPID number(5), SSN number(9),
EMPNAME varchar(30), EMPADDR varchar(75))
partition by range (EMPID)
(partition P1 values less than (33334),
partition P2 values less than (66668),
partition P3 values less than (1000000));
```

```sql
SQL> create index EMPS_IDX
on EMPS (SSN)
local
(partition IP1,
partition IP2,
partition IP3);
```

# 维护操作

有两个基本语句执行所有的分区操作。它们是 `ALTER TABLE` 和 `ALTER INDEX`。`ALTER TABLE` 语句的分区扩展如下：

- `DROP PARTITION`
- `ADD PARTITION`
- `RENAME PARTITION`
- `MODIFY PARTITION`
- `TRUNCATE PARTITION`
- `SPLIT PARTITION`
- `MOVE PARTITION`
- `EXCHANGE PARTITION`

`ALTER INDEX` 语句的分区扩展如下：

- `DROP PARTITION`
- `RENAME PARTITION`
- `REBUILD PARTITION`
- `MODIFY PARTITION`
- `SPLIT PARTITION`
- `PARALLEL`
- `UNUSABLE`

大多数分区操作对于经验丰富的 Oracle DBA 来说应该是熟悉且不言自喻的，因为它们通常“看起来和用起来”就像普通的表或索引操作（如 `DROP TABLE` 或 `DROP INDEX`）。然而，你将仔细观察那些分区特有的操作（`SPLIT`, `MOVE`, `EXCHANGE` 和 `UNUSABLE`）。列表 10.10 给你一个拆分（split）的示例。

## 列表 10.10 拆分分区维护操作

```sql
SQL> alter table EMPS split partition P3
at (75000)
into (partition P3, partition P4);
```

列表 10.10 中发生的情况是：分区 `P3` 保留了所有 `EMPID` 值小于 `75000` 的行（但大于 `P2` 中的任何值），而新分区 `P4` 存储了所有值等于或大于 `75000` 的行。如你所见，`SPLIT` 总是产生一个额外的分区。

## 列表 10.11 移动分区

```sql
SQL> alter table EMPS move partition P3
tablespace;
```

## 列表 10.12 交换分区

```sql
SQL> alter table EMPS exchange partition P3
tablespace;
```
