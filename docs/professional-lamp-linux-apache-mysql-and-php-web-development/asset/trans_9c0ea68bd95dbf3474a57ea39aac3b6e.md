
## 内连接

在 SQL 中，连接（join）是通过指定的一列或多列将两个或更多表关联起来的方式。在 MySQL 中，最常使用的两种连接类型是内连接和外连接。

内连接是一种将两个表基于每行共同共享的值进行组合的方法。当你在 `SELECT` 查询中执行内连接时，只需在 `FROM` 子句中指定要连接的表，并提供提示说明它们有哪些共同列。MySQL `INNER JOIN` 语法的通用抽象形式如下：

```
SELECT [column_names] FROM [table1] INNER JOIN [table2] ON [table1.column] = [table2.column]
```

使用假设的汽车经销商库存场景，你希望每个车辆的具体信息旁边都能返回该车辆型号。为了实现这一点，你的查询大致如下：

```
SELECT Models.model_name, New_Vehicles.color, New_Vehicles.modelyear FROM Models INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

对数据库运行此查询将产生以下结果：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Explorer | 深蓝色 | 2005 |
| Tacoma | 亮红色 | 2005 |
| Corvette | 戴通纳日落橙色 | 2005 |

你会注意到，在 `SELECT` 查询中，选择列表中的每个列都带有其所属表的名称前缀。虽然这在技术上不是必需的，但这是一个避免同名列之间冲突的好习惯。如果你存在这样的冲突并且忽略了表前缀，会发生什么？请看这个例子：

```
SELECT model_id, model_name, color, modelyear FROM Models INNER JOIN New_Vehicles ON Models.model_id = New_Vehicles.model_id;
```

如你所见，表前缀已被移除，但 `model_id` 列也被添加到了列表中（因为它在两个表中都存在）。现在尝试运行该查询。你会得到以下错误：

```
ERROR 1052 (23000): Column 'model_id' in field list is ambiguous
```

当你尝试使用在两个表中都存在的列名，而没有使用表前缀时，执行该查询时会抛出此类错误。

如果你更喜欢简洁的 SQL 查询，别担心——有一种简单的方法可以缩短所有这些表前缀。在 `FROM` 子句中，你可以为调用的每个表指定一个*别名*，如下所示：

```
SELECT [column_names] FROM [table1] alias1 INNER JOIN [table2] alias2 ON [alias1.column] = [alias2.column]
```

由于表别名可以短至单个字符，你可以大幅缩短库存查询：

```
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n ON m.model_id = n.model_id;
```

还不够简短？好吧，还有另一种整理连接的方法。MySQL 提供了 USING 语句，用于替代 ON 语句来链接你的表。当两个连接列恰好拥有完全相同的列名时，使用 USING 语句。带有 USING 的内连接通用形式如下：

```
SELECT [column names] FROM [table1] INNER JOIN [table2] USING (column list)
```

由于 New_Vehicles 表和 Models 表都有一个 model_id 列，你可以在连接中使用 USING 语句：

```
SELECT m.model_name, n.color, n.modelyear FROM Models m INNER JOIN New_Vehicles n USING (model_id);
```

在某些情况下，你需要在查询中连接两个以上的表。MySQL 可以轻松地处理这一点——你只需要按照希望评估的顺序将连接链接在一起。在车辆库存数据库中，你需要使用多个连接来返回每辆车的制造商及其记录，如下所示：

```
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma INNER JOIN Models mo USING (make_id) INNER JOIN New_Vehicles n USING (model_id);
```

当你运行此查询时，应该看到以下内容：

| make_name | model_name | color | modelyear |
| :--- | :--- | :--- | :--- |
| Ford | Explorer | 深蓝色 | 2005 |
| Toyota | Tacoma | 亮红色 | 2005 |
| Chevrolet | Corvette | 戴通纳日落橙色金属漆 | 2005 |

如你所见，Makes 表基于 make_id 连接到 Models 表，然后该连接的结果再与 New_Vehicles 表连接，从而在一个查询中提供制造商、型号和车辆信息。

在继续下一组连接之前，你应该知道还有另一种执行内连接的方法。第二种方法只是在逗号分隔的列表中指定多个表，并使用 WHERE 语句来指定表如何关联。这种类型内连接的通用形式如下：

```
SELECT [column names] FROM table1, table2 WHERE table1.column = table2.column
```

如果你使用这种内连接形式来上一个查询中提取新车、制造商和型号的列表，它会看起来像这样：

```
SELECT ma.make_name, mo.model_name, n.color, n.modelyear FROM Makes ma, Models mo, New_Vehicles n WHERE ma.make_id = mo.make_id AND mo.model_id = n.model_id;
```

在你的 MySQL 客户端中执行此查询，将返回以下内容：

| make_name | model_name | color | modelyear |
| :--- | :--- | :--- | :--- |
| Ford | Explorer | 深蓝色 | 2005 |
| Toyota | Tacoma | 亮红色 | 2005 |
| Chevrolet | Corvette | 戴通纳日落橙色金属漆 | 2005 |

如你所见，返回了与使用显式内连接时完全相同的结果。如果你省略了 WHERE 子句中的项目会发生什么？试试这个查询：

```
SELECT mo.model_name, n.color, n.modelyear FROM Models mo, New_Vehicles n;
```

对我们的车辆库存运行此查询会产生以下结果（注意 Makes 表已被排除）：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Accord | 深蓝色 | 2005 |
| Golf | 深蓝色 | 2005 |
| Tacoma | 深蓝色 | 2005 |
| Corvette | 深蓝色 | 2005 |
| Explorer | 深蓝色 | 2005 |
| Accord | 石墨珍珠色 | 2004 |
| Golf | 石墨珍珠色 | 2004 |
| Tacoma | 石墨珍珠色 | 2004 |
| Corvette | 石墨珍珠色 | 2004 |
| Explorer | 石墨珍珠色 | 2004 |
| Accord | 亮红色 | 2005 |
| Golf | 亮红色 | 2005 |
| Tacoma | 亮红色 | 2005 |
| Corvette | 亮红色 | 2005 |
| Explorer | 亮红色 | 2005 |
| Accord | 戴通纳日落橙色金属漆 | 2005 |
| Golf | 戴通纳日落橙色金属漆 | 2005 |
| Tacoma | 戴通纳日落橙色金属漆 | 2005 |
| Corvette | 戴通纳日落橙色金属漆 | 2005 |
| Explorer | 戴通纳日落橙色金属漆 | 2005 |
| Accord | 深蓝色 | 2005 |
| Golf | 深蓝色 | 2005 |
| Tacoma | 深蓝色 | 2005 |
| Corvette | 深蓝色 | 2005 |
| Explorer | 深蓝色 | 2005 |

这不太正确。在这种情况下实际发生的是另一种称为*交叉连接*（cross join）的连接。交叉连接仅仅是每个表中每个匹配结果的组合。在这种情况下，Models 表中有五个型号，因此这些行中的每一行都与 *New_Vehicles* 表中的*每一行*进行了匹配。这发生仅仅是因为你省略了 WHERE 语句，而该语句提供了关于如何链接记录的提示给 MySQL。如前所述，你没有让 *Makes* 表参与此查询——如果参与了，由于你的数据库中有五个不同的制造商，结果行数将是原来的五倍。

## 外连接

虽然大多数复杂的链接可以使用内连接实现，但在某些情况下它们会受到限制。如果数据库行没有为被链接的列定义值，它将被内连接忽略。在车辆库存示例中，每次你使用内连接链接 *Models* 表时，只返回了三行。*New_Vehicles* 表中的第四辆车被忽略，因为其 *model_id* 的值为 null。你需要一种方法，无论是否指定了 *model_id*，都返回所有行；如果指定了 *model_id*，则执行请求的连接。对于这种任务，MySQL 提供了*外连接*（outer joins）。

MySQL 中有两种主要类型的外连接：左外连接和右外连接。它们的行为完全相同，唯一的不同在于允许哪个表不包含匹配项。外连接的通用形式与内连接非常相似。看这个简化的左外连接版本：

```
SELECT [column names] FROM table1 LEFT OUTER JOIN table2 USING [column list]
```

左外连接使用通用列名将“右”表（*table2*）与“左”表（*table1*）进行匹配，但如果“左”表包含“右”列中没有匹配项的值，它仍将返回行。右外连接的行为相同，但两个表的角色互换（允许在右表中存在不匹配的值）。

在车辆库存示例中，如果你想返回一组行，其中所有新车都返回，无论其 *model_id* 如何，你可能使用以下代码：

```
SELECT mo.model_name, n.color, n.modelyear FROM New_Vehicles n LEFT OUTER JOIN Models mo USING (model_id);
```

使用此查询查询车辆库存数据库将产生以下结果：

| model_name | color | modelyear |
| :--- | :--- | :--- |
| Explorer | 深蓝色 | 2005 |
| NULL | 石墨珍珠色 | 2004 |
| Tacoma | 亮红色 | 2005 |
| Corvette | 戴通纳日落橙色金属漆 | 2005 |
| Explorer | 深蓝色 | 2005 |

这与你之前查看的内连接查询之一非常相似，但增加了第二行——2004 年款的石墨珍珠色。因为在 *Models* 表中没有匹配项，MySQL 为无法确定的行值返回 NULL——在这种情况下，是 *model_name*。

