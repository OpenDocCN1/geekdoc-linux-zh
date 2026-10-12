

其目的是确保我们移除或转义不可接受的字符，但 PyQt 提供了更好的替代方案：预编译查询。

预编译查询有两种广泛使用的语法形式，一种基于 ODBC 占位符方法，另一种基于 Oracle 命名变量方法。PyQt 支持这两种方法，必要时会在幕后将一种转换为另一种，因此无论底层数据库是什么，两者都能正常工作。

```python
query.prepare("INSERT INTO calls (caller, starttime, endtime, "
              "topic, outcomeid) VALUES (?, ?, ?, ?, ?, ?)")
for name, start, end, topic, outcomeid in data:
    query.addBindValue(QVariant(Qstring(name)))
    query.addBindValue(QVariant(start))      # QDateTime
    query.addBindValue(QVariant(end))        # QDateTime
    query.addBindValue(QVariant(Qstring(topic)))
    query.addBindValue(QVariant(outcomeid))  # int
query.exec_()
```

此示例使用 ODBC 语法。使用占位符的一个好处是，PyQt 会处理引号问题，因此我们不必担心数据的内容，只要传递的类型适合它们将要填充的字段即可。

```python
query.prepare("INSERT INTO calls (caller, starttime, endtime, "
              "topic, outcomeid) VALUES (:caller, :starttime, "
              ":endtime, :topic, :outcomeid)")
for name, start, end, topic, outcomeid in data:
    query.bindValue(":caller", QVariant(Qstring(name)))
    query.bindValue(":starttime", QVariant(start))
    query.bindValue(":endtime", QVariant(end))
    query.bindValue(":topic", QVariant(Qstring(topic)))
    query.bindValue(":outcomeid", QVariant(outcomeid))
query.exec_()
```

第二个示例执行与第一个相同的工作，但使用 Oracle 风格的命名变量。PyQt 还支持其他几种预编译查询语法的变体，但它们并未增加我们在前面展示的两种语法形式中无法实现的功能。对于支持预编译查询的数据库，预编译查询可以提高性能；对于不支持的数据库，则没有区别。

预编译查询也可用于调用存储过程，但我们将不涵盖这一主题，因为对存储过程的支持既不普遍也不统一。例如，并非所有数据库都支持存储过程，且调用存储过程及获取 Qut 值的语法因数据库而异。此外，返回值的存储过程并未得到完全支持。

我们可以使用 QSqlQuery 执行任何任意 SQL 语句。例如：

```python
query.exec_("DELETE FROM calls WHERE id = 12")
```

查询执行后，我们可以通过调用 QsqlQuery.isActive() 来检查是否发生错误；如果返回 False，则表明发生了错误，并且可以通过调用 QsqlQuery.lastError().text() 以 QString 形式获取错误消息。

如果我们执行可能影响多行数据的查询，例如 WHERE 子句可能匹配多条记录的 DELETE 或 UPDATE，我们可以调用 QsqlQuery.numRowsAffected()；发生错误时它返回 -1。

我们可以通过访问驱动程序并调用 hasFeature() 来了解底层数据库是否支持各种功能，如事务和 BLOB（二进制大对象）。例如：

```python
driver = QSqlDatabase.database().driver()
if driver.hasFeature(QsqlDriver.Transactions):
    print "Can commit and rollback"
```

使用 QsqlQuery 时，我们可以调用 QsqlDatabase.database().transaction() 来启动事务，然后调用 QsqlDatabase.database().commit() 或 QsqlDatabase.database().rollback()。

我们将通过查看如何使用 QsqlQuery 执行 SELECT 语句以及如何遍历结果记录来结束对 QsqlQuery 的介绍。

```python
DATETIME_FORMAT = "yyyy-MM-dd hh:mm"
ID, CALLER, STARTTIME, ENDTIME, TOPIC, OUTCOMEID = range(6)

query.exec_("SELECT id, caller, starttime, endtime, topic, "
            "outcomeid FROM calls ORDER by starttime")
while query.next():
    id = query.value(ID).toInt()[0]
    caller = unicode(query.value(CALLER).toString())
    starttime = unicode(query.value(STARTTIME).toDateTime() \
                .toString(DATETIME_FORMAT))
    endtime = unicode(query.value(ENDTIME).toDateTime() \
                .toString(DATETIME_FORMAT))
    topic = unicode(query.value(TOPIC).toString())
    outcomeid = query.value(OUTCOMEID).toInt()[0]
    subquery = QsqlQuery("SELECT name FROM outcomes "
                     "WHERE id = %d" % outcomeid)
    outcome = "invalid foreign key"
    if subquery.next():
        outcome = unicode(subquery.value(0).toString())
    print "%02d: %s - %s %%s [%%s]" % (id, caller, starttime, endtime, topic, outcome)
```

执行 SELECT 语句时，我们可以使用 QsqlQuery.next()、QsqlQuery.previous() 和 QsqlQuery.seek() 等方法遍历结果集。在成功的 SELECT 之后，isActive() 将返回 True，但内部记录指针并不指向有效记录。每个导航方法只有在查询的内部记录指针成功移动到有效记录时才返回 True；这就是为什么我们在访问第一条记录之前要调用 QSqlQuery.next()。如果发生错误或越过最后（或第一）条记录，它们将返回 False。

在遍历大型结果集时，只要我们要么仅使用 next()，要么仅向前使用 seek()，我们就可以调用 QSqlQuery.setForwardOnly(True)。在某些数据库上，这可以显著改善性能或减少内存开销，或两者兼得。

QSqlQuery.value() 方法接受一个基于 SELECT 语句中给定字段名顺序的索引位置参数。因此，不建议使用 SELECT *，因为在这种情况下，我们不知道字段的顺序。每个字段都作为 QVariant 返回，因此必须转换为适当的类型。对于日期/时间，我们首先将它们从 QVariant 转换为 QDateTime，然后转换为 QString，最后转换为 unicode，以便打印到控制台。

我们使用额外的查询根据其 ID 查找结果名称，如果数据库不具备关系完整性，则提供错误文本。对于大型数据集，使用预编译查询来处理子查询会更有效率。

我们可以使用 QsqlQuery 完成我们想要的所有数据库工作，但在 GUI 编程中，使用 PyQt 的 SQL 模型要简单得多，而且这并不妨碍我们在需要时使用 QsqlQuery。

## 选定的 QSqlQuery 方法

| 语法 | 描述 |
| :--- | :--- |
| q.addBindValue(v) | 在使用 QSqlQuery q 进行位置值绑定时，将 QVariant v 添加为下一个变量 |
| q.bindValue(p, v) | 在使用 QSqlQuery q 进行占位符值绑定时，将 QVariant v 设置为字符串 p 占位符的值 |
| q.boundValue(p) | 返回 QSqlQuery q 中字符串 p 占位符的 QVariant 值 |
| q.driver() | 返回与 QSqlQuery q 关联的 QSqlDriver。QSqlDriver 类提供 hasFeature() 来报告底层数据库支持哪些功能。 |
| q.exec_(s) | 在 QSqlQuery q 上执行字符串 s 中的 SQL 查询 |
| q.first() | 在执行 SELECT 查询后，导航到 QSqlQuery q 结果集中的第一条记录 |
| q.isActive() | 如果查询处于“活动”状态（例如，在执行 SELECT 查询后），则返回 True |
| q.isValid() | 如果查询定位在有效记录上，则返回 True；在 SELECT 查询之后，只有当 isActive() 为 True 且已导航到一条记录时，它才为 True |
| q.last() | 在执行 SELECT 查询后，导航到 QSqlQuery q 结果集中的最后一条记录 |
| q.lastError() | 返回一个 QSqlError 对象；该对象提供 errorString() 方法 |
| q.next() | 在执行 SELECT 查询后，导航到 QSqlQuery q 结果集中的下一条记录。这是遍历结果集所需的一个方法。 |
| q.numRowsAffected() | 返回刚执行的 SQL 查询影响的行数，前提是该查询不是 SELECT，且底层数据库支持此功能 |
| q.prepare(s) | 准备字符串 s 中的查询，以便 q 执行它 |
| q.previous() | 在执行 SELECT 查询后，导航到 QSqlQuery q 结果集中的上一条记录 |
| q.record() | 返回包含 QSqlQuery q 当前记录的 QSqlRecord 对象（如果有）；使用带字段索引参数的 QSqlQuery.value() 通常更方便 |
| q.size() | 返回 SELECT 结果集中的行数，如果未执行 SELECT 或底层数据库不支持此功能，则返回 -1 |
| q.value(i) | 如果存在，返回当前记录中字段索引 int i 的 QVariant 值 |

### 使用数据库表单视图

为数据库数据提供用户界面时，最简单的方式之一是每次显示单条记录字段的表单。在本节中，我们将开发一个使用此类表单的应用程序，最初是前面介绍的电话日志数据库的简化版本，然后是全功能版本，包含外键字段。

本节中提供的示例依赖于 Qt 4.2 中引入的 QtDataWidgetMapper 类。下一节的示例使用 SQL 表模型和 QTableView，可用于 Qt 4.1 或更高版本。

![](img/9bfe0a027fcc8793bb087287001100dd_465_0.png)

简化后的应用程序如**图 15.2**所示，其源代码位于 chapp15/phoneLog.pyw；完整版本位于 chapp15/phoneLog-fk.pyw。当这些应用程序首次运行时，它们会创建一个包含虚构记录的数据库，并在后续运行中使用该数据库。使用 Qt 内置的 SQLite 生成这些记录在 Linux 上速度很快，但在某些 Windows 机器上非常慢。（使用闪屏来掩盖这种缓慢。）

简化后的应用程序只有一个表 calls，没有外键字段。表单由 PhoneLogDlg 类表示。初始化方法相当长，
