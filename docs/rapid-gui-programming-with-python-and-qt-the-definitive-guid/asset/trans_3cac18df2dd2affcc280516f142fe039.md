

此方法会被表单的初始化器调用一次，此后每当用户导航到不同的资产（即资产表视图中的不同行）时也会调用。

如果视图中新位置的模型索引有效，我们从模型中检索该行的完整记录，并在日志模型上设置一个过滤器，该过滤器仅选择那些 assetid 与当前行 ID 对应的日志记录。（这相当于执行 `SELECT * FROM logs WHERE assetid = id` 操作。）然后我们调用 select() 以用选定的日志记录刷新日志视图。如果模型索引无效，我们将 ID 设置为一个已知不存在的值，从而确保不会检索到任何行，日志视图将为空。最后，如果没有日志记录可显示，我们将隐藏日志视图的列标题。

`record()` 方法是 QsqlTableModel 和 QsqlRelationalTableModel 类提供的扩展之一，这些扩展是在其 QAbstractItemModel 基类方法之外的，旨在使其更易于数据库使用。其他扩展包括 setQuery()，它允许我们使用 SQL 语法编写自己的 SELECT 语句，以及 insertRecord()，用于添加记录。

将 assetChanged() 方法连接起来以及该方法的实现，是我们建立两个模型（因此也是它们的视图）之间主从关系所需做的全部工作。

```python
def done(self, result=1):
    query = QSqlQuery()
    query.exec_("DELETE FROM logs WHERE logs.assetid NOT IN"
                 "(SELECT id FROM assets)")
    QDialog.log.done(self, 1)
```

当应用程序终止时，我们执行最后一个查询，以删除那些针对不存在（已删除）资产存在的任何日志记录。在理论上，这永远不需要，因此什么都不做。这是因为，对于支持事务的数据库，我们使用事务来确保如果删除了一个资产，其日志记录也会被删除。

```python
def addAction(self):
    index = self.assetView.currentIndex()
    if not index.isValid():
        return
    QSqlDatabase.database().transaction()
    record = self.assetModel.record(index.row())
    assetid = record.value(ID).toInt()[0]
    row = self.logModel.rowCount()
    self.logModel.insertRow(row)
    self.logModel.setData(self.logModel.index(row, ASSETID),
                          QVariant(assetid))
    self.logModel.setData(self.logModel.index(row, DATE),
                          QVariant(QDate.currentDate()))
    QSqlDatabase.database().commit()
    index = self.logModel.index(row, ACTIONID)
    self.logView.setCurrentIndex(index)
    self.logView.edit(index)
```

如果用户请求添加一个动作（一条新的日志记录），就会调用此方法。我们检索当前资产的 assetid，然后将一条新的日志记录作为 logs 表中的最后一条记录插入。然后我们设置该记录的 assetid 外键为我们检索到的值，并提供一个初始默认日期。最后，我们检索新日志记录的动作组合框的模型索引，并启动编辑，以便用户选择合适的动作。

在检索 assetid 之前，我们开始一个事务。这是为了防止一种理论上的可能性：即在检索 assetid 后，在创建新日志记录之前该资产恰好被删除。如果发生这种情况，该日志记录将指向一个不存在的资产，这可能会导致后来的崩溃或细微问题。一旦我们调用 commit()，我们就知道该资产和新的日志记录都存在。如果有人现在试图删除该资产，他们可以这样做——但该资产的日志记录（包括这条记录）将被正确地随之删除。

为了采取真正防御性的方法，我们可以将事务代码结构化为如下形式：

```python
class DatabaseError(Exception):
    pass

rollback = False
try:
    if not QSqlDatabase.database().transaction():
        raise DatabaseError
    rollback = True
    # execute commands that affect the database
    if not QSqlDatabase.database().commit():
        raise DatabaseError
    rollback = False
finally:
    if rollback:
        if not QSqlDatabase.database().rollback():
            raise DatabaseError
```

这试图确保，如果发生某些问题导致无法到达 commit 或者无法成功执行 commit，我们将回滚到之前的位置，从而保留数据库的关系完整性。然而，如果回滚失败，则一切皆有可能出错。错误信息可以从 QSqlDatabase.database().lastError().text() 中获取，该方法返回一个 QString。

事务的范围是从调用 transaction() 时开始，直到事务被提交或回滚为止。无论数据库是通过 QSqlDatabase 还是通过模型访问的，这一点都无关紧要。只要它们应用于同一事务上下文中的同一数据库，该事务的上下文就适用于所有 SQL 语句，包括由独立查询和不同模型执行的语句。

如果我们使用的是 Python 2.6，或者在 Python 2.5 中使用 `from __future__ import statement`，我们可以通过创建和使用上下文管理器来简化前面显示的代码。

面向事务的方法试图安排事务，使问题不会发生。另一种方法是假设一切都能正常工作，并依靠数据库来维护外键关系和数据完整性的其他方面。这在 SQLite 3 中不起作用，因为它不强制实行关系完整性，但它在某些其他数据库中是有效的。采用这种方法，我们通常可以不用事务进行编码。大多数时候事情都会正常运行，而在极少数发生问题的情况下，我们依靠数据库拒绝执行任何违反其规则的操作，并向我们提供我们可以向用户报告错误信息。

请注意，事务设置在数据库上，通过静态方法 QSqlDatabase.database() 访问。也可以通过调用模型上的 database() 方法来访问数据库。每个数据库连接一次只能处理一个事务，因此如果我们想同时拥有多个事务，我们必须为希望使用的每个额外事务建立一个额外的连接。

```python
def deleteAction(self):
    index = self.logView.currentIndex()
    if not index.isValid():
        return
    record = self.logModel.record(index.row())
    action = record.value(ACTIONID).toString()
    if action == "Acquired":
        QMessageBox.information(self, "Delete Log",
                                "The ‘Acquired’ log record cannot be deleted.<br>"
                                "You could delete the entire asset instead.")
        return
    when = unicode(record.value(DATE).toString())
    if QMessageBox.question(self, "Delete Log",
                            "Delete log<br>%s &gt;" % (when, action),
                            QMessageBox.Yes|QMessageBox.No) == QMessageBox.No:
        return
    self.logModel.removeRow(index.row())
    self.logModel.submitAll()
```

对于删除动作，我们实现的逻辑是用户不能删除“已获取”（“Acquired”）日志记录，即第一条日志记录。（但他们可以删除资产，并随之删除其所有日志记录，正如我们稍后所见。）如果日志记录是用户被允许删除的，并且他们确认删除，我们只需在日志模型上调用 `removeRow()`，然后调用 `submitAll()` 以更新底层数据库。

```python
def editActions(self):
    form = ReferenceDataDlg("actions", "Action", self)
    form.exec_()

def editCategories(self):
    form = ReferenceDataDlg("categories", "Category", self)
    form.exec_()
```

由于动作和类别参考表具有相同的结构，当我们需要深入添加、编辑和删除它们的记录时，可以使用同一个智能对话框。我们将数据库中的表名以及要在用户界面中显示的参考数据名称（例如在对话框的标题栏中）提供给对话框。

![](img/9bfe0a027fcc8793bb087287001100dd_481_0.png)

**图 15.6** *资产管理器参考数据表单*

我们不会审查图 15.6 中显示的 ReferenceDataDlg 的代码，因为它没有教给我们任何新东西。它使用一个 QTableView，其 QSqlTableModel 设置为传递给构造函数的表。编辑是就地进行的，由表视图和表模型自动处理。添加记录只需在模型中插入一个新行并将视图设置到该记录即可。

对于参考数据的删除，我们执行一个查询来查看特定的参考数据记录是否正被其他表使用，即某个动作是否被 logs 表中的任何记录使用，或者某个类别是否被 assets 表中的任何记录使用。如果该记录正在使用中，我们会弹出一个信息性错误消息，并不允许删除发生。否则，我们对模型中相关的行调用 `removeRow()`，然后调用 `submitAll()` 将更改提交到数据库，正如我们在删除动作时所做的那样。

与参考数据不同，资产的添加和删除由主表单的方法处理。

```python
def addAsset(self):
    row = self.assetView.currentIndex().row()
```

