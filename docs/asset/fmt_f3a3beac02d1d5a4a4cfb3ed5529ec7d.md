
使用带空格的破折号分隔 `Room`、`Cupboard` 和 `Rack` 字段，并使用 `AS` 语句分配别名，该别名用于对列表框的内容进行排序。在继续之前，请关闭并保存 SQL 命令编辑器和 `Properties`（属性）框。

对于最后的修改，在控件表中右键单击 `ArticleID`（文章ID）并选择上下文菜单中的 `Delete column`（删除列）。虽然表单现在已准备就绪，但仍需修改字段大小，你还可以更改 `CategoryID` 和 `PlaceID` 标签。

在表单中导航、搜索数据记录等操作可以在屏幕底部的 `Navigation Bar`（导航栏）中进行（图 8），一旦输入数据，该导航栏会自动显示。

有时，在输入字段旁边单独使用一个导航栏也是可取的。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_1.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_2.png)

![](img/e39350c3a7c0d527d71b0e4097a0ba66_42_3.png)

要创建此导航栏，你需要再次打开表单进行编辑。首先单击主表单中的字段，然后单击左侧边栏底部的 `More Controls`（更多控件）图标。通过 `Ctrl-单击` 新控件中的 `Navigation Bar`（导航栏），表单中会出现一个新的导航栏，其中包含与屏幕底部导航栏几乎相同的字段。

## 搜索数据集

Base 本身内置了一些搜索功能。不幸的是，在使用表单时这些功能更难管理。为了改变这一点，你需要深入一点，这就需要具备 `SQL` 代码的基础知识。对于一般性帮助，你可以参考可下载的 Base 手册。

首先，使用 `Tables | Create Table in Design View`（表 | 在设计视图中创建表）创建另一个表来保存搜索词，并添加字段：

- `ID` 作为 `Yes/No` [BOOLEAN]
- `Search` 作为 `Text` [VARCHAR]

右键单击 `ID` 字段使其成为主键，并以 `Search` 的名称保存该表。在表的第一行中插入 "ID" = `true`。此表应仅保存这一个数据集。

打开 `Queries | Create Query in SQL View`（查询 | 在 SQL 视图中创建查询），以便比在 `Design View`（设计视图）中更快地输入代码，并输入：

```sql
SELECT * FROM "Article"
WHERE "Article" LIKE COALESCE
(
  (SELECT "Search"
   FROM "Search"
   WHERE "ID" = TRUE
  ), "Article"
)
```

![](img/e39350c3a7c0d527d71b0e4097a0ba66_43_0.png)

图 9：表单导航器显示了表单的所有元素。

`COALESCE` 函数检查 `Search`（搜索）是否为空；然而，如果为 `TRUE`，`Article` 和 `Article` 总是应该包含内容，并且 `Article` 应该始终与 `Article` 相同，该关键字现在显示所有 `Article` 表数据。如果在 `Search` 中输入一个单词，则只显示与输入值匹配的 `Article` 项。需要对此查询稍作改进，以便搜索条目的一部分也能显示结果：

```sql
SELECT * FROM "Article"
WHERE "Article" LIKE COALESCE
( '%' ||
  (SELECT "Search"
   FROM "Search"
   WHERE "ID" = TRUE
  ) || '%', "Article"
)
```

要测试查询，请单击工具栏中的 `Run Query`（运行查询）图标或按 `F5`。将显示 `Article` 表中的所有数据集。最后一行在 `ID` 字段中显示 `AutoField`（自动字段）。

修改代码以在 `Search` 表中查找值为 `Search` 的条目，并将其与 `Article` 表中的 `Article` 字段进行比较：

```sql
SELECT * FROM "Article"
WHERE "Article" LIKE
(
  SELECT "Search"
  FROM "Search"
  WHERE "ID" = TRUE
)
```

此时你可能不会看到任何值，因为 `Search` 表中的 `Search` 字段内容为空。再次修改代码：

![](img/e39350c3a7c0d527d71b0e4097a0ba66_43_1.png)

图 10：仅循环遍历活动记录 – 无导航栏，无新行，...

通过使用 `%`，搜索词的命中结果现在可以在词前后包含任意数量的字符。因此，一次输入可能会获得多个命中结果。唯一的缺点是它仍然区分大写字母和小写字母。以下查询现在允许输入 `Article` 字段中任意位置包含的文本，无论大小写如何：

```sql
SELECT * FROM "Article"
WHERE LOWER ( "Article" ) LIKE COALESCE
( '%' ||
  (
    SELECT LOWER ( "Search" )
    FROM "Search"
    WHERE "ID" = TRUE
  ) || '%', "Article"
)
```

现在将此查询保存为 `qrySearchArticle`，在表单下复制已创建的表单，粘贴副本作为名为 `ArticleSearch` 的新表单，并通过右键单击选择 `Edit`（编辑）来打开此新表单进行编辑。

![](img/e39350c3a7c0d527d71b0e4097a0ba66_43_2.png)

图 11：带有搜索功能的表单。在内容中包含 `Meter` 的情况下找到了九条记录。

要在现有表单中添加 `Search`（搜索）输入区域，你需要打开 `Form Navigator`（表单导航器）（图 9）。在打开的对话框中，右键单击 `Forms`（表单）并选择 `New | Form`（新建 | 表单）。然后将在 `MainForm` 旁边添加一个新表单。

通过其上下文菜单打开此表单的属性。在 `Data`（数据）选项卡中，在 `Content`（内容）下拉菜单中选择 `Search`。选择 `Cycle | Active record`（循环 | 活动记录）尤为重要。图 10 中显示的其余设置确保始终编辑和更改相同的数据集。

接下来，选择 `MainForm` 中可用的一个表单字段并调出其 `Properties`（属性）对话框，并在 `Properties`（属性）| `General`（常规）| `Action`（操作）| `Refresh form`（刷新表单）中设置。

关闭新表单的 `Properties`（属性）对话框后，选择 `MainForm`。在 `Data`（数据）选项卡中，将 `Content type`（内容类型）选择为 `Query`（查询），将 `Content`（内容）选择为 `qrySearchArticle`。接下来，`Ctrl-单击` 侧边栏中的 `Push Button`（按钮）图标。此按钮应出现在 `MainForm` 中（请检查 `Form Navigator`）。在按钮的 `Properties`（属性）对话框的 `General`（常规）选项卡中，选择 `Action`（操作）| `Refresh form`（刷新表单）。现在，每当你点击此按钮时，表单都会再次进行扫描。

在 `Form Navigator`（表单导航器）中，再次选择 `Search` 表的新表单，并通过选择 `Text Box`（文本框）图标并使用鼠标绘制一个框来创建输入区域。在此框的 `Properties`（属性）对话框的 `Data`（数据）选项卡中，将 `Data field`（数据字段）设置为 `Search`，将 `Input required`（必须输入）设置为 `No`（否）。现在，当点击 `MainForm` 中的按钮时，此文本框的内容将自动保存（图 11）。

如果你对表单满意且不希望进行任何设计更改，现在就可以保存它。

## 结论

起初，创建内部 Firebird 数据库比在 Calc 中创建表花费的时间要多得多，但一旦数据库构建完成，数据输入比在电子表格中输入数据要准确且快速得多。另一个优势是可以生成报告。

除了 Base 内部数据库外，Base 还允许你连接到外部数据库（例如，MySQL/MariaDB、PostgreSQL、电子邮件地址簿等）。此时，Base 仅访问表并提供图形用户界面。

由于 Base 可以访问如此多的数据库，具备 SQL 基础知识总是很有优势的。否则，访问将很快局限于仅包含单个表且只使用 Base 内置搜索功能的数据库。

### 信息

- [1] LibreOffice 入门指南：https://documentation.libreoffice.org/en/getting-started/getting-started-guide/
