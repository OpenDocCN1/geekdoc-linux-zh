
| firstname | lastname | streetaddr | city | state | zipcode |
+----------------+----------------------+-----------+----------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------+----------------------+-----------+----------+----------+

以下命令显示 `name` 表中所有 `lastname` 设置为 "Jones" 的记录。你不仅可以使用 `lastname`，还可以搜索表表使用的任何列名对应的值。

```
mysql> SELECT * FROM name WHERE lastname = "Jones";
```

| firstname | lastname | streetaddr | city | state | zipcode |
+----------------+----------------------+-----------+----------+----------+
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
+----------------+----------------------+-----------+----------+----------+

使用 `OR` 运算符，你可以选择匹配多个不同值的记录。在以下命令中，匹配并显示 `firstname` 为 "Chris" 或 "Howard" 的记录。

```
mysql> SELECT * FROM name WHERE firstname = "Chris" OR firstname = "Howard";
```

| firstname | lastname | streetaddr | city | state | zipcode |
+----------------+----------------------+-----------+----------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
+----------------+----------------------+-----------+----------+----------+

要根据记录中两个列的值来匹配并显示记录，你可以使用 `AND` 运算符。在以下命令中，匹配任何 `firstname` 为 "Chris" 且 `lastname` 为 "Smith" 的记录。

```
mysql> SELECT * FROM name WHERE firstname = "Chris" AND lastname = "Smith";
```

| firstname | lastname | streetaddr | city | state | zipcode |
+----------------+----------------------+-----------+----------+----------+
| Chris | Smith | 175 Harrison Street | Gig Harbor | WA | 98999 |
+----------------+----------------------+-----------+----------+----------+

# 第 24 章：设置 MySQL 数据库服务器 (949)

## 显示指定的列

你不需要显示每一列数据。与其使用前面示例中显示的星号（`*`）来匹配所有列，不如输入一个用逗号分隔的列名列表。以下命令显示 `name` 表中所有记录的 `firstname`、`lastname` 和 `zipcode` 记录：

```
mysql> SELECT firstname, lastname, zipcode FROM name;
```

| firstname | lastname | zipcode |
| :--- | :--- | :--- |
| Chris | Smith | 98999 |
| John | Jones | 54889 |
| Howard | Manty | 10028 |

同样，你可以按照你选择的任何顺序对列排序。输入以下命令显示三列，并将 `zipcode` 列显示在第一个：

```
mysql> SELECT zipcode, firstname, lastname FROM name;
```

| zipcode | firstname | lastname |
| :--- | :--- | :--- |
| 98999 | Chris | Smith |
| 54889 | John | Jones |
| 10028 | Howard | Manty |

你还可以像下面的示例那样将列选择与记录选择结合：

```
mysql> SELECT firstname, lastname,city FROM name WHERE firstname = "Chris";
```

| firstname | lastname | city |
| :--- | :--- | :--- |
| Chris | Smith | Gig Harbor |

## 排序数据

你可以根据选择的任何列中的值对记录进行排序。例如，使用 `ORDER BY` 运算符，可以根据 `lastname` 列显示记录：

```
mysql> SELECT * FROM name ORDER BY lastname;
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54899 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |
| Chris | Smith | 167 Small Road | Gig Harbor | WA | 98999 |

### 第四部分：Fedora RHEL 网络和服务器设置

要按名称排序记录，可以使用以下命令：

```
mysql> SELECT * FROM name ORDER BY city;
```

| firstname | lastname | streetaddr | city | state | zipcode |
| :--- | :--- | :--- | :--- | :--- | :--- |
| John | Jones | 18 Talbot Road NW | Coventry | NJ | 54889 |
| Chris | Smith | 167 Small Road | Gig Harbor | WA | 98999 |
| Howard | Manty | 1515 Broadway | New York | NY | 10028 |

你可以添加 `ASC` 或 `DESC` 来指示排序顺序，因为 MySQL 不保证数据的显示顺序。现在你输入并显示了数据库记录，你可能会发现需要修改某些内容。
