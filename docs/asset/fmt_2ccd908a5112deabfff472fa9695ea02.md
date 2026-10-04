
```cpp
SqlQuery query("SELECT firstname, lastname FROM employees");
QSqlRecord record = query.record();
while (query.next()) {
  QString firstname = query.value(record.indexOf("firstname")).toString();
  QString lastname = query.value(record.indexOf("lastname")).toString();
  qDebug() << query.at() << ":*" << lastname << ":*";
}
```

对于更改数据库内容的操作（如 `UPDATE` 或 `DELETE`），`numRowsAffected()` 返回涉及的数据集数量：

```cpp
// sqlexample/main.cpp (继续)

query.exec("DELETE FROM employees WHERE lastname = 'Hasse'");
qDebug() << query.numRowsAffected(); // "1"
```

对于 `INSERT` 指令，情况有点复杂。由于它们被用于将程序数据值写入数据库，构造相应的字符串可能会变得复杂。由于原因，我们需要不同的路径：使用 `prepare()` 在 `QSqlQuery` 对象中保存带有占位符的所需命令：

```cpp
// sqlexample/main.cpp (继续)

query.prepare("INSERT INTO employees (lastname, firstname, department)"
  VALUES(:lastname, :firstname, :department)");
query.bindValue(":lastname", "Hasse");
query.bindValue(":firstname", "Peter");
query.bindValue(":department", 3);
query.exec();
```

源自 Oracle 世界的 SQL 命令中的命名通配符以冒号开始：我们可以使用 `bindValue()` 命令替换它们。

`SqlQuery` 也可以使用 `addBindValue()` 处理来自 ODBC 的未知参数。对此方法的每次调用按它们出现的顺序替换 `VALUES` 子句中的问号：

```cpp
// sqllexample/main.cpp (继续)

query.prepare("INSERT INTO employees (lastname, firstname, department)"
  VALUES (?, ?, ?);
query.addBindValue("Hasse");
query.addBindValue("Peter");
query.addBindValue(3);
query.exec();
```

## 9.5 事务

并不是所有的数据库都支持事务，事务将多个 SQL 操作组合为一个原子操作。为了帮助 Qt 程序员保持代码的可移植性，因此可以通过 `hasFeature()` 询问 `QSqlDriver` 的事务能力。

```cpp
if (db.driver()->hasFeature(QSqlDriver::Transactions)) ...;
```

如果驱动程序支持事务，我们可以通过 `transaction()` 方法引入事务。如果所有操作完成，则使用 `commit()` 关闭事务。如果发生错误，`rollback()` 将撤销当前事务。

## 9.6 嵌入式数据库

Qt 的 SQLite 驱动允许数据存储在关系数据库中并查询，而无需外部数据库服务器。当然，存在限制，但对嵌入式数据库的需求通常比位于专用服务器的数据库要小，而 SQLite 正是为这种情况设计的。然而，它非常适用于需要基础关系数据存储的应用程序。完美的例子是 KDE 音乐播放器 Amarok，它在 SQLite 数据库中存储音乐元数据。

要打开 SQLite 数据库的连接，只需要指定数据库名称。在这种，SQLite 驱动程序期望一个文件名：

```cpp
QSqlDatabase db = QSqlDatabase::addDatabase("SQLITE");
db.setDatabaseName("firma.db");
```

如果数据库仅在程序运行期间保留在内存中，则可以通过将数据库名称括在冒号内来生成临时数据库，如下所示。`:results:` 数据库在程序终止时不会保存为文件：

```cpp
QSqlDatabase db = QSqlDatabase::addDatabase("SQLITE");
db.setDatabaseName(":results:");
```

你可以像往一样操作此数据库，但要理解对它进行的任何更改之后都会丢失。如果数据已经是关系型本质，则临时数据库不需要自有的数据结构。

## 9.7 在 Interview 中使用 SQL 模型类

为了显示数据库的内容，通常使用表格视图（table views）是合适的，在某些情况下也能看到列表视图（list views）。这就是为什么 QtSql 模块为 Interview 提供了一系列模型（见第 207 页第 8 章）。

### 9.7.1 在表格和树中显示不带外键的 SQL 表

`QTableModel` 允许将表直接显示在表格或树视图中。列头对应于 SQL 表的字段名（属性、列）。在我们第 261 页表 9.2 的的人员数据库中，这些字段是 id、first name、last name 和 department。每一行对应一个数据集。为了更好地说明这一点，我们将查看下面的示例，该示例假设已经打开了连接：

```cpp
// sqlmv/main.cpp

TableView tableView;
QSqlTableModel tableModel;
tableModel.setTable("employees");
tableModel.select();
tableModel.removeColumn(0);
tableView.setModel(&tableModel);
tableView.setWindowTitle("employees table");
tableView.show();
```

首先我们创建一个表，然后是模型。我们将其分配给当前数据库，以便使用 `select()` 获取数据。然后我们使用 `removeColumn()` 从视图中移除列（图 9.2）。该方法源于 `QAbstractItem`，它是所有模型的终极基类。最后，我们将模型绑定到表格视图，赋予表名并显示它。

图 9.2：`QTableModel` 负责 Interview 中的 SQL 表。

| 'employees' 表 | | | | |
|---|---|---|---|---|
| 1 Werner | Max | 1 | | |
| 2 Lehmann | Daniel | 2 | | |
| 3 Roetzel | David | 1 | | |
| 4 Schergen | David | 2 | | |
| 5 Kupfer | Andreas | 2 | | |
| 6 Scheidweiler | Najda | 2 | | |

### 9.7.2 解决外键

`SqlRelationalTableModel` 扩展了表格模型的功能，用于关系型数据库。此外，此类类中的对象会触发外键关系。我们可以利用 departments 表将 department 字段中无意义的数字替换为部门名称（见第 261 页表 9.3）。

图 9.3：`SqlRelationalTableModel` 通过第二个表记录了外键 id。

| 已解析关系的表 | | | | | |
|---|---|---|---|---|---|
| 1 Werner | Max | Management | | | |
| 2 Lehmann | Daniel | R&D | | | |
| 3 Roetzel | David | Manager | | | |
| 4 Schergen | David | Management | | | |
| 5 Kupfer | Andreas | Marketing | | | |
| 6 Scheidweiler | Najda | Accounting | | | |
| 7 Jueppner | Daniela | R&D | | | |
| 8 Hasse | Peter | Accounting | | | |
| 9 Siebiegeroth | Jennfer | Marketing | | | |

为了描述这种关系，使用了 `setRelation()` 方法：它期望第一个参数是包含外键的列索引。在我们的示例中，departments 表中的 name 字段应该出现在第三列，而不是 departments 表中外键字段（即 id 字段）的值。这些信息被封装在 `QSqlRelation` 类的实例 `rel` 中，我们将其作为第二个参数传递给 `setRelation()`。

在在上一个示例中，现在我们可以开始查询 `select()`，将模型绑定到视图并显示结果：

接下来是一个只有在与 `QRelationalTableModel` 结合时才起作用的特性。一个名为 `QSqlRelationalDelegate` 的特殊代理允许用户在编辑定义了关系的列时从列表中选择值（图 9.3）。它独立于所使用的 `QSqlRelation` 编译这些内容。在示例中，它从 `name` 列获取建议；相反，写回表的值来自 `id` 列。

### 9.7.3 显示查询结果

为了显示无法简单通过 `QTableModel` 过滤器进行建模的特别复杂的 `SELECT` 查询结果，请使用 `QSqlQueryModel`。接下来的示例评估了公司每个部门有多少员工。此外，列应该是描述性名称，如图 9.4 所示。

| department | employee count |
|---|---|
| 1 Management | 2 |
| 2 R&D | 4 |
| 3 Marketing | 1 |
| 4 Accounting | 2 |

图 9.4：`SqlQueryModel` 可作为 Interview 中所有类型查询的源。

实例化模型后，将查询作为字符串传递给 `setQuery()`。另一种方法是使用 `QSqlQuery` 对象。由于在复杂的查询中可能会发生错误，我们应该在查询执行后立即引入错误检查。`lastError()` 返回 SQL 对象报告的错误：

```cpp
// sqlview/main.cpp (continued)
TableView view;
QSqlQueryModel queryModel;
queryModel.setQuery("SELECT departments.name, COUNT(employees.id) AS count "
                   "FROM departments LEFT JOIN employees ON departments.id = employees.department "
                   "GROUP BY departments.name");
view.setModel(&queryModel);
view.setWindowTitle("employee count");
if (queryModel.lastError().isValid()) {
    qDebug() << queryModel.lastError().text();
}
view.show();
```

我们可以通过使用自定义字符串替换列头来实现友好的表头，这是所有模型的默认设置。这也可以进行国际化。

### 9.7.4 编辑策略

所有这些表格模型都是可写的。但我们还没有仔细查看模型将数据写入数据库的时机。有三种策略：

- `SqlTableModel::FieldChange`：一旦用户更改了字段中的值，就会将更改传输到数据库。
- `SqlTableModel::RowChange`：在用户选择另一个数据集（即视图中的另一行）之前，临时保存所有更改。
- `SqlTableModel::OnManualSubmit`：在调用 `submitAll()` 槽或触发 `revertAll()` 槽之前，保存模型的所有更改。后者会拒绝所有缓存并从数据库恢复状态（详情见第 270 页 9.7.5）。

我们将修改第 265 页的示例来说明最后一种场景，使其在表格视图下方布局了两个按钮。其他命令保持不变。

```cpp
// sqlmvd/main.cpp (continued)
QWidget w;
QPushButton *submitPb = new QPushButton(QObject::tr("Save Changes"));
QPushButton *revertPb = new QPushButton(QObject::tr("Roll back changes"));
GridLayout *lay = new QGridLayout(&w);
QTableView *manualTableView = new QTableView;
lay->addWidget(manualTableView, 0, 0, 2);
lay->addWidget(submitPb, 1, 0);
lay->addWidget(revertPb, 1, 1);
SqlTableModel *manualTableModel = new SqlTableModel;
manualTableModel->setTable("employees");
manualTableModel->select();
manualTableModel->setEditStrategy(SqlTableModel::OnManualSubmit);
manualTableView->setModel(manualTableModel);
QObject::connect(submitPb, SIGNAL(clicked(bool)), &manualTableModel, SLOT(submitAll()));
QObject::connect(revertPb, SIGNAL(clicked(bool)), &manualTableModel, SLOT(revertAll()));
w.setWindowTitle("manual revertable table");
w.show();

return app.exec();
```

# 9 QtSql 模块

![](img/b663c93885d7333a091a433460ee647f_271_0.png)

我们不能忘记将主控件作为新的顶层控件显示。结果如图 9.5 所示。

## 9.7.5 表模型中的错误

Qt 4.1 中与表模型相关的几个问题在目前应该暂不予处理。其中一个是在删除列后，编辑器操作并不总是能可靠地运行。`QTableModel` 甚至完全忽略了 `removeColumn()` 指令。作为通变方案，这里使用过滤掉不需要的数据集的代理模型。如果只需要显示数据，你可以直接在 `QSqlQuery` 之上放置一个 SQL 查询。

另一个问题涉及 `revertAll()` 槽，它用于在 `OnManualSubmit`（手动提交）编辑策略下撤销关系表中的任何更改。然而，对于通过 `setRelation()` 定义了外键关系的列，`revertAll()` 不会恢复到旧值。到目前，唯一的解决方案是将按钮的槽连接到一个自定义的槽上，该槽用具有相同属性的新模型替换当前模型。由于模型临时保存数据，通过这种方式数据将会丢失，新模型将显示数据库中的原始数据。

# 第 10 章

# "Arthur" 图形库

本章介绍了由 Trolltech 命名为 "Arthur" 的类库的绘制方法，可能是参考了微软的 "Avalon" 技术。在本章中，我们将通过示例观察 Qt 如何在图形缓冲区、主内存缓冲区以及控件和其他设备上进行“绘图”的。此外，我们将详细介绍属于 Arthur 的类及其经典的应用领域。在此之前，我们必须更精确地解释 Qt 中的绘图是如何工作的。首先，我们将查看 Qt 使用的颜色规范。

## 10.1 颜色

颜色规范在图形界面中具有至关重要的地位，包括如何生成颜色以及如何命名已知颜色以便我们能够高效地处理它们。本节专门讨论开发者如何管理颜色。

### 10.1.1 RGB 颜色空间

Qt 将颜色封装在 `QColor` 类中。这基于 RGB 模型，每个颜色分配 8 位，表示从 0 到 255 的值范围。此外，`QColor` 还指定了另一个值，即所谓的 alpha 值，也称为 alpha 通道。这定义了像素的透明度。

`QColor` 也可以处理整数以外的值。对于每个接受整数的颜色命令，都存在一个浮点变体，允许更精确地指定颜色。下文每讨论 `QColor` 方法信息时，你可以用相关的浮点变体代替它，它接受真实值。例如，`setRGB()` 方法接受红、绿、蓝颜色分量的整数值并接受一个可选的 alpha 值，它有一个对应的浮点等效的 `setRGB()` 对象。

有几种方法可以生成新的 `QColor`。基本的 `QColor()` 构造函数创建一个无效的颜色。此外，还有一个接受使用整数描述的颜色的构造函数。这里的语义与 `setRGB()` 相同。没有单独的接受浮点数作为参数的构造函数，因为这会产生歧义，C++ 会自动将整数值转换为浮点值。要用浮点值初始化颜色，你首先创建一个空的（初始为无效的）`QColor` 对象，然后通过 `setRGB()` 设置颜色。

早期的示例经常使用另一个构造函数，它接受从 `GlobalColor` 举举定义的 20 种定义颜色中选择的颜色。它还包含了描述一些特殊情况的值：例如，“颜色” `QColor::transparent` 对应 `QColor(0, 0, 0, 0)`，并允许背景颜色显示出来。
