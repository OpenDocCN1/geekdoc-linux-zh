
```cpp
{
    add = new QAction(tr("Add"), this);
    add->setIcon(QIcon(tr("icon/add")));
    connect(add, SIGNAL(triggered()), this, SLOT(add()));

    clear = new QAction(tr("Clear"), this);
    clear->setIcon(QIcon(tr("icon/clear")));
    connect(clear, SIGNAL(triggered()), this, SLOT(clear()));
}
```

`createActions()` 函数创建了添加、编辑、删除、发送和清除动作。虽然可以使用 Qt 资源 (`.qrc`) 文件，但在编写 Qtopia 应用程序时，图标的标准做法是将它们存储在 `pics` 子目录中，并拷贝到设备上（得益于 `.pro` 文件的 `INSTALLS`）。这些图标可以在多个应用程序之间共享，Qtopia 使用特殊数据库优化了对它们的访问。

在 Qt 或 Qtopia 期望名称的地方，我们都可以提供 Qtopia 资源名称。这些名称通过文件名开头的冒号来标识，后跟一个指定资源种类的单词。如果我们想指定图标时提供一个文件名，例如 `:icon/add`，则省略文件扩展名。Qtopia 将在多个标准位置查找合适的图标，从应用程序的 `pictory` 目录开始。详细信息请参见 http://doc.trolltech.com/qtopia4.2/qtopia-resource-system.html。

```cpp
void ExpenseWindow::createMenuToolbar()
{
#ifdef QTOPIA_TOPIC
QMenu *menuToolbar = QMenuBar::menuFor(Widget);
#else
QToolbar *menuToolbar = new QToolbar;
addToolbar(menuToolbar);
#endif
}
```

```cpp
menuToolbar->addAction(addAction);
menuToolbar->addAction(editAction);
menuToolbar->addAction(deleteAction);
menuToolbar->addAction(sendAction);
menuToolbar->addAction(clearAction);
{
```

某些手机具有“软键”，即动作取决于应用程序上下文的多功能键。`QMenuBar` 类在软键可用时利用它们，在不可用时提供弹出菜单。对于 PDA，我们通常使用工具栏而不是弹出菜单。`#ifdef` 指令确保了如果目标是手机，则将动作添加到软菜单中，如果目标是 PDA，则将动作添加到工具栏中。

用户将能够关闭应用程序，而不必强制显式保存数据。他们还期望在稍后重新启动应用程序时能够恢复数据。这通过在构造函数中调用 `loadData()` 并在应用程序的 `closeEvent()` 中保存数据可以轻松实现。Qtopia 为数据存储提供了许多选择，包括保存到 SQLite 数据库的表中或保存到文件中。由于支出数据非常小，我们将使用 `Settings`。我们将查看它是如何保存的，然后是数据加载的。

```cpp
QSettings settings("BookSoft Ltd", "Expenses");
```

```cpp
settings.setValue("data", data);
event->accept();
}
```

我们创建一个 `QByteArray` 并将其写入 `Settings`。由于 Qtopia 提供了数据存储的许多选择，我们会在 `closeEvent()` 中允许应用程序关闭。

```cpp
void ExpenseWindow::closeEvent(QCloseEvent *event)
{
    QSettings settings("BookSoft Ltd", "Expenses");
    QByteArray data;
    DataStream out(&data, QIODevice::WriteOnly);
    out.setVersion(QDataStream::Qt_4);
    for (const Expense &expense : expenses) {
        out << expense.date() << expense.description() << expense.amount();
    }
    settings.setValue("data", data);
    event->accept();
}
```

```cpp
void ExpenseWindow::loadData()
{
    QSettings settings("BookSoft Ltd", "Expenses");
    QByteArray data = settings.value("data").toByteArray();
    if (data.isEmpty()) {
        return;
    }
    DataStream in(&data, QIODevice::ReadOnly);
    in.setVersion(QDataStream::Qt_4);
    while (!in.atEnd()) {
        QDate date;
        QString desc;
        qreal amount;
        in >> date >> desc >> amount;
        expenses.append(Expense(date, desc, amount));
    }
}
```

一旦应用程序运行，用户可以添加、编辑或删除支出、发送列出所有支出的 SMS 消息，或清除它们。支出以值的形式存储在 `QList<Expense>` 中。

构造函数创建了一个 `QList` 和两个 `QLabel`。一个标签显示“Total”（总计）文本，另一个显示支出的总和。动作通过 `createActions()` 函数创建，菜单或工具栏由 `createMenuOrToolbar()` 函数创建。任何待处理的支出会在构造函数结束时通过调用 `loadData()` 函数加载。我们将跳过构造函数本身，转而回顾它所调用的函数。

```cpp
void ExpenseWindow::createActions()
{
    add = new QAction(tr("Add"), this);
    add->setIcon(QIcon(tr("icon/add")));
    connect(add, SIGNAL(triggered()), this, SLOT(add()));
    clear = new QAction(tr("Clear"), this);
    clear->setIcon(QIcon(tr("icon/clear")));
    connect(clear, SIGNAL(triggered()), this, SLOT(clear()));
}
```

`createActions()` 函数创建了添加、编辑、删除、发送和清除动作。虽然可以使用 Qt 资源 (`.qrc`) 文件，但在编写 Qtopia 应用程序时，图标的标准做法是将它们存储在 `pics` 子目录中，并拷贝到设备上（得益于 `.pro` 文件的 `INSTALLS`）。这些图标可以在多个应用程序之间共享，Qtopia 使用特殊数据库优化了对它们的访问。

在 Qt 或 Qtopia 期望名称的地方，我们都可以提供 Qtopia 资源名称。这些名称通过文件名开头的冒号来标识，后跟一个指定资源种类的单词。如果我们想指定图标时提供一个文件名，例如 `:icon/add`，则省略文件扩展名。Qtopia 将在多个标准位置查找合适的图标，从应用程序的 `pictory` 目录开始。详细信息请参见 http://doc.trolltech.com/qtopia4.2/qtopia-resource-system.html。

```cpp
void ExpenseWindow::createMenuToolbar()
{
#ifdef QTOPIA_TOPIC
QMenu *menuToolbar = QMenuBar::menuFor(Widget);
#else
QToolbar *menuToolbar = new QToolbar;
addToolbar(menuToolbar);
#endif
}
```

```cpp
menuToolbar->addAction(addAction);
menuToolbar->addAction(editAction);
menuToolbar->addAction(deleteAction);
menuToolbar->addAction(sendAction);
menuToolbar->addAction(clearAction);
{
```

某些手机具有“软键”，即动作取决于应用程序上下文的多功能键。`QMenuBar` 类在软键可用时利用它们，在不可用时提供弹出菜单。对于 PDA，我们通常使用工具栏而不是弹出菜单。`#ifdef` 指令确保了如果目标是手机，则将动作添加到软菜单中，如果目标是 PDA，则将动作添加到工具栏中。

用户将能够关闭应用程序，而不必强制显式保存数据。他们还期望在稍后重新启动应用程序时能够恢复数据。这通过在构造函数中调用 `loadData()` 并在应用程序的 `closeEvent()` 中保存数据可以轻松实现。Qtopia 为数据存储提供了许多选择，包括保存到 SQLite 数据库的表中或保存到文件中。由于支出数据非常小，我们将使用 `Settings`。我们将查看它是如何保存的，然后是数据加载的。

```cpp
QSettings settings("BookSoft Ltd", "Expenses");
```

### 使用 Qtopia API

```cpp
void ExpenseDialog::createMenuToolbar()
{
    #ifdef QTOPIA_PHONE
    QMenu *menuToolbar = QSoftMenuBar::menu(this);
#else
    QToolBar *menuToolbar = new QToolbar;
    menuToolbar->setMovable(false);
    addToolbar(menuToolbar);
#endif

    menuToolbar->addAction(okAction);
    menuToolbar->addAction(cancelAction);
}
```

如果用户接受对话框，我们会设置当前费用的日期、描述和金额属性，并让调用者通过对话框的 `expense()` 函数来获取这些信息。

如果用户选择发送操作，将会调用 `send()` 函数。该函数会提示用户选择一个联系人来发送费用，准备要发送的消息文本，然后使用 SMS 协议发送消息（见图 2.4）。
