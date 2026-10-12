
重新实现）。对于大多数委托对象，我们完全不需要重新实现 `paint()` 或 `sizeHint()`，只需重新实现 `createEditor()`、`setEditorData()` 和 `setModelData()` 即可。

在下一章中，我们将看到更多模型/视图架构的示例，包括纯视图、自定义委托以及内置的 SQL 数据库模型。

## 练习

- 向 `ShipTableModel` 添加一个新方法 `sortByTEU()`。可以使用任何你喜欢的排序技术；我们使用了 DSU。然后，在 `MainForm.sortTable()` 中使用该方法。总共只需几行代码即可完成。

- 扩展 `ShipTableModel.data()` 方法以提供工具提示。提示内容通常只需是数据项的文本，但对于 TEU（标准箱），文本应为（本地化的）数字后跟“twenty foot equivalents”。请注意，工具提示中的 HTML 格式正确。这很容易实现，只需十二行代码左右。

- 修改 `ShipTableDelegate.setModelData()`，使其仅当新文本长度至少为三个字符时才更改名称、所有者或国家。将这些列的工具提示扩展为包含文本“（最少 3 个字符）”。这大约需要十几行代码即可完成。

- 添加一个“导出”按钮，按下时提示用户输入后缀为 .txt 的文件名，并使用 UTF-8 编码保存数据，每艘船占一行，格式如下：

```
name|owner|country|teu|description
```

使用竖线“|”（管道符）作为分隔符。数据应通过模型的 `data()` 方法获取，并按国家/所有者顺序输出；描述字段中不包含 HTML 标签，且 TEU 仅输出数字（不含逗号、句号或空格）。最后弹出一个消息框，报告错误或成功。请使用 Python 或 PyQt 来编写文件；我们使用了 PyQt。如果你使用的是 4.1 之前版本的 PyQt，则在将 TEU 写入文本流之前，需要将其转换为 `QString`。`export()` 方法可以在不到 50 行代码内完成。

提供的解决方案位于 `chap14/ships_ans.py` 和 `chap14/ships-delegate-ans.py` 中。

## 15 数据库

- 连接数据库
- 执行 SQL 查询
- 使用数据库表单视图
- 使用数据库表格视图

PyQt 通过 **QtSql** 模块和 PyQt 的模型/视图架构提供了一致的跨平台数据库访问 API。Python 本身也有一个完全不同的数据库 API，称为 DB-API，但在 PyQt 中不需要使用它，这里也不会介绍。Qt 的商业版附带许多数据库驱动程序，而 GPL 版本由于许可证限制，附带的驱动程序较少。可用的驱动程序包括用于 IBM 的 DB2、Borland 的 Interbase、MySQL、Oracle、ODBC（用于 Microsoft SQL Server）、PostgreSQL、SQLite 和 Sybase。然而，就像 PyQt 的其他方面一样，如果我们需要某些不可用的数据库驱动程序，也可以创建额外的数据库驱动程序。

当从源代码构建 Qt 时，我们可以配置它包含 **SQLite**，这是一种公有领域的进程内数据库。对于二进制 Qt 包（如 Windows 和 Mac OS X 的 GPL 包），SQLite 是内置的。本章中的示例使用 SQLite，但除了初始连接到数据库和我们将提到的原始 SQL 语法的几个方面外，这些示例应该适用于任何 **SQL** 数据库。

PyQt 在两个层面上提供数据库访问。高层涉及使用 **QSqlTableModel** 或 **QSqlRelationalTableModel**。这些模型提供了处理数据库表的抽象，具有与其他 **QAbstractItemModel** 子类相同的 API，并提供了一些特定的数据库扩展。SQL 模型可以与视图（如 **QTableView**，我们将在本章最后一节中看到）一起使用，或者与用于表单视图的 **QDataWidgetMapper** 一起使用（这是本章第二节的主题）。

低层方法也是最具灵活性的，基于使用 **QSqlQuery**。该类可以接受任何 **DDL**（数据定义语言）或 **DML**（数据操纵语言） **SQL** 语句并在数据库上执行它们。例如，我们可以使用 **QSqlQuery** 创建表，并在表中插入、更新和删除记录。我们将在本章第一看到 **QSqlQuery** 的实际应用。

*本章假设读者了解 PyQt 的模型/视图架构（前章已覆盖），以及基本的 SQL 知识。

445

### 连接数据库

但在我们对数据库进行任何操作之前，我们必须建立与其的连接。在许多数据库应用程序中，这是在创建 `QApplication` 对象之后、创建或显示主表单之前完成的。其他应用程序稍后才建立连接——例如，仅在需要时才建立。

要使用 PyQt 的 SQL 类，我们必须导入 `QSql` 模块：

```python
from Py4.QtSql import *
```

数据库连接是通过调用静态方法 `QSqlDatabase.addDatabase()` 建立的，传入我们要使用的驱动程序名称。然后，我们必须设置各种属性，如数据库名称、用户名和密码。最后，我们必须调用 `open()` 来建立连接。

```python
db = QSqlDatabase.addDatabase("QSLITE")
db.setDatabaseName(filename)
if not db.open():
    QMessageBox.warning(None, "Phone Log",
        QString("Database Error: %1".arg(db.lastError().text())))
    sys.exit(1)
```

对于 SQLite，我们只需要指定数据库的名称。这通常是一个文件名，但也可以是特殊名称“:memory:”用于内存数据库。当我们使用 SQLite 驱动程序调用 `QSqlDatabase.open()` 时，如果文件不存在，它将被创建，此时它将没有表或记录。

请注意，我们将 `None` 作为消息框的父对象传递：这是因为我们在创建主窗口之前尝试建立连接，因此没有可能的父对象。由于此应用程序依赖于数据库，如果无法建立连接，它只会向用户显示接收到的错误消息并终止应用程序。

如果数据库连接成功打开，从现在开始，所有数据库方法都将应用于此连接。如果我们有两个或更多独立的连接，无论是到同一个数据库还是不同的数据库，我们必须向 `addDatabase()` 传递第二个参数，给连接一个名称，然后我们可以使用它来区分不同的连接。

### 执行 SQL 查询

既然我们已经有连接了，我们可以执行一些 SQL 语句。

```python
query = QSqlQuery()
query.exec_("""CREATE TABLE outcomes (
    id INTEGER PRIMARY KEY AUTOINCREMENT UNIQUE NOT NULL,
    name VARCHAR(40) NOT NULL)""")

query.exec_("""CREATE TABLE calls (
  id INTEGER PRIMARY KEY AUTOINCREMENT UNIQUE NOT NULL,
  caller VARCHAR(40) NOT NULL,
  starttime DATETIME NOT NULL,
  endtime DATETIME NOT NULL,
  topic VARCHAR(80) NOT NULL,
  outcomeid INTEGER NOT NULL,
  FOREIGN KEY (outcomeid) REFERENCES outcomes)""")
```

我们没有指定要使用的特定数据库连接，因此 PyQt 将使用我们之前建立的默认（未命名）连接。SQL 调用创建的表在图 15.1 中示意性地展示出来。

`AUTOINCREMENT` 语法告诉 SQLite 自动填充 `id` 字段，每个 ID 比前一个多 1，第一个为 1。同样，`FOREIGN KEY` 语法告诉 SQLite 关于外键关系。SQLite 3 不强制外键关系，仅允许我们将其作为文档辅助进行表达。在其他数据库中，实现自动 ID 和外键的语法可能不同。

![](img/9bfe0a027fcc8793bb087287001100dd_461_0.png)

**图 15.1** *电话日志数据库设计*

许多数据库拥有自己的一组数据类型。例如，SQLite 3 有它所谓的“存储类”，包括 INTEGER、REAL 和 TEXT。PyQt 支持标准 SQL 数据类型，包括 VARCHAR、NUMBER、DATE 和 DATETIME，并在幕后透明地在数据库的原生数据类型之间进行转换。对于文本，PyQt 使用 Unicode，除了那些不支持 Unicode 的数据库，在这种情况下 PyQt 会在数据库的原生编码之间进行转换。

现在我们已经创建了表，我们可以向其中填充数据。

```python
for name in ("Resolved", "Unresolved", "Calling back", "Escalate",
             "Wrong number"):
    query.exec_("INSERT INTO outcomes (name) VALUES ('%s')" % name)
```

我们不需要提供 ID，因为我们已经要求数据库为我们生成 ID。不幸的是，前面的代码并不健壮：例如，如果名称中包含单引号，它将失败。处理这种情况的一种方法

