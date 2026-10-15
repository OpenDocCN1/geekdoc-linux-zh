
`Department_LocationId = 2`

}

```

我们将首先查看头文件中的`MainForm`类定义：

```cpp
class MainForm : public QWidget
{
  Q_OBJECT
public:
  MainForm();
private slots:
  void updateEmployeeView();
  void addDepartment();
  void deleteDepartment();
  void editEmployees();
private:
  void createDepartmentPanel();
  void createEmployeePanel();
  SqlRelationalTableModel *departmentModel;
  SqlRelationalTableModel *employeeModel;
  QWidget *departmentPanel;
...
  QDialogButton *buttonBox;
};
```

为了建立主从关系，我们必须确保当用户导航到不同的记录（行）时，我们更新详情视图以仅显示相关记录。这是通过私有槽`updateEmployee()`实现的。其他三个槽的作用与其名称一致，而两个私有函数是构造函数的辅助函数。

构造函数的大部分代码涉及创建用户界面和设置信号-槽连接。我们将关注与数据库编程的部分。

```cpp
MainForm::MainForm()
{
  createDepartmentPanel();
  createEmployeePanel();
```

构造函数通过调用两个辅助函数开始。第一个函数创建部门模型和视图，第二个函数对员工模型和视图执行相同的操作。我们将跳过构造函数的细节。

```cpp
connect(addButton, SIGNAL(clicked()), this, SLOT(addDepartment()));
connect(deleteButton, SIGNAL(clicked()), this, SLOT(deleteDepartment()));
connect(editButton, SIGNAL(clicked()), this, SLOT(editEmployees()));
connect(quitButton, SIGNAL(clicked()), this, SLOT(close()));
departmentView->setCurrentIndex(departmentModel->index(0, 0));
```

我们将按钮连接到槽，并确保第一个项目是当前项目。

现在我们看到了构造函数，我们将查看`createDepartmentPanel()`辅助函数设置的部门模型和视图：

```cpp
void MainForm::createDepartmentPanel()
{
  departmentPanel = new QWidget;
  departmentModel = new SqlRelationalTableModel(this);
  departmentModel->setTable("department");
  departmentModel->setRelation("LocationId", "location", "id", "name");
  departmentModel->setSort(Department_Name, Qt::AscendingOrder);
```

## 展示数据

`createEmployeePanel()`内部的代码与我们看到的类似，但有一些重要的区别：

```cpp
void MainForm::createEmployeePanel()
{
  employeePanel = new QWidget();
  employeeModel = new SqlRelationalTableModel(this);
  employeeModel->setTable("employee");
  employeeModel->setRelation(DepartmentId, "department", "id", "name");
  employeeModel->setSort(EmployeeName, Qt::AscendingOrder);
  employeeView = new QTableView();
  employeeView->setModel(employeeModel);
  employeeView->setSelectionMode(QAbstractView::SingleSelection);
  employeeView->setSelectionBehavior(QAbstractView::SelectRows);
  employeeView->horizontalHeader()->setStretchSection(true);
  employeeLabel = new QLabel("employees");
  employeeLabel->setBuddy(employeeView);
  connect(departmentView, SIGNAL(selectionChanged(const QItem&)), this, SLOT(updateEmployeeView()));
}
```

视图的编辑触发器被设置为`QAbstractView::NoEditTriggers`，使视图变为只读。在此应用程序中，用户可以通过点击“编辑员工”（`Edit Employees`）来添加、编辑和删除员工记录，这将调用上一节中开发的`EmployeeForm`。

这一次我们隐藏了三个列，而不仅仅是一个。因为再次对用户来说没有意义。我们还隐藏了部门列，因为任何时候显示的员工都是当前选择部门的员工。最后，我们隐藏了`startdate`列，因为它并不相关，可以通过点击“编辑员工”来访问。

我们将视图的`currentRowChanged()`信号连接到`updateEmployee()`槽。

## 以表格形式展示数据

每当当前部门发生变化（包括启动）时，都会调用此槽。如果存在有效的当前部门，该函数将获取部门的`ID`并在员工模型上设置过滤器。这会将显示的员工限制在匹配的部门`ID`外键上。（过滤器仅仅是一个不带`WHERE`关键字的`WHERE`子句。）我们还会更新显示在员工表格上标签，以显示员工所属部门的名称。

如果没有有效的部门（例如，数据库为空），我们将设置过滤器匹配一个不存在的部门`ID`，以确保没有记录匹配。

随后，我们对模型执行`select()`操作以应用过滤器。反之，这将发出信号，视图将响应这些信号并更新自身。最后，我们显示或隐藏员工表格的列标题，用以指示是否显示了员工。

```cpp
void MainForm::addDepartment() {
  int row = departmentModel->rowCount();
  departmentModel->insertRow(row);
  QIndex index = departmentModel->index(row, Department_Name);
  departmentView->setCurrentIndex(index);
  departmentView->edit(index);
}
```

如果用户点击“添加”按钮，我们会在部门表格末尾插入新行，使该行成为当前行，并启动部门名称的编辑，就像用户按了`F2`或双击了它一样。如果我们需要提供某些默认值，可以在调用`insertRow()`之后立即调用`setData()`来。

我们不需要担心为新记录创建唯一键，因为我们已经使用了自增计数器来为我们处理。如果这种方法不可行或不合适，我们可以连接模型的`beforeInsert()`信号。该信号在用户编辑后、在数据库执行插入操作之前发出。这是放置`ID`或处理用户数据的理想时机。类似的还有`beforeDelete()`和`beforeUpdate()`信号；这些对于创建审计跟踪非常有用。

```cpp
void MainForm::deleteDepartment() {
  QIndex index = departmentView->currentIndex();
  if (!index.isValid())
    return;
  SqlDatabase::database().transaction();
  SqlRecord record = departmentModel->record(row);
  int id = record.value(Department_Id).toInt();
  int numEmployees = 0;
  SqlQuery query(qString("SELECT COUNT(*) FROM employee "
  "WHERE departmentid = %1").arg(id));
  if (query.next()) {
    numEmployees = query.value(0).toInt();
    if (numEmployees > 0) {
        int r = QMessageBox::warning(this, tr("Delete Department"),
            tr("Delete %1 and all its employees?"),
            arg(record.value(Department_Name).toString()),
            QMessageBox::Yes | QMessageBox::No);
        if (r == QMessageBox::No) {
            SqlDatabase::database().rollback();
        }
        return;
    }
    query.exec(QString("DELETE FROM employee " +
        "WHERE departid = %1").arg(id));
    dependentModel->removeRow(index.row());
    dependentModel->submit();
    SqlDatabase::database().commit();
    updateEmployeeView();
    departmentView->setFocus();
}
```

如果用户想要删除一个部门，如果该部门有员工，我们允许他们直接操作。但如果它有员工，我们会要求用户确认删除，如果他们确认了，我们将执行级联删除，以确保数据库的关联完整性。为了实现这一点，至少对于像`SQLite 3`这样不为我们强制关联完整性的数据库，我们必须使用事务。

一旦启动事务，我们就会执行查询以查找该部门中有多少员工。如果至少有一个，我们就会弹出一个对话框请求确认。如果用户说“否”，我们将回滚事务并返回。否则，我们将删除该部门的所有员工以及部门本身，并提交事务。

```cpp
void main::editEmployees() {
    int employeeId = -1;
    QModelIndex index = employeeView->currentIndex();
    if (index.isValid()) {
        SqlRecord record = employeeModel->record(index.row());
        employeeId = record.value(Employee_Id).toInt();
    }
    EmployeeForm form(employeeId, this);
    form.exec();
    updateEmployeeView();
}
```

每当用户点击“编辑员工”按钮时，就会调用`editEmployees()`槽。我们首先分配一个无效的员工`ID`。然后，尽可能用当前员工的`ID`覆盖它。然后，我们构建`EmployeeForm`并模态显示它。最后，我们调用`updateEmployeeView()`槽，让主表单的详情视图刷新自身，因为员工数据发生了变化。

本章展示了`Qt`的模型/视图类使得在`SQL`数据库中查看和编辑数据变得尽可能简单。在我们需要使用表单视图呈现记录的情况下，我们可以使用`QDataWidgetMapper`将用户界面中的控件映射到数据库中记录的字段上。设置主从关系非常简单，只需要一个信号-槽连接和一个实现一个简单的槽。下钻查询（`Drill-down`）也十分直观，只需要在下钻视图表单的构造函数中导航到选定的记录，或者在未选择记录时转到第一条记录。

## 13. 数据库

- 创建线程
- 同步线程
- 与主线程通信
- 在线程中使用`Qt`类

## 14. 多线程

传统的`GUI`应用程序只有一个执行线程，并且一次只执行一个操作。如果用户从界面调用了耗时长的操作，界面在操作进行期间通常会冻结。多线程是另一种解决方案。在多线程应用程序中，`GUI`运行在自己的线程中，导致即使在进行密集处理期间，`GUI`也能保持响应状态。在日益常见的多处理器系统中，多线程应用程序可以同时执行多个线程，从而获得更好的性能。在本章中，我们将首先展示如何子类`QThread`以及如何使用`QMutex`、`QSemaphore`和`WaitCondition`来同步线程。然后我们将看到哪些`Qt`类可以用于辅助线程，哪些不能。*这里假设你已经理解了多线程的基础知识，因此重点在于如何开发多线程应用程序，而不是线程主题本身。*

*`Qt 4.4`将提供更高级别的线程`API`。*

在`Qt`应用程序中提供多个线程很简单：我们只需要子类`QThread`并重新实现它的`run()`函数。为了展示这是如何工作的，我们将首先回顾一个非常简单的`QThread`代码，它在控制台上重复输出给定的字符串。应用程序的用户界面如图`14.1`所示。

```cpp
class Thread : public QThread
{
    Q_OBJECT
public:
    Thread();
    void setMessage(const QString &message);
    void stop();
protected:
    void run();
private:
    QString messageStr;
    volatile bool stopped;
};
```

`Thread`派自`QThread`并重新实现了它的`run()`函数。它提供了两个额外的函数：`setMessage()`和`stop()`。

`stopped`变量被声明为`volatile`，因为它在不同的线程间访问，我们希望确保每次需要时读取的都是最新的。如果我们忽略了`volatile`关键字，编译器可能会对该变量进行优化，从而导致结果错误。

```cpp
Thread::Thread() {
    stopped = false;
}
```

```cpp
void Thread::run()
{
    while (!stopped) {
        std::cerr << qPrintable(messageStr);
        stopped = false;
        std::cerr << std::endl;
    }
}
```

调用`run()`开始执行线程。只要`stopped`变量为假，该函数就会不断向控制台打印消息。当控制离开`run()`函数时，线程终止。

```cpp
void Thread::stop()
{}
```

## 创建线程 341

```cpp
stopped = true;
}
```

`stop()`函数将`stopped`变量设置为`true`，从而告诉`run()`停止向控制台打印文本。该函数可以在任何线程的任何时间调用。对于本示例而言，我们假设对`bool`的赋值是一个原子操作。考虑到`bool`只有两种状态，这是一个合理的假设。我们将在本节稍后的部分介绍如何使用`QMutex`来保证对变量的赋值是一个原子操作。

`Thread`提供了一个`terminate()`函数，可以在线程仍在运行时强制终止其执行。不建议使用`terminate()`，因为它可以在任何点停止线程，并且没有给线程留下清理现场的机会。像我们这里这样使用`stopped`变量和`stop()`函数总是更安全的。

![](img/930c1c6fda99d425284503ebcbc940ea_363_0.png)

图`14.1`. `Threads`应用程序

现在我们将看到如何在一个小型`Qt`应用程序中使用`Thread`类，该程序除了主线程外，还使用了两个线程`A`和`B`。

```cpp
class ThreadDialog : public QDialog
{
    Q_OBJECT
public:
    ThreadDialog(QWidget *parent = 0);
protected:
    void closeEvent(QCloseEvent *event);
private slots:
    void startOrStopThreadA();
    void startOrStopThreadB();
private:
    Thread threadA;
    Thread threadB;
    QPushButton *threadABButton;
    QPushButton *threadButton;
    QPushButton *quitButton;
};
```
