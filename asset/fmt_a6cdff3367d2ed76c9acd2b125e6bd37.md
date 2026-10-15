
前面命令的输出如下：

```
Query OK, 3 rows affected (0.02 sec)
Records: 3 Deleted: 0 Skipped: 0 Warnings: 0
```

在 `mysql>` 提示符下输入以下内容，以确保记录已正确添加：

```
mysql> SELECT * FROM name;
```

前面命令的输出如下：

| firstname | lastname | streetaddr   | city  | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Ramesh  | Patil    | 10BD N Road  | Mumbai | MH   | 400058  |
| Mayank  | Agarwal  | 24D MSEB Road | Thane | MH   | 400184  |
| Venkat  | Raje     | 16F Church Road | Mumbai | MH  | 400065  |

在创建表并向表中添加数据之后，让我们现在学习如何显示 MySQL 数据库。

## 显示 MySQL 数据库

在 `mysql` 会话期间，有许多不同的方法来排序和显示数据库记录。如果你尚未连接到 `mysql` 会话，请键入以下命令（假设 `mysql` 用户名是 root）：

```
$ mysql -u root -p
Enter password: ******
mysql>
```

当你在你的 `mysql` 会话中（并且已经选择了数据库）时，你可以显示全部或选定的表记录，选择显示哪些列，或者选择如何对记录进行排序。

## 显示全部或选定记录

假设当前数据库是 allusers（如前面的示例所示），键入以下命令以从 `name` 表中选择（SELECT）所有记录（*）并按它们输入数据库的顺序显示它们：

```
mysql> SELECT * FROM name;
```

前面命令的输出如下：

前面的表格显示了 `name` 表的所有记录。

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Ramesh | Patil | 10B D N Road | Mumbai | MH | 400058 |
| Mayank | Agarwal | 24 D M 5E B Road | Thane | MH | 400184 |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

以下命令显示 `name` 表中 `lastname` 列设置为 Jones 的所有记录。你可以搜索表中使用的任何列名的值，而不仅仅是 `lastname`。

```
mysql> SELECT * FROM name WHERE lastname = "Raje";
```

前面命令的输出如下：

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

使用 `OR` 运算符，你可以选择匹配多个不同值的记录。使用以下命令来显示 `firstname` 为 Mayank 或 Venkat 的记录：

```
mysql> SELECT * FROM name WHERE firstname = "Mayank" OR firstname = "Venkat";
```

表格显示以下输出：

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Mayank | Agarwal | 24 D M 5E B Road | Thane | MH | 400184 |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

要根据记录中两个列的值匹配并显示记录，你可以使用 `AND` 运算符。使用以下命令来显示任何 `firstname` 为 Mayank 且 `lastname` 为 Smith 的记录：

```
mysql> SELECT * FROM name WHERE firstname = "Venkat" AND lastname = "Raje";
```

下表显示了前面命令的预期输出：

| firstname | lastname | streetaddr | city | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Venkat | Raje | 16 F Church Road | Mumbai | MH | 400065 |

## 显示选定列

你不需要显示每一列数据。可以使用前面示例中所示的星号（`*`）来匹配所有列，或者输入逗号分隔的列名列表。以下命令显示 `name` 表中所有记录的 `firstname`、`lastname` 和 `zipcode` 记录：

```
mysql> SELECT firstname,lastname,zipcode FROM name;
```

下表显示了具有 `firstname`、`lastname` 和 `zipcode` 列名的表格：

| firstname | lastname | zipcode |
| :-- | :-- | :-- |
| Ramesh | Patel | 400058 |
| Mayank | Agarwal | 400184 |
| Venkat | Rajee | 400065 |

同样，你可以按任意顺序对列进行排序。键入以下命令以显示相同的三列，但将 `zipcode` 列首先显示：

```
mysql> SELECT zipcode,firstname,lastname FROM name;
```

下表显示了前面命令的输出：

| zipcode | firstname | lastname |
| :-- | :-- | :-- |
| 400058 | Ramesh | Patel |
| 400184 | Mayank | Agarwal |
| 400065 | Venkat | Rajee |

## 排序数据

你可以基于任意选定列中的值对记录进行排序。例如，使用 `ORDER BY` 运算符，你可以基于 `lastname` 列显示记录：以下命令用于对记录进行排序：

```
mysql> SELECT * FROM name ORDER BY lastname;
```

前面命令的输出如下所示：

| firstname | lastname | streetaddr   | city  | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Mayank    | Agarwal | 24D MSEB Road | Thane  | MH | 400184 |
| Ramesh    | Patil   | 10BD N Road   | Mumbai | MH | 400058 |
| Venkat    | Raje    | 16F Church Road| Mumbai | MH | 400065 |

要根据城市名称对记录进行排序，你可以使用以下命令：

```
mysql> SELECT * FROM name ORDER BY city;
```

前面命令的输出如下所示：

| firstname | lastname | streetaddr   | city  | state | zipcode |
| :-- | :-- | :-- | :-- | :-- | :-- |
| Ramesh    | Patil   | 10BD N Road   | Mumbai | MH | 400058 |
| Venkat    | Raje    | 16F Church Road| Mumbai | MH | 400065 |
| Mayank    | Agarwal | 24D MSEB Road | Thane  | MH | 400184 |

在上一节中，你学习了如何显示记录。在下一节中，你将学习如何对表和记录进行修改。

# 更新和删除 MySQL 记录

你可以基于任意选定的值选择记录，并更新这些记录中的任意值。当你在你的 `mysql` 会话中时，可以使用 `UPDATE` 来更改选定表中的值。使用以下命令来更新 `name` 表中的记录：
