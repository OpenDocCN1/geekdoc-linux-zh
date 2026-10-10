
```
$ mysql -u root -
Enter password: ********
mysql>
```

当你处于 `mysql` 会话中（并且已选择了一个数据库）时，你可以显示所有选定的记录、选择显示的列，或者指定记录的排序方式。

### 显示所有或选定的记录

假设当前数据库是 `allusers`（在之前的示例中），输入以下命令从 `name` 表中选择 (`*`) 记录并按照它们输入数据库的顺序显示它们。

```
mysql> SELECT * FROM name;
+----------------------+----------------------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+----------------------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------------+----------------------+----------+
```

以下命令显示 `name` 表中所有 `lastname` 设置为 `Jones` 的记录。你可以不使用 `lastname`，而是搜索表中运用的任何列的值。

```
mysql> SELECT * FROM name WHERE lastname = "Jones";
+----------------------+----------------------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+----------------------+----------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
```

使用 `OR` 操作符，你可以选择具有不同值的记录。在以下命令中，将匹配并显示 `firstname` 为 `Chris` 或 `Howard` 的记录。

```
mysql> SELECT * FROM name WHERE firstname = "Chris" OR firstname = "Howard";
+----------------------+----------------------+----------+
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------------+----------------------+------++
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------------+----------------------+----------+
```

要根据两个列的值匹配并显示记录，你可以使用 `AND` 操作符。在以下命令中，将匹配任何 `firstname` 为 `Chris` 且 `lastname` 为 `Smith` 的记录。

```
mysql> SELECT * FROM name WHERE firstname = "Chris" AND lastname = "Smith";
+-------------+-----------+----------+
| firstname | streetaddr | city | state | zipcode |
+-------------+-----------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
+-------------+-----------+----------+
```

### 显示选定的列

你不需要显示每一列数据。与其使用之前示例中的星号 (`*`) 来匹配所有列，不如使用逗号分隔的列列表。以下命令显示 `name` 表中所有记录的 `firstname`、`lastname` 和 `zipcode` 记录：

```
mysql> SELECT firstname, lastname, zipcode FROM name;
+-------------+-------------+----------+
| firstname | lastname | zipcode |
+-------------+-------------+----------+
| Chris | Smith | 98999 |
| John | Jones | 54889 |
| Howard | Manty | 10028 |
+-------------+-------------+----------+
```

同样，你可以按照你选择的任何顺序对列进行排序。输入以下命令显示 `zipcode` 在前的相同三列：

```
mysql> SELECT zipcode, firstname, lastname FROM name;
+----------+-------------+-------------+
| zipcode | firstname | lastname |
+----------+-------------+-------------+
| 98999 | Chris | Smith |
| 54889 | John | Jones |
| 10028 | Howard | Manty |
+----------+-------------+-------------+
```

你还可以像下面的示例所示，将选择与记录选择结合：

```
mysql> SELECT firstname, lastname,city FROM name WHERE firstname = "Chris";
+-------------+-------------+----------+
| firstname | lastname | city |
+-------------+-------------+----------+
| Chris | Smith | Gig Harbor |
+-------------+-------------+----------+
```

### 排序数据

你可以根据选择的任何列对记录进行排序。例如，使用 `ORDER BY` 操作符，可以根据 `lastname` 列显示记录：

```
mysql> SELECT * FROM name ORDER BY lastname;
+----------------------+-------------+-------+
```
| firstname | lastname | streetaddr | city | state | zipcode |
|---|---|---|---|---|---|
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |

要按城市名称排序，可以使用以下命令：

```
mysql> SELECT * FROM name ORDER BY city;
+----------------------+-------------+-------+
