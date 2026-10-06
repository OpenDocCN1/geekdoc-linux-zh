
对数据类型非常宽容。事实上，它允许将任何类型的数据存储在任何指定的数据类型中，甚至允许在单列中混合数据类型。这与所有其他数据库完全不兼容，依赖这一点将是非常糟糕的实践。在这次冒险的剩余部分中，我们将遵循传统的数据类型和行为。

## 插入数据

继续我们的 SQL 流，我们看到流的大部分由 INSERT 语句组成。这是向表中添加行的方法。INSERT（插入）某种程度上是一个误称，因为 INSERT 语句实际上是将行追加到表中。

我们将 INSERT 语句封装在 `BEGIN TRANSACTION` 和 `COMMIT` 之间。这样做是为了出于性能考虑。如果我们省略这些语句，行仍然会被添加到表中，但每一条行都将被视为一个独立的事务，这极大地增加了添加大量行所需的时间。这样处理事务还有一个重要的好处：在接收到 `COMMIT` 语句之前，SQL 不会将事务应用到数据库，因此可以编写 SQL 代码，以便在出现问题时放弃事务，更改将将回滚，使数据库保持不变。

让我们开始创建第一张表，并添加包名和描述。

```
me@linux:~/adventure-sql$ sqlite3 adv-sql.sqlite \
< insert_Package_Descriptions.sql
```

我们执行 `sqlite3` 程序并指定 `adv-sql.sqlite` 为用于存储表的文件。文件名的选择是任意的。我们将 SQL 流读入标准输入，`sqlite3` 执行这些语句。

## 执行查询

现在我们已经有了一个数据库（尽管很小），让我们来看看它。为了做到这一点，我们将启动 `sqlite3` 提示符并与其交互。

```
me@linux:~/adventure-sql$ sqlite3 adv-sql.sqlite
SQLite version 3.22.0 2018-01-22 18:45:57
Enter "help" for usage hints.
sqlite>
```

我们首先将使用一些 SQLite 命令检查数据库的结构。

```
sqlite> .tables
Package_Descriptions
sqlite> .schema Package_Descriptions
CREATE TABLE Package_Descriptions (
 package_name VARCHAR(60),
description VARCHAR(120)
);
```

`.tables` 点命令显示数据库中的表列表，而 `.schema` 点命令列出用于创建指定表的语句。

接下来，我们将使用 `SELECT` 进入一些真正的 SQL 操作，这可能是最常用的 SQL 语句。

```
sqlite> SELECT * FROM Package_Descriptions;
a2ps (GNU) a2ps 'Anything to PostScript' converter and pretty-printer
accountserver-query and manipulate user account information
acl control utilities
acpi-support scripts for handling many ACPI events
acpidid Advanced Configuration and Power Interface event daemon
adduser remove users and groups
adium-theme-abuntu Adium message style for Ubuntu
adwaita-icon-theme default icon theme of GNOME (small subset)
alaislerot solitaire card game collection
alsa-base ALSA driver configuration files
```

这是 `SELECT` 语句最简单的形式。语法是单词 `SELECT` 后面跟一个列列表或计算值，以及一个指定数据源的 `FROM` 子句。此示例使用了 `*`，意味着所有列。或者，我们可以显式地命名列名，如下：

```
sqlite> SELECT package_name, description FROM Package_Descriptions
```

并获得相同的结果。

## 控制输出

正如我们从上面的输出中所看到的，对于人类阅读来说，默认格式是可以接受的。我们可以通过一些命令调整输出格式。我们还在查询末尾添加了 `LIMIT` 子句来输出 10 行。

```
sqlite> .headers on
sqlite> .mode column
sqlite> SELECT * FROM Package_Descriptions LIMIT 10;
package_name      description
-----------------
a2ps               GNU a2ps 'Anything to PostScript' converter and pretty-printer
accountserver-query and manipulate user account information
acl
acpi-support scripts for handling many ACPI events
acpidid Advanced Configuration and Power Interface event daemon
adduser remove users and groups
adium-theme-abuntu Adium message style for Ubuntu
adwaita-icon default icon theme of GNOME (small subset)
alaislerot GNOME solitaire card game collection
alsa-base ALSA driver configuration files
```

通过使用 `.headers` 和 `.mode` 命令，我们更改了输出格式。`column` 模式使输出更具读性。

## 模式描述

| Mode | 描述 |
| --- | --- |
| csv | 逗号分隔值 |
| column | 列对齐 |
| html | HTML 表格 |
| list | 列表格式 |
| list | 每列占新行 |
| markdown | Markdown 风格表格格式 |
| tabs | 制表符分隔值 |

`.mode` 命令允许我们更改结果的的方式。例如，`column` 模式让输出更容易读。

## 排序输出

除非我们 `SELECT` 对数据进行排序，否则它们将按照插入顺序列出。可以添加 `ORDER BY` 子句来确定使用哪个列进行排序。为了演示，让我们按描述对输出排序。

```
sqlite SELECT * FROM Package_Descriptions ORDER BY description LIMIT 10;
package_name      description
-----------------
a2ps               GNU a2ps 'Anything to PostScript' converter and pretty-printer
accountserver-query and manipulate user account information
acl
acpi-support scripts for handling many ACPI events
acpidid Advanced Configuration and Power Interface event daemon
adduser remove users and groups
adium-theme-abuntu Adium message style for Ubuntu
adwaita-icon default icon theme of GNOME (small subset)
alaislerot GNOME solitaire card game collection
alsa-base ALSA driver configuration files
```

默认排序顺序是升序的，但我们也可以在名称后包含 `DESC` 来进行降序。可以命名多个列，并使用 `ASC` 来指定升序。

## 添加另一张表

为了演示 `SELECT` 能做的事情，我们需要一个更大的数据库。我们有一个可以添加的第二个 .csv 文件。为了节省步骤，我们将文件过滤为 SQL 并将其直接管道传输到 `sqlite3`。

