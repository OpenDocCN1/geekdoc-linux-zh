
在`okToContinue()`中，我们检查`windowModified`属性的状态。如果为`true`，我们显示图 3.9 中的消息框。该消息框有是、否和取消三个按钮。

`QMessageBox`提供了许多标准按钮，并会自动尝试将一个按钮设为默认按钮（用户按 Esc 时激活），并将另一个按钮设为逃逸键按钮（用户按 Esc 时激活）。也可以选择特定的按钮作为默认和逃逸键按钮，并自定义按钮文本。

`warning()`的调用初看起来可能有点令人生畏，但通用语法非常直接：

```cpp
QMessageBox::warning(parent, title, message, buttons);
```

除了`warning()`之外，`QMessageBox`还提供了`information()`、`question()`和`critical()`，每个函数都有自己的图标。图标在图 3.10 中。

![](img/930c1c6fda99d425284503ebcbc940ea_80_0.png)

```cpp
void MainWindow::open()
{
    if (okToContinue()) {
        QString fileName = QFileDialog::getFileName(this,
            tr("打开电子表格"), ".",
            tr("电子表格文件 (*.sp)"));
        if (!fileName.isEmpty()) {
            loadFile(fileName);
        }
    }
}
```

`open()`槽对应文件|打开。像`new()`一样，它首先调用`okToContinue()`来处理任何未保存的更改。然后它使用静态便利函数`QFileDialog::getFileName()`从用户处获取文件名。如果用户点击“取消”，则返回`false`。`QFileDialog::getFileName()`的第一个参数是父窗口。如果文件已有名称（因为已打开或已保存），`save()`将使用该名称调用`saveFile()`；否则它简单地调用`saveAs()`。

`saveAs()`槽对应文件|另存为。我们调用`QFileDialog::getSaveFileName()`从用户处获取文件名。如果用户点击“取消”，我们返回`false`，这将传递给调用者（`save()`或`okToContinue()`）。

如果文件已存在，`getFileName()`函数将询问用户是否要覆盖。这种行为可以通过将`QFileDialog::DontOverwrite`作为额外参数来更改。

```cpp
bool MainWindow::saveAs() {
	QString fileName = QFileDialog::getSaveFileName(this,
		r("保存电子表格"),".
		("("表格文件 (*.sp)"));
		if (fileName.isEmpty()) {
			return false;
		}
	return saveFile(fileName);
}
```

```cpp
void MainWindow::closeEvent(QCloseEvent *event) {
	if (okToContinue()) {
		writeSettings();
		event->accept();
	} else {
		event->ignore();
	}
}
```

当用户点击退出或窗口标题栏中的关闭按钮时，会调用`Widget::close()`槽。这向控件发送“关闭”事件。通过重写`Widget::closeEvent()`，我们可以拦截关闭主窗口尝试并决定是否关闭。

如果有未保存的更改且用户选择“取消”，我们“忽略”事件并让窗口不受影响。在正常情况下，我们接受事件，导致 Qt 隐藏窗口。我们还调用私有函数`writeSettings()`保存应用程序当前的设置。

当最后一个窗口关闭时，应用程序终止。如果需要，我们可以通过将`QApplication::quitLastWindow`属性设置为`false`来禁用此，在这种情况下，应用程序将一直运行直到我们调用`QApplication::quit()`。

```cpp
void MainWindow::setCurrentFile(const QString &fileName) {
	curFile = fileName;
	setWindowModified(false);
}
```

## 实现文件菜单

```cpp
QString shownName = tr("Untitled");
if (!curFile.isEmpty()) {
 shownName = strippedName(curFile);
recentFiles.removeAll(curFile);
recentFiles.prepend(curFile);
updateRecentFileActions();
}
```

```cpp
setWindowTitle(tr("%1[*] - %2%").arg(shownName)
             arg(tr("Spreadsheet")));
```

```cpp
QString MainWindow::strippedName(const QString &fullFileName)
{
 return QFileInfo(fullFileName).fileName();
}
```

在`setCurrentFile()`中，我们设置了存储正在编辑的文件名的曲线变量。在标题栏中显示文件名之前，我们使用`strippedName()`移除了文件的路径，使其对用户更加友好。

每个小部件（Widget）都有一个`modified`属性，如果窗口文档有未保存的更改，该属性应设置为`true`，否则设置为`false`。在 Mac OS 上，未保存的文档通过窗口标题栏底部按钮的一个点来表示；在其他平台上，它们通过文件名后的后的星号`*`来表示。Qt 会自动处理这种行为，因此我们只需要保持`modified`属性是最新的，并在需要显示星号的窗口标题中使用标记符`"*"`即可。

我们传递给`setWindowTitle()`函数的文本是：

```cpp
tr("%1[*] - %2%").arg(shownName)
.arg(tr("Spreadsheet"));
```

`QString::arg()`函数将编号最低的`%n`参数替换为其参数值并返回生成的字符串。在这种情况下，`arg()`用于两个`"%n"`参数。第一次调用`arg()`替换了`"%1"`；第二次调用替换了`"%2"`。如果文件名为`"budget.sp"`且没有加载翻译文件，生成的字符串将是`"budget.sp" - Spreadsheet`。写成下面这样会更简单：

```cpp
setWindowTitle(shownName + tr("%1[*] - Spreadsheet"));
```

但使用`arg()`为人类翻译人员提供了更大的灵活性。

如果存在文件名，我们就更新`recentFiles`，即应用程序最近打开的文件列表。我们调用`removeAll()`移除列表中任何出现的文件名以避免重复；然后调用`prepend()`将文件名作为第一项添加。更新列表后，我们调用函数`updateRecentFileActions()`来更新文件菜单中的项。

```cpp
void MainWindow::updateRecentFileActions()
{
 QMutableStringListIterator i(recentFiles);
```

# 3. 创建主窗口

```cpp
while (i.hasNext()) {
    if (!QFile::exists(i.next())) {
        i.remove();
    }
}
for (int j = 0; j < MaxRecentFiles; ++j) {
    if (j < recentFiles.count()) {
        QString text = tr("&1 %2")
            arg(j + 1)
            arg(strippedName(recentFiles[j]));
        recentFileActions[j]->setText(text);
        recentFileActions[j]->setData(recentFiles[j]);
        recentFileActions[j]->setVisible(true);
    } else {
        recentFileActions[j]->setVisible(false);
    }
}
separatorAction->setVisible(!recentFiles.isEmpty());
```

我们首先使用 Java 风格的迭代器移除任何不再的文件。某些文件可能在之前的会话中使用过，但此后已被删除。`recentFiles`变量的类型是`QStringList`（`QString`列表）。第 11 章详细解释了作为`QString`的容器类，展示了它们如何与 C++ 标准模板库 (STL) 相关，以及 Qt 的 Java 风格迭代器的用法。

![](img/930c1c6fda99d425284503ebcbc940ea_84_0.png)

图 3.11. 最近打开文件的菜单

然后我们再次遍历文件列表，这次使用一个和符号（&）、一个数字 (j + 1）、一个空格和文件名（不带路径）。对于每个文件，我们创建一个由这些部分组成的字符串。我们设置对应的动作使用此文本。例如，如果第一个文件是`C:\My Documents\tab04.sp`，则第一个动作的文本将是`"&1 tab04.sp"`。图 3.11 显示了`recentFileArray`与生成的菜单之间的对应关系。

## 实现文件菜单

每个动作都可以关联一个`QVariant`类型的“data”项。`QVariant`可以持有许多 C++ 和 Qt 类型的值；我们将在第 11 章中介绍它。在这里，将文件的完整名称存储在动作的“data”项中，以便我们以后轻松检索它。我们还设置了动作为可见。

如果文件动作比最近文件多，我们就隐藏多出的动作。最后，如果至少有一个最近的文件，我们就设置分隔符为可见。

```cpp
void MainWindow::openFile()
{
    if (okToContinue()) {
        QAction *action = qobject_cast<QAction *>(sender());
        if (action)
            loadFile(action->data().toString());
    }
}
```

当用户选择一个最近的文件时，会调用`openFile()`槽。`okToContinue()`函数用于检查是否有未保存的更改，并且在用户没有取消的情况下，我们通过`QObject::sender()`找出是哪个动作被调用。

`qobject_cast<T>()`函数在元对象系统上执行动态转换。如果对象是类型`T`，则返回指向该对象的指针，否则返回空。

## 使用对话框

在本节中，我们将解释如何使用对话框——如何创建并运行它们，以及对选择做出响应。我们将使用第 2 章创建的查找、转到单元格和排序对话框。我们还将创建一个简单的“关于”框。

我们将从 3.11 中的查找对话框开始。为了让用户能够在主窗口和查找对话框之间切换，查找对话框必须是非模态的。非模态窗口是可以独立运行的窗口。创建非模态对话框时，通常会将它们的信号连接到槽。

# 3. 创建主窗口

```cpp
void MainWindow::find()
{
  if (!findDialog) {
    findDialog = new FindDialog(this);
    connect(findDialog, SIGNAL(findNext(const QString &, Qt::CaseSensitivity)),
      spreadsheet, SLOT(findNext(const QString &, Qt::CaseSensitivity)));
    connect(findDialog, SIGNAL(findPrevious(const QString &, Qt::CaseSensitivity)),
      spreadsheet, SLOT(findPrevious(const QString &, Qt::CaseSensitivity)));
  }

  findDialog->show();
  findDialog->raise();
  findDialog->activateWindow();
}
```

查找对话框允许用户在电子表格中搜索文本。当用户点击“编辑-查找”时，会调用`find()`槽。此时，可能出现几种情况：

- 这是用户第一次调用查找对话框。

- 用户之前调用过查找对话框，但尚未关闭。

- 查找对话框之前已调用过且仍然可见。

![](img/930c1c6fda99d425284503ebcbc940ea_86_0.png)

图 3.12. 应用程序的查找对话框

如果查找对话框不存在，我们就创建它并将`findNext()`和`findPrevious()`信号连接到相应的电子表格槽。我们也可以在`MainWindow`构造函数中创建对话框，但延迟创建可以加快应用程序启动速度。此外，如果从未使用对话框，它就不会被创建，从而节省时间和内存。

然后我们调用`show()`、`raise()`和`activateWindow()`以确保窗口可见、置顶并激活。调用一次`show()`就足以让隐藏的窗口变为可见、置顶并激活，查找对话框可能在可见时被调用。在这种情况下，`show()`将不起作用，我们必须调用`raise()`和`activateWindow()`来使窗口置顶并激活。另一种写法将是

## 使用对话框

```cpp
if (findDialog->isHidden()) {
    findDialog->show();
} else {
    findDialog->raise();
    findDialog->activateWindow();
}
```

但这在编程上等同于在过单行道之前向两边看。

我们现在来看图 3.13 所示的“跳转单元格”对话框。我们希望用户弹出它、使用它并关闭它，而无法切换到应用程序中的其他窗口。这意味着“跳转单元格”对话框必须是模态的（modal）。模态窗口是在被调用时弹出并阻塞应用程序的窗口，防止在窗口关闭之前发生任何处理或交互。我们之前使用的对话框文件和消息都是模态的。

![](img/930c1c6fda99d425284503ebcbc940ea_87_0.png)

图 3.13 电子表格应用程序的“跳转单元格”对话框

如果使用`show()`调用，它就是非模态的（modeless）（除非我们事先设置了`setModal`使其变为模态）；如果使用`exec()`调用，它就是模态的。

```cpp
void mainWindow::gotoCell() {
    GoToCellDialog dialog(this);
    if (dialog.exec()) {
        QString str = dialog.lineEdit->text().toUpperCase();
        spreadsheet->setCurrentCell(str.mid(1).toInt() - 1,
        str[0].unicode() - 'A');
    }
}
```

`QDialog::exec()`函数在对话框被接受时返回真值（`QDialog::Accepted`），否则返回假值（`QDialog::Rejected`）。回想一下，我们在第 2 章中使用 Qt Designer 创建了“跳转单元格”对话框，并将 OK 连接到`accept()`，将取消连接到`reject()`。如果用户选择 OK，我们将当前单元格设置为行编辑框中的值。

`TableWidget::setCurrentCell()`函数期望：一个行索引和一个列索引。在电子表格应用程序中，A1 是单元格 (0,0)，单元格 B27 是单元格 (26,1)。要从`QLineEdit::text()`获取行索引，我们使用`QString::mid()`提取行号（它返回从起始位置到字符串结束的子字符串），使用`QString::toInt()`将其转换为整数并减去 1。对于列数，我们从字符串大写首字母的数值值减去`'A'`的数值值。我们知道字符串将具有正确的格式，因为我们为对话框创建的`QRegEvaluator`允许仅在字母后面跟最多三个数字时，OK 按钮才可用。

`goToCell()`与目前为止的代码的不同在于，它在栈上作为一个变量创建了一个控件（`GoCellDialog`）。以多写一行的代价，我们同样容易地使用`new`和`delete`：
