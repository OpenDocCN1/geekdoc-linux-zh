
`$ mysql -u root -p`

Enter password: ********

`mysql>`

```
当你处于 mysql 会话中（并且已选择数据库），你可以显示所有选定的表记录、选择要显示的列，或者排序记录。
```

## 第 24 章：设置 MySQL 数据库

### 显示所有或选定的记录

假设当前数据库为全部（如前面的示例所示），输入以下命令从 `names` 表中选择所有记录 (`*`)，并按照它们被输入数据库的顺序显示它们。

```mysql
mysql> SELECT * FROM names;
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | | 18 Talbot Road NW | | NJ | 54889 |
| Howard | | | 1515 Broadway | New York | NY | 10028 |

以下命令显示 `names` 表中所有 `lastname` 设置为 "Jones" 的记录。你可以不使用 `lastname`，而是搜索表中使用的任何任意列的值。

```mysql
mysql> SELECT * FROM names WHERE lastname = "Jones";
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |

使用 `OR` 运算符，你可以选择匹配多个不同值的记录。在以下命令中，匹配并显示 `firstname` 为 "Chris" 或 "Howard" 的记录。

```mysql
mysql> SELECT * FROM names WHERE firstname = "Chris" OR firstname = "Howard";
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |

要根据记录中两个列的值显示记录，你可以使用 `AND` 运算符。在以下命令中，将匹配任何 `firstname` 为 "Chris" 且 `lastname` 为 "Smith" 的记录。

```mysql
mysql> SELECT * FROM names WHERE firstname = "Chris" AND lastname = "Smith";
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |

## 第四部分：Fedora 和 RHEL 网络与服务器设置

### 显示选定的列

你不需要显示每一列数据。与其使用前面示例中的星号 (`*`) 来匹配所有列，不如输入一个用逗号分隔的列名列表。以下命令显示 `names` 表中所有记录的 `firstname`、`lastname` 和 `zipcode` 记录：

```mysql
mysql> SELECT firstname,lastname,zipcode FROM names;
```

| firstname | lastname | zipcode |
| :--- | :--- | :--- |
| Chris | Smith | 98999 |
| John | Jones | 54889 |
| Howard | Manty | 10028 |

同样，你可以按照选择的任何顺序对列进行排序。使用以下命令显示 `zipcode` 在最前的三列：

```mysql
mysql> SELECT zipcode, firstname, lastname FROM names;
```

| zipcode | firstname | lastname |
| :--- | :--- | :--- |
| 98999 | Chris | Smith |
| 54889 | John | Jones |
| 10028 | Howard | Manty |

你可以像下面的示例那样将列选择与记录选择结合：

```mysql
mysql> SELECT firstname,lastname,city FROM names WHERE firstname = "Chris";
```

| firstname | lastname | city |
| :--- | :--- | :--- |
| Chris | Smith | Gig Harbor |

### 排序数据

你可以根据你选择的任何列的值对记录进行排序。例如，使用 `ORDER BY` 运算符，你可以根据 `lastname` 列显示记录：

```mysql
mysql> SELECT * FROM names ORDER BY streetaddr;
```

| firstname | lastname | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
| Chris | Smith | 167 Small Road | Gig Harbor | WA | 98999 |

要根据城市名称对记录排序，你可以使用以下命令：

```mysql
mysql> SELECT * FROM names ORDER BY city;
```
