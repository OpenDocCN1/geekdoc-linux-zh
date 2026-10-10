
第一个参数是按钮标签的文本，第二个是父级控件，最后一个是 Qt 内部使用的按钮名称。

`parent`参数是所有 `QWidget`共有的，父级控件控制它的何时显示和销毁。将 `NULL`作为父级参数表示该控件是顶级的，并创建一个空白窗口来包含它。在我们的示例中，我们通过此传递了当前的窗口对象，这会将按钮添加到 `QPushButton`的主区域中。

`name`参数设置了 Qt 内部使用的控件名称。如果 Qt 遇到错误，将在错误消息中打印该控件，因此选择合适的名称是一个好主意，这在调试时是一个巨大的优势。

你可能已经注意到，我们粗略地通过 `QPushButton`构造函数的父级参数将 `QPushButton`添加到了 `BrowserWindow`中。我们没有指定位置、大小、边框或类似的设置。如果我们想对布局进行精确控制（这对于创建一个吸引人的界面至关重要），我们必须使用 Qt 的布局对象。让我们现在来看看这些。

在 Qt 中有多种方法来安排控件的位置和布局。我们已经看到通过调用 `setGeometry`使用绝对坐标的方法，但这很少使用，因为当窗口调整大小时，控件不会缩放和调整以适应窗口。

`QLayout`和框控件（box widgets）之间的关键区别在于布局对象不是控件。

相比之下，布局类派自 `QObject` 和 `QWidget`，因此我们使用它们的方式受到限制。例如，我们将一个 `QBoxLayout` 设置为 `MainWindow` 的中心控件。

框控件（例如 `QPushButton` 和 `QBox`）派自 `Widget`，因此我们可以将它们视为普通的控件。你可能很好奇为什么 `QLayouts` 和 `QWidgets` 都具有重复的功能。实际上，`QBox` 控件是为了方便而设计的，它们本质上封装了一个 `QLayout`。布局类派自 `QObject` 和 `QWidget`，相比之下，我们使用它们的方式受到限制。

# 第 17 章

三种感兴趣的 `QLayout` 子类：
- `QHBoxLayout`：水平布局
- `QVBoxLayout`：垂直布局
- `QGridLayout`：网格布局

## 控件 (Widgets)

Qt 中有适用于各种情况的控件，查看它们将占据书的剩余部分。在本节中，我们将介绍常见的 Qt 控件，包括数据输入控件、按钮和列表控件。

## `QLineEdit`

`QLineEdit` 是 Qt 的单行文本输入控件。我们使用它来输入少量的文本，可以使用输入 mask 掩码进行限制，或者进行最终控制。`QLineEdit` 具有编辑功能，允许我们选择文本的一部分、剪切、粘贴、撤销和重做。从用户的角度来看，构造函数和最有用的方法有：

```cpp
#include <qlineedit.h>

QLineEdit(QWidget *parent, const char *name = 0)
QLineEdit(const QString &contents, QWidget *parent, const char *name = 0)
QLineEdit(const QString &contents, const QString &inputMask, QWidget *parent, const char *name = 0)

void setInputMask(const QString &inputMask)
void insert(const QString &text)
bool isModified(void)
void setLength(int length)
void setReadOnly(bool read)
void setText(const QString &text)
QString text(void)
void setEchoMode(EchoMode mode)
```

在构造函数中，我们像往常一样设置父控件和控件名称。一个有趣的属性是 `EchoMode`，它决定了文本在控件中的显示方式。它可以接受以下值：

- `QLineEdit::Normal`: 显示输入字符（默认）
- `QLineEdit::Password`: 用星号代替字符
- `QLineEdit::NoEcho`: 不显示内容

```cpp
lineEdit->setEchoMode(QLineEdit::Password);
```

Qt 3.2 引入的增强功能是 `inputMask`，它根据掩码规则限制输入。

## 使用 Qt `inputMask`

`inputMask` 是一个由字符组成的字符串，每个字符对应一个接受特定字符范围的规则。如果你熟悉正则表达式，那么 `inputMask` 使用了相同的原理。有两种 `inputMask` 字符：一种表示某些字符必须存在，另一种表示如果字符存在，则将其限制在规则范围内。

| 含义 | 必需字符 | 可选字符 |
|---|---|---|
| ASCII A-Z, a-z | n | A, a |
| ASCII A-Z, a-z, 0-9 | N | n |
| 任意字符 | X | x |
| 数字 0–9 | 9 | 0 |
| 数字 1–9 | D | d |

我们的 `inputMask` 是由这些字符组合字符串，可选以分号结尾。还有进一步具有含义的特殊字符：

| | 含义 |
|---|---|
| # | 允许但不要求的数字 |
| > | 将后续输入转换为大写 |
| < | 将后续输入转换为小写 |
| ! | 停止大小转换 |
| \ | 转义字符，将特殊字符作为分隔符 |

`inputMask` 中的所有其他字符在 `QLineEdit` 中都作为分隔符。是一些掩码示例及其允许的输入：

| | 描述 |
|---|---|
| "AAAAAA-999D" | 允许 Athens-2004 但不允许 Sydney-2000 或 Atlanta-1996。 |
| "AAAAnn-99-99;" | 允许 March-03-12 但不允许 May-03-12 或 September-03-12。 |
| "000.000.000" | 允许 IP 地址，例如 192.168.0.1。 |

## 尝试一下 — `QLineEdit`

现在让我们看看 `QLineEdit` 的运行情况。

1. 首先是头文件 `Edit.h`：

```cpp
#include <mainwindow.h>

#include <qlineedit.h>

#include <string.h>

class LineEdit : public QMainWindow {

  Q_OBJECT

public:

    QLineEdit(QWidget *parent = 0, const char *name = 0);

    QLineEdit *password_entry;

private slots:

    void Clicked();

};
```

2. `LineEdit.cpp` 是熟悉的类实现文件：

```cpp
#include "LineEdit.moc"

#include <pushbutton.h>

#include <application.h>

#include <label.h>

#include <layout.h>

#include <iostream>

LineEdit::LineEdit(QWidget *parent, const char *name) : QMainWindow(parent, name) {

    QWidget *widget = new QWidget(this);

    setCentralWidget(widget);

}
```

3. 我们将使用 `QGridLayout` 来排列控件。我们指定行和列数、边距设置和间距。

```cpp
QGridLayout *grid = new QGridLayout(widget,3,2,10,10,"grid");

QLineEdit *username_entry = new LineEdit(widget,"username_entry");

QLineEdit *password_entry = new LineEdit(widget,"password_entry");

password_entry->setEchoMode(QLineEdit::Password);

grid->addWidget(new QLabel("Username"), widget,"userlabel"), 0, 0, 0);

grid->addWidget(new QLabel("Password"), widget,"passwordlabel"), 1, 0, 0);

grid->addWidget(username_entry, widget, 0, 1);

grid->addWidget(password_entry, widget, 1, 1);

grid->addWidget(new QPushButton("OK"), widget), 2, 0);
```
