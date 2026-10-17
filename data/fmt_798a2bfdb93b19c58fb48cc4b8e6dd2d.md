
# 18. 国际化

让我们查看一个“呼叫中心”应用程序源代码的相关部分。该应用程序提供语言菜单……

使用“语言”菜单更改应用程序的语言。

我们设置了每个 `QAction` 的文本、状态提示，以及那些具有非标准快捷键的动作快捷键。我们还设置了每个 `QMenu` 的标题以及窗口标题。

之前介绍的 `createMenus()` 函数调用了 `createLanguageMenu()`，以便在“语言”菜单中填充语言列表：

### 代码视图

```cpp
void MainWindow::createLanguageMenu()
{
  languageMenu = new QMenu(this);
  languageActionGroup = new QActionGroup(this);
  connect(languageActionGroup, SIGNAL(triggered(QAction *)),
          *this, SLOT(switchLanguage(QAction *)));
  QDir qmDir = directoryOf("translations");
  QStringList fileNames =
      qmDir.entryList(QStringList("callcenter_*.qm"));

  for (int i = 0; i < fileNames.size(); ++i) {
    QString locale = fileNames[i];
    locale.remove(0, locale.indexOf('_') + 1);
    locale.chop(3);

    QTranslator translator;
    translator.load(fileNames[i], qmDir.absolutePath());
    QString language = translator.translate("MainWindow",
                                          "English");
    QAction *action = new QAction(tr("&%1 %2")
                                     .arg(i + 1).arg(language), this);
    action->setCheckable(true);
    action->setData(locale);
    languageMenu->addAction(action);
    languageActionGroup->addAction(action);
    if (language == "English")
      action->setChecked(true);
  }
}
```

我们并没有硬编码应用程序支持的语言，而是为应用程序 `translations` 目录下的每个 `.qm` 文件创建一个菜单条目。

`directoryOf()` 函数与我们在第 17 章（第 410 页）使用的函数相同。

为了简单起见，我们假设英语也有一个 `.qm` 文件。另一种方案是在用户选择英语时对 `QTranslator` 对象调用 `clear()`。

一个特别的困难之处在于为每个 `.qm` 文件提供的语言呈现一个良好的名称。仅根据 `.qm` 文件名将“English”显示为“en”或将“Deutsch”显示为“de”看起来很粗糙，并且会误导某些用户。`createLanguageMenu()` 中使用的解决方案是检查“MainWindow”上下文中字符串“English”的翻译。该字符串在德语翻译中应被翻译为“Deutsch”，在法语翻译中翻译为“Français”，在日语翻译中应翻译为“日本語（此处原文截断）”。

![图片](img/1bc72df8c60cf85926d3aefcc273027d_700_0.png)

我们为每种语言创建一个可勾选的 `QAction`，并将区域设置名称（locale name）存储在动作的 `data` 项中。我们将它们添加到 `QActionGroup` 对象中，以确保一次只有一个语言菜单项被选中。当用户从组中选择一个动作时，`QActionGroup` 会发出 `triggered(QAction *)` 信号，该信号连接到 `switchLanguage()`。

```cpp
void MainWindow::switchLanguage(QAction *action)
{
  QString locale = action->data().toString();
  QString qmPath = directoryOf("translations").absolutePath();
  appTranslator.load("callcenter_" + locale, qmPath);
  qtTranslator.load("qt_" + locale, qmPath);
  retranslateUi();
}
```

当用户从“语言”菜单选择一种语言时，会调用 `switchLanguage()` 槽。我们加载应用程序和 Qt 的相关翻译文件，并调用 `retranslateUi()` 来重新翻译主窗口的所有字符串。

在 Windows 上，提供“语言”菜单的替代方案是响应 `LocaleChange` 事件，这是 Qt 在检测到环境区域设置发生变化时发出的一种事件类型。该事件类型存在 Qt 支持的所有平台上，但只有在 Windows 上，当用户更改系统区域设置（在控制面板的“区域和语言”选项中）时才会实际生成。为了处理 `LocaleChange` 事件，我们可以如下重实现 `QWidget::changeEvent()`：

```cpp
void MainWindow::changeEvent(QEvent *event)
{
  if (event->type() == QEvent::LocaleChange) {
    QString qmPath = directoryOf("translations").absolutePath();
    appTranslator.load("callcenter_"
                       + QLocale::system().name(), qmPath);
    qtTranslator.load("qt_" + QLocale::system().name(), qmPath);
    retranslateUi();
  }
  QMainWindow::changeEvent(event);
}
```

如果用户在应用程序运行时切换了区域设置，我们将尝试为新的区域设置加载正确的翻译文件并调用 `retranslateUi()` 更新用户界面。在所有情况下，我们都会将事件传递给基类的 `changeEvent()` 函数，因为基类可能也对 `LocaleChange` 或其他更改事件感兴趣。

我们现在完成了对 `MainWindow` 代码的审查。接下来，我们将查看应用程序部件类之一——`JournalView` 类的代码，看看需要哪些更改来使其支持动态翻译。

```cpp
JournalView::JournalView(QWidget *parent)
 : QTableWidget(parent)
{
  ...
  retranslateUi();
}
```

`JournalView` 类是 `QTableWidget` 的子类。在构造函数的末尾，我们调用了 `retranslateUi()`。

`retranslateUi()` 函数更新新翻译的列头，完成手写部件的翻译相关代码。对于使用 Qt Designer 开发的部件和对话框，`uic` 工具会自动生成一个类似于 `retranslateUi()` 的函数，该函数在响应 `LocaleChange` 时被自动调用。

```cpp
void JournalView::changeEvent(QEvent *event)
{
  if (event->type() == QEvent::LocaleChange) {
    retranslateUi();
  }
  QTableWidget::changeEvent(event);
}
```

如果用户在应用程序运行时切换区域设置，我们将尝试为新的区域设置加载正确的翻译文件并调用 `retranslateUi()` 更新用户界面。这与我们在 `MainWindow` 中的做法类似。

```cpp
void JournalView::retranslateUi()
{
  QStringList labels;
  labels << tr("Time") << tr("Priority") << tr("Phone Number")
         << tr("Subject");
  setHorizontalHeaderLabels(labels);
}
```

### 翻译应用程序

翻译包含 `tr()` 用的应用程序是一个三步过程：

1. 运行 `lupdate` 从应用程序代码中提取所有用户可见的字符串。
2. 使用 Qt Linguist 翻译应用程序。
3. 运行 `lrelease` 生成 `QTranslator` 可以加载的二进制 `.qm` 文件。

步骤 1 和 3 由开发人员执行。步骤 2 由翻译人员处理。此循环可以在应用程序开发和生命周期内反复进行。

作为一个示例，我们将展示如何翻译第 3 章中的 `Spreadsheet` 应用程序。

首先，我们必须稍微修改应用程序的 `.pro` 文件以指定我们要支持的语言。例如，如果我们除英语外还支持德语和法语，可以在 `spreadsheet.pro` 中添加以下 `TRANSLATIONS`：

```pro
TRANSLATIONS = spreadsheet_de.ts \
               spreadsheet_fr.ts
```

在这里，我们指定了两个翻译文件：一个德语和一个法语。这些文件会在第一次运行 `lupdate` 时创建，并在后续每次运行 `lupdate` 时进行更新。

假设我们位于 Spreadsheet 应用程序源码目录，从命令行对 `spreadsheet.pro` 运行 `lupdate` 如下：

```bash
lupdate -verbose spreadsheet.pro
```

`-verbose` 选项告诉 `lupdate` 提供比通常更多的反馈。以下是预期的输出：

```text
Updating 'spreadsheet_de.ts'...
  找到 98 个源文本（98 个新的，0 个已存在）

Updating 'spreadsheet_fr.ts'...
  找到 98 个源文本（98 个新的，0 个已存在）
```

应用程序源代码中任何出现在 `tr()` 调用中的字符串都将存储在 `.ts` 文件中，并带有一个空翻译。出现在应用程序的 `.ui` 文件中的字符串也会被包含在内。

`lupdate` 工具默认假设 `tr()` 的参数是 Latin-1 字符串。如果情况并非如此，我们必须在 `.pro` 文件中添加 `CODECFORTR` 条目。例如：

```pro
CODECFORTR = EUC-JP
```

这必须在应用程序的 `main()` 函数中调用 `QTextCodec::setCodecForTr()` 之外完成。

然后需要使用 Qt Linguist 向 `spreadsheet_de.ts` 和 `spreadsheet_fr.ts` 文件中添加翻译。（图 18.2 显示了 Qt Linguist 的用法。）

**图 18.2. Qt Linguist 的用法**

[查看全尺寸图像]

![图片](img/1bc72df8c60cf85926d3aefcc273027d_705_0.png)

要运行 Qt Linguist，在 Windows 的启动菜单中点击 Qt by Trolltech v4.x.y|Linguist，在 Unix 命令行中输入 `linguist`，或在 Mac OS X 访达中双击 `Linguist`。要开始向 `.ts` 文件添加翻译，点击 `File|Open` 并选择要翻译的文件。

Qt Linguist 主窗口的左侧显示树视图。顶层项目是正在翻译的应用程序的上下文。对于 `Spreadsheet` 应用程序，这些项目是 `"FindDialog"`、`"GoToCellDialog"`、`"MainWindow"`、`"SortDialog"` 和 `"Spreadsheet"`。每个上下文都有零或多个子项。每个子项占据三列，第一列显示完成（Done）标志，第二列显示源文本，第三列显示任何翻译。右上角区域显示当前源文本及其翻译；这里是添加和编辑翻译的地方。右下角区域是 Qt Linguist 自动提供的建议列表。

一旦我们有了翻译好的 `.ts` 文件，我们需要将其转换为二进制 `.qm` 文件以便 `QTranslator` 使用。要在 Qt Linguist 内部执行此操作，点击 `File|Release`。通常，我们首先只翻译几个字符串，并使用 `.qm` 文件运行应用程序，以确保一切正常工作。

如果我们想为所有 `.ts` 文件重新生成 `.qm` 文件，可以如下使用 `lrelease` 工具：

```bash
lrelease -verbose spreadsheet.pro
```

假设我们将 19 个字符串翻译成了法语，并点击了其中 17 个的完成标志，`lrelease` 会产生以下输出：

```text
Updating 'spreadsheet_de.qm'...
  生成 0 个翻译（0 个完成，0 个未完成）
  忽略 98 个未翻译的源文本

Updating 'spreadsheet_fr.qm'...
  生成 19 个翻译（17 个完成，2 个未完成）
  忽略 79 个未翻译的源文本
```

运行应用程序时，未翻译的字符串将以原始语言显示。`lrelease` 会忽略完成标志；它可以供翻译人员识别哪些翻译已完成，哪些必须重新审视。

当我们修改应用程序的源代码时，翻译文件可能会过时。解决方案是再次运行 `lupdate`，为新字符串提供翻译，并重新生成 `.qm` 文件。一些开发团队发现频繁运行 `lupdate` 很有用，而另一些则倾向于等到应用程序几乎发布。

`lupdate` 和 Qt Linguist 工具非常智能。不再使用的翻译将保留在 `.ts` 文件中，以防在后的发布中需要。在更新 `.ts` 文件时，`lupdate` 使用一种智能合并算法，可以为翻译人员处理不同上下文中相同或相似的文本节省大量时间。

关于 Qt Linguist、`lupdate` 和 `lrelease` 的更多信息，请参阅 [http://doc.trolltech.com/4.3/linguist-manual.html](http://doc.trolltech.com/4.3/linguist-manual.html) 上的 Qt Linguist 手册。手册包含了对 Qt Linguist 用户界面的完整解释以及面向程序员的逐步教程。

# 19. 外观与外观自定义

![图片](img/1bc72df8c60cf85926d3aefcc273027d_707_0.png)

## 使用 Qt 样式表 (Qt Style Sheets)

派生 `QStyle`

在某些情况下，我们可能想要更改 Qt 内置控件的外观特征。我们可能只想进行一些微小的自定义以稍稍调整美感，或者我们可能希望实现一种全新的样式，为我们的应用程序或系列应用程序提供独特且别的外观。在这两种情况下，重新定义 Qt 内置控件外观种主要方法：

- 我们可以对单个控件类进行派生，并重新实现它们的绘制和鼠标事件处理程序。这提供了完全的控制，但涉及大量工作。这也意味着我们必须遍历所有的代码和 Qt Designer 表单，将所有 Qt 控件类的出现更改为使用我们的派生类。
- 我们可以派生 `QStyle` 或预定义的样式（如 `QStyle`）。这种方法非常强大；被不同的平台使用。

从 Qt 4.2 开始，我们可以使用样式表，它的灵感来自 CSS（级联样式表）。由于样式表是纯文本，它们比调整调色板（`palette`）提供了更可靠的结果。例如，`QWindowsStyle` 使用 `Base` 条目来填充。

### 使用样式表

![图片](img/1bc72df8c60cf85926d3aefcc273027d_708_0.png)

调色板。相比之下，样式表保证无论激活何种样式，指定的颜色都会被使用。

`QApplication::setStyleSheet()` 为整个应用程序设置样式表：

```cpp
qApp->setStyleSheet("QLineEdit { background-color: yellow; }");
```

我们也可以使用 `QWidget::setStyleSheet()` 为控件及其子设置样式表。例如：

```cpp
dialog->setStyleSheet("QLineEdit { background-color: yellow; }");
```

如果我们直接在 `QLineEdit` 上设置样式表，可以省略 `QLineEdit` 选择器和大括号：

```cpp
lineEdit->setStyleSheet("background-color: yellow;");
```

到为止，我们只为单个控件类设置了单个属性。在实践中，样式规则经常组合使用。例如，以下规则设置了六个控件类及其子类的前景色和背景色：

```css
QCheckBox, QComboBox, QLineEdit, QListView, QRadioButton, QSpinBox {
    color: #050505;
    background-color: yellow;
}
```

颜色可以通过名称指定、以 `#RRGGBB` 格式的 HTML 风格字符串指定，或者通过 RGB 或 RGBA 值指定：

```css
QLineEdit {
    color: rgb(0, 88, 152);
    background-color: rgba(97%, 80%, 9%, 50%);
}
```
