

因此，我们将分段进行讲解，跳过布局部分，因为本章的重点在于数据库编程。

```python
class PhoneLogDlg(QDialog):
    FIRST, PREV, NEXT, LAST = range(4)

    def __init__(self, parent=None):
        super(PhoneLogDlg, self).__init__(parent)

        callerLabel = QLabel("&Caller:")
        self.callerEdit = QLineEdit()
        callerLabel.setBuddy(self.callerEdit)
        today = QDate.currentDate()
        startLabel = QLabel("&Start:")
        self.startDateTime = QDateTimeEdit()
        startLabel.setBuddy(self.startDateTime)
        self.startDateTime.setDateRange(today, today)
        self.startDateTime.setDisplayFormat(DATE_TIME_FORMAT)
        endLabel = QLabel("&End:")
        self.endDateTime = QTimeEdit()
        endLabel.setBuddy(self.endDateTime)
        self.endDateTime.setDateRange(today, today)
        self.endDateTime.setDisplayFormat(DATE_TIME_FORMAT)
        topicLabel = QLabel("&Topic:")
        topicEdit = QLineEdit()
        topicLabel.setBuddy(topicEdit)
        firstButton = QPushButton()
        firstButton.setIcon(QIcon(":/first.png"))
```

我们为每个字段创建一个标签和一个合适的编辑控件。我们还创建了表单的所有按钮，尽管我们只展示了第一个按钮的创建过程。我们向添加、删除和退出按钮的构造函数传递字符串，除了给它们图标之外，还为其设置标题。

```python
self.model = QSqlTableModel(self)
self.model.setTable("calls")
self.model.setSort(STARTTIME, Qt.AscendingOrder)
self.model.select()
```

在控件就位后，我们创建一个 `QSqlTableModel`。由于我们未指定特定的数据库连接，它将使用默认连接。我们告诉模型要操作哪张表，并调用 `select()` 使其填充数据。我们还选择为表应用排序顺序。

现在，既然我们拥有了合适的控件和模型，就必须以某种方式将它们联系起来。这是通过使用 `QDataWidgetMapper` 来实现的。

```python
self.mapper = QDataWidgetMapper(self)
self.mapper.setSubmitPolicy(QDataWidgetMapper.ManualSubmit)
self.mapper.setModel(self.model)
self.mapper.addMapping(self.callerEdit, CALLER)
self.mapper.addMapping(self.startTimeEdit, STARTTIME)
self.mapper.addMapping(self.endTimeEdit, ENDTIME)
self.mapper.addMapping(topicEdit, TOPIC)
self.mapper.toFirst()
```

要使数据小部件映射器正常工作，我们必须为其提供一个模型，以及表单中的小部件与模型中相应列之间的一组映射。（变量 `ID`、`CALLER`、`STARTTIME` 等在该文件开头分别被设置为 `0, 1, 2` 等。）映射器可以设置为自动提交更改，或者仅在被告知时提交。我们倾向于后一种方法，因为它赋予我们更细的控制权，并且意味着当用户导航到不同的记录时，我们可以确保任何未保存的更改都被保存。一旦设置好映射，我们需要让映射器用小部件填充一条记录；我们通过调用 `toFirst()` 实现了这一点，这意味着在启动时，会显示第一条记录。

```python
self.connect(firstButton, SIGNAL("clicked()"),
            lambda: self.saveRecord(PhoneLogDlg.FIRST))
self.connect(prevButton, SIGNAL("clicked()"),
            lambda: self.saveRecord(PhoneLogDlg.PREV))
self.connect(nextButton, SIGNAL("clicked()"),
            lambda: self.saveRecord(PhoneLogDlg.NEXT))
self.connect(lastButton, SIGNAL("clicked()"),
            lambda: self.saveRecord(PhoneLogDlg.LAST))
self.connect(addButton, SIGNAL("clicked()"), self.addRecord)
self.connect(deleteButton, SIGNAL("clicked()"),
            self.deleteRecord)
self.connect(quitButton, SIGNAL("clicked()"), self.accept)
self.setWindowTitle("Phone Log")
```

前四个连接提供导航功能。在每种情况下，我们都调用 `saveRecord()`，它会保存任何未保存的更改，然后根据包裹在 lambda 语句中的参数进行导航。这意味着我们只需要一个方法 `saveRecord()`，而不是为每个导航按钮各创建一个方法。但是，这些连接仅适用于 PyQt 4.1.1 或更高版本。对于早期版本，我们必须保持一个实例变量（例如，一个列表），其中包含对 lambda 函数的引用，以防止它们被垃圾回收。

```python
def accept(self):
    self.mapper.submit()
    QDialog.accept(self)
```

如果用户点击退出，我们调用 `QDataWidgetMapper.submit()`，它将当前记录写回到底层模型，然后关闭窗口。

```python
def saveRecord(self, where):
    row = self.mapper.currentIndex()
    self.mapper.submit()
    if where == PhoneLogDlg.FIRST:
        row = 0
    elif where == PhoneLogDlg.PREV:
        row = 0 if row <= 1 else row - 1
    elif where == PhoneLogDlg.NEXT:
        row += 1
        if row >= self.model.rowCount():
            row = self.model.rowCount() - 1
    elif where == PhoneLogDlg.LAST:
        row = self.model.rowCount() - 1
    self.mapper.setCurrentIndex(row)
```

如果用户进行导航，我们必须记住当前行，因为在调用 `submit()` 之后该行会被遗忘。然后，在保存当前记录后，我们将行设置为用户请求的导航所对应的行（但保持在边界内），然后使用 `setCurrentIndex()` 移动到适当的记录。

```python
def addRecord(self):
    row = self.model.rowCount()
    self.mapper.submit()
    self.model.insertRow(row)
    self.mapper.setCurrentIndex(row)
    now = QDateTime.currentDateTime()
    self.startDateTime.setDateTime(now)
    self.endDateTime.setDateTime(now)
    self.callerEdit.setFocus()
```

我们选择总是将新记录添加到末尾。为此，我们找到最后一行之后的行，保存当前记录，然后在模型的最后一行插入一条新记录。然后我们将映射器的当前索引设置为新行，初始化几个字段，并让呼叫者字段获得焦点，以便用户开始输入。

```python
def deleteRecord(self):
    caller = self.callerEdit.text()
    starttime = self.startDateTime.dateTime().toString(DATE_TIME_FORMAT)
    if QMessageBox.question(self, QString("Delete"),
                      QString("Delete call made by<b> %1 on %2")
                      .arg(caller).arg(starttime),
                      QMessageBox.Yes | QMessageBox.No) == QMessageBox.No:
        return
    row = self.mapper.currentIndex()
    self.model.removeRow(row)
    self.model.submitAll()
    if row + 1 >= self.model.rowCount():
        row = self.model.rowCount() - 1
    self.mapper.setCurrentIndex(row)
```

如果用户点击删除，我们从当前记录中选取一些信息，并在询问用户确认删除时使用这些信息。如果他们确认，我们获取当前行，从模型中移除该行，并调用 `submitAll()` 以强制模型将更改写回底层数据源（在本例中为数据库）。然后，我们通过导航到下一条记录来完成操作。

我们使用 `submitAll()`，因为我们是在模型上执行删除，而不是在映射器上，对于数据库，除非视图（或数据小部件映射器）已设置为自动提交，否则我们必须通过调用此方法来确认对模型的更改。数据小部件映射器的 API 不允许我们添加或删除记录，只能编辑现有记录，因此，我们必须使用底层模型来添加或删除记录。

到目前为止，我们使用的技术可以应用于任何数据库表或可编辑的数据库视图，为用户提供一种导航、添加、更新和删除记录的手段。然而，在大多数情况下，我们需要考虑外键，以及我们将在回顾图 15.3 中所示的电话记录应用程序时解决的问题。

![](img/9bfe0a027fcc8793bb087287001100dd_469_0.png)

通话表（在第 447 页显示）有一个外键 outcomeid 字段。我们希望该字段在表单中显示为组合框，显示结果表中的名称

