
```cpp
showGridAction = new QAction(tr("&Show Grid"), this);
showGridAction->setChecked(true);
showGridAction->setChecked(spreadsheet->showGrid());
showGridAction->setStatusTip(tr("Show or hide the spreadsheet-grid"));

connect(showGridAction, SIGNAL (oggled(bool)),
       spreadsheet, SLOT(showGrid(bool)));
```

显示网格是一个可点击的动作。它在菜单中以带复选框的形式渲染，并在工具栏中实现为切换按钮。当动作开启时，电子表格组件会显示网格。我们使用表格组件的默认值初始化该动作，以便它们在启动时保持同步。然后，我们将显示网格动作的 `oggled(bool)` 信号连接到表格组件的 `setGrid(bool)` 槽函数，后者继承自 `QTableWidget`。一旦此动作添加到菜单或工具栏中，用户就可以切换网格的开启和关闭。

显示网格和自动重新计算（Auto-Recalculate）动作是独立的可点击动作。Qt 支持通过动作组（Action group）实现互斥动作。

```cpp
aboutQtAction = new QAction(tr("About &Qt"), this);
aboutQtAction->setStatusTip(tr("Show the Qt library's About box"));
```

## 3. 创建主窗口

```cpp
connect(aboutQtAction, SIGNAL (triggered()), qApp, SLOT (aboutQt()));
}
```

对于关于 Qt 的动作，我们使用 `QApplication` 对象的 `aboutQt()` 槽函数，可以通过全局变量 `qApp` 访问。

![](img/34bd675de80edd220dc2d53b429caf78_67_0.png)

图 3.4 关于 Qt

现在我们已经创建了动作，可以构建包含这些动作的菜单系统了：

```cpp
void MainWindow::createMenus()
{
    fileMenu = menuBar()->addMenu(tr("&File"));
    fileMenu->addAction(newAction);
    fileMenu->addAction(openAction);
    fileMenu->addAction(saveAction);
    separator = fileMenu->addSeparator();
    for (int i = 0; i < MaxRecentFiles; ++i)
        fileMenu->addAction(recentFileActions[i]);
    fileMenu->addSeparator();
    fileMenu->addAction(exitAction);
}
```

在 Qt 中，菜单是 `QMenu` 的实例。`addMenu()` 函数创建一个带有指定文本的 `QMenu` 控件并将其添加到菜单栏。`MainWindow::menuBar()` 返回 `QMenuBar` 的指针。菜单栏在第一次调用 `menuBar()` 时创建。

我们首先创建文件菜单，然后将新建、打开、保存和另存为动作添加到其中。插入一个分隔符在视觉上对相关项分组。我们使用循环从 `recentFileActions` 数组中添加（初始隐藏的）动作，然后在最后添加退出动作。

我们保留了其中一个分隔符的指针。这将允许我们隐藏分隔符（如果没有最近文件）或显示它，因为我们不希望两个分隔符之间什么都没有。

```cpp
editMenu = menuBar()->addMenu(tr("&Edit"));
editMenu->addAction(cutAction);
editMenu->addAction(copyAction);
```

## 创建菜单和工具栏

```cpp
editMenu->addAction(pasteAction);
editMenu->addAction(deleteAction);
```

```cpp
selectSubMenu = editMenu->addMenu(tr("Select"));
selectSubMenu->addAction(selectRowAction);
selectSubMenu->addAction(selectColumn);
selectSubMenu->addAction(selectAllAction);
```

```cpp
editMenu->addSeparator();
editMenu->addAction(findAction);
editMenu->addAction(gotoCellAction);
```

现在我们创建编辑菜单，像之前处理文件菜单一样使用 `QMenu::addAction` 添加动作，并在我们希望出现的位置使用 `QMenu::menu()` 添加子菜单。子菜单像它所属的菜单一样也是一个 `QMenu`。

```cpp
toolsMenu = menuBar()->addMenu(tr("Tools"));
toolsMenu->addAction(calculateAction);
toolsMenu->addAction(sortAction);
```

```cpp
optionsMenu = menuBar()->addMenu(tr("Options"));
optionsMenu->addAction(showGridAction);
optionsMenu->addAction(autoRecalculate);
```

```cpp
menuBar()->addSeparator();

helpMenu = menuBar()->addMenu(tr("Help"));
helpMenu->addAction(aboutAction);
helpMenu->addAction(aboutQtAction);
}
```

## 3. 创建主窗口

![](img/34bd675de80edd220dc2d53b429caf78_69_0.png)

图 3.5 Qt 样式下的菜单栏

![](img/34bd675de80edd220dc2d53b429caf78_69_1.png)

图 3.6 电子表格的工具栏

## 设置状态栏

当菜单和工具栏完成后，我们准备好处理状态栏了。

```cpp
void MainWindow::createStatusBar()
{
    locationLabel = new QLabel("");
    locationLabel->setAlignment(Qt::AlignCenter);
    locationLabel->setMinimumSize(locationLabel->sizeHint());

    formulaLabel = new QLabel();
    formulaLabel->setIndent(3);

    statusBar()->addWidget(locationLabel);
    statusBar()->addWidget(formulaLabel, 1);

    connect(spreadsheet, SIGNAL(currentChanged(int, int, int, int)),
           this, SLOT(updateStatusBar()));
    connect(spreadsheet, SIGNAL(modified())),
           this, SLOT(spreadsheetModified()));

    updateStatusBar();
}
```

在正常状态下，状态栏包含两个指示器：当前单元格的位置和当前单元格的公式。状态栏也用于显示状态提示或临时消息。

| | |

|---|---|

| 正常 | =A1+A2 |

| 打开现有电子表格文件 | |

| 状态提示 | |

| 文件保存 | |

| 临时消息 | |

图 3.7 电子表格状态栏

图 3.8 显示两个标签具有不同的需求。单元格位置指示器需要的很少，当窗口调整大时，任何额外空间都应该给右侧的公式标签。这是通过在公式标签的 `QStatusBar::addWidget()` 调用中指定拉伸因子为1来实现。位置指示器具有默认的拉伸因子0，意味着它倾向于不被拉伸。

当 `QStatusBar` 布局控件时，它尝试尊重由 `Q::sizeHint()` 给出的每个控件的理想大小，然后拉伸可拉伸控件以填充可用空间。控件的理想大小本身取决于控件的内容，并随着内容的改变而变化。为了避免位置指示器频繁调整大小，我们将其最小宽度设为足够宽

## 54 3. 创建主窗口

为了包含尽可能长的文本 ("W999")

在函数末尾，我们将 `spreadsheet->signals` 的两个信号连接到 `MainWindow` 的两个槽：`updateStatusBar()` 和 `spreadsheetModified()`。

```cpp
void MainWindow::updateStatusBar()
{
    labelText->setText(spreadsheet->currentLocation());
    formulaLabel->setText(spreadsheet->currentFormula());
}
```

`updateStatusBar()` 槽更新单元格位置和单元格公式指示器。它在用户将单元格指针移动到新单元格时被调用。该槽在 `createStatusBar()` 结束作为普通函数使用，用于初始化指示器。这是必要的，因为 Spreadsheet 在启动时不会发出 `currentCellChanged()` 信号。

```cpp
void MainWindow::spreadsheetModified()
{
    setWindowModified(true);
    updateStatusBar();
}
```

`spreadsheetModified()` 槽将 `modified` 属性设置为 true，从而更新标题栏。该函数还更新了位置和公式指示器，以便它们反映当前状态。

## 实现文件菜单

在本节中，我们将实现必要的槽和私有函数，以使“文件”菜单选项能够工作并管理最近打开的文件列表。

```cpp
void MainWindow::newFile()
{
    if (okToContinue()) {
        spreadsheet->clear();
        setCurrentFile("");
    }
}
```

当用户点击“文件|新建”菜单选项或点击“新建”工具栏时，会调用 `newFile()` 槽。如果有未保存的更改，私有函数 `okToContinue()` 会询问用户“您要保存更改吗？”如果用户选择“是”或“否”（选择“是”时保存文档），它返回 true；如果用户选择“取消”，则返回 false。`Spreadsheet::clear()` 函数清除表格所有的单元格和公式。`setCurrentFile()` 私有函数更新窗口标题，指示正在编辑一个未命文档，同时设置 `curFile` 私有变量并更新最近打开的文件列表。

## 实现文件菜单

![](img/34bd675de80edd220dc2d53b429caf78_72_0.png)

**图 3.9. 您要保存更改吗？**

```cpp
bool MainWindow::okToContinue()
{
    if (isWindowModified()) {
        int r = QMessageBox::warning(this, tr("$spreadsheet"),
            tr("文档已修改过。\n")
            tr("您要保存更改吗？"),
            QMessageBox::Yes | QMessageBox::Default,
            QMessageBox::No,
            QMessageBox::Cancel | QMessageBox::Escape);
        if (r == QMessageBox::Yes)
            return save();
        else if (r == QMessageBox::Cancel)
            return false;
    }
    return true;
}
```

在 `okToContinue()` 中，我们检查 `windowModified` 属性的状态。如果为 true，我们显示图 3.9 所示的消息框。该消息框有“是”、“否”和“取消”按钮。`QMessageBox::Default` 修饰符使“是”成为默认按钮。`QMessageBox::Escape` 修饰符使 Esc 键成为“取消”的同义词。

调用 `warning()` 看起来可能有点吓人，但通用语法非常直观：

```cpp
QMessageBox::warning(parent, title, message, button0, button1, ...);
```

QMessageBox 还提供了 `information()`、`question()` 和 `critical()`，每个都有自己特定的图标。

![](img/34bd675de80edd220dc2d53b429caf78_72_1.png)

**图 3.10. 消息框图标**

```cpp
void MainWindow::open()
{
    if (okToContinue())
}
```

## 3. 创建主窗口

```cpp
QString fileName = QFileDialog::getFileName(
    tr("打开表格"),
    tr("表格文件 (*.sp)"));

if (!fileName.isEmpty()) {
    loadFile(fileName);
}
```

`open()` 槽对应于“文件|打开”。`newFile()` 首先调用 `okToContinue` 来处理任何未使用的更改。它使用静态便利函数 `QFileDialog::getFileName()` 从用户处获取新文件名。该函数会弹出一个文件对话框，允许用户选择文件，如果用户点击“取消”，则返回文件名或空字符串。

`QFileDialog::getFileName()` 的第一个参数是父部件。父子关系在对话框中的含义与其他部件并不相同。对话框始终在自己的窗口中，但如果它有一个父部件，默认情况下会居中位于父部件上方。对话框还共享父部件的任务栏条目。

第二个参数是选择使用的对话框。第三个参数告诉它应该从哪个目录开始，在我们的案例中是当前目录。

第四个参数指定文件过滤器。文件过滤器由文本和通配符模式组成。如果我们除了 Spreadsheet 原生格式外还支持逗号分隔值文件和 Lotus 1-2-3 文件，我们将使用以下代码：

```cpp
tr("表格文件 (*.sp)\n"
"逗号分隔值文件 (*.csv)\n"
"Lotus 1-2-3 文件 (*.wk1, *.wks)")
```

`loadFile()` 私有函数在 `open()` 中调用以加载文件。我们将其作为一个独立函数，因为我们需要加载最近打开的文件的功能。

```cpp
bool MainWindow::loadFile(const QString &fileName) {
    if (!spreadsheet->readFile(fileName)) {
        statusBar()->showMessage(tr("加载文件失败"));
        return false;
    }
    return true;
}
```

## 实现文件菜单

保持 `windowModified` 属性更新，并在窗口标题中放置标记“****”，这样在需要时星号就会出现在该处。

我们传递给 `setWindowTitle()` 函数的文本是：

```cpp
tr("%1[*] - %2").arg(showName)
.arg("Spreadsheet")
```

`QString::arg()` 将编号最低的 "%n" 参数替换为其参数值，并返回生成的字符串。在这种情况下，`arg()` 被用于处理两个 "%1"，第二次调用替换了 "%2"。如果文件名为 "budget.sp" 且没有加载翻译文件，生成的字符串将是 "budget.sp* - Spreadsheet"。虽然写成这样会更简单：

```cpp
setWindowTitle(showName + tr("[*] - Spreadsheet"));
```

但使用 `arg()` 为翻译人员提供了灵活性。

如果存在文件名，我们使用 `recentFiles()`，即应用程序最近打开的文件列表。我们使用 `removeAll()` 移除列表中出现的任何文件名以避免重复；然后使用 `prepend()` 将文件名作为第一项添加。更新列表后，我们调用私有函数 `updateRecentFileActions()` 来更新文件菜单中的条目。
