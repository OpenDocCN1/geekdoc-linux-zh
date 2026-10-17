
注意 `setSalary()` 槽是如何实现的。只有当 `newSalary != mySalary` 时，我们才发射 `salaryChanged()` 信号。

## 快速对话框设计

程序员完全通过编写源代码来开发整个应用程序并不罕见。尽管如此，许多程序员更倾向于使用可视化方法设计表单，因为他们觉得这样更自然、更快速，并且希望快速方便地尝试设计。

`Qt Designer` 通过提供可视化设计能力扩展了程序员的选项。可以使用 `Qt Designer` 开发应用程序的所有或大部分表单。使用 `Qt Designer` 创建的表单最终变为 C++ 代码，因此 `Qt Designer` 可以配合传统的工具链使用，且对编译器没有特殊要求。

在本节中，我们将使用 `Qt Designer` 创建如图 2.4 所示的跳转单元对话框。无论是在代码中还是在 `Qt Designer` 中进行，创建对话框始终涉及相同的根本步骤：

- 创建并初始化子小部件。
- 将子小部件放入布局。
- 设置 Tab 顺序。
- 建立信号-槽连接。
- 实现对话框的自定义槽。

![](img/930c1c6fda99d425284503eb940ea_45_0.png)

**图 2.4.** 跳转单元对话框

要启动 `Qt Designer`，在 Windows 的开始菜单中点击 `Qt by Trolltech v4.x|Designer`，在 Unix 命令行输入 `designer`，或在 Mac OS Finder 中双击 `Designer`。

默认情况下，`Qt Designer` 的用户界面由多个顶级窗口组成。如果你更倾向于 MDI 风格的界面（即一个顶级窗口和多个子窗口，如图 2.5 所示），请点击 `Edit|Preferences` 并将界面模式设置为停靠窗口（Docked Window）。

# 2. 创建对话框

![](img/930c1c6fda99d425284503ebcbc940ea_46_0.png)

图 2.5 Windows Vista 上停靠模式下的 `Qt Designer`

第一步是创建子控件并将它们放置在表单上。创建一个标签（label）、一个行编辑器（line editor）、一个水平间隙（horizontal spacer）和两个按钮（push buttons）。对于每个项目，从 `Qt Designer` 的控件框中拖动其名称或图标，将其释放到表单大致的位置。间隙项目在最终表单中是不可见的，在 `Qt Designer` 中显示为蓝色弹簧形状。

现在向上拖动表单的底部使其变短。这应该产生一个与图 2.6 类似的表单。不要在表单物品的定位上花费太多时间；Qt 的布局管理器稍后会精确地布置它们。

![](img/930c1c6fda99d425284503ebcbc940ea_46_1.png)

图 2.6 带有某些控件的表单

使用 `Qt Designer` 的属性编辑器设置每个控件的属性：

1. 点击文本标签。确保其 `objectName` 属性为“label”，并将 `text` 属性设置为“&Cell Location:”。
2. 点击行编辑器。确保其 `objectName` 属性为“lineEdit”。
3. 点击第一个按钮。将 `objectName` 属性设置为 "okButton"，`enabled` 属性设置为 "false"，`text` 属性设置为 "OK"，并将 `default` 属性设置为 "true"。
4. 点击第二个按钮。将 `objectName` 属性设置为 "cancelButton" 并将 `text` 属性设置为 "Cancel"。
5. 点击表单，现在看起来没问题了，但显示 &Cell Location 的文本标签除外。点击 `Edit|Edit Buddies` 进入一个允许设置伙伴（buddies）的特殊模式。接下来，点击（标签）并将红色箭头线拖到行编辑器上，然后释放。标签现在应该显示为 Cell Location，如图 2.7 所示，并以行编辑器作为其伙伴。点击 `Edit|Edit Widgets` 退出伙伴模式。

![](img/930c1c6fda99d425284503ebcbc940ea_47_0.png)

**图 2.7.** 设置了属性的表单

下一步是在表单上布局控件：

1. 点击 Cell Location 标签，并在点击其旁边的行编辑器时按住 Shift 键，以便它们同时被选中。点击 `Form|Lay Out Horizontally`。
2. 点击间隙，然后在按住 Shift 时点击表单的 OK 和 Cancel 按钮。点击 `Form|Lay Out Horizontally`。
3. 点击表单背景以取消所有选中项，然后点击 `Form|Lay Out Vertically`。
4. 点击 `Form|Adjust Size` 将表单调整为其所需尺寸。

表单上出现的红线显示了已创建的布局，如图 2.8 所示。它们在表单运行时不会出现。

![](img/930c1c6fda99d425284503ebcbc940ea_47_1.png)

**图 2.8.** 带有布局的表单

# 2. 创建对话框

现在点击 `Edit|Edit Tab Order`。每个可以接受焦点的控件旁边都会出现一个蓝色框中的数字，如图 2.9 所示。按照你希望它们接受焦点的顺序点击每个控件，然后点击 `Edit|Edit Widgets` 退出标签顺序模式。

![](img/930c1c6fda99d425284503ebcbc940ea_48_0.png)

图 2.9. 设置表单的标签顺序

要预览对话框，点击 `Form|Preview` 菜单选项。反复按 Tab 键检查标签顺序。使用标题栏中的关闭按钮关闭对话框。

将对话框保存为 `gotocelldialog.ui` 并放入名为 `gotocell` 的目录，并在同一目录下使用纯文本编辑器创建一个 `main.cpp` 文件：

```cpp
#include <QApplication>
#include <QDialog>
#include "ui_gotocelldialog.h"

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    Ui::GoToCellDialog ui;
    QDialog *dialog = new QDialog;
    ui.setup(dialog);
    dialog->show();
    return app.exec();
}
```

现在运行 `qmake` 来创建 .pro 文件和 Makefile (`qmake -project; qmake gotocell`)。`qmake` 工具足够智能检测用户界面文件 `gotocell-dialog.ui` 并生成相应的 Makefile 规则来调用 `ui`（Qt 的用户界面编译器）。`uic` 工具将 `gotocelldialog.ui` 转换为 C++ 并结果放在 `ui_gotocelldialog.h` 中。

生成的 `gotocelldialog.h` 文件包含了 `Ui::GoToCellDialog` 类的定义，它是 `gotocelldialog.ui` 文件的 C++ 等效文件。该类声明了存储表单子控件和布局的成员变量，以及一个初始化表单的 `setupUI()` 函数。生成的类如下：

```cpp
class Ui::GoToCellDialog {
public:
    QLabel *label;
    QLineEdit *lineEdit;
    QSpacerItem *spacer;
    QPushButton *okButton;
    QPushButton *cancelButton;
    void setupUI(QWidget *widget);
};
```

```cpp
void Ui::GoToCellDialog::setupUi(QWidget *widget) {
    QWidget *centralwidget = new QWidget(widget);
    QVBoxLayout *mainLayout = new QVBoxLayout(centralwidget);

    label = new QLabel("&Cell Location:", centralwidget);
    lineEdit = new QLineEdit(centralwidget);
    spacer = new QSpacerItem();
    okButton = new QPushButton("OK", centralwidget);
    okButton->setEnabled(false);
    cancelButton = new QPushButton("Cancel", centralwidget);

    QHBoxLayout *hLayout = new QHBoxLayout();
    hLayout->addWidget(label);
    hLayout->addWidget(lineEdit);
    hLayout->add(spacer);
    hLayout->addWidget(okButton);
    hLayout->addWidget(cancelButton);

    mainLayout->addLayout(hLayout);
    widget->setLayout(mainLayout);
}
```

## 快速对话框设计 29

对于部件，父级具有额外的含义：子部件显示在父部件的区域内。当我们删除父级部件时，子部件不仅会从内存中消失，还会从屏幕上消失。

在构造函数的结束处，我们将 OK 按钮连接到 `QDialog` 的 `accept()` 槽，并将取消按钮连接到 `reject()` 槽。这两个槽都会关闭对话框，`accept()` 将对话框的结果值设置为 `QDialog::Accepted`（等于 1），而 `reject()` 将结果设置为 `QDialog::Rejected`（等于 0）。当我们使用这个对话框时，可以使用该结果来判断用户是否点击了 OK 并采取相应的操作。

在 `lineEdit::textChanged()` 槽中，我们根据行编辑器是否包含有效单元格来启用或禁用 OK 按钮。`QLineEdit::hasAcceptableInput()` 使用我们在构造函数中设置的验证器。

对话框到此完成。现在我们可以重写 `main.cpp` 来使用它：

```cpp
#include <QApplication>
#include "gotocelldialog.h"

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);
    GoToCellDialog *dialog = new GoToCellDialog;
    dialog->show();
    return app.exec();
}
```

使用 `qmake -project` 重新 `gotocell.pro`（因为我们向项目添加了源文件），运行 `qmake gotocell.pro` 更新 Makefile，然后重新编译并运行应用程序。在行编辑器中输入“A12”，注意到 OK 按钮变为可用。尝试输入一些随机文本以查看验证器是如何工作的。点击取消关闭对话框。

对话框工作正常，但对于 Mac OS X 用户来说，按钮的顺序是反的。我们需要单独添加每个按钮以展示是如何操作的，但实际上我们应该使用 `QButtonBox`，它是一个包含按钮的部件，并能指定按照应用程序运行的窗口系统的正确方式来展示它们，如图 2.10 所示。

为了让对话框使用 `QPushButton`，我们必须同时更改设计和代码。在 `Qt Designer` 中，只需四个步骤：

1. 点击表单（而不是任何部件或布局），然后点击 `Form|Break Layout`（表单|打破布局）。
2. 点击并删除 OK 按钮、取消按钮、水平间距器以及（现在为空的）水平布局。
3. 将一个“Button Box”拖到表单上，位于单元格位置标签和行编辑器下方。
4. 点击表单，然后点击 `Form|Lay Out Vertically`（表单|垂直布局）。

## 30 2. 创建对话框

如果我们只是进行设计上的更改，例如更改对话框的布局和部件属性，我们可以简单地重新构建应用程序。但在这里我们删除了一些部件并添加了一个新部件，在这种情况下我们通常也必须更改代码。

我们必须做的更改都在 `gotocelldialog.cpp` 文件中。这是构造函数的新版本：

```cpp
GoToCellDialog::GoToCellDialog(QWidget *parent)
    : QDialog(parent)
{
    setupUi(this);
    buttonBox->button(QDialogButton::OK)->setEnabled(false);
    QRegExp regExp("[A-Za-z][1-9][0-9]*");
    lineEdit->setValidator(new QRegExpValidator(regExp, this));
    connect(buttonBox, SIGNAL(accepted()), this, SLOT(accept()));
    connect(buttonBox, SIGNAL(rejected()), this, SLOT(reject()));
}
```

在之前的版本中，我们最初在 `Qt Designer` 中禁用了 OK 按钮。对于 `QDialogButtonBox` 我们无法这样做，因此我们在代码中调用 `setupUI()` 后立即禁用。`QDialogButtonBox` 类有一个标准按钮枚举，我们可以利用它来访问特定按钮，在本例中使用 OK 按钮。

![](img/930c1c6fda99d425284503ebcbc940ea_52_0.png)

图 2.10. Windows 和 Mac OS X 上的跳转单元格对话框

非常方便，`Qt Designer` 对 `QDialogButtonBox` 的默认名称是 `buttonBox`。两个连接都是从按钮发出的，而不是按钮本身。当点击具有 `AcceptRole` 的按钮时，会发射 `accepted()` 信号，而具有 `RejectRole` 的按钮主要会发射 `rejected()` 信号。默认情况下，标准的 `QDialogButtonBox::OK` 按钮具有 `AcceptRole`，而 `QDialogButtonBox::Cancel` 按钮具有 `RejectRole`。

```cpp
void GoToCellDialog::on_lineEdit_textChanged()
{
    buttonBox->button(QDialogButtonBox::OK)->setEnabled(
        lineEdit->hasAcceptableInput());
}
```
