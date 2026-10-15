
第一个数据分区的起始值是包含的，因为整体起始边界（`'1/1/1992'`）是包含的（默认）。同样，最后一个数据分区的结束边界是包含的，因为整体结束边界（`'12/31/1992'`）是包含的（默认）。剩余的 `STARTING` 值是包含的，剩余的 `ENDING` 值都是排斥的。每个数据分区持有 `n` 个键，其中 `n` 由 `EVERY` 子句给出。使用公式 `start + every` 找到每个数据分区范围的结束。如果 `EVERY` 值不能整除 `START` 和 `END` 范围，最后一个数据分区的键可能会较少。

在示例 13-9 中，有一个语句会产生 10 个数据分区，每个分区包含 100 个键值（`1 < b <= 101`, `101 < b <= 201`, ..., `901 <= b <= 1000`）。

# 示例 13-9 创建具有 10 个数据分区的表

```sql
CREATE TABLE t(a INT, b INT)
PARTITION BY RANGE(b) (STARTING FROM (1)
EXCLUSIVE ENDING AT (1000) EVERY (100))
```

第一个数据分区（`b > 1` 且 `b <= 101`）的起始值是排他的，因为整体的起始边界（`1`）是排他的。同样，最后一个数据分区（`b > 901` `b <= 1000`）的结束边界是排他的，因为整体结束边界（`1000`）是包含的。剩余的 `STARTING` 值都是排他的，剩余的 `ENDING` 值都是包含的。每个数据分区持有由 `EVERY` 子句给定的 `n` 个键值。

最后，如果整体子句的起始和结束边界都是排他的，那么第一个数据分区的起始值是排他的，因为整体起始边界（`1`）是排他的。该分区是排他的，因为整体结束边界（`1000`）是排他的。剩余的 `STARTING` 值都是排他的，`ENDING` 值都是包含的。每个数据分区（最后一个除外）持有 `n` 个键值，`n` 由 `EVERY` 子句给出。

# 13.7.2 手动生成范围

手动生成会为 `PARTITION BY` 子句中列出的每个范围创建一个新的数据分区。这种语法形式允许在定义范围时具有更大的灵活性，从而增加了您的数据和 LOB 放置选项。示例 3 和 4 展示了如何使用 `CREATE TABLE` 语句来定义并手动生成数据分区指定的范围。

在示例 13-10 中，我们看到一个对两个日期列进行分区的语句，这两个列都是自动生成的。注意这里使用了自动生成的 `CREATE TABLE` 语法形式，并且每个范围只指定了一个端。另一个端是根据相邻的数据分区和使用 `INCLUSIVE` 选项推断出来的。

# 示例 13-10 在两个数据列上创建分区表

```sql
CREATE TABLE sales(invoice_date, inv_month INT NOT NULL
GENERATED ALWAYS AS (month(invoice_date)), inv_year INT NOT
NULL GENERATED ALWAYS AS (year(invoice_date)), item_id INT NOT NULL,
cust_id INT NOT NULL)
PARTITION BY RANGE (inv_year, inv_month)
(
PART Q01_02 STARTING (2002,1) ENDING (2002, 3) INCLUSIVE,
PART Q02_02 ENDING (2002, 6) INCLUSIVE,
PART Q03_02 ENDING (2002, 9) INCLUSIVE,
PART Q04_02 ENDING (2002,12) INCLUSIVE,
PART CURRENT ENDING (MAXVALUE, MAXIMUM)
);
```

允许范围存在间隙。`CREATE TABLE` 语法支持间隙，允许您为范围指定一个 `STARTING` 值，该值与上一个数据分区的 `ENDING` 值对齐。

示例 13-11 创建了一个在 101 和 200 之间存在间隙的表。

# 示例 13-11 创建带有范围间隙的分区表

```sql
CREATE TABLE foo (a INT)
PARTITION BY RANGE (a)
(STARTING FROM (1) ENDING AT (100),
STARTING FROM (201) ENDING AT (300))
```

使用 `ALTER TABLE` 语句允许添加或删除数据分区，这也会导致范围出现间隙。

当向分区表插入行时，它会根据其键值和所属的范围自动放置在适当的数据分区中。如果它落在表定义的任何范围之外，插入将失败并向应用程序返回错误：

```sql
SQL0327 The row cannot be inserted into table <tablename> because it is outside the bounds of the defined data partition ranges.
SQLSTATE=22255
```

# 13.8 限制

在使用数据分区时，我们可以识别表级限制和语句级限制。

- 表级限制：
使用自动生成语法形式（包含 `EVERY` 子句）创建的表被限制在在表分区键中使用数值或日期类型。

- 语句级限制：
在 SQL 语句级别，我们可以识别出以下限制：
- 自动生成语法形式中不支持 `MINVALUE` 和 `MAXVALUE`。
- 范围是升序的。
- 自动生成语法形式中只能指定一列。
- `EVERY` 子句中的增量必须大于零。
- `ENDING` 值必须大于或等于 `STARTING` 值。

# HACMP 应用服务器脚本

在本附录中，我们提供了在 HACMP 环境下的 HADR 中使用的应用程序服务器脚本。应用程序服务器的启动和停止脚本用于自动化 HADR 切换。

# A.1 hadr_primary_takeover.ksh

示例 A-1 显示了带有 HACMP 环境的 HADR 中 HADR 切换的示例脚本。

示例：A-1 `hadr_primary_takeover.ksh`

```ksh
#!/usr/bin/ksh -x
############################################################
# hadr_primary_takeover.ksh
# 此脚本在旋转资源组启动时被调用。
# 在正常 HACMP 启动期间跳过进程。
# 在发生故障时触发 hadr 切换。
############################################################
exec >> /tmp/`basename $0`.log
exec 2&1
echo "######################################################################"
date
echo "################################################################################"
set -x
############################################################
# set PARAMETER
############################################################
. /home/hadrinist/scripts/env
############################################################
# set START_MODE
############################################################
# LOCAL=HOMLOCAL!HOME
# PRE="NOMALLFALLOVER(manual online operation
# PRE!="*FALLBACKFALLOVER
### [ /usr/es/sbin/cluster/utilities/clRGinfo -a >dev/null 2>&1
### if [ $? -ne 0 ]; then
### echo HACMP V5.2 must be running
### exit 1
### fi
/usr/es/sbin/cluster/clRGinfo -a
```

404 High Availability and Scalability Guide for DB2 on Linux, UNIX, and Windows

```ksh
/usr/es/sbin/cluster/utilities/clRGinfo -a | grep $R_RG \
| awk -F\" '{print $2}' | awk -F\: '{print $1}' | read PRENODE
```
