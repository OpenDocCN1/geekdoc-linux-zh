
# 优化器

网络代价适用于分布式查询或通过数据库链接引用远程对象的查询。在这种情况下，CBO 将确定查询的最优驱动站点。驱动站点控制 Oracle 应该将行从本地数据库推送到远程数据库，还是由 Oracle 将行从远程站点拉取到本地数据库中。例如，考虑以下情况：

```sql
select c.customer_id,c.customer_name,
    a.street_no,a.street_name,a.city
from customer,
    addresses@mydblink a
where    c.customer_id = a.customer_id and
    c.customer_id = :b1
```

在上面的示例中，优化器可以通过获取单个客户记录并将行推送到远程站点，根据客户 ID 与地址表连接；或者将地址行拉取到本地数据库并与客户表连接。后者的方法显然效率较低，因为将处理更多的行。在这种情况下，优化器将确定该查询的驱动站点为本地数据库。

## 4.6 The Optimizer

### Execution Plan

```sql
SELECT STATEMENT Cost=33193,58453 bytes=1636684 ,
FILTER Cost=$, bytes=
TABLE ACCESS BY INDEX ROWID PA_EXPENDITURE_ITEMS_ALL
Cost=33193,58453 bytes=1636684 ,
INDEX RANGE SCAN PA_EXPENDITURE_ITEMS_N2 Cost=127,58453 bytes=-
```

When analyzing an execution plan for a particular query, it is important to generate the execution plan based on the original SQL statement. For example, if the SQL statement uses `bind variables`, you should evaluate the execution plan with the `bind variables`, and not with the substituted literal values. The optimizer uses different selectivity and cardinality estimates for queries which use `bind variables` than it uses for queries which use literal scales.

The selectivity of an `AND` expression is defined as:

> `((selectivity of expression 1) × (selectivity of expression 2))`

The selectivity of an `OR` expression is defined as:

> `((selectivity of expression 1 + selectivity of expression 2) – (selectivity of expression 1 × selectivity of expression 2))`

For example, consider the following query.

```sql
select ei.expenditure_item_id,ei.task_id,
ei.project_rate_type
from pa_expenditure_items_all ei
where ei.task_id between :b1 and :b2
```

Since the query contains a `BETWEEN` operator and variable, the default selectivity of 5 percent is used. The cost of the index probe on `PA_EXPENDITURE_ITEMS_N2` is 127, and the cardinality is 58453.

## 4.6.2.3 CBO 术语

`基数`、`代价`、`选择性`等术语是 CBO 架构不可或缺的一部分。

### 4.6.2.3.1 代价
是 CBO 分配给每个操作（如访问、连接和排序）的指标。对于每个索引访问或表访问，CBO 会为该操作分配一个代价，该代价很大程度上取决于特定访问方法所需的 I/O 数量。全表扫描代价基于多块 I/O 因子，该因子通过 `init.ora` 参数 `db_file_multiblock_read_count` 指定。

### 4.6.2.3.2 基数
基数是指表中的行数。CBO 预期给定操作返回的行。例如，对于特定的索引访问，计算出的基数可能报告为 100，意味着优化器估计在探测此索引后将返回 100 行。

估计或计算的基数可以表示如下：

`Ec = (selectivity) × (number of rows)`

### 4.6.2.3.3 选择性
选择性是 0 到 1 之间的一个值，表示根据过滤或连接表达式从表中返回的行比例。

`Se = 返回的行数 / 总行数`

如果在 SQL 语句中使用字面量，CBO 能够利用数据字典中的列统计信息，将字面量与该列的高值和低值进行比较。然而，对于绑定变量，CBO 使用默认的选择性估计，因为在计划生成时不会检查变量的值。对于形式为 `[col :b1]` 的等值表达式，默认选择性为 `1/NDV`。对于 `<=` 或 `>=` 等范围谓词，默认选择性为 5%。涉及 `BETWEEN` 操作符的谓词会被转换为等效的 `<` 和 `>=`。

AND 表达式的选择性定义为：

> `((表达式 1 的选择性) × (表达式 2 的选择性))`

OR 表达式的选择性定义为：

> `((表达式 1 的选择性 + 表达式 2 的选择性) – (表达式 1 的选择性 × 表达式 2 的选择性))`

由于查询包含 `BETWEEN` 操作符和变量，因此使用了 5% 的默认选择性。在 `PA_EXPENDITURE_ITEMS_N2` 上的索引探测代价为 127，基数为 58453。
