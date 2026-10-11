
尽管该列上存在索引。当 SQL 语句的 WHERE 子句中对索引列应用了任何函数或操作时，就会出现这种行为。*基于函数的索引* 通过在创建索引时将函数纳入索引中来解决此问题。B-Tree 索引和位图索引都可以创建为基于函数的索引。以下是一个在 EMPLOYEE 表的 FIRST_NAME 列上创建的基于函数的索引示例：

```sql
SQL> CREATE INDEX employee_first_name_upper_idx
  2  ON employee (UPPER(first_name));
```

优化器现在可能会考虑使用新的 EMPLOYEE_FIRST_NAME_UPPER_IDX 索引，从而在检索名为 Reginald 的员工时避免全表扫描。

基于函数的索引的另一个实用例子是，当你希望在使用派生列的语句 WHERE 子句中避免全表扫描时。例如，在下面的查询中，列 TOTAL_SALE 并不是表中的实际列；相反，它是通过将 UNITS 乘以 PRICE 派生出来的：

```sql
SQL> SELECT product_id, units, price, price*units 'TOTAL_SALE'
  2  FROM sales
  3  WHERE (price*units) > 10000;
```

然而，我们可以在派生列 TOTAL_SALE 上创建一个基于函数的 B-Tree 索引，然后使用该索引来消除查询中本应发生的全表扫描：

```sql
SQL> CREATE INDEX sales_total_sale_idx
  2  ON sales (price*units)
  3  TABLESPACE appl_idx;
```

优化器现在能够在为上一个查询制定执行计划时考虑使用该索引。

![](img/832fbc6aca8b6075843ca6f2356c0a8d_196_0.png)

必须将 init.ora 参数 QUERY_REWRITE_ENABLED 设置为 TRUE 才能使用基于函数的索引。

## 反向键索引

反向键索引（RKI）是一种特殊类型的 B-Tree 索引。当在包含顺序数字的列上构建索引时，RKI 非常有用。如果在包含此类数据的列上构建传统 B-Tree 索引，索引往往会发展出许多层级。由于 B-Tree 的深度超过四层会降低性能，因此 RKI 非常适合这种情况。

反向键索引通过简单地反转索引列中的数据来解决这个问题：它将每个列键值的字节反转，然后对新的反转数据进行索引。与原始顺序数据相比，这种新的数据在值范围内通常分布得更加均匀。

例如，如果你确定需要在 EMPLOYEE 表的 EMP_ID 列上建立索引，那么反向键索引是合适的，因为存储在 EMP_ID 列中的数据是顺序的：

```sql
SQL> SELECT *
  2  FROM employee;
```

| EMP_ID | LAST_NAME | FIRST_NAME | TITLE | DEPT_ID | GENDER |
| :----- | :--------- | :----------- | :------------------- | :------ | :----- |
| 100 | Baker | Benda | Dir Web Development | 601 | F |
| 101 | Douglass | Laura | Dir of Research | 301 | F |
| 102 | Jim | Schwarz | Dir of IS | 401 | M |
| 110 | Block | Robin | Corporate Counsel | 501 | F |
| 106 | Bron | Reginald | Dir of Marketing | 601 | M |
| 108 | Weishan | Matt | Technical Writer | 601 | M |
| 107 | Gastel | Tony | Oracle DBA | 401 | M |

```sql
SQL> CREATE INDEX employee_emp_id_idx
  2  ON employee (emp_id)
  3  REVERSE
  4  TABLESPACE APPL_IDX;
```

使用 ALTER INDEX 命令也可以将现有的非反向键索引重建为反向键索引：

```sql
ALTER INDEX employee_emp_id_idx REBUILD REVERSE;
```

图 3.17 展示了一个示例，说明 EMPLOYEE 表上 EMP_ID 列的反向键索引在内部看起来是什么样子的。

| ORIGINAL ID | REVERSED ID | ROWID |
| :---------- | :---------- | :---------------------------------- |
| 100         | 001         | AAAD7IAAJAAAAAM8AAA               |
| 101         | 101         | AAAD7IAAJAAAAAM8AAB               |
| 102         | 201         | AAAD7IAAJAAAAAM8AAC               |
| 110         | 011         | AAAD7IAAJAAAAAM8AAD               |
| 106         | 601         | AAAD7IAAJAAAAAM8AAE               |
| 108         | 801         | AAAD7IAAJAAAAAM8AAF               |
| 107         | 701         | AAAD7IAAJAAAAAM8AAG               |

索引是反向键这一事实对应用程序开发人员和用户来说是透明的。在查询中使用它不需要特殊的语法。

反向键索引仅适用于等值和非等值搜索。在反向键索引列上执行范围扫描（例如，使用 `BETWEEN`、`>`、`<`）的查询将无法使用该索引，并会导致全表扫描。

## 索引组织表

使用 B-Tree、位图（Bitmapmed）和反向键索引所带来的性能提升，源于这些索引中的条目直接指向索引底层表中对应数据的行 ID。这是从行未按任何特定顺序物理存储的表中检索行的一种有效方式。这种类型的表被称为 *堆表*（Heap Tables）。Oracle 在大多数表中以堆方式存储行数据，因为行在表内的块中分配方式或多或少是随机的。这种随机性是因为 Oracle 在决定存储位置时不考虑行的内容。相反，Oracle 只是将行存储在表的自由列表（Freelist）中找到的第一个块上。

### Oracle 学习目标

解释索引组织表

![](img/832fbc6aca8b6075843ca6f2356c0a8d_199_0.png)

> 有关自由列表如何用于管理表的块，请参阅第 8 章“磁盘 I/O 调优”。

如果你确实希望以特定顺序存储表数据，那么你就不能使用堆表。Oracle 专门为此目的提供了索引组织表（IOTs）。索引组织表不再存储指向行数据其余部分存储位置的行 ID 指针，而是将行数据完整地存储在索引本身中。这带来了两个性能好处：

- 表行按索引顺序存储。如果你使用主键访问表，IOT 比传统表能更快地返回行。
- 使用 B-tree 索引时，读取索引然后读取表所产生的额外 I/O 被消除了。

假设你决定创建一个名为 EMPLOYEE_HISTORY 的新应用表，它将按 EMP_ID 存储员工信息。由于你预计会按 EMP_ID 访问此表，创建此表时选择 IOT 可能是一个不错的选择：

```sql
SQL> CREATE TABLE employee_history
  2  (employee_id number primary key,
  3   last_name varchar2(20),
  4   first_name varchar2(20),
  5   title varchar2(30),
  6   hire_date date,
  7   departure_date date)
  8  ORGANIZATION INDEX TABLESPACE app1_idx
  9  PCTTHRESHOLD 25
 10  INCLUDING first_name
 11  OVERFLOW TABLESPACE app1_of
 12  MAPPING TABLE;
```

![](img/832fbc6aca8b6075843ca6f2356c0a8d_200_0.png)

所有索引组织表都必须在作为索引基础的列上定义主键约束。IOT 不能包含唯一约束，也不能进行聚簇。聚簇将在后续章节中讨论。

与 IOT 创建相关的 CREATE TABLE 语法的重要部分总结在表 3.22 中。

### 表 3.22 IOT 创建语法

| 子句 | 描述 |
| :--- | :--- |
| ORGANIZATION INDEX | 指定此表是 IOT。 |
| PCTTHRESHOLD | 指定保留多少百分比的整个数据块以存储与主键值相关的行数据，该值必须在 0 到 50 之间（默认为 50）。 |
| INCLUDING | 指定当行长度超过 PCTTHRESHOLD 预留的大小时，在哪一列将行拆分为两部分。 |
| OVERFLOW TABLESPACE | 指定当行长度超过 PCTTHRESHOLD 预留的大小时，行数据的第二半部分将存储的表空间。 |
| MAPPING TABLE | 促使创建关联的映射表，这是在 IOT 上创建位图索引所需的。映射表在本节末尾有详细描述。 |

在此表中填充数据后，其内容可能类似于图 3.18 所示。

