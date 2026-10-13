
# `mysql -u root -p`

Enter password: ******

`mysql>`

当您处于 `mysql` 会话中（并且已选择数据库）时，您可以显示所有或选定的表记录，选择显示哪些列，或选择记录的排序方式。

### 显示所有或选定的记录

假设当前数据库是 `allusers`（如前例所示），键入以下命令以从 `names` 表中选择（`SELECT`）所有记录（`*`）并按其输入数据库的顺序显示它们。

```
mysql> SELECT * FROM names;
+----+--------+--------------+----------+------+--------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----+--------+--------------+----------+------+--------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Mantsy | 1515 Broadway | New York | NY | 10028 |
+----+--------+--------------+----------+------+--------+
```

以下命令显示 `names` 表中 `lastname` 列设置为 `Jones` 的所有记录。您可以改用 `lastname`，也可以搜索表中使用的任何列名的值。

```
mysql> SELECT * FROM names WHERE lastname = "Jones";
+----+-------+---------------+----------+------+--------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----+-------+---------------+----------+------+--------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
+----+-------+---------------+----------+------+--------+
```

使用 `OR` 运算符，您可以选择匹配多个不同值的记录。在以下命令中，`firstname` 为 `Chris` 或 `Howard` 的记录将被匹配并显示。

```
mysql> SELECT * FROM names WHERE firstname = "Chris" OR firstname = "Howard";
+--------+--------+---------------+----------+-------+--------+
| firstname | lastname | streetaddr | city | state | zipcode |
+--------+--------+---------------+----------+-------+--------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Mantsy | 1515 Broadway | New York | NY | 10028 |
+--------+--------+---------------+----------+-------+--------+
```

要根据记录中两个列的值匹配并显示记录，您可以使用 `AND` 运算符。在以下命令中，`firstname` 为 `Chris` 且 `lastname` 为 `Smith` 的任何记录都将被匹配。

```
mysql> SELECT * FROM names WHERE firstname = "Chris" AND lastname = "Smith";
+--------+--------+------------+------+-------+--------+
| firstname | lastname | streetaddr | city | state | zipcode |
+--------+--------+------------+------+-------+--------+
```

| firstname | lastname | streetaddr | city | state | zipcode |
|---|---|---|---|---|---|
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |

## 显示选定列

您不需要显示数据的每一列。与前面示例中所示使用星号（`*`）来匹配所有列不同，您可以输入以逗号分隔的列名列表。以下命令显示 “names” 表中所有记录的 `firstname`、`lastname` 和 `zipcode` 记录：

```
mysql> SELECT firstname,lastname,zipcode FROM names;
```

| firstname | lastname | zipcode |
|---|---|---|
| Chris | Smith | 98999 |
| John | Jones | 54889 |
| Howard | Manty | 10028 |

同样，您可以根据需要按任意顺序排列列。输入以下命令以显示相同的三列，其中 `zipcode` 列排在最前面：

```
mysql> SELECT zipcode,firstname,lastname FROM names;
```

| zipcode | firstname | lastname |
|---|---|---|
| 98999 | Chris | Smith |
| 54889 | John | Jones |
| 10028 | Howard | Manty |

您还可以将列选择与记录选择混合使用，如以下示例所示：

```
mysql> SELECT firstname,lastname,city FROM names WHERE firstname = "Chris";
```

| firstname | lastname | city |
|---|---|---|
| Chris | Smith | Gig Harbor |

## 排序数据

您可以根据所选列中的值对记录进行排序。例如，使用 `ORDER BY` 运算符，您可以根据 `lastname` 列显示记录：

```
mysql> SELECT * FROM names ORDER BY lastname;
```

| firstname | lastname | streetaddr | city | state | zipcode |
|---|---|---|---|---|---|
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
| Chris | Smith | 167 Small Road | Gig Harbor | WA | 98999 |

要按城市名称对记录进行排序，可以使用以下命令：

```
mysql> SELECT * FROM names ORDER BY city;
```

| firstname | lastname | streetaddr | city | state | zipcode |
|---|---|---|---|---|---|
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Chris | Smith | 167 Small Road | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |

现在您已输入并显示了数据库记录，您可能会发现需要更改其中一些记录。以下部分介绍如何在 `mysql` 会话期间更新数据库记录。

## 修改表和记录

当您开始使用 MySQL 数据库时，您会发现需要对数据库表的结构和内容进行更改。以下部分介绍如何更改 MySQL 表的结构以及更改 MySQL 记录的内容。如果您尚未连接到 `mysql` 会话，请键入以下命令（假设 `mysql` 用户名为 `root`）：

```
# mysql -u root -p

Enter password: ******

mysql>
```
