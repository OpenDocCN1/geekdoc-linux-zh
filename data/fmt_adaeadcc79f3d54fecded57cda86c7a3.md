
若要使用默认遍历顺序导入 `EMPLOYEE` 表在内的所有表，请执行以下命令：

```
IMPORT... ALL TABLES IN HIERARCHY STARTING Employee...
```

> **注意：** 如果复合组中的其中一条记录无法插入，则所有记录都将被拒绝。只有在您确定数据是正确的条件下，才要使用此选项。

## 使用控制中心调用导入

也可以从控制中心（`Control Center`）调用 `IMPORT` 实用程序。选择目标表并点击鼠标右键，然后选择 **Import**（导入）选项。图 10–11 显示了导入工作簿（Import Notebook）的文件选项卡。接下来的示例将演示导入工作簿的使用。

![](img/ca7cfad01341360e684d5dd2379b19e9_543_0.png)

**图 10–11** 控制中心中的导入 GUI

要求 DBA 将一个名为 `C:\SANFRANCIS\PROJECT.DEL` 的文件导入到名为 `PROJECT` 的现有表。。该表是空的，因此 `DEL` 文件中的所有数据都必须插入。DBA 选择文件 `C:\SANFRANCIS\PROJECT.MSG` 作为导入消息文件。由于要导入大量记录，DBA 决定使用 `COMMITCOUNT` 50，以确保日志文件不会填满。他还决定使用 `COMPOUND=5` 文件类型修饰符。这将导致插入时每五条记录分在一组。这将提高导入性能。

## 数据移动工具

![](img/ca7cfad01341360e684d5dd2379b19e9_544_0.png)

图 10–12 分隔符选项（Delimited Options）

图 10–12 显示了适用于 `DEL` 文件的特定文件选项。由于已选了 `DATESISO` 选项，因为该文件是使用此选项生成的。

![](img/ca7cfad01341360e684d5dd2379b19e9_544_1.png)

图 10–13 列（Columns）选项卡

列选项卡可用于指定源文件中存在的列。用户还可以使用它来指定列的顺序，并且如果文件是 `IXF` 文件且要使用 `CREATE` 或 `REPLACE_CREATE` 选项创建表，则指定新名称。

如果要从单独的文件导入 `LOB`（大对象），请填写此面板底部的字段。

## 第 10 章维护数据

一旦在相关面板中捕获了所有信息，用户可以选择点击 `OK` 按钮来运行 `IMPORT` 命令。或者，用户可以选择查看将执行的命令。图 10–14 显示了将文件导入到 `PROJECT` 表生成的命令。用户还可以选择将命令保存到脚本文件中，以便稍后执行。

```
connect to:SAMPLE;
IMPORT FROM C:sanfranciscoproject OF DEL MODIFIED BY COMPOUND=5 CHARDEL,"COLDEL" DATESISO DECP, METHOD (1, 2, 3, 4, 5, 6, 7, 8) COMMITCOUNT 50 MESSAGES
C:sanfranciscoproject/insert tsg REPLACE INTO BILLW PROJECT
(PROUNO, PRJNAME, DEPNO, RESEMP, PRSTAFF, PRSTATE,
PRENDATE, MAPROJ);
connect reset;
```

图 10–14 生成的 `IMPORT` 命令

## IMPORT 注意事项

将数据导入到表或视图时，需要以下信息：

- 存储要导入数据的路径和输入文件名。
- 导入要导入数据的目标表或视图的名称或别名。
- 输入文件中数据的格式。该格式可以是 `IXF`、`DEL`、`ASC` 或 `WSF`。
- 输入文件中的数据是要插入、更新到表或视图中，还是替换现有数据。

您还可以提供以下内容：

- 消息文件
- 在向表提交更改之前要插入的行数
- 在开始导入之前要跳过的文件中记录数
- 插入数据的目标表或视图中的列名

> 注意：`IMPORT` 实用程序将根据导入的成功与否发布 `COMMIT`（提交）或 `ROLLBACK`（回滚）。

## 使用 EXPORT 和 IMPORT 的示例

第一个示例展示了如何从 `SALES` 数据库的 `PRODUCT` 表导出信息。导出到文件 `product.ixf` 且输出为 `IXF` 格式：

```
EXPORT TO product.ixf OF IXF MESSAGES product.msg
SELECT * FROM products
```

在执行命令之前，您必须连接到数据库。若要将数据导入另一个数据库并在名为 `SMS1` 的现有表空间创建一个名为 `PRODS` 的表，可以使用以下命令：

```
IMPORT FROM product.ixf OF IXF
COMMITCOUNT 50 MESSAGES product.msg
CREATE INTO PRODS IN SMS1
```

注意 `COMMITCOUNT` 选项的使用。这可以防止日志文件填满。

在第二个示例中，导出 `SALES` 数据库中定义的表层次结构中的所有数据。表层级定义如下：

![](img/ca7cfad01341360e684d5dd2379b19e9_544_0.png)

**图 10–12** 分隔符选项

图 10–12 显示了适用于 `DEL` 文件的特定文件选项。已选了 `DATESISO` 选项，因为该文件是使用此选项生成的。

![](img/ca7cfad01341360e684d5dd2379b19e9_544_1.png)

图 10–13 列选项卡

列选项卡可用于指定源文件中存在的列。用户还可以使用它来指定列的顺序，并且如果文件是 `IXF` 文件且要使用 `CREATE` 或 `REPLACE_CREATE` 选项创建表，则指定新名称。

如果要从单独的文件导入 `LOB`，请填写此面板底部的字段。
